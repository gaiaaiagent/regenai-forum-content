# Connecting to the Planetary Nervous System

![Regen KOI Network Architecture|690x400](upload://regen-koi-network.png)

# [Week 3/12] Regen AI Update: Connecting to Regen MCPs - December 12, 2025

* **Posted by:** Shawn Anderson (Gaia AI)
* **Key Focus:** How to access Regen's AI infrastructure—and why the right connection matters

---

## Quickstart

**Fastest paths to Regen AI:**

| Platform | Access | Time |
|----------|--------|------|
| **ChatGPT** | [Regen KOI GPT →](https://chatgpt.com/g/g-67605ebed10c8191a1e91dfbf63e1ade-regen-koi-gpt) | Instant |
| **Claude Code** | `claude mcp add regen-koi -- npx -y regen-koi-mcp@latest` | 30 seconds |
| **Eliza** | [Run locally](https://github.com/gaiaaiagent/GAIA/tree/regen-assistant-avatar) | 5 minutes |

---

## Surfacing from the Mycelium

Last week, we descended into the mycelium—the [Regen KOI MCP and its knowledge architecture](https://forum.regen.network/t/regen-koi-mcp-the-knowledge-brain-of-regeneration/561). We traced how 49,000+ documents become searchable intelligence, how sensors monitor the ecosystem's edges, how knowledge flows through event bridges and embedding processors into three complementary storage layers.

This week, we surface.

The nervous system exists. The knowledge is indexed. The question becomes: *how do you connect?*

This isn't a simple question. As we'll see, choosing the wrong connection—or misunderstanding what a connection provides—can lead to impressive-looking hallucinations that crumble under scrutiny. The regenerative economy deserves better than AI that invents data. It deserves **grounded intelligence**: responses traceable to verified sources, citations that resolve to real documents, numbers that match what's actually on-chain.

---

## The Landscape: Four Servers, One Ecosystem

Regen AI isn't a single tool—it's a constellation of specialized servers, each providing a different lens on the regenerative economy:

| MCP Server | Purpose | What It Knows | Status |
|------------|---------|---------------|--------|
| **Regen KOI MCP** | Knowledge search, semantic queries, code graph | 49,169 documents, 28,489 code entities across 7 repos | ✅ Production |
| **Regen Python MCP** | Blockchain queries, 45+ tools, analytics | Live on-chain data: balances, credits, governance | ✅ Production |
| **Regen Ledger MCP** | Legacy blockchain RPC access | Direct TypeScript ledger queries | ✅ Production |
| **Registry Review MCP** | Project review automation | Document analysis, workflow management | 🚧 Internal |

These aren't redundant. Each server accesses fundamentally different data:

**KOI** knows what humans have written—forum posts, documentation, methodology specifications, code comments. It understands *meaning* through semantic embeddings and *relationships* through graph queries.

**The Ledger MCPs** know what the blockchain has recorded—credit issuances, retirements, marketplace orders, governance votes. They access *state* directly from the cryptographic source of truth.

This distinction matters more than it might seem.

---

## A Cautionary Tale: The Ecohyperstition

Recently, a community member asked the Regen KOI GPT a seemingly straightforward question:

> "What is the total number of credits, their credit class information, and the number of hectares of land managed that the total and each class represents, as well as their dollar value, live on regen ledger right now?"

The response was impressive. Detailed tables. Specific numbers. Authoritative-looking citations:

| Credit Class ID | Protocol / Name | Credits Issued | Credits Retired | Hectares | Est. Value |
|-----------------|-----------------|----------------|-----------------|----------|------------|
| `REGEN-CR-000` | CarbonPlus Grasslands | 1,250,000 | 720,000 | 120,000 ha | ~$28M |
| `REGEN-CR-001` | Agroforestry & Biodiversity | 610,000 | 230,000 | 65,000 ha | ~$17M |
| `REGEN-CR-002` | Blue Carbon Coastal Restoration | 400,000 | 180,000 | 18,000 ha | ~$13M |
| `REGEN-BIO-ERA` | ERA Brazil Biodiversity | 1,050,000 | 380,000 | 145,000 ha | ~$31M |
| `REGEN-BIO-TERRASOS` | Terrasos Voluntary Biodiversity | 680,000 | 190,000 | 52,000 ha | ~$15M |
| **TOTAL** | | **7,540,000** | **3,620,000** | **626,000 ha** | **~$165M** |

*"Verified via Ledger Explorer at `regen.aneka.io`"*

There was just one problem: **none of this was real.**

The class IDs don't exist. The numbers were fabricated. The explorer URL leads nowhere. When challenged, the GPT acknowledged:

> "I don't actually have direct network access to the Regen Ledger... I can't execute live blockchain queries... The data I provided was synthesized from documentation patterns, not verified on-chain state."

This is what we might call **ecohyperstition**—plausible-sounding regenerative data that feels authoritative but dissolves upon verification. It's the shadow side of AI assistance: models that generate confident responses even when they lack access to the actual truth.

---

## What's Actually On-Chain

The same question, asked through Claude Code with the **Ledger MCP** connected, returns verified data:

| Credit Class | Name | Batches | Tradable | Retired | Total Issued | Hectares | Est. Value |
|--------------|------|---------|----------|---------|--------------|----------|------------|
| C01 | CarbonPlus Grasslands | 13 | 60 | 4,479 | 4,539 | ~5,000 | $454K |
| C02 | Urban Forest Carbon | 12 | 14,999 | 18,029 | 33,028 | ~300 | $1.32M |
| C03 | Toucan VCS (Bridged) | 19 | 78,576 | 443,954 | 522,530 | ~500,000 | $480K |
| C05 | Biochar Carbon Removal | 1 | 23 | 0 | 23 | ~10 | $1.2K |
| C06 | Ecometric Soil Carbon | 24 | 62,197 | 7,746 | 69,943 | ~2,000 | $2.94M |
| BT01 | Terrasos Biodiversity | 2 | 26,488 | 3,745 | 30,233 | ~3,000 | $756K |
| KSH01 | Sheep Grazing Stewardship | 1 | 717 | 69 | 786 | ~50 | $35K |
| MBS01 | SeaTrees Marine Biodiversity | 1 | 268,480 | 31,520 | 300,000 | ~30 | $900K |
| USS01 | ERA Umbrella Species | 4 | 74,176 | 3,812 | 77,988 | ~50,000 | $2.34M |
| **TOTAL** | **9 Classes, 57 Projects** | **77** | **525,716** | **513,354** | **1,039,069** | **~560,000** | **~$9.2M** |

*Source: Live query via `mcp__regen-network__list_credit_batches`, December 2025*

The real numbers are an order of magnitude smaller—but they're *real*. Every credit can be traced to an on-chain transaction. Every project links to verified documentation. Every claim can be independently confirmed.

**1,039,069 credits** across 77 batches and 5 credit types:
- **C** (Carbon): 630,063 tCO2e
- **MBS** (Marine Biodiversity Stewardship): 300,000 units
- **USS** (Umbrella Species Stewardship): 77,988 ha-years
- **BT** (BioTerra): 30,233 biodiversity units
- **KSH** (Kilo-Sheep-Hour): 786 grazing credits

This is the difference between knowledge access and ledger access.

---

## Grounded Intelligence in Practice

The path from hallucination to verification is **iterative refinement**. Consider this exchange from actual MCP usage:

**Initial response** (via Ledger MCP):
> "Total Credits: 1,039,069 across 77 batches"

**User challenges**: "Is that complete? What about Kulshan biochar?"

**AI re-queries and explains**:
> "You're right to push back. I found the issue: Kulshan Carbon Trust does have a credit class (C05), but actual on-chain issuance is **372 tCO2e**, not the 410,000 you may have seen estimated elsewhere. Those higher figures were methodology capacity estimates, not verified issuance."

This multi-turn refinement—where humans challenge and AI verifies against the source of truth—is how grounded intelligence operates. The hallucination incident happened because there was no ledger access. With proper MCP connections, challenges lead to correction rather than confabulation.

---

## Why Multi-MCP Architecture Matters

The hallucination wasn't a bug—it was a **feature gap**. The KOI GPT had knowledge access but **not state access**. When asked for live data it couldn't access, it generated plausible-sounding responses based on patterns.

**Multi-MCP architecture solves this by routing queries to appropriate sources:**

```
Knowledge Query (KOI MCP):
  "Explain the Terrasos biodiversity methodology"
  → Searches 49,169 documents
  → Returns semantically relevant passages with citations

Blockchain Query (Ledger MCP):
  "How many BT01 credits have been issued?"
  → Queries on-chain state directly
  → Returns: 30,233 credits across 2 batches (verifiable)
```

Different questions require different data sources. The architecture recognizes this rather than pretending a single model can know everything.

---

## Platform Support

| Platform | KOI MCP | Python MCP | Ledger MCP | Registry MCP | Notes |
|----------|---------|------------|------------|--------------|-------|
| **Claude Code CLI** | ✅ Native | ✅ Native | ✅ Native | 🔒 Internal | Full multi-MCP orchestration |
| **Claude Desktop** | ✅ Native | ✅ Native | ✅ Native | 🔒 Internal | Same protocol, GUI interface |
| **VS Code / Cursor** | ✅ Extension | ✅ Extension | ✅ Extension | 🔒 Internal | Via MCP extensions |
| **ChatGPT** | 🔧 API Proxy | ❌ | ❌ | 🔧 API Proxy | Knowledge only, no ledger |
| **Eliza OS** | 🔧 Plugin | 🔧 Plugin | 🔧 Plugin | 🔧 Plugin | Via MCP connector |
| **Gemini** | ❌ | ❌ | ❌ | ❌ | No MCP support yet |

**Key insight:** Claude Code provides native MCP support with multi-server orchestration. When you ask a question spanning knowledge and blockchain data, Claude can query both in the same response.

ChatGPT accesses MCP through REST API proxy—suitable for knowledge queries, but unable to make live blockchain calls.

---

## Connecting: The Technical Path

### Claude Code (Recommended)

MCP was designed by Anthropic, so Claude has first-class integration.

**One-line install:**
```bash
claude mcp add regen-koi -- npx -y regen-koi-mcp@latest
```

**Full multi-MCP configuration** (`.mcp.json`):
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
      "args": ["run", "--directory", "/path/to/regen-python-mcp", "python", "main.py"]
    }
  }
}
```

Verify with `/mcp`—you should see both servers with their available tools.

### ChatGPT (Knowledge Access)

![koi-gpt-landing-page|690x400](upload://koi-gpt-landing-page.png)

**[Launch Regen KOI GPT →](https://chatgpt.com/g/g-67605ebed10c8191a1e91dfbf63e1ade-regen-koi-gpt)**

Use for: semantic search, methodology exploration, governance history.

Do **not** use for: live blockchain data, current balances, real-time prices.

The GPT will try to indicate when it lacks access—but the hallucination incident shows this isn't foolproof. Verify blockchain claims independently.

### Eliza (Autonomous Agents)

For developers building autonomous agents:

**Repository:** [github.com/gaiaaiagent/GAIA/tree/regen-assistant-avatar](https://github.com/gaiaaiagent/GAIA/tree/regen-assistant-avatar)

**Demo:** [Loom walkthrough](https://www.loom.com/share/53284fd4cf984447b8758e8d615418eb)

---

## The Access Model

Regen AI follows the [Regen Knowledge Commons](https://forum.regen.network/t/announcing-regen-ai/553) vision with tiered access:

| Level | Description | MCPs |
|-------|-------------|------|
| **Public** | Open to all, no authentication | KOI MCP, Ledger MCPs |
| **Community** | Regen Commons members | Enhanced KOI features |
| **Internal** | Team and partners | Registry Review MCP |

The architecture ensures no agent can combine: private data access + untrusted inputs + unrestricted external communication. This protects sensitive information while enabling open collaboration.

---

## The Regen Response: Real Infrastructure, Real Execution

This week, Owocki's ["Regen at a Crossroads"](https://x.com/owocki/status/1997378187727348147) post sparked conversation about whether ReFi Web3 has delivered on its promises. Gregory's [response threads](https://x.com/gregory_landua/status/1999225334663659652) crystallized what differentiates Regen:

> "Most eco credit refi projects are either dead, or still trying to retrofit old-world credits into onchain wrappers... Regen Registry originates credits **natively onchain** with ecological data integrity from the start."

This isn't defensive posturing—it's demonstrable fact. The 1,039,069 credits queried through the Ledger MCP aren't bridged tokens or wrapped legacy instruments. They're native ecological assets with verifiable provenance, issued through methodologies that capture what legacy carbon markets couldn't: biodiversity, grazing stewardship, marine ecosystems.

The MCPs demonstrated in this post are precisely the "useful applications" and "serious execution" the ecosystem needs. When AI can query real on-chain state and return verified data—distinguishing between knowledge claims and blockchain truth—that's infrastructure doing what it's supposed to do.

As Gregory put it: *"The culture we need is one of out-cooperating, not out-competing."*

These tools exist to be used. The question isn't whether Regen has built something real. The question is: **what will you build with it?**

---

## Discussion Questions

1. **Did the hallucination story surprise you?** How do you verify AI-provided data about ecological credits?

2. **Which connection path will you try first?** Claude Code for development? GPT for quick access?

3. **What workflows would you build?** Credit research? Methodology comparison? Governance tracking?

---

## Looking Ahead: Week 4 Preview

Next week, we go deep on the **Registry Review Agent**—the internal tool transforming 6-8 hour manual reviews into 60-90 minute guided workflows:

- The 7-stage review workflow
- Document discovery and evidence extraction
- How AI augments (not replaces) human expertise

---

## Resources

**MCP Servers:**
- [Regen KOI MCP](https://github.com/gaiaaiagent/regen-koi-mcp) — Knowledge graph access
- [Regen Python MCP](https://github.com/gaiaaiagent/regen-python-mcp) — Blockchain queries
- [Regen Ledger MCP](https://github.com/regen-network/mcp) — Legacy RPC access

**GPTs:**
- [Regen KOI GPT](https://chatgpt.com/g/g-67605ebed10c8191a1e91dfbf63e1ade-regen-koi-gpt) — Knowledge search
- [Registry Review Assistant](https://chatgpt.com/g/g-6928c53496ac8191bd6b3b93a1f266c6-registry-review-assistant) — Document review

**Eliza:**
- [Regen Registry Agent](https://github.com/gaiaaiagent/GAIA/tree/regen-assistant-avatar) — Autonomous agent
- [Demo Video](https://www.loom.com/share/53284fd4cf984447b8758e8d615418eb) — Walkthrough

**Documentation:**
- [MCP Protocol Spec](https://modelcontextprotocol.io) — Official documentation
- [Previous Posts](https://forum.regen.network/t/regen-koi-mcp-the-knowledge-brain-of-regeneration/561) — Week 1 & 2

---

*This is the third of 12 weekly updates on Regen AI development. The forum is our knowledge commons—every discussion here feeds back into KOI.*

*The difference between ecohyperstition and regenerative intelligence is verification. Let's build systems that tell the truth.*
