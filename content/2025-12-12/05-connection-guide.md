# Section 5: Connecting - The Technical Path

## Claude Code (Recommended)

MCP was designed by Anthropic, so Claude has first-class integration with the protocol. Unlike other platforms that require API proxies or wrapper layers, Claude Code speaks native JSON-RPC 2.0 over stdio and HTTP/SSE transports—providing direct, low-latency access to MCP servers.

### Quick Start: One-Line Install

The fastest way to connect to Regen KOI:

```bash
claude mcp add regen-koi -- npx -y regen-koi-mcp@latest
```

This command:
- Adds the Regen KOI MCP server to your configuration
- Uses `npx` to run the latest published version
- Requires no local build or repository cloning
- Automatically configures the default API endpoint

Verify the connection:
```bash
claude
> /mcp
```

You should see `regen-koi: connected` in the server status.

### Full Multi-MCP Configuration

For serious development work, you'll want access to multiple Regen MCPs simultaneously. This enables asking questions that span knowledge and blockchain data in the same conversation.

**Step 1: Clone and Build the Servers**

```bash
# Create working directory
mkdir regen-mcps
cd regen-mcps

# Clone repositories
mkdir mcps
cd mcps
git clone https://github.com/gaiaaiagent/regen-koi-mcp.git
git clone https://github.com/gaiaaiagent/regen-python-mcp.git
git clone https://github.com/regen-network/mcp.git
cd ..

# Build Node.js servers
cd mcps/regen-koi-mcp
npm install && npm run build
cd ../mcp/server
npm install && npm run build
cd ../../..

# Setup Python server
cd mcps/regen-python-mcp
uv sync
cd ../..
```

**Step 2: Enable Project MCP Servers**

Create `.claude/settings.json`:

```bash
mkdir -p .claude
cat > .claude/settings.json << 'EOF'
{
  "enableAllProjectMcpServers": true
}
EOF
```

**Step 3: Configure All Servers**

Create `.mcp.json` in your project root:

```json
{
  "mcpServers": {
    "regen-koi": {
      "command": "node",
      "args": ["./mcps/regen-koi-mcp/dist/index.js"],
      "env": {
        "KOI_API_ENDPOINT": "https://regen.gaiaai.xyz/api/koi",
        "JENA_ENDPOINT": "https://regen.gaiaai.xyz/api/koi/fuseki/koi/sparql"
      },
      "description": "Knowledge graph access - 49,169 documents, 28,489 code entities"
    },
    "regen-network": {
      "command": "uv",
      "args": [
        "run",
        "--directory",
        "./mcps/regen-python-mcp",
        "python",
        "main.py"
      ],
      "env": {
        "PYTHONPATH": "./mcps/regen-python-mcp/src",
        "REGEN_MCP_LOG_LEVEL": "INFO"
      },
      "description": "Blockchain queries - 45+ tools for live on-chain data"
    },
    "regen": {
      "command": "node",
      "args": ["./mcps/mcp/server/dist/index.js"],
      "env": {
        "NODE_ENV": "production",
        "REGEN_RPC_ENDPOINT": "https://regen-rpc.publicnode.com:443"
      },
      "description": "Legacy TypeScript ledger access"
    }
  }
}
```

**Note:** Use absolute paths (replace `./` with full paths like `/home/user/regen-mcps/mcps/...`) if you encounter connection issues.

**Step 4: Start Claude Code**

```bash
cd regen-mcps
claude
```

Inside Claude, verify all servers are connected:
```
> /mcp
```

Expected output:
```
MCP Server Status:
- regen-koi: connected (23 tools)
- regen-network: connected (45 tools)
- regen: connected (12 tools)
```

### The Multi-MCP Advantage

With all three servers connected, you can ask questions that would be impossible with a single data source:

**Query spanning knowledge + blockchain:**
```
"Explain the Terrasos methodology using KOI docs, then show me
the actual on-chain issuances for BT01 credits using the ledger."
```

Claude will:
1. Query `regen-koi` for methodology documentation
2. Extract relevant passages with source citations
3. Query `regen-network` for live BT01 credit data
4. Present both semantic context and verified blockchain state
5. Distinguish clearly between documented intent and on-chain reality

**Verification workflow:**
```
"Search KOI for all mentions of 'ERA Brazil', then verify which
projects have actually issued credits on-chain."
```

Claude orchestrates:
- `query_code_graph` → finds USS01 references
- `search_knowledge` → retrieves forum posts and documentation
- `list_credit_batches` → confirms 77,988 credits issued across 4 batches
- Cross-references knowledge claims against blockchain evidence

This is the difference between ecohyperstition (plausible-sounding fabrications) and regenerative intelligence (knowledge grounded in verifiable sources).

### Troubleshooting

**Server shows "disconnected":**
- Check that paths in `.mcp.json` are absolute
- Verify Node.js (v20+) and Python (3.10+) are installed
- For Python servers, ensure `uv` is in your PATH: `which uv`
- Restart Claude Code completely (not just `/clear`)

**Tools not appearing:**
- Confirm `.claude/settings.json` exists with `enableAllProjectMcpServers: true`
- Check for JSON syntax errors: `python -m json.tool .mcp.json`
- Enable debug mode: `claude --mcp-debug`

**Network errors:**
- Test endpoints manually: `curl https://regen.gaiaai.xyz/api/koi`
- Check firewall settings for outbound HTTPS
- Verify you're not behind a restrictive corporate proxy

---

## ChatGPT (Knowledge Access)

ChatGPT Custom GPTs can access Regen KOI through an HTTP REST API proxy. This provides semantic search capabilities but **not live blockchain access**.

### Launch the Regen KOI GPT

![koi-gpt-landing-page|690x400](upload://koi-gpt-landing-page.png)

**Direct link:** [Launch Regen KOI GPT →](https://chatgpt.com/g/g-67605ebed10c8191a1e91dfbf63e1ade-regen-koi-gpt)

Requires ChatGPT Plus subscription ($20/month).

### What It Can Do

**Semantic Search:**
- Query 49,169 documents in the knowledge graph
- Find forum discussions, methodology specifications, governance proposals
- Explore code relationships across 7 repositories
- Retrieve historical context from past conversations

**Methodology Exploration:**
- Explain credit class methodologies in accessible language
- Compare different verification approaches
- Trace governance decisions through forum history
- Identify experts who've contributed to specific topics

**Example Queries:**
```
"What discussions have happened about biodiversity monitoring methodologies?"
"Explain the difference between CarbonPlus Grasslands and Ecometric Soil Carbon approaches"
"Who are the key contributors to governance proposal #47?"
```

### What It Cannot Do

**Live Blockchain Data:**
- Cannot query current credit balances
- Cannot verify on-chain transactions
- Cannot check real-time marketplace orders
- Cannot access governance voting status

**Real-Time Prices:**
- Cannot fetch current market prices
- Cannot calculate portfolio values
- Cannot track price changes over time

**Transaction Execution:**
- Cannot buy, sell, or retire credits
- Cannot interact with smart contracts
- Cannot sign blockchain transactions

### The Hallucination Warning

![koi-gpt-tool-call-confirmation|690x400](upload://koi-gpt-tool-call-confirmation.png)

The GPT will attempt to indicate when it lacks access to requested data. However, the [ecohyperstition incident](/home/ygg/Workspace/RegenAI/regenai-forum-content/docs/other/2025-12-09-koi-gpt-hallucination.md) demonstrates this isn't foolproof:

**What happened:**
- User asked for "total credits live on Regen Ledger right now"
- GPT generated detailed tables with specific numbers
- Cited non-existent block explorer (`regen.aneka.io`)
- Claimed 7.5M credits when actual on-chain total was 1.04M
- Fabricated credit class IDs that don't exist

**Why it happened:**
- GPT has knowledge access (documentation) but not state access (blockchain)
- Language models generate plausible-sounding responses when uncertain
- No direct verification mechanism against on-chain data
- Confidence tone doesn't correlate with factual accuracy

**How to protect yourself:**

1. **Verify blockchain claims independently:**
   - Use [Regen Registry Explorer](https://registry.regen.network)
   - Cross-check with Claude Code + Ledger MCP
   - Look for source citations (not just "verified via...")

2. **Recognize capability boundaries:**
   - GPT knows **about** things (documentation, discussions)
   - GPT doesn't know **current state** (balances, prices, live data)
   - Treat numbers as estimates requiring verification

3. **Watch for warning signs:**
   - Specific transaction hashes or batch IDs (GPT can't generate these)
   - Real-time price data (GPT can't access exchanges)
   - Exact on-chain balances (GPT can't query blockchain)
   - URLs to tools it can't actually access

![koi-gpt-governance-search-results|690x400](upload://koi-gpt-governance-search-results.png)

### Best Use Cases

The Regen KOI GPT excels at:
- Research and discovery across historical documents
- Understanding regenerative finance concepts
- Finding relevant governance discussions
- Exploring methodology documentation
- Identifying community experts and contributors

Use it as a **knowledge assistant**, not a **data oracle**.

---

## Eliza (Autonomous Agents)

For developers building autonomous agents that can operate independently, Eliza provides a full-stack framework with MCP integration capabilities.

### What is Eliza?

ElizaOS is an open-source TypeScript framework for building AI agents with:
- Persistent personalities and memory
- Multi-agent coordination
- Plugin architecture for extending capabilities
- Native blockchain integration
- Support for Discord, Telegram, Twitter, and more

### The Regen Registry Agent

**Repository:** [github.com/gaiaaiagent/GAIA/tree/regen-assistant-avatar](https://github.com/gaiaaiagent/GAIA/tree/regen-assistant-avatar)

**Demo:** [Loom walkthrough](https://www.loom.com/share/53284fd4cf984447b8758e8d615418eb)

This agent demonstrates:
- MCP integration for accessing Regen data
- Autonomous document review workflows
- Multi-step reasoning and decision-making
- Integration with internal systems

### Quick Start

**Prerequisites:**
- Node.js 23+
- Python 3.10+
- bun or npm

**Installation:**
```bash
# Clone the repository
git clone https://github.com/gaiaaiagent/GAIA.git
cd GAIA
git checkout regen-assistant-avatar

# Install dependencies
bun install

# Configure environment
cp .env.example .env
# Edit .env with your API keys

# Start the agent
bun run dev
```

### MCP Integration

Eliza agents connect to Regen MCPs through the `@fleek-platform/eliza-plugin-mcp` plugin:

```typescript
// Character configuration
const character = {
  name: "RegenAgent",
  plugins: [
    "@elizaos/plugin-bootstrap",
    "@fleek-platform/eliza-plugin-mcp"
  ],
  settings: {
    mcpServers: {
      "regen-koi": {
        type: "http",
        endpoint: "https://regen.gaiaai.xyz/api/koi"
      }
    }
  }
}
```

### Why Eliza for Regen?

**Autonomous Operation:**
- Agents can monitor data feeds continuously
- Execute multi-step workflows without human intervention
- Make decisions based on predefined strategies

**Multi-Agent Coordination:**
- Specialized agents for different tasks (monitoring, analysis, verification)
- Agents can delegate to other agents
- Consensus mechanisms for high-stakes decisions

**Blockchain Native:**
- Direct wallet integration for transactions
- Smart contract interactions
- Cross-chain capabilities via IBC

### Coming Next Week

**Deep Dive: Registry Review Agent**

Next week's post will explore:
- The 7-stage automated review workflow
- How AI extracts evidence from project documents
- Human-in-the-loop verification patterns
- Transforming 6-8 hour reviews into 90-minute processes

The Registry Review Agent represents the frontier of AI-augmented expertise—using automation to handle tedious extraction work while keeping human judgment at the center of verification decisions.

### Learning Resources

**Eliza Documentation:**
- [Official Docs](https://elizaos.github.io/eliza/docs/intro)
- [Plugin Development Guide](https://developers.flow.com/blockchain-development-tutorials/use-AI-to-build-on-flow/agents/eliza/build-plugin)
- [MCP Integration Guide](https://resources.fleek.xyz/blog/announcements/fleek-eliza-mcp-plugin/)

**Community:**
- [Eliza Discord](https://discord.gg/elizaos)
- [Regen AI Forum](https://forum.regen.network/c/regen-ai)

---

## Platform Comparison

| Feature | Claude Code | ChatGPT GPT | Eliza Agent |
|---------|-------------|-------------|-------------|
| **MCP Support** | Native JSON-RPC | HTTP Proxy | Plugin-based |
| **Multi-MCP** | ✅ Orchestrates multiple | ❌ Single endpoint | ✅ Multiple connections |
| **Knowledge Access** | ✅ Full KOI | ✅ Full KOI | ✅ Full KOI |
| **Blockchain Access** | ✅ Live queries | ❌ No | ✅ Direct wallet |
| **Setup Time** | 30 seconds - 5 minutes | Instant | 5-15 minutes |
| **Cost** | Free (needs Anthropic key) | $20/month | Free (needs API keys) |
| **Autonomy** | Interactive | Interactive | Autonomous |
| **Best For** | Development & research | Quick exploration | Production automation |

### Choosing Your Path

**Start with ChatGPT if:**
- You need instant access with zero setup
- You're exploring documentation and governance history
- You want conversational knowledge search
- You won't be querying live blockchain data

**Use Claude Code if:**
- You're building or researching seriously
- You need both knowledge and blockchain access
- You want to verify GPT claims against on-chain data
- You're comfortable with terminal/CLI tools

**Build with Eliza if:**
- You're a developer creating autonomous systems
- You need agents that run continuously
- You're integrating with Discord/Telegram/Twitter
- You want multi-agent coordination

---

## What's Next

Now that you're connected, what can you do?

**Week 4 Preview:** Next week, we dive deep into the **Registry Review Agent**—the internal tool that's transforming how Regen Network reviews ecological credit project proposals. We'll explore:

- The 7-stage review workflow (from eligibility to final verification)
- Document discovery and evidence extraction techniques
- How AI augments (not replaces) human expertise
- Reducing 6-8 hour manual reviews to 90-minute guided workflows
- The architecture that makes it work (Registry Review MCP)

The Registry Review Agent represents the frontier of AI-augmented professional work—where automation handles the tedious parts so humans can focus on judgment.

---

**Resources Referenced:**

- [Regen KOI MCP Repository](https://github.com/gaiaaiagent/regen-koi-mcp)
- [Regen Python MCP Repository](https://github.com/gaiaaiagent/regen-python-mcp)
- [Regen Ledger MCP Repository](https://github.com/regen-network/mcp)
- [Registry Review Agent Demo](https://www.loom.com/share/53284fd4cf984447b8758e8d615418eb)
- [Claude Code MCP Documentation](https://code.claude.com/docs/en/mcp)
- [Eliza Framework Documentation](https://elizaos.github.io/eliza/docs/intro)
- [MCP Protocol Specification](https://modelcontextprotocol.io)

---

*The difference between knowledge and wisdom is verification. Choose your connection path, but always verify blockchain claims against the source of truth.*
