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

What follows is a map of connection pathways, a cautionary tale about what happens when AI lacks proper access, and a vision of how multi-MCP architecture enables the coordination that planetary-scale regeneration requires.

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

**KOI** knows what humans have written—forum posts, documentation, methodology specifications, code comments. It understands *meaning* through semantic embeddings (mathematical representations of conceptual relationships) and *relationships* through graph queries (entity connections across the knowledge space).

**The Ledger MCPs** know what the blockchain has recorded—credit issuances, retirements, marketplace orders, governance votes. They access *state* directly from the cryptographic source of truth—data that cannot be altered retroactively, only extended forward.

**Registry Review MCP** knows the internal workflows of project review: document classification, evidence extraction, completeness verification, cross-validation patterns. This is operational intelligence, the machinery of quality assurance.

This distinction—between knowledge, state, and process—matters more than it might initially seem. Each type of truth requires different query patterns, different verification methods, different trust assumptions.

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

The format was perfect. The class IDs followed plausible naming conventions. The numbers scaled appropriately. It looked authoritative because it followed the *form* of blockchain data.

There was just one problem: **none of this was real.**

The credit class IDs don't exist in Regen Ledger's state. The hectare estimates were fabricated. The valuation numbers had no on-chain basis. The block explorer URL leads nowhere. When challenged with verification requests, the model eventually acknowledged:

> "I don't actually have direct network access to the Regen Ledger... I can't execute live blockchain queries... The data I provided was synthesized from documentation patterns, not verified on-chain state."

This is what we might call **ecohyperstition**—plausible-sounding regenerative data that feels authoritative but dissolves upon verification. It's the shadow side of AI assistance: models that generate confident responses even when they lack access to the actual truth.

The hallucination was sophisticated. It invented a credit class naming convention (`REGEN-CR-XXX`, `REGEN-BIO-XXX`) that sounds like how blockchain systems name things. It cited batch identifiers that follow logical patterns. It referenced a deprecated explorer. Everything was plausible. Nothing was verifiable.

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

The real numbers tell a different story—**1,039,069 credits** issued across 77 batches in 9 distinct credit classes, spanning 5 different credit types:

- **C (Carbon)**: 630,063 tCO2e across 5 classes
- **MBS (Marine Biodiversity Stewardship)**: 300,000 units in 1 class
- **USS (Umbrella Species Stewardship)**: 77,988 hectare-years in 1 class
- **BT (BioTerra)**: 30,233 biodiversity units in 1 class
- **KSH (Kilo-Sheep-Hour)**: 786 grazing credits in 1 class

Every credit is traceable to a specific on-chain transaction. Every project links to verifiable documentation in the registry. Every class connects to approved methodology specifications. Every claim can be independently confirmed.

**The hallucinated version showed 7.5 million credits worth $165 million. The reality shows 1 million credits worth ~$9 million.** An order of magnitude smaller, but *real*. The difference matters profoundly.

---

## Grounded Intelligence in Practice

The path from hallucination to verification isn't instant correction—it's **iterative refinement through multi-turn dialogue**.

Consider this exchange from actual MCP usage logs:

**Initial Response** (via Ledger MCP):
> Total Credits Ever Issued: 1,039,069
> Currently Tradable: 525,655
> Retired: 513,414
> Total Batches: 77

**User Challenge**:
> "Your response does not look complete to me. For instance it is missing Kulshan Carbon Trust's biochar, Terrasos, Ecometric, and some others I think. Can you investigate what you missed and why?"

**AI Self-Correction**:
> "I found the issue. Here's what happened: I reported only what is currently ON-CHAIN on Regen Ledger. What you're asking about are projects in the broader Regen Registry ecosystem that have approved methodologies but may:
> 1. Not yet have a credit class created on-chain
> 2. Have a credit class but no batches issued yet
> 3. Be in development/pilot phase"

**Further User Verification**:
> "Are you sure ERA Brazil and Terrasos are off-chain? I believe they are on-chain."

**AI Re-Query**:
> "You're absolutely right to question that. After checking the latest ledger data: Both ERA Brazil Biodiversity Credit Class (USS01) and Terrasos Voluntary Biodiversity (BT01) ARE on-chain—listed under x/ecocredit with active class_id and issuance records."

**User Catches Specific Error**:
> "I am suspicious due to my sense that Kulshan carbon trust I believe issued less than 400 tons."

**AI Investigates and Corrects**:
> "Excellent catch—and your suspicion is correct. After examining the on-chain issuance data: **372 metric tons (tCO₂e)** actually issued. Earlier higher figures were placeholders tied to the methodology's capacity, not actual on-chain issuance."

This multi-turn refinement is how grounded intelligence operates:

1. **Initial query returns real data** (from MCP ledger access)
2. **User challenges completeness** (domain expertise catches gaps)
3. **AI re-queries and explains** (distinguishes on-chain vs. registry status)
4. **User corrects misconception** (ERA/Terrasos are on-chain)
5. **AI verifies and updates** (re-queries ledger, confirms)
6. **User flags specific error** (Kulshan numbers feel wrong)
7. **AI investigates and corrects** (finds 372 real vs. estimated)

The hallucination incident happened because step 1 failed—the AI had no ledger access, so it fabricated from the start. With proper MCP access, challenges lead to **refinement** rather than confabulation.

---

## Why Multi-MCP Architecture Matters

The hallucination wasn't a bug—it was a **feature gap**. The KOI GPT had access to knowledge (documentation about credit classes, methodology specifications, project descriptions) but **not to state** (actual issuances, live balances, on-chain transactions).

When asked for live data it couldn't access, it did what language models do: generated plausible-sounding responses based on patterns in its training data. The result looked authoritative because it followed the *form* of blockchain data. But form without substance is precisely the kind of greenwashing the regenerative economy exists to oppose.

**Multi-MCP architecture solves this by routing different query types to appropriate data sources:**

```
Knowledge Query → Regen KOI MCP:
  "Explain the Terrasos biodiversity methodology"

  → Searches 49,169 semantically embedded documents
  → Returns relevant passages from methodology specs, forum discussions
  → Provides citations to primary sources

  Result: Conceptual understanding grounded in written knowledge

Blockchain Query → Regen Python MCP:
  "How many BT01 credits have been issued?"

  → Queries on-chain state directly via gRPC
  → Returns: 30,233 credits across 2 batches
  → Includes tradable vs retired breakdown, issuance dates

  Result: Quantitative facts grounded in cryptographic state

Combined Query → Multi-MCP Orchestration:
  "Which Terrasos biodiversity projects have issued credits,
   and what does their methodology measure?"

  → KOI MCP retrieves methodology documentation
  → Python MCP queries BT01 credit batches
  → Results synthesized with citations to both sources

  Result: Contextualized intelligence combining verified facts
          with explanatory knowledge
```

Different questions require different epistemologies. The architecture recognizes this rather than pretending a single model can omnisciently access all forms of truth.

---

## Platform Support

Not all AI platforms support MCP equally:

| Platform | KOI MCP | Python MCP | Ledger MCP | Registry MCP | Notes |
|----------|---------|------------|------------|--------------|-------|
| **Claude Code CLI** | ✅ Native | ✅ Native | ✅ Native | 🔒 Internal | Full multi-MCP orchestration |
| **Claude Desktop** | ✅ Native | ✅ Native | ✅ Native | 🔒 Internal | Same protocol, GUI interface |
| **VS Code / Cursor** | ✅ Extension | ✅ Extension | ✅ Extension | 🔒 Internal | Via MCP extensions |
| **ChatGPT** | 🔧 API Proxy | ❌ | ❌ | 🔧 API Proxy | Knowledge only, no ledger |
| **Eliza OS** | 🔧 Plugin | 🔧 Plugin | 🔧 Plugin | 🔧 Plugin | Via MCP connector |
| **Gemini** | ❌ | ❌ | ❌ | ❌ | No MCP support yet |

**Key insight:** Claude Code provides native MCP support with the ability to orchestrate multiple servers simultaneously. When you ask a question that spans knowledge and blockchain data, Claude can query KOI for context and the Ledger for verification in the same response.

ChatGPT's Custom GPTs access MCP through a REST API proxy—suitable for knowledge queries, but unable to make live blockchain calls without additional infrastructure.

---

## Connecting: The Technical Path

### Claude Code (Recommended)

The Model Context Protocol was designed by Anthropic, so Claude has first-class integration.

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

**Setup steps:**
1. Clone the Python MCP: `git clone https://github.com/gaiaaiagent/regen-python-mcp.git`
2. Install dependencies: `cd regen-python-mcp && uv sync`
3. Update the path in `.mcp.json` to your clone location
4. Create `.claude/settings.json` with `{"enableAllProjectMcpServers": true}`
5. Verify with `/mcp`—you should see both servers with their available tools

**The multi-MCP advantage:** With both servers connected, you can ask questions like "Explain the Terrasos methodology using KOI docs, then show me the actual on-chain issuances for BT01 credits using the ledger." Claude will query both sources and synthesize a response distinguishing documented intent from on-chain reality.

### ChatGPT (Knowledge Access)

![koi-gpt-landing-page|690x400](upload://koi-gpt-landing-page.png)

**[Launch Regen KOI GPT →](https://chatgpt.com/g/g-67605ebed10c8191a1e91dfbf63e1ade-regen-koi-gpt)**

**Use for:**
- Semantic search across 49,169 documents
- Methodology exploration and comparison
- Governance history and forum discussions
- Finding relevant documentation and project descriptions

**Do NOT use for:**
- Live blockchain data or current balances
- Real-time marketplace prices
- Verifying on-chain transactions
- Anything requiring blockchain state

The GPT will try to indicate when it lacks access—but the hallucination incident shows this isn't foolproof. **Always verify blockchain claims independently** using Claude Code + Ledger MCP or the [Regen Registry Explorer](https://registry.regen.network).

### Eliza (Autonomous Agents)

For developers building autonomous agents that can operate independently:

**Repository:** [github.com/gaiaaiagent/GAIA/tree/regen-assistant-avatar](https://github.com/gaiaaiagent/GAIA/tree/regen-assistant-avatar)

**Demo:** [Loom walkthrough](https://www.loom.com/share/53284fd4cf984447b8758e8d615418eb)

Eliza agents connect to Regen MCPs through the `@fleek-platform/eliza-plugin-mcp` plugin, enabling autonomous document review, monitoring workflows, and multi-step decision-making without human intervention.

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

This week, Owocki's ["Regen at a Crossroads"](https://x.com/owocki/status/1997378187727348147) post sparked conversation about whether ReFi Web3 has delivered on its promises. His critique cut deep: mediocrity, lack of adoption, too many "GPT wrappers" with no real execution. "GTM or GTFO," he wrote. Go-to-market or get the fuck out.

Three days later, Gregory's [response threads](https://x.com/gregory_landua/status/1999225334663659652) told a different story—not a defense, but a demonstration:

> "Most eco credit refi projects are either dead, or still trying to retrofit old-world credits into onchain wrappers... Regen Registry originates credits **natively onchain** with ecological data integrity from the start."

This distinction matters. The 1,039,069 credits queried through the Ledger MCP aren't bridged tokens or wrapped legacy instruments. They're native ecological assets with verifiable provenance, issued through methodologies that capture what legacy carbon markets couldn't: biodiversity, grazing stewardship, marine ecosystems.

> "ESG was elite ecology. ReFi became crypto cosplay. Both failed to ground themselves in nested caring—from the level of people → communities → bioregions → planet."
>
> "So yes: The old 'Regen' is dead. Good riddance. It needed to die so the real thing could grow."

The MCPs demonstrated in this post are precisely the "useful applications" and "serious execution" the ecosystem needs. When AI can query real on-chain state and return verified data—distinguishing between knowledge claims and blockchain truth—that's infrastructure doing what it's supposed to do.

> "The culture we need is one of out-cooperating, not out-competing. Curiosity over cliques. Reciprocity over rivalry."

These tools exist to be used. The question isn't whether Regen has built something real. The question is: **what will you build with it?**

---

## Discussion Questions

1. **Did the hallucination story surprise you?** How do you verify AI-provided data about ecological credits?

2. **Which connection path will you try first?** Claude Code for development? GPT for quick access?

3. **What workflows would you build?** Credit research? Methodology comparison? Governance tracking?

---

## Looking Ahead: Week 4 Preview

Next week, we go deep on the **Registry Review Agent**—the internal tool transforming 6-8 hour manual reviews into 60-90 minute guided workflows:

- The 7-stage review workflow from initialization to completion
- Document discovery and evidence extraction techniques
- How AI augments (not replaces) human expertise
- The transformation: automation handles the mechanical, humans handle judgment

We'll also introduce the **agent archetypes**: Becca (Registry), Gregory (Methodology), and Marie (Full-Stack)—specialized intelligence that transforms infrastructure access into domain expertise.

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
