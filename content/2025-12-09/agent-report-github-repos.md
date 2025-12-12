# Regen MCP GitHub Repositories Research Report

**Date:** 2025-12-09
**Author:** Claude Agent Research
**Purpose:** Blog post research on Regen Network MCP ecosystem

---

## Executive Summary

This report documents four Model Context Protocol (MCP) repositories in the Regen Network ecosystem:

1. **regen-network/mcp** - TypeScript MCP server/client for Regen Ledger
2. **gaiaaiagent/regen-koi-mcp** - Knowledge base access via KOI infrastructure
3. **gaiaaiagent/regen-python-mcp** - Python MCP server for blockchain queries
4. **gaiaaiagent/regen-registry-review-mcp** - Automated carbon credit review workflow

All four repositories implement the Model Context Protocol, an open standard introduced by Anthropic in November 2024 for connecting AI applications to external systems.

---

## 1. regen-network/mcp

### Repository Information
- **URL:** https://github.com/regen-network/mcp
- **Description:** TypeScript implementation of MCP server and CLI client for Regen Ledger and Cosmos ecosystem
- **License:** Not specified in package.json
- **Stars:** 1 (as of research date)
- **Status:** Active development, no published releases

### Main Technologies
- **Primary Language:** TypeScript (95.2%)
- **JavaScript:** 4.8%
- **Architecture:** Monorepo with separate client and server workspaces
- **Package Name:** `@mcp-typescript/server` (internal)
- **NPM Package:** Not published to npm registry
- **SDK:** @modelcontextprotocol/sdk ^1.12.1

### Key Features

**Regen-Specific Modules:**
- Ecocredit baskets
- Marketplace queries
- Credit classes, projects, and batches

**Cosmos Integrations:**
- Bank (balances, supply)
- Staking
- Distribution
- Governance
- Feegrant
- Group
- Mint
- Parameters
- Transactions
- Upgrades

**Architecture:**
- Full MCP server and client implementation
- Query support (read-only)
- Transaction support planned but not yet implemented
- Extensible design for custom queries

### Installation Instructions

```bash
# Clone the repository
git clone https://github.com/regen-network/mcp.git
cd mcp

# Install dependencies
npm install

# Build the project
npm run build

# Start the server
npm run dev:server

# In another terminal, connect via CLI
npm run dev:client -- connect
```

### Available Scripts

```bash
npm run build      # Compile all workspace projects
npm run dev:server # Run development server
npm run dev:client # Run development client
npm run test       # Execute tests
npm run lint       # Analyze code quality
npm run format     # Format TypeScript, JSON, and Markdown files
```

### Adding to Claude Code

**Method 1: Manual Configuration**

Add to `.mcp.json` or Claude Desktop config:

```json
{
  "mcpServers": {
    "regen": {
      "command": "node",
      "args": ["/absolute/path/to/mcp/server/dist/index.js"],
      "env": {
        "NODE_ENV": "production",
        "REGEN_RPC_ENDPOINT": "https://regen-rpc.publicnode.com:443"
      }
    }
  }
}
```

**Method 2: Claude MCP Add (after building locally)**

```bash
claude mcp add --transport stdio regen --scope project -- node /absolute/path/to/mcp/server/dist/index.js
```

### Current Limitations
- Query-only functionality (transactions not yet supported)
- No published npm package
- Requires manual build and local installation
- Limited documentation on available tools/prompts

---

## 2. gaiaaiagent/regen-koi-mcp

### Repository Information
- **URL:** https://github.com/gaiaaiagent/regen-koi-mcp
- **Description:** MCP server providing AI assistants access to Regen Network's knowledge base through KOI infrastructure
- **License:** MIT
- **Stars:** 1
- **Status:** Active, version 1.2.1

### Main Technologies
- **Primary Language:** TypeScript
- **Package Name:** `regen-koi-mcp`
- **NPM Package:** Published (version 1.2.1)
- **Infrastructure:** KOI (Knowledge Organization Infrastructure)
- **API Endpoint:** https://regen.gaiaai.xyz/api/koi

### Key Features

**Knowledge Base Coverage:**
- 15,000+ documents indexed
- Topics: carbon credits, regenerative agriculture, blockchain sustainability, climate action
- 26,768+ code entities (Methods, Functions, Structs, Interfaces)
- 5 repositories indexed

**Search Capabilities:**
- Hybrid search combining vector embeddings and graph queries
- Reciprocal Rank Fusion algorithm
- Date filtering support
- Auto-routing for entity vs. conceptual queries

**Specialized Features:**
- Code Knowledge Graph navigation
- Weekly digest generation from community discussions
- GitHub documentation access
- Team authentication for @regen.network members (OAuth)
- Public access for general queries (no auth required)

### Installation Instructions

**Quick Install (Recommended):**

```bash
# Claude Code CLI
claude mcp add regen-koi npx regen-koi-mcp@latest

# Codex
codex mcp add regen-koi npx "-y regen-koi-mcp@latest"

# Warp
/add-mcp regen-koi npx -y regen-koi-mcp@latest

# Amp
amp mcp add regen-koi -- npx -y regen-koi-mcp@latest
```

**Alternative: Automated Script**

```bash
curl -fsSL https://raw.githubusercontent.com/gaiaaiagent/regen-koi-mcp/main/install.sh | bash
```

Note: Always review installation scripts before executing.

**Manual Installation:**

```bash
npm install -g regen-koi-mcp@latest
```

### Available Tools

**Knowledge Base Search:**
- `search_knowledge` - Hybrid search with optional date filtering
- `hybrid_search` - Auto-routing for entity vs. conceptual queries
- `get_stats` - Knowledge base statistics
- `generate_weekly_digest` - Community activity summaries
- `get_notebooklm_export` - Complete forum posts and documentation

**Code Graph Queries:**
- `query_code_graph` - Relationship queries (keeper-message mappings, call graphs)

**GitHub Integration:**
- `search_github_docs` - Search Regen repositories
- `get_repo_overview` - Repository summaries
- `get_tech_stack` - Technology information

**Authentication (Team Only):**
- `regen_koi_authenticate` - OAuth login for internal documentation access

### Adding to Claude Code

**Method 1: CLI (Recommended)**

```bash
claude mcp add --transport stdio regen-koi -- npx regen-koi-mcp@latest
```

**Method 2: Manual Configuration**

Add to `.mcp.json`:

```json
{
  "mcpServers": {
    "regen-koi": {
      "command": "npx",
      "args": ["regen-koi-mcp@latest"],
      "env": {
        "KOI_API_ENDPOINT": "https://regen.gaiaai.xyz/api/koi"
      }
    }
  }
}
```

Config file locations:
- **Mac:** `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`
- **Linux:** `~/.config/Claude/claude_desktop_config.json`

### Example Queries

```
What repositories are indexed in KOI?
Search for functions containing 'keeper' in regen-ledger
Explain the ecocredit module architecture
What functions call CreateBatch?
Generate a weekly digest of Regen Network discussions
```

### Deployment Options

1. **Hosted API** (default) - Uses public endpoint, no setup required
2. **Self-Hosted API** - Run your own server for direct database access
3. **Full Pipeline** - Deploy complete infrastructure (koi-sensors + koi-processor)

### Authentication Details

**Public Access:**
- No authentication required for general queries
- Access to 15,000+ public documents

**Team Access:**
- OAuth device authorization flow (RFC 8628)
- Email verification (@regen.network only)
- Browser-based activation code entry
- Local token storage (0o600 permissions)
- ~1 hour token expiration
- Security: SHA-256 hashing, domain enforcement, phishing prevention, rate limiting, JWT validation

---

## 3. gaiaaiagent/regen-python-mcp

### Repository Information
- **URL:** https://github.com/gaiaaiagent/regen-python-mcp
- **Description:** Python-based MCP server for Regen Network blockchain interactions
- **License:** MIT
- **Status:** Active development
- **Focus:** Ecological credit markets (carbon, biodiversity, regenerative agriculture)

### Main Technologies
- **Primary Language:** Python (3.10+)
- **Package Manager:** pip (requirements.txt)
- **SDK:** Python MCP SDK
- **Blockchain:** Regen Ledger (Cosmos-based)
- **NPM Package:** Not applicable (Python project)

### Key Features

**45+ Blockchain Tools** across seven modules:

1. **Bank Module (11 tools)**
   - Account balances
   - Token supplies
   - Denomination metadata

2. **Distribution Module (9 tools)**
   - Validator rewards
   - Delegator information
   - Community pool data

3. **Governance Module (8 tools)**
   - Proposals
   - Votes
   - Deposits
   - Tally results

4. **Marketplace Module (5 tools)**
   - Sell orders
   - Pricing
   - Allowed denominations

5. **Ecocredits Module (4 tools)**
   - Credit types
   - Classes
   - Projects
   - Batches

6. **Baskets Module (5 tools)**
   - Basket operations
   - Balances
   - Fees

7. **Analytics Module (3 tools)**
   - Portfolio impact analysis
   - Methodology comparison

**Additional Features:**
- 8 interactive prompts for guided workflows
- Multiple endpoint failover
- Configurable caching
- Type-safe Pydantic models
- Async/await patterns
- Comprehensive error handling
- Health monitoring

### Installation Instructions

**Prerequisites:**
```bash
# Requires Python 3.10 or higher
python --version
```

**Quick Install:**

```bash
git clone https://github.com/gaiaaiagent/regen-python-mcp.git
cd regen-python-mcp
pip install -r requirements.txt
python main.py
```

**With UV (Recommended):**

```bash
git clone https://github.com/gaiaaiagent/regen-python-mcp.git
cd regen-python-mcp
uv sync
uv run python main.py
```

### Configuration

Create a `.env` file:

```bash
# Optional custom endpoints
REGEN_RPC_ENDPOINTS=https://rpc.regen.network:443,https://regen-rpc.publicnode.com:443
REGEN_REST_ENDPOINTS=https://api.regen.network:443

# Cache settings
REGEN_MCP_ENABLE_CACHE=true
REGEN_MCP_CACHE_TTL_SECONDS=300

# Logging
REGEN_MCP_LOG_LEVEL=INFO
```

### Available Prompts

1. Chain exploration
2. Ecocredit queries
3. Marketplace investigation
4. Governance analysis
5. Distribution queries
6. Bank operations
7. Analytics workflows
8. Configuration setup

### Adding to Claude Code

**Method 1: CLI with UV**

```bash
claude mcp add --transport stdio regen-network \
  --env PYTHONPATH=/absolute/path/to/regen-python-mcp/src \
  -- /path/to/uv run --directory /absolute/path/to/regen-python-mcp python main.py
```

**Method 2: Manual Configuration**

Add to `.mcp.json`:

```json
{
  "mcpServers": {
    "regen-network": {
      "command": "/path/to/uv",
      "args": [
        "run",
        "--directory",
        "/absolute/path/to/regen-python-mcp",
        "python",
        "main.py"
      ],
      "env": {
        "PYTHONPATH": "/absolute/path/to/regen-python-mcp/src",
        "REGEN_MCP_LOG_LEVEL": "INFO"
      }
    }
  }
}
```

**Method 3: Traditional Python**

```json
{
  "mcpServers": {
    "regen-network": {
      "command": "python",
      "args": ["/absolute/path/to/regen-python-mcp/main.py"],
      "env": {
        "PYTHONPATH": "/absolute/path/to/regen-python-mcp/src"
      }
    }
  }
}
```

### Example Queries

```
What is the current price of NCT carbon credits?
Show me all ecocredit classes on Regen Network
What are the governance proposals currently in voting?
Calculate the impact of my ecocredit portfolio
Show validator rewards for validator X
```

---

## 4. gaiaaiagent/regen-registry-review-mcp

### Repository Information
- **URL:** https://github.com/gaiaaiagent/regen-registry-review-mcp
- **Description:** MCP server automating carbon credit project documentation review
- **License:** MIT
- **Version:** 2.0.0
- **Status:** Phases 1-4.2 complete, Phase 5 (human review) planned

### Main Technologies
- **Primary Language:** Python (≥3.10)
- **Package Manager:** UV (recommended)
- **LLM:** Claude Sonnet 4 (for extraction)
- **Test Coverage:** 99 tests, 100% passing, 73.9% coverage
- **NPM Package:** Not applicable (Python project)

### Key Features

**Core Capabilities:**
- Session management with atomic state persistence
- Document discovery and smart classification
- PDF text extraction with caching
- Evidence extraction mapping requirements to documents
- Cross-document validation (dates, land tenure, project IDs)
- Structured report generation (Markdown and JSON)
- Complete audit trails with page citations

**Phase 4.2 Additions (LLM-Native Extraction):**
- LLM-powered field extraction for dates, land tenure, project IDs
- Intelligent date parsing (80%+ recall on real documents)
- Fuzzy name deduplication for owner matching
- Prompt caching (90% cost reduction)
- 99 comprehensive tests (100% pass rate)

**Impact:**
- Transforms 6-8 hour manual process into 60-90 minute workflow
- Automated evidence extraction
- Consistent review standards
- Full audit trail for compliance

### Installation Instructions

**Requirements:**
- Python ≥3.10
- UV package manager
- 4GB RAM minimum (8GB recommended)
- 3GB disk space for ML models

**Setup:**

```bash
git clone https://github.com/gaiaaiagent/regen-registry-review-mcp.git
cd regen-registry-review-mcp
uv sync
cp .env.example .env
# Add your Anthropic API key to .env
uv run python -m registry_review_mcp.server
```

### Configuration

Create `.env` file:

```bash
# Required for LLM extraction
REGISTRY_REVIEW_ANTHROPIC_API_KEY=sk-ant-api03-...

# LLM settings
REGISTRY_REVIEW_LLM_EXTRACTION_ENABLED=true
REGISTRY_REVIEW_LLM_MODEL=claude-sonnet-4-20250514

# Optional: Custom cache directory
REGISTRY_REVIEW_CACHE_DIR=/path/to/cache
```

### Available Tools

**Session Management:**
- `create_session` - Initialize new review session
- `load_session` - Load existing session
- `list_sessions` - View all sessions
- `delete_session` - Remove session

**Document Processing:**
- `discover_documents` - Find and classify PDFs
- `extract_pdf_text` - Extract text with caching
- `extract_gis_metadata` - Process GIS data

**Evidence & Validation:**
- `extract_evidence` - LLM-powered field extraction
- `map_requirement` - Link requirements to documents
- `cross_validate` - Validate across documents
- `validate_date_alignment` - Check date consistency

**Reporting:**
- `generate_review_report` - Create comprehensive report
- `export_review` - Export to Markdown/JSON

### The 3-Stage Workflow

**Stage 1 - Initialize:**
```
/initialize Botany Farm 2022-2023, /absolute/path/to/examples/22-23
```

**Stage 2 - Document Discovery:**
```
/document-discovery
```

**Stage 3 - Evidence Extraction:**
```
/evidence-extraction
```

The prompts automatically select your most recent session and guide through each step.

### Adding to Claude Code

**Method 1: CLI**

```bash
claude mcp add --transport stdio registry-review \
  --env REGISTRY_REVIEW_ANTHROPIC_API_KEY=sk-ant-... \
  -- uv --directory /absolute/path/to/regen-registry-review-mcp run python -m registry_review_mcp.server
```

**Method 2: Manual Configuration**

Add to `.mcp.json`:

```json
{
  "mcpServers": {
    "registry-review": {
      "command": "uv",
      "args": [
        "--directory",
        "/absolute/path/to/regen-registry-review-mcp",
        "run",
        "python",
        "-m",
        "registry_review_mcp.server"
      ],
      "env": {
        "REGISTRY_REVIEW_ANTHROPIC_API_KEY": "sk-ant-api03-..."
      }
    }
  }
}
```

### Development & Testing

```bash
# Run all tests
uv run pytest

# Run specific test suite
uv run pytest tests/test_evidence_extraction.py -v

# Format and lint
uv run black src/ tests/
uv run ruff check src/ tests/

# Type checking
uv run mypy src/
```

### Example Use Cases

1. **Annual Monitoring Report Review**
   - Upload monitoring reports
   - Extract dates, land tenure, project IDs
   - Validate consistency across documents
   - Generate compliance report

2. **Project Registration Review**
   - Process new project documentation
   - Extract all required evidence
   - Cross-validate against registry requirements
   - Create audit trail

3. **Batch Review**
   - Review multiple projects
   - Consistent standards across all
   - Parallel processing support
   - Comparative analysis

---

## Comparison Matrix

| Feature | regen-network/mcp | regen-koi-mcp | regen-python-mcp | regen-registry-review-mcp |
|---------|-------------------|---------------|------------------|---------------------------|
| **Language** | TypeScript | TypeScript | Python | Python |
| **NPM Package** | No | Yes (1.2.1) | No | No |
| **Primary Use** | Blockchain queries | Knowledge base | Blockchain queries | Document review |
| **Tools Count** | ~30+ | 11 | 45+ | 15+ |
| **Auth Required** | No | Optional (team) | No | API key required |
| **Installation** | Build from source | `npx` one-liner | `pip` or `uv` | `uv sync` |
| **Deployment** | Local only | Hosted/Self-hosted | Local only | Local only |
| **Status** | Active dev | Published | Active dev | Phases 1-4.2 done |
| **Best For** | TypeScript devs | Quick knowledge access | Python devs | Carbon credit reviews |

---

## Installation Quick Reference

### Claude MCP Add Commands

```bash
# regen-koi-mcp (NPM package)
claude mcp add regen-koi npx regen-koi-mcp@latest

# regen-network/mcp (local build required)
cd /path/to/mcp && npm install && npm run build
claude mcp add --transport stdio regen -- node /path/to/mcp/server/dist/index.js

# regen-python-mcp (UV recommended)
claude mcp add --transport stdio regen-network \
  -- uv run --directory /path/to/regen-python-mcp python main.py

# regen-registry-review-mcp (requires API key)
claude mcp add --transport stdio registry-review \
  --env REGISTRY_REVIEW_ANTHROPIC_API_KEY=sk-ant-... \
  -- uv --directory /path/to/regen-registry-review-mcp run python -m registry_review_mcp.server
```

### Manual Configuration Template

```json
{
  "mcpServers": {
    "regen-koi": {
      "command": "npx",
      "args": ["regen-koi-mcp@latest"]
    },
    "regen": {
      "command": "node",
      "args": ["/path/to/mcp/server/dist/index.js"]
    },
    "regen-network": {
      "command": "uv",
      "args": ["run", "--directory", "/path/to/regen-python-mcp", "python", "main.py"]
    },
    "registry-review": {
      "command": "uv",
      "args": ["--directory", "/path/to/regen-registry-review-mcp", "run", "python", "-m", "registry_review_mcp.server"],
      "env": {"REGISTRY_REVIEW_ANTHROPIC_API_KEY": "sk-ant-..."}
    }
  }
}
```

---

## Understanding MCP Architecture

### What is Model Context Protocol (MCP)?

MCP is an open standard introduced by Anthropic in November 2024 that standardizes how AI systems like LLMs integrate with external tools, systems, and data sources.

**Think of it as:** USB-C for AI applications - a universal connector.

### MCP Components

1. **MCP Servers** - Expose data and functionality
2. **MCP Clients** - AI applications that connect to servers
3. **MCP SDKs** - Development tools (TypeScript, Python, C#, Java)
4. **MCP Protocol** - Standardized communication spec

### Benefits

- **Standardization:** One protocol for all integrations
- **Reusability:** Build once, use with any MCP client
- **Security:** Controlled access with clear permissions
- **Extensibility:** Easy to add new tools and capabilities

### Industry Adoption

Major adopters include:
- Anthropic (Claude)
- OpenAI
- Google DeepMind
- Block, Apollo
- Zed, Replit, Codeium, Sourcegraph

---

## Common MCP Workflows

### 1. Knowledge Retrieval (regen-koi-mcp)

```
User: What is the ecocredit module architecture?
Claude → regen-koi → search_knowledge("ecocredit module")
Claude → Receives documentation and code examples
Claude → Explains architecture to user
```

### 2. Blockchain Query (regen-python-mcp)

```
User: Show me active carbon credit sell orders
Claude → regen-network → marketplace_sell_orders()
Claude → Receives order data
Claude → Formats and presents to user
```

### 3. Document Review (regen-registry-review-mcp)

```
User: /initialize Project XYZ, /path/to/docs
Claude → registry-review → create_session()
User: /document-discovery
Claude → registry-review → discover_documents()
User: /evidence-extraction
Claude → registry-review → extract_evidence()
Claude → Generates complete review report
```

### 4. Hybrid Analysis

```
User: Analyze the CreateBatch function and find related marketplace orders
Claude → regen-koi → query_code_graph("CreateBatch")
Claude → regen-network → marketplace_sell_orders()
Claude → Synthesizes information from both sources
Claude → Provides comprehensive analysis
```

---

## Troubleshooting

### Common Issues

**1. Connection Closed Error (Windows)**

On native Windows, wrap `npx` commands with `cmd /c`:
```bash
claude mcp add regen-koi -- cmd /c npx regen-koi-mcp@latest
```

**2. Python Path Issues**

Always set PYTHONPATH environment variable:
```json
"env": {"PYTHONPATH": "/absolute/path/to/src"}
```

**3. UV Not Found**

Install UV package manager:
```bash
pip install uv
# or
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**4. MCP Server Not Connecting**

1. Check server is listed: `claude mcp list`
2. Verify paths are absolute, not relative
3. Check environment variables are set
4. Restart Claude Desktop/Code
5. Check logs for error messages

**5. API Key Issues (registry-review)**

- Ensure API key starts with `sk-ant-`
- Check `.env` file is in correct directory
- Verify environment variable is loaded
- Test with `echo $REGISTRY_REVIEW_ANTHROPIC_API_KEY`

---

## Security Considerations

### MCP Security Model

As of April 2025, security researchers identified several MCP security concerns:

1. **Prompt Injection** - MCP tools can be vulnerable to injected prompts
2. **Tool Permissions** - Combining tools can exfiltrate files
3. **Lookalike Tools** - Malicious tools can silently replace trusted ones

### Best Practices

**For regen-koi-mcp:**
- Review installation script before running
- Use hosted API (default) for public data
- Self-host for sensitive internal data
- Team auth uses OAuth with domain enforcement

**For regen-python-mcp:**
- Use environment variables, not hardcoded endpoints
- Validate RPC/REST endpoints before use
- Monitor blockchain queries for unexpected behavior

**For regen-registry-review-mcp:**
- Store API keys in `.env`, never in code
- Use file permissions 0o600 for sensitive files
- Review extracted data before publishing reports
- Maintain audit trails for compliance

**General MCP Security:**
- Only install MCP servers from trusted sources
- Review source code when possible
- Use scoped configurations (project vs. user vs. local)
- Monitor tool invocations and outputs
- Keep MCP SDKs and servers updated

---

## Resources

### Documentation

- [Model Context Protocol Official Docs](https://docs.claude.com/en/docs/mcp)
- [Anthropic MCP Announcement](https://www.anthropic.com/news/model-context-protocol)
- [MCP GitHub Organization](https://github.com/modelcontextprotocol)
- [Claude Code MCP Guide](https://docs.claude.com/en/docs/claude-code/mcp)

### Repositories

- [regen-network/mcp](https://github.com/regen-network/mcp)
- [gaiaaiagent/regen-koi-mcp](https://github.com/gaiaaiagent/regen-koi-mcp)
- [gaiaaiagent/regen-python-mcp](https://github.com/gaiaaiagent/regen-python-mcp)
- [gaiaaiagent/regen-registry-review-mcp](https://github.com/gaiaaiagent/regen-registry-review-mcp)

### Community

- [Regen Network Forum](https://forum.regen.network)
- [MCP Server Registry](https://github.com/modelcontextprotocol/registry)
- [GitHub MCP Registry](https://github.com/mcp)

### Tools & SDKs

- [@modelcontextprotocol/sdk (TypeScript)](https://www.npmjs.com/package/@modelcontextprotocol/sdk)
- [MCP Python SDK](https://github.com/modelcontextprotocol/python-sdk)
- [UV Package Manager](https://github.com/astral-sh/uv)

---

## Conclusion

The Regen Network MCP ecosystem provides comprehensive tooling for:

1. **Blockchain Access** (regen-network/mcp, regen-python-mcp) - Query Regen Ledger and Cosmos modules
2. **Knowledge Management** (regen-koi-mcp) - Access 15,000+ documents with hybrid search
3. **Workflow Automation** (regen-registry-review-mcp) - Streamline carbon credit reviews

All four repositories implement the Model Context Protocol, enabling seamless integration with Claude Desktop, Claude Code, and other MCP clients.

**Quick Start Recommendation:**

- **For quick access to Regen knowledge:** Start with `regen-koi-mcp` (one-line install)
- **For blockchain development:** Use `regen-python-mcp` (Python) or `regen-network/mcp` (TypeScript)
- **For carbon credit reviews:** Deploy `regen-registry-review-mcp` with LLM extraction

**Next Steps:**

1. Install regen-koi-mcp: `claude mcp add regen-koi npx regen-koi-mcp@latest`
2. Test connection: Ask Claude "What repositories are indexed in KOI?"
3. Explore tools: Use `/mcp` command in Claude to browse available tools
4. Add more servers based on your use case

---

## Sources

### Web Search Results

- [Regen Network GitHub](https://github.com/regen-network)
- [regen-network/regen-ledger](https://github.com/regen-network/regen-ledger)
- [GAIA AI GitHub](https://github.com/gaiaaiagent)
- [Model Context Protocol Documentation](https://docs.claude.com/en/docs/mcp)
- [Anthropic MCP Announcement](https://www.anthropic.com/news/model-context-protocol)
- [Model Context Protocol - Wikipedia](https://en.wikipedia.org/wiki/Model_Context_Protocol)
- [Connect Claude Code to tools via MCP](https://docs.claude.com/en/docs/claude-code/mcp)
- [Add MCP Servers to Claude Code Guide](https://mcpcat.io/guides/adding-an-mcp-server-to-claude-code/)
- [@regen-network/api npm package](https://www.npmjs.com/package/@regen-network/api)
- [@modelcontextprotocol/sdk npm](https://www.npmjs.com/package/@modelcontextprotocol/sdk)

### Repository Analysis

All repository information was gathered through direct analysis of:
- GitHub repository pages
- README.md files
- package.json configurations
- Source code structure
- Installation scripts

---

**Report Generated:** 2025-12-09
**Research Method:** Web search, repository analysis, documentation review
**Tools Used:** WebSearch, WebFetch, Bash, Read
**Contact:** For questions about this report, please contact the Regen AI team on the Regen Network forum.
