# RegenAI KOI Architecture Specification v2.0

**Purpose:** Comprehensive specification for creating the next-generation RegenAI KOI Architecture diagram
**Date:** November 27, 2025
**Status:** Phase 2c Complete - Full-Stack Technical Assistant

---

## Architecture Overview

The RegenAI KOI (Knowledge Organization Infrastructure) is a distributed knowledge processing system that ingests content from 12+ sources, processes it through multiple specialized pipelines, stores it in hybrid databases, and exposes it through 8 MCP tools for AI agent consumption.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        REGENAI KOI ARCHITECTURE v2.0                        │
│                   "The Mycelial Mind of Regenerative AI"                    │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Layer 1: Sensory Array (12 Active Sensors)

These sensors monitor the Regen ecosystem and emit FUN events (Forget, Update, New).

### Documentation Sensors (Blue - Primary Knowledge)
| Sensor | Source | Content Type | Update Frequency |
|--------|--------|--------------|------------------|
| **Website Sensor** | docs.regen.network, guides.regen.network, registry.regen.network | Technical docs, tutorials, registry info | Daily |
| **GitHub Sensor** | regen-network/*, gaiaaiagent/* | Code, READMEs, issues, PRs | Real-time |
| **GitHub Activity** | Repository events | Commits, releases, discussions | Real-time |
| **GitLab Sensor** | Internal repositories | Private code, documentation | Daily |
| **Notion Sensor** | Internal workspace | Research notes, planning docs | Daily |

### Community Sensors (Green - Social Knowledge)
| Sensor | Source | Content Type | Update Frequency |
|--------|--------|--------------|------------------|
| **Discourse Sensor** | forum.regen.network | Forum posts, proposals, discussions | Real-time |
| **Telegram Sensor** | Regen community channels | Chat messages, announcements | Real-time |
| **Twitter Sensor** | @raboracle, community accounts | Tweets, threads, announcements | Hourly |
| **Discord Sensor** | Regen Discord server | Channel messages, threads | Real-time |

### Media Sensors (Orange - Narrative Knowledge)
| Sensor | Source | Content Type | Update Frequency |
|--------|--------|--------------|------------------|
| **Medium Sensor** | Regen Medium publication | Blog posts, thought leadership | Daily |
| **Podcast Sensor** | Planetary Regeneration Podcast | Transcripts, episode metadata | Weekly |

### Blockchain Sensor (Purple - On-Chain Knowledge)
| Sensor | Source | Content Type | Update Frequency |
|--------|--------|--------------|------------------|
| **Ledger Sensor** | Regen Ledger mainnet | Proposals, credit batches, projects | Block-time |

---

## Layer 2: Coordination Hub

### KOI Coordinator (Port 8005)
The central routing hub that:
- Registers sensors and processors as they join
- Maintains network topology graph
- Routes FUN events to interested subscribers
- Enables node discovery for AI agents
- Implements the BlockScience KOI-net protocol

```
         ┌─────────────────┐
         │  KOI Coordinator │
         │    Port 8005     │
         └────────┬────────┘
                  │
    ┌─────────────┼─────────────┐
    │             │             │
    ▼             ▼             ▼
[Sensors]   [Processors]   [Services]
```

---

## Layer 3: Processing Pipeline

### Event Bridge v2 (Port 8100)
The orchestration layer that:
- Receives events from Coordinator
- Deduplicates content (same content from multiple sources → one record)
- Versions content (tracks changes over time)
- Routes to appropriate downstream processors
- Manages the processing queue

### Embedding Processors

#### BGE Embeddings (Port 8090)
- Model: BAAI/bge-large-en-v1.5
- Dimension: 1024-dimensional vectors
- Purpose: Semantic similarity search
- Handles: All text content

#### OpenAI Embeddings (Optional)
- Model: text-embedding-3-large
- Dimension: 3072-dimensional vectors
- Purpose: Enhanced semantic understanding
- Handles: Premium/priority content

### Code Graph Service (Port 8350) - NEW
Automatic code entity extraction pipeline:

```
GitHub Sensor ──► Coordinator ──► Event Bridge v2 ──► Code Graph Service
                                         │                    │
                                         ▼                    ▼
                                     pgvector           Apache AGE
                                   (embeddings)      (code entities)
```

**Entity Types Extracted:**
| Entity | Description | Example |
|--------|-------------|---------|
| Repository | Code repository | regen-ledger |
| Function | Function/method definition | CreateClass |
| Class | Class definition | MsgClient |
| Interface | Interface/protocol | QueryServer |
| Keeper | Cosmos SDK keeper | ecocreditKeeper |
| Message | Cosmos SDK message | MsgCreateBatch |
| Event | Cosmos SDK event | EventCreateClass |
| Query | Cosmos SDK query | QueryClassInfo |
| Sensor | KOI sensor implementation | DiscourseSensor |
| Handler | Request handler | HandleCreateProject |

**Language Support:**
- Python: Full support (AST parsing)
- Go: Full support (Cosmos SDK aware)
- TypeScript/JavaScript: Full support
- Rust: Partial support

**Current Stats:**
- 6,278 code entities extracted
- 16,445 relationships mapped
- 5 Regen repositories indexed:
  - `regen-ledger` - Core blockchain module
  - `regen-web` - Frontend applications
  - `regen-data-standards` - Data schemas and standards
  - `regen-registry-handbook` - Registry documentation
  - `regen-registry-methodology-library` - Methodology definitions

### Entity Extractor (Knowledge Graph)
Extracts semantic entities and relationships:
- People, organizations, projects
- Methodologies, credit classes
- Geographic locations
- Temporal relationships

---

## Layer 4: Storage Systems

### PostgreSQL + pgvector
**Purpose:** Vector database for semantic search
**Port:** 5432
**Contents:**
- 15,000+ document embeddings
- Full text content
- Metadata (source, timestamp, author)
- RID (Resource Identifier) index

### Apache Jena Fuseki (Port 3030)
**Purpose:** RDF triplestore for knowledge graph
**Contents:**
- 3,900+ semantic triples
- Entity relationships
- Ontology definitions
- SPARQL query endpoint

### Apache AGE (Graph Extension)
**Purpose:** Code entity graph database
**Contents:**
- 6,278 code entities
- 16,445 code relationships
- Function call graphs
- Module dependencies

---

## Layer 5: Query & Access Services

### MCP Server (Port 8200)
Model Context Protocol server exposing 8 tools:

| Tool | Purpose | Query Type |
|------|---------|------------|
| `search_knowledge` | Semantic document search | Vector + Graph hybrid |
| `get_stats` | Knowledge base statistics | Metadata |
| `generate_weekly_digest` | Create activity digests | Aggregation |

### Hybrid RAG API (Port 8301)
Reciprocal Rank Fusion combining:
- Vector similarity (pgvector)
- Graph traversal (Jena + AGE)
- Keyword matching (PostgreSQL FTS)

**Query Flow:**
```
Query ──► Hybrid RAG API
              │
    ┌─────────┼─────────┐
    │         │         │
    ▼         ▼         ▼
 Vector    Graph     Keyword
 Search   Traverse   Match
    │         │         │
    └─────────┼─────────┘
              │
              ▼
    Reciprocal Rank Fusion
              │
              ▼
       Ranked Results
```

### Full-Stack Technical Assistant (8 MCP Tools)

**Core KOI Tools:**
| Tool | Function | Data Source |
|------|----------|-------------|
| `search_knowledge` | Hybrid vector + graph search | pgvector + Jena |
| `get_stats` | System statistics | All databases |
| `generate_weekly_digest` | Weekly summaries | Curator output |

**Full-Stack Technical Tools (NEW):**
| Tool | Function | Data Source |
|------|----------|-------------|
| `query_code_graph` | Query code entities and relationships | Apache AGE |
| `search_github_docs` | Search across Regen GitHub repos | GitHub sensor data |
| `get_repo_overview` | Get repo structure/overview | RAPTOR summaries |
| `get_tech_stack` | See languages, frameworks, dependencies | Code graph |

**Example Prompts:**
- "How does MsgCreateBatch work in the ecocredit module?"
- "What keepers handle credit retirement?"
- "Search for validator setup documentation"
- "Show me the tech stack for regen-ledger"

---

## Layer 6: Intelligence Services

### RAPTOR Summaries
Hierarchical Abstraction for Retrieval:
- 66 module summaries generated
- Multi-level abstraction (file → module → package → repo)
- Enables high-level conceptual queries

### Daily Curator
- Analyzes each day's knowledge changes
- Identifies patterns and highlights
- Prepares summaries for stakeholders
- Runs: End of each day

### Weekly Curator
- Synthesizes week's activity
- Generates comprehensive digests
- Feeds automated podcast generation
- Output: digest.gaiaai.xyz

### Eliza Agents Integration
Autonomous AI agents that:
- Query MCP tools for knowledge
- Engage with communities
- Answer questions
- Generate content
- Participate in governance

---

## Layer 7: Output & Actuators

### Automated Podcast
**URL:** digest.gaiaai.xyz
**Pipeline:**
```
Weekly Curator ──► Digest Generation ──► TTS ──► Audio File ──► Podcast Feed
```

### Dashboard (Port 8400)
- Real-time system status
- Ingestion metrics
- Query analytics
- Health monitoring

### API Endpoints
- REST API for external integrations
- WebSocket for real-time updates
- GraphQL (planned)

---

## Service Port Reference

| Port | Service | Status |
|------|---------|--------|
| 5432 | PostgreSQL + pgvector | Active |
| 3030 | Apache Jena Fuseki | Active |
| 8005 | KOI Coordinator | Active |
| 8090 | BGE Embeddings | Active |
| 8100 | Event Bridge v2 | Active |
| 8200 | MCP Server | Active |
| 8301 | Hybrid RAG API | Active |
| 8350 | Code Graph Service | Active |
| 8400 | Dashboard | Active |

---

## Data Flow Summary

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                              DATA FLOW                                        │
└──────────────────────────────────────────────────────────────────────────────┘

1. INGESTION
   Sensors ──► KOI Coordinator ──► Event Bridge v2
                                        │
2. PROCESSING                           │
   ┌────────────────────────────────────┼────────────────────────────────────┐
   │                                    │                                    │
   ▼                                    ▼                                    ▼
BGE Embeddings               Code Graph Service                    Entity Extractor
   │                                    │                                    │
   ▼                                    ▼                                    ▼
pgvector                          Apache AGE                          Jena Fuseki
   │                                    │                                    │
   └────────────────────────────────────┼────────────────────────────────────┘
                                        │
3. QUERY & ACCESS                       │
                                        ▼
                              ┌─────────────────┐
                              │  Hybrid RAG API │
                              │   (Port 8301)   │
                              └────────┬────────┘
                                       │
                                       ▼
                              ┌─────────────────┐
                              │   MCP Server    │
                              │   (Port 8200)   │
                              └────────┬────────┘
                                       │
4. CONSUMPTION                         │
   ┌───────────────────────────────────┼───────────────────────────────────┐
   │                                   │                                   │
   ▼                                   ▼                                   ▼
Claude Desktop                   Eliza Agents                      Weekly Curator
   │                                   │                                   │
   ▼                                   ▼                                   ▼
Human Users                    Community Engagement              digest.gaiaai.xyz
```

---

## Visual Design Recommendations

### Color Scheme
- **Blue:** Sensors (input nodes)
- **Red:** Coordinator (central hub)
- **Purple:** Processors (transformation)
- **Pink:** Storage (databases)
- **Cyan:** Services (query/access)
- **Orange:** Curators (synthesis)
- **Green:** Outputs/Actuators

### Layout Approach
1. **Layered Architecture:** Top-to-bottom flow from sensors to outputs
2. **Central Hub:** Coordinator prominently centered
3. **Parallel Pipelines:** Show vector, graph, and code paths side-by-side
4. **Port Labels:** Include port numbers for technical reference
5. **Stats Callouts:** Highlight key metrics (15k docs, 6k entities, etc.)

### Key Differentiators from v1
1. **Code Graph Service:** New pipeline for code entity extraction
2. **Hybrid RAG:** Explicit Reciprocal Rank Fusion visualization
3. **8 MCP Tools:** Enumerate all tools with their purposes
4. **RAPTOR Summaries:** Show hierarchical abstraction layer
5. **Expanded Sensors:** 12 sensors vs previous 9
6. **Apache AGE:** New graph database for code entities
7. **Service Ports:** All ports clearly labeled

---

## Metrics Snapshot (November 2025)

| Metric | Value |
|--------|-------|
| Documents Indexed | 15,000+ |
| Semantic Embeddings | 15,000+ |
| Knowledge Graph Triples | 3,900+ |
| Code Entities | 6,278 |
| Code Relationships | 16,445 |
| RAPTOR Module Summaries | 66 |
| Active Sensors | 12 |
| MCP Tools | 7 (3 core + 4 full-stack) |
| Regen Repositories Indexed | 5 |

---

## Technical Trajectory

### Recently Completed (Phase 2c)
- Full-stack technical assistant MCP tools
- Code Graph Service with multi-language support
- RAPTOR hierarchical summaries
- Hybrid RAG with Reciprocal Rank Fusion
- HTTP API for external integrations

### In Progress
- Interactive 3D podcast visualization
- Enhanced entity extraction
- Cross-repository dependency mapping

### Planned
- Real-time streaming updates
- Multi-tenant knowledge isolation
- Federated KOI network connections
- GraphQL API layer

---

*This specification provides the complete context needed to create an accurate, comprehensive architecture diagram for the RegenAI KOI system.*
