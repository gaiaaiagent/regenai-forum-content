# The Knowledge Brain of Planetary Intelligence

![KOI MCP Architecture|690x388](upload://koiMcpArchitecture.jpeg)

# [Week 2/12] Regen AI Update: KOI MCP Deep Dive - November 25, 2025

* **Posted by:** Shawn Anderson (Gaia AI)
* **Key Focus:** Understanding how Knowledge Organization Infrastructure enables planetary intelligence through distributed knowledge networks

---

## The Nervous System of Regeneration

Last week we introduced the three MCP servers forming the backbone of Regen AI. This week, we dive deep into the **KOI MCP** - the knowledge brain that makes planetary intelligence possible.

But KOI is more than a database. It's a living nervous system for regenerative knowledge.

When we talk about creating a "legibility layer" for ecological data, we're describing something profound: the ability for any intelligent agent - human or artificial - to ask questions of the regenerative economy and receive coherent, contextualized answers. *What methodologies have proven most effective for soil carbon sequestration in tropical regions? How has the Regen community's thinking evolved on biodiversity credits? What patterns emerge when we trace the connections between projects, people, and protocols?*

These questions require more than search. They require understanding.

---

## The Philosophy Behind KOI

At its heart, KOI embodies a radical proposition: **knowledge itself should be decentralized, versioned, and self-organizing** - just like the ecological systems we seek to regenerate.

The KOI protocol (Knowledge Organization Infrastructure) draws inspiration from how mycorrhizal networks share resources between trees. In a forest, information about nutrients, water stress, and threats flows through fungal highways connecting root systems. No central controller directs this flow - it emerges from the network topology itself.

KOI-net works similarly. Rather than a monolithic database controlled by a single entity, KOI creates a **federation of knowledge nodes** that discover each other, negotiate relationships, and broadcast updates through event propagation. When new knowledge enters the system - a forum post, a methodology update, a governance proposal - it ripples outward through the network, transformed and enriched at each step.

This is infrastructure for the Symbiocene: technology that mirrors natural patterns of distributed intelligence.

---

## How KOI Actually Works: A Technical Journey

Let's trace how knowledge flows from source to insight. Understanding this architecture illuminates why KOI enables capabilities impossible with traditional search.

### The Node Architecture

Every participant in the KOI network is a **node**. The `NodeInterface` class serves as the embodiment of each node, wiring together multiple interconnected subsystems:

```
NodeInterface
├── identity      (who am I in the network?)
├── cache         (what do I remember locally?)
├── effector      (how do I resolve references?)
├── graph         (who do I know, and how?)
├── pipeline      (how do I process knowledge?)
├── processor     (how do I handle specific events?)
└── network_interface (how do I communicate?)
```

Nodes come in two types:

**Full Nodes** operate as web servers, receiving knowledge through webhooks. They maintain persistent connections and can broadcast to many subscribers simultaneously. Think of these as the major hub cities in a transportation network.

**Partial Nodes** operate as web clients, polling for updates. They're lighter weight and can run anywhere - in a browser, a mobile app, or an AI agent's runtime. These are the local stations that keep smaller communities connected.

This hybrid architecture means KOI can scale from a single laptop running a sensor to a global network processing millions of knowledge updates daily.

### The Language of Knowledge: RIDs and Bundles

Every piece of knowledge in KOI receives a **Resource Identifier (RID)** - a unique, permanent address in the global knowledge space. RIDs use the ORN (Object Resource Name) format:

```
orn:web.page:docs.regen.network/1ef62e1ed208c19c
orn:discourse.post:forum.regen.network/12345
orn:methodology:regen.network/C01-methodology-v3
```

These aren't just identifiers - they're *commitments*. When you reference a RID, you're pointing to a specific piece of knowledge that can be resolved anywhere in the network through the **effector system**. The effector tries three strategies in sequence:

1. **Cache** - Do I already have this locally?
2. **Action** - Can I generate or fetch it myself?
3. **Network** - Ask neighbors who might know

This pattern of local-first with network fallback mirrors how biological systems conserve energy while maintaining resilience.

Knowledge travels in **Bundles** - containers with two parts:
- **Manifest**: Metadata describing the content (hash, timestamp, source, type)
- **Contents**: The actual knowledge payload

The manifest's cryptographic hash ensures integrity: you can verify that knowledge hasn't been tampered with as it flows through the network.

### The FUN Events: How Knowledge Propagates

KOI uses three event types (forming the mnemonic **FUN**):

* **FORGET** - This knowledge is no longer valid; remove it from your understanding
* **UPDATE** - This knowledge has changed; here's the new version
* **NEW** - This knowledge didn't exist before; add it to your understanding

When a sensor detects that docs.regen.network has changed, it emits an UPDATE event. This event flows through the **knowledge pipeline** - a five-phase processing system:

```
RID Phase → Manifest Phase → Bundle Phase → Network Phase → Final Phase
```

At each phase, **handlers** can inspect, transform, enrich, or block the knowledge object. For example:

* The **RID handler** blocks events about yourself (prevents infinite loops)
* The **Manifest handler** compares timestamps and hashes to detect actual changes
* The **Edge negotiation handler** manages relationships between nodes
* The **Network output handler** routes updates to interested subscribers

This pipeline architecture means nodes can customize their knowledge processing without breaking protocol compatibility. A methodology-focused node might add handlers that extract entity relationships, while a governance-focused node might prioritize proposal content.

### The NetworkGraph: Knowledge Topology

Each node maintains a **NetworkGraph** using directed graph structures. This graph answers questions like:

* Which nodes subscribe to my updates?
* Which nodes should I poll for knowledge?
* What's the shortest path to reach a particular knowledge source?

The graph isn't static - it evolves through **edge negotiation**. When two nodes want to establish a relationship, they exchange proposals specifying:

* **Edge type**: Provider (I'll send you knowledge) or Subscriber (I want your knowledge)
* **RID filter**: What kinds of knowledge flow through this edge?
* **Capabilities**: What can each node offer?

This negotiation happens automatically through the pipeline's edge handlers. The result is a self-organizing topology where knowledge flows efficiently to where it's needed.

---

## From Protocol to Intelligence: The Regen KOI Implementation

The KOI protocol provides the foundation. The **Regen KOI implementation** adds the intelligence layers that transform raw knowledge into actionable insight.

### Active Sensors: The Eyes and Ears

Our sensor network continuously monitors knowledge sources:

| Source | Documents | Update Frequency |
|--------|-----------|------------------|
| Discourse Forums | 440+ posts | Real-time |
| GitHub/GitLab | 70+ files | Hourly |
| Websites | 60+ pages | 30-minute intervals |
| Medium/Blog | 160+ articles | Daily |
| Podcast Transcripts | 52 episodes | Weekly |
| Notion Archive | 585 pages | On-demand |

Each sensor is a KOI partial node that emits events when content changes. The **website sensor**, for example, tracks 9 core websites including docs.regen.network, registry.regen.network, and partner sites. When a page changes, it:

1. Computes a content hash
2. Compares against the cached hash
3. If different, extracts content and metadata
4. Emits an UPDATE event with the new bundle

This is continuous monitoring, not periodic scraping. Knowledge enters the system within seconds of publication.

### BGE Embeddings: The Language of Meaning

Raw text becomes searchable through **vector embeddings** - 1024-dimensional mathematical representations of meaning. We use the BGE-large-en-v1.5 model, which excels at capturing semantic relationships in technical and scientific content.

When a document enters the system:

```
Document → Chunking (1000 characters) → BGE Embedding → PostgreSQL + pgvector
```

These embeddings enable semantic search: *"projects that increased soil organic carbon"* matches documents discussing *"SOC improvement"*, *"carbon sequestration in topsoil"*, and *"enhanced humus formation"* - even without exact keyword matches.

### Apache Jena: The Relationship Map

Parallel to vector embeddings, knowledge transforms into **RDF triples** stored in Apache Jena. These triples capture explicit relationships:

```sparql
:SoilCarbonMethodology :developedBy :RegenNetworkTeam .
:ProjectX :usesMethodology :SoilCarbonMethodology .
:ProjectX :locatedIn :BrazilianCerrado .
:BrazilianCerrado :isPartOf :TropicalBiome .
```

The graph currently contains **3,900+ triples** expressing relationships between entities across the Regen ecosystem. This enables queries impossible with keyword search alone:

*"Show me all projects in tropical biomes using methodologies developed by the Regen team"*

### Hybrid Search: Best of Both Worlds

The KOI MCP combines both approaches through **Reciprocal Rank Fusion (RRF)**. When you search:

1. Vector search finds semantically similar documents
2. SPARQL queries find structurally related entities
3. RRF merges results, boosting items found by both methods

Items appearing in both result sets receive amplified scores - a strong signal of relevance. This hybrid approach outperforms either method alone, especially for complex queries that need both semantic understanding and structural reasoning.

---

## The Weekly Digest: Knowledge in Motion

One of KOI's most powerful features is automatic **digest generation**. Every week, the system:

1. Collects all new and updated knowledge from the past 7 days
2. Clusters content by theme and topic
3. Identifies key developments, proposals, and discussions
4. Generates a structured summary with source citations

These digests power the **Planetary Regeneration Podcast** at [digest.gaiaai.xyz](https://digest.gaiaai.xyz/) - automatically generated audio briefings on Regen Network activity. What once required hours of human curation now happens continuously, ensuring no important development goes unnoticed.

The digest isn't just summary - it's synthesis. By processing knowledge through the pipeline, the system identifies patterns that might escape individual attention: recurring themes in governance discussions, convergent developments across projects, emerging questions that need community attention.

---

## Connect to KOI: A Practical Tutorial

Ready to tap into the knowledge brain yourself? Here's how to connect the KOI MCP to your AI environment.

### For Claude Code Users

Add the KOI MCP server with a single command:

```bash
claude mcp add regen-koi -- npx -y regen-koi-mcp@latest
```

This registers the MCP server in Claude Code's configuration. Restart Claude Code, and you'll have access to three tools:

* **search_knowledge** - Hybrid semantic + graph search
* **get_stats** - Knowledge base statistics
* **generate_weekly_digest** - Create activity summaries

Try asking Claude: *"Search the Regen knowledge base for information about biodiversity credit methodologies"*

### For Claude Desktop

Add to your Claude Desktop config file (`claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "regen-koi": {
      "command": "npx",
      "args": ["-y", "regen-koi-mcp@latest"],
      "env": {
        "KOI_API_ENDPOINT": "https://regen.gaiaai.xyz/api/koi"
      }
    }
  }
}
```

Config location: `~/Library/Application Support/Claude/` (macOS) or `%APPDATA%\Claude\` (Windows)

### For VSCode with Cline Extension

Add to your VSCode `settings.json`:

```json
{
  "cline.mcpServers": {
    "regen-koi": {
      "command": "npx",
      "args": ["-y", "regen-koi-mcp@latest"],
      "env": {
        "KOI_API_ENDPOINT": "https://regen.gaiaai.xyz/api/koi"
      }
    }
  }
}
```

### For ChatGPT (Custom GPT via Actions)

ChatGPT uses GPT Actions (OpenAI's API mechanism) rather than MCP. Create a Custom GPT with the following action configuration:

```yaml
openapi: 3.0.0
info:
  title: Regen KOI API
  version: 1.0.0
servers:
  - url: https://regen.gaiaai.xyz/api/koi
paths:
  /query:
    post:
      operationId: searchKnowledge
      summary: Search the Regen knowledge base
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                query:
                  type: string
                  description: Search query
                limit:
                  type: integer
                  default: 5
      responses:
        '200':
          description: Search results
```

### Self-Hosted Option

For full control, clone and run locally:

```bash
git clone https://github.com/gaiaaiagent/regen-koi-mcp.git
cd regen-koi-mcp
npm install
npm run build
npm start
```

Configure with environment variables:
* `KOI_API_ENDPOINT` - API endpoint (default: https://regen.gaiaai.xyz/api/koi)
* `JENA_ENDPOINT` - SPARQL endpoint for graph queries
* `EMBEDDING_SERVICE_URL` - BGE embedding service

---

## The Deeper Implications

KOI isn't just infrastructure - it's a statement about how knowledge should work in the regenerative economy.

**Decentralization matters** because knowledge shouldn't have gatekeepers. Anyone can run a KOI node, contribute knowledge, or build on the protocol. The network's value comes from its connectivity, not control.

**Versioning matters** because knowledge evolves. Methodologies improve. Understanding deepens. Mistakes get corrected. KOI preserves this evolution through its event system, creating an auditable history of how our collective understanding has grown.

**Semantic structure matters** because regeneration requires synthesis. Climate action doesn't happen in silos. Projects connect to methodologies connect to governance connect to communities. KOI's graph structure makes these connections queryable and explorable.

Perhaps most importantly, **accessibility matters**. Every AI agent, every researcher, every curious community member should be able to ask questions of our collective knowledge and receive intelligent answers. KOI makes the regenerative economy *legible* - comprehensible to minds both human and artificial.

This is how we build planetary intelligence: not through a single superintelligent system, but through a network of connected intelligences - each node contributing its perspective, each connection enabling new insights, each query deepening our collective understanding.

---

## Discussion Questions

**What knowledge sources should we add next?**

We're expanding our sensor network. Priority candidates include:
* Scientific literature databases (research papers, peer-reviewed journals)
* Social media (X/Twitter ecosystem discussions)
* Partner organization content (ecoToken, NCT, other ReFi projects)
* On-chain event logs (governance votes, credit retirements)

What sources would be most valuable for your work?

**How do you envision using KOI?**

Some possibilities we're exploring:
* Research assistants that synthesize across all Regen documentation
* Governance advisors that surface relevant precedents for proposals
* Onboarding guides that answer newcomer questions from the knowledge base
* Impact reporters that compile evidence for specific projects or methodologies

What use cases would make the biggest difference for you?

---

## Looking Ahead: Week 3 Preview

Next week we shift focus to the **Registry Review MCP** - where AI meets real-world impact *today*:

* The 7-stage workflow for automated document verification
* How AI assists Becca and the registry team
* Early wins in document classification and evidence extraction
* Demo of completeness checking against methodology requirements
* Time savings projections and accuracy metrics

We'll show how AI amplifies human expertise rather than replacing it, creating a partnership between registry reviewers and intelligent assistants.

---

## Resources & Links

* **KOI MCP Repository**: [github.com/gaiaaiagent/regen-koi-mcp](https://github.com/gaiaaiagent/regen-koi-mcp)
* **KOI Protocol Library**: [github.com/BlockScience/koi-net](https://github.com/BlockScience/koi-net)
* **Weekly Digest Podcasts**: [digest.gaiaai.xyz](https://digest.gaiaai.xyz/)
* **Hosted API**: https://regen.gaiaai.xyz/api/koi
* **Tuesday Stand-up**: Every Tuesday (join us!)
* **Previous Update**: [Week 1 - Foundation & Kickoff](link-to-week-1)

---

*This is Week 2 of 12 weekly updates documenting the development of Regen AI. The knowledge brain is live and growing - every search helps train better retrieval, every question reveals gaps we can fill, every connection strengthens the network. Join us in building planetary intelligence, one query at a time.*

*What aspect of KOI would you like to explore further? Drop your questions below - next week's content responds to what you want to learn.*
