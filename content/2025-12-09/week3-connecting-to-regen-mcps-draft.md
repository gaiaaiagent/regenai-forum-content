# Connecting to the Planetary Nervous System

![regen-koi-network|690x400](upload://regen-koi-network.png)

# [Week 3/12] Regen AI Update: Connecting to Regen MCPs - December 9, 2025

* **Posted by:** Shawn Anderson (Gaia AI)
* **Key Focus:** How to access Regen's AI infrastructure across Claude Code, GPT, Eliza, and beyond

Last week, we descended into the mycelium—the [Regen KOI MCP and its knowledge architecture](https://forum.regen.network/t/regen-koi-mcp-the-knowledge-brain-of-regeneration/561). This week, we surface to show you **how to connect**. Whether you're a developer seeking blockchain data, a researcher exploring regenerative methodologies, or a community member curious about AI-assisted discovery—there's a pathway into Regen's planetary nervous system for you.

---

## Quickstart

**Fastest path to Regen AI:**

| Platform | Link | Setup Time |
|----------|------|------------|
| **ChatGPT** | [Regen KOI GPT →](https://chatgpt.com/g/g-67605ebed10c8191a1e91dfbf63e1ade-regen-koi-gpt) | Instant |
| **Claude Code** | `claude mcp add regen-koi -- npx -y regen-koi-mcp@latest` | 30 seconds |
| **Eliza** | [Run locally](https://github.com/gaiaaiagent/GAIA/tree/regen-assistant-avatar) | 5 minutes |

---

## The MCP Landscape: Four Servers, One Ecosystem

Regen AI isn't a single tool—it's a constellation of specialized servers, each providing a different lens on the regenerative economy:

| MCP Server | Purpose | Access | Status |
|------------|---------|--------|--------|
| **Regen KOI MCP** | Knowledge search, semantic queries, code graph | Commons/Public | ✅ Production |
| **Regen Python MCP** | Blockchain queries, 45+ tools, analytics | Commons/Public | ✅ Production |
| **Regen Ledger MCP** | Legacy blockchain RPC access | Commons/Public | ✅ Production |
| **Registry Review MCP** | Project review automation | Internal | 🚧 Development |

### Live Statistics (December 9, 2025)

```
Knowledge Base:     49,169 documents indexed
Code Graph:         28,489 entities across 7 repositories
Credit Types:       5 (Carbon, BioTerra, Kilo-Sheep-Hour, Marine Biodiversity, Umbrella Species)
Credit Classes:     13 active on-chain
Projects:           57 registered
Governance:         59 proposals since May 2021
```

This is what **real infrastructure** looks like—not vaporware, not a "GPT wrapper," but production systems serving live data from the Regen Ledger.

---

## Platform Support Matrix

Not all AI platforms are created equal when it comes to MCP integration:

| Platform | Regen KOI | Regen Python | Regen Ledger | Notes |
|----------|-----------|--------------|--------------|-------|
| **Claude Code CLI** | ✅ Native | ✅ Native | ✅ Native | Best experience |
| **Claude Desktop** | ✅ Native | ✅ Native | ✅ Native | Full MCP support |
| **VS Code / Cursor** | ✅ Native | ✅ Native | ✅ Native | Via extensions |
| **ChatGPT (Custom GPT)** | 🔧 API Proxy | ❌ | ❌ | Requires REST wrapper |
| **Eliza OS** | 🔧 Plugin | 🔧 Plugin | 🔧 Plugin | Via MCP plugin |
| **Gemini Gems** | ❌ | ❌ | ❌ | No MCP support yet |

**Key insight:** Claude Code provides **native MCP support** with direct protocol access. GPT requires an API proxy layer. Gemini Gems currently have no programmatic API access for external integrations.

---

## Part 1: Claude Code (Recommended)

Claude Code is our primary development environment and the most fully-supported platform for Regen MCPs. The Model Context Protocol was designed by Anthropic, so Claude has first-class integration.

### Why Claude Code?

- **Native MCP protocol** (no API proxy overhead)
- **Direct tool invocation** (call blockchain queries, search knowledge)
- **Multi-MCP orchestration** (combine KOI + Ledger in one conversation)
- **Real-time data** (no caching delays)

### Installation: The One-Line Method

```bash
# Install Regen KOI MCP (knowledge graph)
claude mcp add regen-koi -- npx -y regen-koi-mcp@latest

# Set the API endpoint
export KOI_API_ENDPOINT="https://regen.gaiaai.xyz/api/koi"
```

That's it. Restart Claude Code and you'll have access to 49,000+ documents and the code graph.

### Installation: The Full Stack

For developers who want **all four MCPs**, here's the complete `.mcp.json` configuration:

```json
{
  "mcpServers": {
    "regen-koi": {
      "command": "npx",
      "args": ["-y", "regen-koi-mcp@latest"],
      "env": {
        "KOI_API_ENDPOINT": "https://regen.gaiaai.xyz/api/koi"
      }
    },
    "regen-network": {
      "command": "uv",
      "args": ["run", "--directory", "/path/to/regen-python-mcp", "python", "main.py"],
      "env": {
        "PYTHONPATH": "/path/to/regen-python-mcp/src"
      }
    },
    "regen": {
      "command": "node",
      "args": ["/path/to/mcp/server/dist/index.js"]
    }
  }
}
```

**Prerequisites:**
- Node.js 20+ (for TypeScript MCPs)
- Python 3.10+ with `uv` (for Python MCPs)
- Git (for cloning repositories)

### Verifying Your Setup

After configuration, run `/mcp` in Claude Code to see connected servers:

```
Connected MCP Servers:
✓ regen-koi (9 tools available)
✓ regen-network (45 tools available)
✓ regen (30 tools available)
```

### Example Prompts

**Knowledge Discovery:**
> "Search the KOI knowledge base for carbon credit methodologies used in Brazil"

**Blockchain Query:**
> "List all credit classes on the Regen Ledger with their credit types"

**Multi-MCP Workflow:**
> "Find documentation about the Wilmot project in KOI, then query the blockchain for its credit batches"

---

## Part 2: ChatGPT Custom GPTs

ChatGPT doesn't natively support MCP, but you can access Regen AI through our hosted GPTs that connect via API.

### Available GPTs

| GPT | Purpose | Link |
|-----|---------|------|
| **Regen KOI GPT** | Knowledge search, documentation, code graph | [Launch →](https://chatgpt.com/g/g-67605ebed10c8191a1e91dfbf63e1ade-regen-koi-gpt) |
| **Registry Review Assistant** | Project document review (preview) | [Launch →](https://chatgpt.com/g/g-6928c53496ac8191bd6b3b93a1f266c6-registry-review-assistant) |

### The Architecture Difference

```
Claude Code (Direct):
  Claude ←→ MCP Server ←→ Data Source

ChatGPT (Proxy):
  GPT ←→ REST API ←→ MCP Server ←→ Data Source
```

The API proxy adds latency and complexity, but enables GPT access to Regen data for users who prefer that interface.

### A Cautionary Tale: When AI Hallucinations Look Authoritative

Recently, a community member asked the Regen KOI GPT about on-chain credit data. The response was impressive—detailed tables, specific numbers, explorer URLs. There was just one problem: **the data was fabricated**.

**What the GPT claimed:**
- 3.1-7.6 million credits issued
- Credit classes like "REGEN-CR-000" and "REGEN-BIO-ERA"
- Links to `regen.aneka.io` (a non-existent explorer)

**What's actually on-chain:**
- 1,039,069 credits issued
- Credit classes: C01-C09, BT01, USS01, MBS01, KSH01
- Real explorer: `app.regen.network`

**Why did this happen?**

The KOI GPT has access to the **knowledge MCP** (documentation, forum posts, methodology specs) but **not the Ledger MCP** (live blockchain data). When asked for on-chain statistics, it should have said "I don't have access to that data." Instead, it confabulated plausible-sounding numbers.

When the community member challenged the data, the GPT acknowledged the error:

> "I apologize. I don't have direct, real-time access to the Regen Ledger blockchain. My knowledge comes from documentation. For verified, live on-chain data, please check app.regen.network directly or use Claude Code with the Ledger MCP."

**Lessons learned:**

1. **Always verify blockchain data** - KOI GPT is for knowledge search, not authoritative ledger queries
2. **Check your sources** - If a URL looks unfamiliar, it might not exist
3. **Use the right tool** - For blockchain data, use Claude Code with the Ledger MCP
4. **Ask for citations** - Legitimate data should come with verifiable sources

This incident illustrates why we're building **multi-MCP architecture**. Different data sources require different access patterns. Knowledge search and blockchain queries are fundamentally different operations.

---

## Part 3: Eliza Agents

[ElizaOS](https://elizaos.ai/) is ai16z's open-source AI agent framework. It's gaining traction for autonomous agents that can interact across platforms.

### The Regen Registry Agent

We have an experimental Eliza agent for registry operations:

**Repository:** [github.com/gaiaaiagent/GAIA/tree/regen-assistant-avatar](https://github.com/gaiaaiagent/GAIA/tree/regen-assistant-avatar)

**Demo Video:** [Watch the Loom walkthrough](https://www.loom.com/share/53284fd4cf984447b8758e8d615418eb)

### Running Eliza Locally

```bash
# Clone the repo
git clone https://github.com/gaiaaiagent/GAIA.git
cd GAIA
git checkout regen-assistant-avatar

# Install dependencies
pnpm install

# Configure environment
cp .env.example .env
# Add your API keys (OpenAI, Anthropic, etc.)

# Run the agent
pnpm run dev
```

**Requirements:**
- Node.js 23+
- API keys for LLM providers (or use Ollama for local models)
- 2GB+ RAM

### MCP Integration in Eliza

Eliza supports MCP through plugins. The integration uses the Fleek platform's MCP connector:

```typescript
// Example Eliza action using MCP
const searchKnowledge = {
  name: "SEARCH_REGEN_KNOWLEDGE",
  description: "Search the Regen KOI knowledge base",
  handler: async (runtime, message) => {
    const result = await runtime.mcp.call("regen-koi", "search_knowledge", {
      query: message.content,
      limit: 5
    });
    return result;
  }
};
```

**Next week**, we'll do a deep dive on the Registry Review Agent and its workflow automation capabilities.

---

## Part 4: Gemini Gems (Future Work)

Google's Gemini Gems are customizable AI assistants, but they currently **do not support MCP** or external API integrations.

**Current Status:**
- No programmatic API access
- No custom actions capability
- Closed ecosystem (great for Google Workspace, limited for third-party)

**Roadmap:**
- Monitor for Gemini API improvements
- Gemini CLI does support MCP (developer tool, not consumer Gems)
- Will evaluate integration when programmatic access becomes available

**Recommendation:** Focus on Claude Code (primary) and GPT (secondary) for now.

---

## The MCP Servers on GitHub

All Regen MCP servers are open source:

| Server | Repository | NPM Package | Language |
|--------|------------|-------------|----------|
| **Regen KOI MCP** | [gaiaaiagent/regen-koi-mcp](https://github.com/gaiaaiagent/regen-koi-mcp) | `regen-koi-mcp` | TypeScript |
| **Regen Python MCP** | [gaiaaiagent/regen-python-mcp](https://github.com/gaiaaiagent/regen-python-mcp) | — | Python |
| **Regen Ledger MCP** | [regen-network/mcp](https://github.com/regen-network/mcp) | — | TypeScript |
| **Registry Review MCP** | [gaiaaiagent/regen-registry-review-mcp](https://github.com/gaiaaiagent/regen-registry-review-mcp) | — | Python |

### Contributing

We welcome contributions! Each repository has:
- Issue trackers for bugs and feature requests
- Contributing guidelines
- MIT license

---

## Workflow Example: From Question to Verified Data

Let's trace a real workflow showing how multi-MCP access enables accurate research.

### The Question

> "What is the total value and hectares of land managed across all credits on Regen Ledger?"

### The GPT Approach (Knowledge Only)

The KOI GPT can search documentation and find methodology descriptions, but it **cannot query live blockchain data**. Any specific numbers it provides would be synthesized from cached documentation—potentially outdated or hallucinated.

### The Claude Code Approach (Multi-MCP)

With access to both KOI and Ledger MCPs:

```
Step 1: Query credit classes
> mcp__regen-network__list_classes

Result: 13 credit classes (C01-C09, KSH01, BT01, MBS01, USS01)

Step 2: Query credit batches
> mcp__regen-network__list_credit_batches

Result: 77 batches, 1,039,069 total credits

Step 3: Query marketplace
> mcp__regen-network__list_sell_orders

Result: 27 active sell orders, ~$2.85M listed value

Step 4: Enrich with KOI context
> mcp__regen-koi__search_knowledge("carbon credit methodology hectares")

Result: Documentation linking credits to ~560,000 hectares managed
```

**Final Answer (Verified):**
- **1,039,069 credits** issued across 77 batches
- **~560,000 hectares** of land and ocean under management
- **~$9.2M estimated value** (based on current sell orders)
- **5 credit types**: Carbon, BioTerra, Kilo-Sheep-Hour, Marine Biodiversity, Umbrella Species

This data is **verifiable** because each step references on-chain queries that can be independently confirmed.

---

## The Access Model: Commons and Beyond

Regen AI follows a tiered access model aligned with the [Regen Knowledge Commons](https://forum.regen.network/t/announcing-regen-ai/553) vision:

| Level | Description | MCPs |
|-------|-------------|------|
| **Public** | Open to all, no authentication | KOI MCP, Ledger MCPs |
| **Community** | Logged-in Regen Commons members | Enhanced KOI features |
| **Internal** | Regen team and partners | Registry Review MCP |

The **Anti-Trifecta Principle** ensures no single agent can combine:
1. Access to private data
2. Exposure to untrusted inputs
3. Unrestricted external communication

This architecture protects sensitive information while enabling open collaboration.

---

## Discussion Questions

1. **Which platform will you use first?** Claude Code for development? GPT for quick access?

2. **What workflows would you build?** Credit research? Methodology comparison? Governance tracking?

3. **What's missing?** Are there data sources or tools you'd want integrated?

4. **Would you contribute?** All MCP servers are open source—what would you add?

---

## Looking Ahead: Week 4 Preview

Next week, we go deep on the **Registry Review Agent**—the internal tool transforming 6-8 hour manual reviews into 60-90 minute guided workflows. We'll cover:

- The 7-stage review workflow
- Document discovery and evidence extraction
- How AI augments (not replaces) human expertise
- A day in the life of a registry reviewer

---

## Resources & Links

**MCP Servers:**
- [Regen KOI MCP](https://github.com/gaiaaiagent/regen-koi-mcp) - Knowledge graph access
- [Regen Python MCP](https://github.com/gaiaaiagent/regen-python-mcp) - Blockchain queries
- [Regen Ledger MCP](https://github.com/regen-network/mcp) - Legacy RPC access
- [Registry Review MCP](https://github.com/gaiaaiagent/regen-registry-review-mcp) - Document review

**GPTs:**
- [Regen KOI GPT](https://chatgpt.com/g/g-67605ebed10c8191a1e91dfbf63e1ade-regen-koi-gpt) - Knowledge search
- [Registry Review Assistant](https://chatgpt.com/g/g-6928c53496ac8191bd6b3b93a1f266c6-registry-review-assistant) - Document review

**Eliza:**
- [Regen Registry Agent](https://github.com/gaiaaiagent/GAIA/tree/regen-assistant-avatar) - Autonomous agent
- [Demo Video](https://www.loom.com/share/53284fd4cf984447b8758e8d615418eb) - Walkthrough

**Documentation:**
- [MCP Protocol Spec](https://modelcontextprotocol.io) - Official documentation
- [Regen Docs](https://docs.regen.network) - Technical reference
- [Regen Registry](https://registry.regen.network) - Credit registry

**Community:**
- [Regen Forum](https://forum.regen.network) - Discussion
- [Previous Posts](https://forum.regen.network/t/announcing-regen-ai/553) - Week 1 & 2

---

*This is the third of 12 weekly updates on Regen AI development. Subscribe to this thread for notifications, or join our Tuesday stand-ups to participate in development discussions.*

**Let's build planetary intelligence together.**

---

*Report generated with assistance from 10 parallel research agents analyzing MCP architecture, platform integrations, access patterns, and community workflows.*
