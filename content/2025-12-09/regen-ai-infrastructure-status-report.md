# Regen AI Infrastructure Status Report

**Date:** December 9, 2025
**Status:** All Systems Operational
**Report Type:** Infrastructure Incident Resolution & System Overview

---

## Executive Summary

On December 9, 2025, we identified and resolved connectivity issues affecting the Regen AI MCP (Model Context Protocol) infrastructure. All three MCP servers are now fully operational, providing AI agents with comprehensive access to Regen Network's knowledge base, blockchain data, and code repositories.

This report documents the incident resolution and provides a complete overview of the current system capabilities.

---

## Systems Overview

### MCP Server Architecture

The Regen AI infrastructure consists of three MCP servers that enable AI assistants like Claude to access Regen Network data:

| MCP Server | Purpose | Status |
|------------|---------|--------|
| **regen-koi** | Knowledge Organization Infrastructure - semantic search, SPARQL queries, code graph | Operational |
| **regen-network** | Regen Ledger blockchain queries - credits, projects, governance | Operational |
| **regen** | Legacy Regen Ledger RPC access | Operational |

---

## Regen KOI MCP Server

### Knowledge Base Statistics

| Metric | Value |
|--------|-------|
| **Total Documents** | 49,169 |
| **Documents Added (Last 7 Days)** | 1,087 |
| **Embeddings Indexed** | 48,675 |
| **Code Entities (Graph)** | 28,489 |

### Data Sources

| Source | Documents | Description |
|--------|-----------|-------------|
| GitHub | 30,127 | Code, documentation, issues from Regen repositories |
| Podcasts (SoundCloud) | 6,063 | Planetary Regeneration podcast transcripts |
| Notion | 4,791 | Internal documentation and notes |
| GitLab | 2,000 | Additional code repositories |
| Discourse Forum | 1,612 | forum.regen.network discussions |
| Web Crawl (Forum) | 1,450 | Archived forum content |
| DeSci | 967 | Decentralized science content |
| Docs Site | 626 | docs.regen.network |
| Registry | 598 | registry.regen.network credit data |
| Guides | 328 | guides.regen.network |
| Handbook | 196 | handbook.regen.network |
| Regen Commons | 199 | Community discourse content |
| Foundation | 64 | regen.foundation |
| Main Site | 51 | regen.network |
| YouTube | 15 | Video transcripts |
| Research Retreat | 26 | researchretreat.org |

### API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/koi/query` | POST | Hybrid RAG search (vector + keyword) |
| `/api/koi/stats` | GET | Knowledge base statistics |
| `/api/koi/health` | GET | Service health check |
| `/api/koi/fuseki/koi/sparql` | POST | SPARQL queries against knowledge graph |
| `/api/koi/graph` | POST | Code entity graph queries (Apache AGE) |

### MCP Tools Available

| Tool | Description |
|------|-------------|
| `search_knowledge` | Hybrid search across KOI with date filtering |
| `get_stats` | Knowledge base statistics and source breakdown |
| `generate_weekly_digest` | Weekly activity summary for Regen Network |
| `search_github_docs` | Search Regen GitHub repositories |
| `get_repo_overview` | Repository structure and documentation |
| `get_tech_stack` | Technical stack information |
| `query_code_graph` | Graph queries over code entities |
| `hybrid_search` | Intelligent graph/vector routing |
| `get_mcp_metrics` | Server performance metrics |

---

## Code Graph Database

### Repository Coverage

The Apache AGE graph database contains code entities extracted from 7 Regen Network repositories:

| Repository | Entities | Description |
|------------|----------|-------------|
| regen-ledger | 19,001 | Cosmos SDK blockchain modules (Go) |
| regen-web | 5,716 | Web frontend application (TypeScript/React) |
| koi-processor | 1,404 | Data processing pipeline |
| koi-sensors | 1,135 | Data collection and sensors |
| regen-koi-mcp | 625 | MCP server implementation |
| koi-research | 602 | Research and analysis code |
| regen-data-standards | 6 | Data standards definitions |
| **Total** | **28,489** | |

### Entity Types

| Type | Count | Description |
|------|-------|-------------|
| Entity | ~21,000 | Generic code entities |
| Type | ~4,500 | Type definitions |
| Interface | ~800 | Interface definitions |
| Function | ~550 | Function declarations |
| Struct | Various | Data structures (Go) |
| Module | ~25 | Cosmos SDK modules |

### Graph Query Capabilities

- **Discovery**: List repositories, entity types, modules
- **Search**: Find entities by name (regex), type, or repository
- **Relationships**: Find message handlers, keeper relationships, module dependencies
- **Cosmos SDK Specific**: Query module structure, message routing, keeper patterns

---

## Regen Network MCP Server

### Blockchain Query Capabilities

Direct access to Regen Ledger (regen-1 mainnet) via Python MCP server:

| Category | Tools |
|----------|-------|
| **Accounts** | List accounts, get balances, spendable balances |
| **Ecocredits** | List credit types, classes, projects, batches |
| **Marketplace** | List sell orders, allowed denoms |
| **Baskets** | List baskets, basket balances |
| **Governance** | List proposals, votes, deposits, tally results |
| **Distribution** | Validator rewards, commission, community pool |
| **Analytics** | Portfolio impact analysis, market trends, methodology comparison |

### RPC Configuration

| Setting | Value |
|---------|-------|
| **Chain ID** | regen-1 |
| **RPC Endpoint** | https://regen-rpc.publicnode.com:443 |
| **Consensus** | CometBFT (Cosmos SDK v0.47) |

---

## Incident Resolution Summary

### Issues Identified

1. **KOI API Endpoints (404)** - nginx missing location blocks for `/api/koi/*`
2. **SPARQL Endpoint (404)** - nginx path routing to Fuseki misconfigured
3. **Code Graph API (404)** - nginx missing location block for `/api/koi/graph`
4. **Legacy Regen MCP (502)** - Polkachu RPC endpoint down

### Fixes Applied

| Issue | Root Cause | Resolution |
|-------|------------|------------|
| KOI API 404s | Missing nginx location blocks | Added priority routes (`^~`) to port 8301 |
| SPARQL 404 | Path not stripped when proxying | Added location block proxying to port 3030 |
| Graph API 404 | Missing nginx location block | Added priority route to port 8301 |
| Regen RPC 502 | Polkachu endpoint offline | Switched to PublicNode endpoint |

### Configuration Changes

**nginx-ssl.conf** - Added MCP endpoint routing:
```nginx
location ^~ /api/koi/query { proxy_pass http://localhost:8301; }
location ^~ /api/koi/stats { proxy_pass http://localhost:8301; }
location ^~ /api/koi/health { proxy_pass http://localhost:8301; }
location ^~ /api/koi/graph { proxy_pass http://localhost:8301; }
location ^~ /api/koi/fuseki/ { proxy_pass http://localhost:3030/; }
```

**.mcp.json** - Updated RPC endpoint:
```json
{
  "regen": {
    "env": {
      "REGEN_RPC_ENDPOINT": "https://regen-rpc.publicnode.com:443"
    }
  }
}
```

---

## Infrastructure Architecture

```
                    ┌─────────────────────────────────┐
                    │      Claude Code / AI Agent     │
                    └───────────────┬─────────────────┘
                                    │ MCP Protocol (stdio)
                    ┌───────────────┴─────────────────┐
                    │                                 │
        ┌───────────▼───────────┐       ┌────────────▼────────────┐
        │   regen-koi MCP       │       │  regen-network MCP      │
        │   (Node.js v1.2.1)    │       │  (Python/uv)            │
        └───────────┬───────────┘       └────────────┬────────────┘
                    │ HTTPS                          │ HTTPS
                    ▼                                ▼
        ┌─────────────────────────────┐  ┌────────────────────────┐
        │  nginx (Docker)             │  │  Regen Ledger RPC      │
        │  regen.gaiaai.xyz           │  │  (PublicNode)          │
        │  - SSL termination          │  └────────────────────────┘
        │  - Basic auth               │
        │  - Reverse proxy            │
        └───────────┬─────────────────┘
                    │
      ┌─────────────┼─────────────┬──────────────┐
      ▼             ▼             ▼              ▼
┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐
│ KOI API  │  │ Fuseki   │  │PostgreSQL│  │ BGE      │
│ (8301)   │  │ (3030)   │  │ + AGE    │  │ Embed    │
│ RAG API  │  │ SPARQL   │  │ + vector │  │ (8090)   │
└──────────┘  └──────────┘  └──────────┘  └──────────┘
```

---

## Usage Examples

### Search the Knowledge Base

```bash
curl -X POST 'https://regen.gaiaai.xyz/api/koi/query' \
  -H 'Content-Type: application/json' \
  -d '{"query": "carbon credit methodology", "limit": 5}'
```

### Query Code Graph

```bash
curl -X POST 'https://regen.gaiaai.xyz/api/koi/graph' \
  -H 'Content-Type: application/json' \
  -d '{"query_type": "search_entities", "entity_name": "MsgCreate", "limit": 10}'
```

### SPARQL Query

```bash
curl -X POST 'https://regen.gaiaai.xyz/api/koi/fuseki/koi/sparql' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -H 'Accept: application/sparql-results+json' \
  -d 'query=SELECT * WHERE { ?s ?p ?o } LIMIT 10'
```

---

## Next Steps

1. **Monitoring** - Set up automated health checks for all endpoints
2. **Documentation** - Update public API documentation
3. **Authentication** - Roll out OAuth authentication for private data access
4. **Expansion** - Continue indexing new content sources

---

## Contact

For questions about the Regen AI infrastructure:
- GitHub: [gaiaaiagent/regen-koi-mcp](https://github.com/gaiaaiagent/regen-koi-mcp)
- Forum: [forum.regen.network](https://forum.regen.network)

---

*Report generated December 9, 2025*
