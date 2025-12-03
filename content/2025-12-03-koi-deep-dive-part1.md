# The Knowledge Brain of Regeneration

![forest_cross_section|690x386](upload://bAR7begGqrlVQEHn7iFTAaM9HzL.jpeg)


# [Week 2/12] Regen AI Update: KOI MCP Deep Dive - November 25, 2025

* **Posted by:** Shawn Anderson (Gaia AI)
* **Key Focus:** How 15,000+ documents become a living planetary intelligence network through Knowledge Organization Infrastructure

Last week, we introduced [Regen AI's three foundational MCP servers](https://forum.regen.network/t/announcing-regen-ai/553). This week, we descend into the mycelium—the vast underground network that connects everything in the forest of regenerative knowledge. Welcome to the Regen KOI MCP: the knowledge brain that transforms scattered documents into planetary intelligence.

---
## Quickstart:

To get started with the KOI Regen MCP, test it out with the KOI Regen GPT:
**[Launch Regen KOI GPT →](https://chatgpt.com/g/g-692f3c6bc5e48191b3d1721f4a8ccdec-regen-koi-gpt)**

To learn additional ways of connecting to the Regen KOI network see **Part 2** of this post (coming next).

---

## The Fragmentation Crisis

Consider the challenge facing anyone entering the regenerative space today. Where does one begin?

The Regen ecosystem sprawls across:
- **Forum discussions** spanning years of governance debates and community insights
- **Technical documentation** for the ledger, registry, and data modules
- **Methodology specifications** for carbon, biodiversity, and soil health credits
- **Blog posts and newsletters** capturing evolving thought leadership
- **Community calls** where decisions are made in conversation
- **GitHub repositories** where code embodies intention
- **Podcast transcripts** distilling hours of wisdom into accessible narrative

This knowledge doesn't just exist—it *lives*. It changes. It connects in ways that no single document can capture. A governance proposal from 2023 references a methodology document that informed a credit class that now has dozens of active projects generating insights that feed back into new proposals.

The tragedy? Most of this knowledge exists in silos. Each piece knows nothing of the others. The collective intelligence remains latent, waiting to be woven together.

This is where KOI enters—not as a database, but as a *nervous system*.

---

## From Data to Wisdom: A Journey Into the Mycelial Mind

*Today's information environment is defined by a strange inversion:* "Instead of inhabiting a shared reality from which a variety of knowledge objects emerge, we inhabit a variety of realities that each emerge from a particular collection of knowledge objects their inhabitants hold in common." — BlockScience, [A Preview of the KOI-net Protocol](https://blog.block.science/a-preview-of-the-koi-net-protocol/) (2024)

**KOI—Knowledge Organization Infrastructure—is a [specification](https://github.com/BlockScience/koi-net) created by [BlockScience](https://block.science/)**, the complex systems engineering and R&D firm, in partnership with Metagov and RMIT. Their research represents a fundamental breakthrough in how distributed organizations can establish shared knowledge while preserving autonomy. We're honored to be among the first to implement their protocol at scale, building what may be the most comprehensive knowledge infrastructure in the regenerative economy. What BlockScience designed as a theoretical framework, we've transformed into a living nervous system for planetary intelligence.

The fundamental insight is profound: **knowledge coordination precedes action coordination**. Before we can act together on planetary-scale challenges, we must first establish common understanding—not by forcing agreement, but by making our respective knowledge legible to one another. At its heart, KOI embodies a radical proposition: **knowledge itself should be decentralized, versioned, and self-organizing** - just like the ecological systems we seek to regenerate.

The KOI protocol draws inspiration from how mycorrhizal networks share resources between trees. In a forest, information about nutrients, water stress, and threats flows through fungal highways connecting root systems. No central controller directs this flow - it emerges from the network topology itself. KOI works similarly. Rather than a monolithic database controlled by a single entity, KOI creates a **federation of knowledge nodes** that discover each other, negotiate relationships, and broadcast updates through event propagation. When new knowledge enters the system - a forum post, a methodology update, a governance proposal - it ripples outward through the network, transformed and enriched at each step.

This is infrastructure for the Symbiocene: technology that mirrors natural patterns of distributed intelligence.

## How KOI Actually Works: A Technical Journey

What follows is a technical journey through each layer, from the atomic unit of a Resource Identifiers to the emergent topology of a knowledge network. For developers, this is a blueprint. For everyone else, it's a window into the machinery that makes planetary intelligence possible.

![koi-node|690x460](upload://k2wngsUE10R8G5y7a2DFmuU2O6a.jpeg)
*A KOI node's internal architecture: components working together to process and route knowledge through the network.*

### The RID Protocol: Every Piece of Knowledge Has a Name

At KOI's foundation lies the **Resource Identifier (RID) protocol**. Every document is assigned a meaningful reference that captures *how* we refer to the content. RIDs are unique, permanent addresses in the global knowledge space. RIDs use the ORN (Object Resource Name) format

```
orn:discourse.forum.regen.network:topic/12345
orn:github.com:regen-network/regen-ledger/blob/main/README.md
orn:web.page:registry.regen.network/carbon-credits
```

RIDs can be resolved anywhere in the network through the **effector system** (the component responsible for turning an RID into actual content). The effector tries three strategies in sequence:

1. **Cache** - Do I already have this locally?
2. **Action** - Can I generate or fetch it myself?
3. **Network** - Ask neighbors who might know

When knowledge is requested from the network, it travels in **Bundles** - containers with two parts:
- **Manifest**: Metadata describing the content (hash, timestamp, source, type)
- **Contents**: The actual knowledge payload

The manifest's cryptographic hash ensures integrity. With identifiers and bundles established, the next question is: how do nodes communicate changes?

### The FUN Event System: Knowledge That Breathes

KOI networks communicate through events, forming the "FUN" triad:

* **FORGET** - This knowledge is no longer valid; remove it from your understanding
* **UPDATE** - This knowledge has changed; here's the new version
* **NEW** - This knowledge didn't exist before; add it to your understanding

When a new forum post appears, the Discourse sensor emits a NEW event. Other nodes in the network decide independently how to respond. One might index it for search. Another might extract entities for a knowledge graph. A third might ignore it entirely if it's outside its domain of interest.

This event-driven architecture means KOI networks are **living systems**. They respond to changes in real-time. They're decentralized by design—no central authority decides what's important. Each node maintains autonomy while contributing to collective intelligence.

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

While the pipeline processes individual events, the broader question remains: how do nodes discover each other and coordinate who sends what to whom?

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

### Nodes, Sensors, Processors, Actuators: The Anatomy of a KOI Network

![koi2|690x482](upload://s2TI75Ilc490E0K3L1GojPNZtVD.jpeg)
*Different types of nodes in a KOI-net, categorized by their relationship to the boundary between the network and the external world. Image created by Luke Miller for BlockScience.*

The KOI-net protocol defines several node types, categorized by their relationship to organizational boundaries:
* **Sensor Nodes** sit at the boundary, reaching into the external world.
* **Processor Nodes** operate internally, transforming knowledge.
* **Coordinator Nodes** facilitate discovery and routing.
* **Actuator Nodes** push information back out.


The beauty of this architecture is its **fractal nature**: a network of nodes can itself appear as a single node to an external observer. Regen's entire KOI infrastructure could be one "knowledge node" in a larger planetary KOI network connecting multiple regenerative organizations.

*To learn more: [KOI Nodes as Neurons](https://blog.block.science/koi-nodes-as-neurons/) and the [KOI-net Protocol Spec](https://github.com/BlockScience/koi-net)*

---

## The Regen KOI Network: A Living Map


![regen-koi-network|690x437](upload://seEtWS8Yip3LFKSluKv8HMzE065.png)
*The complete architecture of RegenAI's Knowledge Organization Infrastructure—from sensors at the edge to intelligent agents at the center.*

The diagram above reveals a production system that has evolved significantly since our initial deployment. What began as a simple document search has grown into a sophisticated knowledge processing pipeline spanning eight sensors, three storage layers, and multiple intelligence services. Let's trace the flow from the network's edges toward its intelligent center.

### Sensors: The Network's Eyes and Ears

At the periphery of the network, eight specialized sensors continuously monitor the Regen ecosystem. Each sensor is purpose-built for its platform, understanding the nuances of how that platform structures and delivers content:

These sensors are what the KOI protocol calls "partial nodes"—they observe and report but don't serve queries directly. This lightweight design means sensors can run anywhere, from cloud servers to edge devices, scaling horizontally as the ecosystem grows.

### The Coordination Layer

All sensor events flow inward to the coordination layer, where three components work together to manage the knowledge pipeline:

**KOI Coordinator** sits at the center of the sensor array, serving as the central routing hub where all events converge. It maintains a registry of every node in the network, tracks their health through periodic heartbeats, and routes events to the processors that need them. When a new sensor comes online, it registers with the Coordinator and immediately becomes part of the knowledge network.

**Forwarder** bridges the Coordinator to the processing pipeline. It ensures reliable event delivery with confirmation tracking—if the Event Bridge is temporarily unavailable, the Forwarder queues events and retries until delivery succeeds. This resilience means no knowledge is lost even during system maintenance.

**Event Bridge** is the workhorse of the entire system. Every piece of knowledge passes through here, where several critical operations occur:
- *Deduplication*: The same content might arrive from multiple sensors (a Medium post that's also shared on Twitter). The Event Bridge recognizes duplicates by their content hash and processes each piece of knowledge exactly once.
- *Versioning*: When content changes, the Event Bridge doesn't overwrite—it creates a new version and marks the previous one as superseded. This preserves the full history of how knowledge evolved.
- *Chunking*: Long documents are split into smaller chunks (1000 characters with 200-character overlap) optimized for embedding and retrieval.
- *Provenance*: Every transformation generates a CAT (Content Addressable Transformation) receipt, creating an auditable chain from source to storage.

### Processing: From Text to Intelligence

Two specialized processors transform raw content into queryable knowledge:

**BGE Embeddings** converts text into 1024-dimensional semantic vectors using the BAAI/BGE-large-en-v1.5 model. These vectors are mathematical representations of *meaning*—documents about similar concepts cluster together in vector space even when they use different words. This is why searching for "soil carbon sequestration" also surfaces documents about "carbon farming" and "regenerative grazing"—the model understands these concepts are related.

**Tree-sitter AST Parser** is our newest addition, enabling deep code intelligence. Rather than treating source code as plain text, it parses code into Abstract Syntax Trees that understand programming language structure. From these trees, it extracts typed entities: Methods, Functions, Structs, Interfaces, and Cosmos SDK-specific constructs like Keepers, Messages, and Queries. This is what powers questions like "Which Keeper handles MsgCreateBatch?" or "What functions call the credit retirement handler?"

### Three Storage Layers

Perhaps the most distinctive aspect of our architecture is maintaining **three complementary knowledge stores**, each optimized for different query patterns:

**PostgreSQL + pgvector** serves as the semantic layer. When you ask a question, your query is embedded into this vector space, and pgvector finds the chunks whose meaning most closely matches. This is fast (sub-second queries) and intuitive—you don't need to know the exact keywords, just the concepts you're interested in.

**PostgreSQL + Apache AGE** provides the code graph. This graph database lets you traverse codebases structurally. Find all functions that call a particular method, identify which Keepers handle which Messages, and understand how modules depend on each other. The graph structure captures relationships that flat search simply cannot.

**Apache Jena Fuseki** maintains the knowledge graph of RDF triples. This is where we store semantic relationships between entities: which methodologies apply to which credit classes, who authored which documents, what projects implement which approaches. The SPARQL query language enables complex reasoning—finding all projects that use a particular methodology AND were registered in 2024 AND involve soil carbon.

### Intelligence Services

The intelligence layer is where knowledge becomes accessible to both humans and AI:

**MCP Server** provides the unified interface that AI agents use to query the knowledge network. When you ask Claude a question about Regen Network, the MCP Server orchestrates queries across all three storage layers in parallel. Vector search finds semantically relevant documents. Graph queries surface structured relationships. SPARQL retrieves precise facts. The results are fused using Reciprocal Rank Fusion (RRF), which intelligently combines rankings from different sources into a single, coherent response—complete with citations back to primary sources.

Any MCP-compatible client can connect: Claude Desktop, Claude Code, VSCode with Copilot, Cursor, Windsurf, and many others. This means the entire Regen knowledge network is accessible from whatever AI tool you prefer.

**Eliza Agents** are autonomous AI personalities that use this knowledge to engage with communities directly. Five agents currently operate: RegenAI (the primary assistant), Voice of Nature (ecological perspective), Governor (governance focus), Advocate (community outreach), and Narrative (storytelling). Each agent can answer questions, generate content, and participate in discussions—grounded in the verified knowledge from KOI rather than hallucinating responses.

### Curation Layer

Finally, two curator services synthesize the constant flow of knowledge into digestible summaries:

**Weekly Curator** takes a longer view, synthesizing seven days of activity into comprehensive digests. These digests capture the arc of ongoing discussions, track how proposals evolve, and identify themes emerging across the ecosystem. The Weekly Curator's output powers the automated podcasts at [digest.gaiaai.xyz](https://digest.gaiaai.xyz/), transforming a week of community activity into a coherent audio narrative.

*To learn more: [KOI Master Implementation Guide](https://github.com/DarrenZal/koi-research/blob/regen-prod/docs/KOI_MASTER_IMPLEMENTATION_GUIDE.md)*

---

## How Knowledge Flows: A Day in the Life

Let's trace a piece of knowledge through the network:


![regen-knowledge-commons|690x388](upload://dCIsZ5cRWnnYTrCDeMSxlzYyziU.jpeg)
*How posting in the community forums or making contributions to Github will trigger cascading contributions to the Regen Knowledge Commons.*

**9:00 AM**: Gregory posts a new governance proposal on forum.regen.network about adjusting credit class parameters.

**9:01 AM**: The Discourse Sensor detects the new topic. It generates an RID (`orn:discourse.forum.regen.network:topic/482`) and emits a NEW event containing the post content, author, timestamp, and category.

**9:02 AM**: The Event Bridge receives the event. It checks: have we seen this RID before? No—this is genuinely new. It routes the event to the embedding processor and the graph processor.

**9:03 AM**: The BGE Embeddings processor generates a semantic vector for the post content. This vector is stored in PostgreSQL alongside the text, making the post discoverable through semantic search.

**9:04 AM**: The graph processor extracts entities from the post: mentions of credit classes (C02), methodologies (VM0042), governance concepts (parameter changes). These are added to Apache Jena as RDF triples, linking this post to the broader knowledge graph.

**9:05 AM**: The Daily Curator notices this is a governance-related post. It flags it for inclusion in today's governance summary.

**9:06 AM**: An AI agent, asked "What's happening with credit class governance?", queries the MCP. The hybrid search finds Gregory's post (high semantic relevance to "credit class governance") and surfaces it with proper citation.

**End of Week**: The Weekly Curator aggregates this post with all other governance activity, generating a digest that feeds into an automated podcast episode.

Total time from post to searchable, graph-connected, citable knowledge: **under 5 minutes**.

---

## The Philosophy of Knowledge Organization

The technical architecture is impressive, but the deeper significance lies in what KOI represents for regenerative practice.

### Knowledge as Commons

As the Regen Registry creates a commons for ecological assets, KOI creates a commons for knowledge. The protocol is open. The data is accessible. Anyone can run a KOI node, contribute knowledge, or build new applications on the infrastructure. Anyone who contributes to a community call or token economics call will have their voice introduced into the automated weekly podcast, and that podcast content will be ingested into the KOI network. As data is ingested, the embedding space and graph structure of the knowledge network expands. Every graph edge connects concepts that add to a shared resource benefiting everyone in the ecosystem.

### Collective Intelligence at Scale

Communities have always organized knowledge—through stories, libraries, institutions. KOI represents a new form: **augmented collective intelligence**. A thoughtful forum post by a community member becomes discoverable by anyone, anywhere, at any time. A governance decision becomes contextualized within the full history of prior decisions. A methodology improvement becomes linked to all the projects that it potentially benefits.

### Regenerative Agency

Here's the connection to our larger mission: **legible knowledge enables coordinated action**. Any Regen agent inherits the collective intelligence of the network through KOI. This is how we scale regenerative agency beyond individuals, by making planetary intelligence accessible at planetary scale.

---

## Discussion Questions

As we build this knowledge infrastructure together, we want your input:

1. **What knowledge sources are we missing?** Are there key documents, sites, or data streams that should feed into KOI?

2. **What queries would you love to ask?** If you could ask the Regen knowledge brain anything, what would it be? These inform our development priorities.

3. **Would you run a KOI node?** For those technically inclined, would you want to run sensors or processors as part of a distributed knowledge network?

Share your thoughts in the comments below!

---

## Looking Ahead

**Next week**, we turn from knowledge to action. We'll explore the **Registry Review MCP**—how AI transforms the project onboarding experience.

**Part 2 of this post** will cover the full Tutorial (how to connect to KOI via Claude Code, NPX, and API) with additional resources.

---

## Resources & Links

**Getting Started:**
- [Regen KOI GPT](https://chatgpt.com/g/g-692f3c6bc5e48191b3d1721f4a8ccdec-regen-koi-gpt) — Try it now on ChatGPT
- [Regen KOI MCP on GitHub](https://github.com/gaiaaiagent/regen-koi-mcp) — Source code and documentation
- [Weekly Digests & Podcast](https://digest.gaiaai.xyz/) — AI-generated summaries of ecosystem activity

**KOI Protocol:**
- [BlockScience](https://block.science/) — Creators of the KOI specification
- [KOI-net Protocol Spec](https://github.com/BlockScience/koi-net) — The open protocol
- [A Preview of the KOI-net Protocol](https://blog.block.science/a-preview-of-the-koi-net-protocol/) — BlockScience introduction
- [KOI Nodes as Neurons](https://blog.block.science/koi-nodes-as-neurons/) — Deep dive on node architecture

**Community:**
- [Previous Update: Announcing Regen AI](https://forum.regen.network/t/announcing-regen-ai/553) — Week 1 of this series

---

*This is the second of 12 weekly updates documenting the development of Regen AI. The forum is our knowledge commons. Every discussion here feeds back into KOI, strengthening our collective intelligence.*
