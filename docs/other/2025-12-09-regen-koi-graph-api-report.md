# Regen KOI Code Graph API - Configuration Report

**Date:** 2025-12-09
**Reported by:** Claude Code diagnostic session
**Severity:** Medium - Feature Unavailable
**Affected Feature:** Code Graph queries via `/api/koi/graph`

---

## Executive Summary

The KOI Code Graph API endpoint (`/api/koi/graph`) is not accessible. This endpoint provides graph-based queries over 26,768+ code entities from Regen Network repositories using Apache AGE (PostgreSQL graph extension). The nginx configuration is missing the location block to route this endpoint.

---

## Current Status

### Working Endpoints (Fixed Earlier)

| Endpoint | Status | Backend Port |
|----------|--------|--------------|
| `/api/koi/query` | Working | 8301 |
| `/api/koi/stats` | Working | 8301 |
| `/api/koi/health` | Working | 8301 |
| `/api/koi/fuseki/koi/sparql` | Working | 3030 |

### Not Working

| Endpoint | Status | Expected Backend |
|----------|--------|------------------|
| `/api/koi/graph` | **404 Not Found** | 8301 |

---

## Test Results

```bash
$ curl -sL -X POST 'https://regen.gaiaai.xyz/api/koi/graph' \
  -H 'Content-Type: application/json' \
  -d '{"query_type": "list_repos"}'

{"detail":"Not Found"}
```

The endpoint returns a generic "Not Found" error, indicating the request is falling through to a catch-all handler instead of being routed to the KOI API.

---

## Required Fix

### 1. Add nginx Location Block

Add to `/opt/projects/GAIA/config/nginx-ssl.conf` (before the catch-all `location /`):

```nginx
# Code Graph API - Apache AGE queries
location ^~ /api/koi/graph {
    proxy_pass http://localhost:8301;
    proxy_http_version 1.1;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_read_timeout 60s;
    proxy_connect_timeout 10s;
}
```

### 2. Reload nginx

```bash
docker exec nginx nginx -s reload
```

---

## Infrastructure Requirements

The graph API requires Apache AGE to be installed and configured on the PostgreSQL database:

### Check Apache AGE Installation

```bash
# SSH to server, then:
psql -d eliza -c "SELECT extversion FROM pg_extension WHERE extname = 'age';"
# Should return version like 1.5.0
```

### Check Graph Data Exists

```bash
psql -d eliza -c "
  SELECT count(*) FROM ag_catalog.cypher('regen_graph_v2', \$\$
    MATCH (n) RETURN count(n) as node_count
  \$\$) as (node_count agtype);
"
# Should return ~26,768 entities
```

### Required Environment Variables

The KOI API server (port 8301) needs these environment variables:

```bash
GRAPH_DB_HOST=localhost
GRAPH_DB_PORT=5432
GRAPH_DB_NAME=eliza
GRAPH_DB_USER=postgres
GRAPH_DB_PASSWORD=<password>
GRAPH_NAME=regen_graph_v2
```

---

## Graph Database Contents

The Apache AGE graph `regen_graph_v2` contains:

| Metric | Value |
|--------|-------|
| **Total Entities** | 26,768 |
| **Entity Types** | Entity, Type, Interface, Function, Struct, etc. |
| **Repositories** | regen-ledger, regen-web, koi-sensors, regen-data-standards, regen-koi-mcp |
| **Primary Language** | Go (regen-ledger), TypeScript (regen-web) |

### Entity Breakdown (Expected)

| Entity Type | Count |
|-------------|-------|
| Entity | ~21,058 |
| Type | ~4,573 |
| Interface | ~804 |
| Function | ~557 |

---

## API Capabilities

Once enabled, the `/api/koi/graph` endpoint supports:

### Discovery Queries
- `list_repos` - List indexed repositories with entity counts
- `list_entity_types` - Show entity types with counts
- `get_entity_stats` - Comprehensive graph statistics

### Search Queries
- `find_by_type` - Find entities by type (Function, Interface, Struct)
- `search_entities` - Regex search by entity name

### Relationship Queries
- `keeper_for_msg` - Find which Keeper handles a Cosmos SDK message
- `msgs_for_keeper` - List all messages a Keeper handles
- `related_entities` - Find entities connected to a given entity

### Module Queries (Cosmos SDK)
- `list_modules` - List all Cosmos SDK modules
- `get_module` - Get module details with entities

---

## Verification Tests

After applying the fix, run these tests:

```bash
# Test 1: List repositories
curl -X POST 'https://regen.gaiaai.xyz/api/koi/graph' \
  -H 'Content-Type: application/json' \
  -d '{"query_type": "list_repos"}'
# Expected: JSON with repo names and entity counts

# Test 2: Search for entities
curl -X POST 'https://regen.gaiaai.xyz/api/koi/graph' \
  -H 'Content-Type: application/json' \
  -d '{"query_type": "search_entities", "entity_name": "MsgCreate", "limit": 5}'
# Expected: JSON with matching code entities

# Test 3: Find module info
curl -X POST 'https://regen.gaiaai.xyz/api/koi/graph' \
  -H 'Content-Type: application/json' \
  -d '{"query_type": "list_modules"}'
# Expected: JSON with Cosmos SDK modules (ecocredit, data, etc.)
```

---

## MCP Client Impact

When this endpoint is unavailable, the MCP server logs:

```
[regen-koi] Graph database configuration not found - hybrid_search and query_code_graph tools will be unavailable
```

Affected MCP tools:
- `query_code_graph` - Primary graph query tool
- `hybrid_search` - Intelligent graph+vector routing (partial impact)

---

## Architecture Context

```
┌─────────────────────────────────────────────────────────────┐
│  Claude Code / MCP Client                                   │
└──────────────────────┬──────────────────────────────────────┘
                       │ stdio
                       ▼
┌─────────────────────────────────────────────────────────────┐
│  Regen KOI MCP Server (Node.js)                             │
│  - query_code_graph tool ← BLOCKED                          │
└──────────────────────┬──────────────────────────────────────┘
                       │ HTTP POST /api/koi/graph
                       ▼
┌─────────────────────────────────────────────────────────────┐
│  nginx (Docker)                                             │
│  - Missing: location ^~ /api/koi/graph { ... }              │
└──────────────────────┬──────────────────────────────────────┘
                       │ ❌ Falls through to catch-all
                       ▼
┌─────────────────────────────────────────────────────────────┐
│  ElizaOS (port 3000) - Returns 404                          │
└─────────────────────────────────────────────────────────────┘

SHOULD BE:
                       │ ✅ Proxy to port 8301
                       ▼
┌─────────────────────────────────────────────────────────────┐
│  KOI API Server (port 8301)                                 │
│  - /api/koi/graph route handler                             │
└──────────────────────┬──────────────────────────────────────┘
                       │ Cypher queries
                       ▼
┌─────────────────────────────────────────────────────────────┐
│  PostgreSQL + Apache AGE                                    │
│  - regen_graph_v2: 26,768 code entities                     │
└─────────────────────────────────────────────────────────────┘
```

---

## Checklist

- [ ] Add `/api/koi/graph` location block to nginx config
- [ ] Reload nginx configuration
- [ ] Verify Apache AGE extension is installed
- [ ] Verify `regen_graph_v2` graph exists with data
- [ ] Verify KOI API server has graph DB environment variables
- [ ] Run verification tests
- [ ] Confirm MCP tools work

---

*Report generated by Claude Code diagnostic session*
