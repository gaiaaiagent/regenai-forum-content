# Regen KOI MCP Service Outage Report

**Date:** 2025-12-09
**Reported by:** Claude Code diagnostic session
**Severity:** Critical - Service Unavailable
**Affected Service:** Regen KOI MCP Server (regen-koi-mcp)

---

## Executive Summary

The Regen KOI MCP server is failing to connect to its backend API services hosted at `regen.gaiaai.xyz`. Both the KOI API endpoint and the Apache Jena Fuseki SPARQL endpoint are returning 404 errors, rendering the MCP server non-functional.

---

## Affected Endpoints

### 1. KOI API Endpoint

| Property | Value |
|----------|-------|
| **URL** | `https://regen.gaiaai.xyz/api/koi` |
| **Expected** | JSON API responses |
| **Actual Response** | `{"success":false,"error":{"message":"API endpoint not found","code":404}}` |
| **HTTP Status** | 404 Not Found |

### 2. SPARQL/Jena Fuseki Endpoint

| Property | Value |
|----------|-------|
| **URL** | `https://regen.gaiaai.xyz/api/koi/fuseki/koi/sparql` |
| **Expected** | SPARQL query endpoint |
| **Actual Response** | `Service Description: /koi/sparql` (partial HTML) |
| **HTTP Status** | 404 Not Found |

### 3. Base Domain Status

| Property | Value |
|----------|-------|
| **URL** | `https://regen.gaiaai.xyz` |
| **HTTP Status** | 401 Unauthorized |
| **Headers** | `www-authenticate: Basic realm="RegenAI Dashboard - Team Access Only"` |
| **Server** | nginx/1.29.3 |

The base domain is responding (returns 401 requiring auth), indicating nginx is running but the `/api/koi` routes are not configured or the upstream service is down.

---

## MCP Server Configuration

The MCP server is configured with these environment variables:

```json
{
  "regen-koi": {
    "command": "node",
    "args": ["/home/ygg/Workspace/sandbox/regen-koi-mcp/dist/index.js"],
    "env": {
      "KOI_API_ENDPOINT": "https://regen.gaiaai.xyz/api/koi",
      "JENA_ENDPOINT": "https://regen.gaiaai.xyz/api/koi/fuseki/koi/sparql"
    }
  }
}
```

---

## Server Startup Behavior

When started, the MCP server outputs:

```
[regen-koi] Starting Regen KOI MCP Server v1.0.0
[regen-koi] KOI API Endpoint: https://regen.gaiaai.xyz/api/koi
[regen-koi] API Key: Not configured (using anonymous access)
[regen-koi] Server running on stdio transport
SPARQL execution error: Error
[regen-koi] Warm-up probes completed
```

The "SPARQL execution error" occurs during the warm-up phase when the server attempts to validate connectivity to the Jena Fuseki endpoint.

---

## Affected Tools

The following MCP tools are non-functional due to this outage:

| Tool | Description | Dependency |
|------|-------------|------------|
| `search_knowledge` | Hybrid search across KOI (vectors + graph) | KOI API + SPARQL |
| `hybrid_search` | Intelligent graph/vector routing | KOI API + SPARQL |
| `get_stats` | Knowledge base statistics | KOI API |
| `generate_weekly_digest` | Weekly activity digest | KOI API |
| `get_notebooklm_export` | Full content export | KOI API |
| `search_github_docs` | GitHub documentation search | KOI API |
| `get_repo_overview` | Repository overviews | KOI API |
| `get_tech_stack` | Technical stack info | KOI API |
| `get_mcp_metrics` | Server metrics | Local only (may work) |
| `regen_koi_authenticate` | OAuth authentication | KOI API |

---

## Likely Causes

1. **Upstream service not running**: The KOI API backend application may not be running on the server
2. **nginx misconfiguration**: The `/api/koi` location block may be missing or misconfigured
3. **Docker/container down**: If the KOI API runs in a container, it may have stopped
4. **Recent deployment issue**: A recent deployment may have failed or changed the routing

---

## Recommended Actions

### Immediate (Server Admin)

1. **Check nginx configuration** for `/api/koi` location block:
   ```bash
   grep -r "api/koi" /etc/nginx/
   ```

2. **Verify backend service status**:
   ```bash
   # If using systemd
   systemctl status koi-api

   # If using Docker
   docker ps | grep koi
   docker logs <container_id>

   # If using PM2
   pm2 status
   ```

3. **Check Jena Fuseki service**:
   ```bash
   # Verify Fuseki is running
   curl http://localhost:3030/$/ping

   # Check Fuseki logs
   journalctl -u fuseki -n 100
   ```

4. **Review nginx error logs**:
   ```bash
   tail -100 /var/log/nginx/error.log
   ```

### Verification Test

Once services are restored, verify with:

```bash
# Test KOI API
curl -s https://regen.gaiaai.xyz/api/koi/health

# Test SPARQL endpoint
curl -s -X POST \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "Accept: application/sparql-results+json" \
  -d "query=SELECT * WHERE { ?s ?p ?o } LIMIT 1" \
  https://regen.gaiaai.xyz/api/koi/fuseki/koi/sparql
```

---

## Alternative: Local Fallback Configuration

If the public endpoint cannot be restored immediately, the MCP server can be configured to use local endpoints:

```json
{
  "env": {
    "KOI_API_ENDPOINT": "http://localhost:8910",
    "JENA_ENDPOINT": "http://localhost:3030/koi/sparql"
  }
}
```

Default fallback values in the code:
- `KOI_API_ENDPOINT`: defaults to `https://regen.gaiaai.xyz/api/koi`
- `JENA_ENDPOINT`: defaults to `http://localhost:3030/koi/sparql`

---

## Timeline

| Time (UTC) | Event |
|------------|-------|
| 2025-12-09 ~00:30 | Issue reported during Claude Code session |
| 2025-12-09 00:33 | Endpoint diagnostics confirmed 404 errors |
| 2025-12-09 00:58 | Full investigation completed |

---

## Contact

Please respond to this report with:
1. Confirmation of root cause
2. ETA for service restoration
3. Any changes to endpoint URLs if applicable

---

*Report generated by Claude Code diagnostic session*
