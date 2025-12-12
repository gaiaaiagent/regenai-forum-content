# Section 2: The Landscape - Four Servers, One Ecosystem

## The Architecture of Intelligence

Regen AI isn't a single tool—it's a constellation of specialized servers, each providing a different lens on the regenerative economy. Understanding the distinction between these servers is fundamental to understanding how planetary-scale intelligence actually works.

## The Four MCP Servers

| Server Name | Purpose | What It Knows | Status |
|-------------|---------|---------------|--------|
| **Regen KOI MCP** | Knowledge search, semantic queries, code graph navigation | 49,169 documents from forums, docs, GitHub, podcasts; 28,489 code entities across 7 repositories | ✅ Production |
| **Regen Python MCP** | Blockchain queries, 45+ analytical tools, portfolio analytics | Live on-chain data: credit balances, marketplace orders, governance proposals, validator rewards | ✅ Production |
| **Regen Ledger MCP** | Legacy TypeScript blockchain RPC access | Direct ledger queries via Cosmos SDK modules | ✅ Production |
| **Registry Review MCP** | Project review workflow automation | Document classification, evidence extraction, compliance checking | 🚧 Internal |

## Why This Isn't Redundant

At first glance, having multiple MCP servers might seem like duplication. It's not. Each server accesses fundamentally different types of data, and this distinction matters more than it might appear.

### Knowledge vs. State: A Critical Distinction

**KOI knows what humans have written.** It indexes forum discussions where the community debates governance proposals, documentation that explains how credit classes work, methodology specifications that define carbon accounting standards, code comments that document developer intentions, and podcast transcripts that capture evolving thought leadership.

When you ask KOI "How does the Terrasos biodiversity methodology work?", it searches through 49,169 documents to find where humans have explained, debated, and documented that methodology. It understands *meaning* through semantic embeddings—so asking about "soil carbon sequestration" will surface documents about "regenerative grazing" and "carbon farming" even when those exact words don't appear. It understands *relationships* through graph queries—so it can trace how a governance proposal references a methodology document that informed a credit class.

**The Ledger MCPs know what the blockchain has recorded.** They query the actual on-chain state: which credits have been issued, how many have been retired, what marketplace orders are active right now, which governance proposals are in voting period, what balances exist at specific addresses.

When you ask the Ledger MCP "How many BT01 credits have been issued?", it doesn't search documents—it queries the blockchain's state directly and returns: 30,233 credits across 2 batches, with 26,488 currently tradable and 3,745 retired. This data is verifiable by anyone running a node. It's the source of truth.

This is the difference between *knowledge* and *state*—between what we understand and what actually is.

## The Cautionary Tale: Why This Distinction Matters

The distinction between knowledge and state isn't academic. Confusing them leads to what we might call "ecohyperstition"—plausible-sounding regenerative data that dissolves under verification.

Recently, a community member asked a GPT with only KOI access: "What is the total number of credits live on regen ledger right now?" The response was impressively detailed: tables showing 7.5 million credits across five credit classes, 626,000 hectares managed, $165 million in estimated value. It even cited a ledger explorer URL.

There was one problem: none of it was real.

The credit class IDs didn't exist. The numbers were fabricated. The explorer URL led nowhere. When challenged, the GPT acknowledged: "I don't actually have direct network access to the Regen Ledger... The data I provided was synthesized from documentation patterns, not verified on-chain state."

The same question, asked through Claude Code with the Ledger MCP connected, returned verified data: 1,039,069 total credits issued, with 525,656 currently tradable and 106,414 retired across 9 active credit classes. These numbers are an order of magnitude smaller—but they're *real*. Every credit can be traced to an on-chain transaction. Every claim can be independently verified.

This is why multi-MCP architecture exists: to ensure that questions about knowledge access verified knowledge, and questions about state access verified state.

## What Each Server Actually Knows

### Regen KOI MCP: The Knowledge Layer

**Data Sources (49,169 total documents):**
- **GitHub** (30,127 docs): Code, documentation, issues from regen-ledger, regen-web, and infrastructure repos
- **Podcasts** (6,063 docs): Planetary Regeneration podcast transcripts, distilling hours of conversation into searchable knowledge
- **Notion** (4,791 docs): Internal team documentation, research notes, working group outputs
- **Discourse Forum** (1,612 docs): Years of governance debates, technical Q&A, community proposals
- **Documentation Sites** (626 docs): Official docs.regen.network technical references
- **Registry** (598 docs): Project documentation from registry.regen.network
- **Methodology Guides** (328 docs): Carbon accounting standards, verification protocols

**Code Graph Coverage (28,489 entities):**
- **regen-ledger** (19,001 entities): Cosmos SDK blockchain modules, Keepers, Messages, Queries
- **regen-web** (5,716 entities): Frontend TypeScript/React components and services
- **koi-processor** (1,404 entities): Knowledge pipeline processing logic
- **koi-sensors** (1,135 entities): Data collection implementations
- **regen-koi-mcp** (625 entities): The MCP server itself
- **koi-research** (602 entities): Research code and experiments
- **regen-data-standards** (6 entities): JSON schema definitions

**Capabilities:**
- Semantic search across all knowledge sources with date filtering
- Code graph navigation showing entity relationships (Keepers, Messages, Functions)
- Repository exploration and tech stack analysis
- Weekly digest generation from community activity
- GitHub repository search across documentation

### Regen Python MCP: The Blockchain Layer

**Live On-Chain Data:**
- **Credit Types** (5 active):
  - **C** (Carbon): metric tons CO2 equivalent
  - **MBS** (Marine Biodiversity Stewardship): restoration activities in marine ecosystems
  - **USS** (Umbrella Species Stewardship): hectares of habitat stewarded per year
  - **BT** (BioTerra): weighted restoration/preservation scores
  - **KSH** (Kilo-Sheep-Hour): regenerative grazing credits

- **Credit Classes** (9 with issued credits): C01-C06, BT01, KSH01, MBS01, USS01
- **Total Batches Issued**: 77 batches across 57 projects
- **Total Credits**: 1,039,069 issued (632,069 live, 407,000 cancelled/bridged)
- **Active Marketplace**: Real-time sell orders, pricing, and liquidity data
- **Governance**: Proposals, votes, deposits, tally results
- **Bank Module**: Account balances, token supplies, denomination metadata
- **Distribution**: Validator rewards, delegator earnings, community pool

**45+ Tools Across 7 Modules:**
- Bank (11 tools): Balances, supplies, metadata, spendable amounts
- Distribution (9 tools): Rewards, commission, slashing events
- Governance (8 tools): Proposals, votes, deposits, parameters
- Marketplace (5 tools): Sell orders by batch, seller, or globally
- Ecocredits (4 tools): Credit types, classes, projects, batches
- Baskets (5 tools): Basket info, balances, creation fees
- Analytics (3 tools): Portfolio impact, market trends, methodology comparison

### Regen Ledger MCP: Legacy RPC Access

The original TypeScript implementation providing direct Cosmos SDK module access. Covers the same on-chain data as the Python MCP but through a different codebase. Used primarily for backwards compatibility and by TypeScript-native applications.

### Registry Review MCP: Internal Workflow Automation

**Document Intelligence (Internal Only):**
- PDF text extraction with table parsing
- GIS metadata extraction from shapefiles
- LLM-powered evidence extraction for dates, land tenure, project IDs
- Cross-document validation for consistency checking
- Structured report generation with complete audit trails

**Workflow Coverage:**
- Soil Carbon methodology v1.2.2 (others planned)
- Session management with atomic state persistence
- 7-stage review process from initialization to completion
- Target: 70% reduction in review time (6-8 hours → 60-90 minutes)

## The Multi-MCP Advantage

With multiple servers connected, an AI agent can orchestrate complex queries that span knowledge and state:

**Question:** "Explain the Terrasos biodiversity methodology and show me how many BT01 credits have been issued."

**Orchestration:**
1. KOI MCP searches 49,169 documents for Terrasos methodology documentation
2. Ledger MCP queries on-chain state for BT01 credit batches
3. Response combines: methodology explanation (from docs) + actual issuance data (from chain) + citations to primary sources

**Result:** Grounded intelligence—knowledge backed by verified state, with every claim traceable to its source.

## Platform Support and Compatibility

Not all AI platforms support MCP equally. Native support means the platform can orchestrate multiple MCP servers simultaneously, while proxy access limits functionality:

| Platform | KOI | Python | Ledger | Registry | Multi-MCP Orchestration |
|----------|-----|--------|--------|----------|------------------------|
| Claude Code CLI | ✅ Native | ✅ Native | ✅ Native | 🔒 Internal | ✅ Full orchestration |
| Claude Desktop | ✅ Native | ✅ Native | ✅ Native | 🔒 Internal | ✅ Full orchestration |
| VS Code/Cursor | ✅ Extension | ✅ Extension | ✅ Extension | 🔒 Internal | ✅ Via MCP extensions |
| ChatGPT | 🔧 API Proxy | ❌ No | ❌ No | 🔧 Limited | ⚠️ Knowledge only |
| Eliza OS | 🔧 Plugin | 🔧 Plugin | 🔧 Plugin | 🔧 Plugin | 🔧 Via custom connectors |

**Key Insight:** Claude platforms provide first-class MCP support with native multi-server orchestration. ChatGPT Custom GPTs can access KOI through a REST API proxy but cannot make live blockchain queries without additional infrastructure.

## The Architecture Philosophy

This multi-server design embodies a core principle: **different questions require different data sources, and pretending a single model can know everything leads to hallucination, not intelligence.**

Knowledge bases tell us what humans understand. Blockchains tell us what actually happened. Document analysis tells us what evidence exists. These are complementary lenses, not redundant systems.

The regenerative economy deserves AI that knows the difference—and knows when to use which lens.

---

**Next:** Section 3 will explore how to actually connect to these servers, with step-by-step instructions for Claude Code, ChatGPT, and Eliza, plus a deep dive into the specific tools each MCP provides.
