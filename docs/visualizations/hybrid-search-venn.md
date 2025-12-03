# Hybrid Search Venn Diagram Specification

**Purpose:** Illustrate how three search methods combine via Reciprocal Rank Fusion
**Tool:** Canva, Figma, or vector graphics
**Style:** Clean, modern infographic

---

## Concept

A Venn diagram showing three overlapping circles representing Vector Search, Graph Traversal, and Keyword Match, with the center intersection representing Hybrid RAG (Reciprocal Rank Fusion).

---

## Visual Layout

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                                                                             │
│                         HYBRID RAG: THE POWER OF THREE                      │
│                         ──────────────────────────────                      │
│                                                                             │
│                              ┌─────────────────┐                            │
│                              │                 │                            │
│                              │  VECTOR SEARCH  │                            │
│                              │    (pgvector)   │                            │
│                              │                 │                            │
│                              │  • Semantic     │                            │
│                              │    similarity   │                            │
│                              │  • "What does   │                            │
│                              │    this mean?"  │                            │
│                   ┌──────────┴────┬────────────┴──────────┐                │
│                   │               │                       │                 │
│                   │               │                       │                 │
│     ┌─────────────┴───────┐       │       ┌───────────────┴─────────┐      │
│     │                     │       │       │                         │      │
│     │   GRAPH TRAVERSAL   │       │       │     KEYWORD MATCH       │      │
│     │    (Jena + AGE)     ├───────┼───────┤     (PostgreSQL FTS)    │      │
│     │                     │       │       │                         │      │
│     │  • Relationships    │  ┌────┴────┐  │  • Exact terms          │      │
│     │  • "Who wrote       │  │         │  │  • "Find mentions of    │      │
│     │    this about       │  │  RRF    │  │    C01-001 credit"      │      │
│     │    what topic?"     │  │ HYBRID  │  │                         │      │
│     │                     │  │         │  │                         │      │
│     └─────────────────────┘  └─────────┘  └─────────────────────────┘      │
│                                   │                                         │
│                                   │                                         │
│                              ┌────┴────┐                                   │
│                              │         │                                   │
│                              │  BEST   │                                   │
│                              │ RESULTS │                                   │
│                              │         │                                   │
│                              └─────────┘                                   │
│                                                                             │
│  ═══════════════════════════════════════════════════════════════════════   │
│                                                                             │
│   Vector finds meaning │ Graph finds connections │ Keywords find specifics  │
│                        │                         │                          │
│                        └─────────┬───────────────┘                          │
│                                  │                                          │
│                          RRF combines all three                             │
│                          for comprehensive results                          │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Three Search Methods Explained

### 1. Vector Search (Semantic)
- **Database:** PostgreSQL + pgvector
- **Method:** Cosine similarity on 1024-dim BGE embeddings
- **Strength:** Understanding meaning and intent
- **Example Query:** "What projects improve soil health?"
- **Finds:** Documents about carbon sequestration, regenerative agriculture, etc.
- **Color:** Blue (#3B82F6)

### 2. Graph Traversal (Relational)
- **Databases:** Apache Jena (RDF) + Apache AGE (Code)
- **Method:** SPARQL queries and Cypher traversal
- **Strength:** Finding connections and relationships
- **Example Query:** "What did Gregory write about governance?"
- **Finds:** All documents by author on topic, related proposals, etc.
- **Color:** Green (#22C55E)

### 3. Keyword Match (Exact)
- **Database:** PostgreSQL Full-Text Search
- **Method:** Term frequency and exact matching
- **Strength:** Finding specific identifiers and terms
- **Example Query:** "C01-001-20210101-20210101-001"
- **Finds:** Exact batch ID references, specific terminology
- **Color:** Orange (#F97316)

---

## Center Intersection: RRF

**Reciprocal Rank Fusion** combines results:

```
RRF Score = Σ (1 / (k + rank_i))
```

Where:
- `k` = constant (typically 60)
- `rank_i` = position in each result list

**Benefits:**
- No single method dominates
- Balances precision and recall
- Handles cases where one method fails
- Produces more robust results

**Color:** Purple (#A855F7) or Gold (#F59E0B)

---

## Visual Elements

### Circle Labels
Each circle should have:
1. **Title** (bold, large)
2. **Database** (smaller, italic)
3. **Key capability** (bullet point)
4. **Example query** (quoted, smaller)

### Intersection Labels
- Vector + Graph: "Semantic relationships"
- Vector + Keyword: "Meaningful mentions"
- Graph + Keyword: "Specific connections"
- All Three (center): "RRF HYBRID"

### Arrow or Flow
Show arrow from center to "BEST RESULTS" box below

---

## Color Scheme

| Element | Color | Hex |
|---------|-------|-----|
| Vector circle | Blue | #3B82F6 |
| Graph circle | Green | #22C55E |
| Keyword circle | Orange | #F97316 |
| RRF center | Purple/Gold | #A855F7 / #F59E0B |
| Background | Light gray or white | #F9FAFB |
| Text | Dark gray | #1F2937 |

---

## Typography

- **Title:** Bold, 24pt, centered above diagram
- **Circle titles:** Bold, 16pt
- **Subtitles:** Regular, 12pt, italic
- **Descriptions:** Regular, 11pt
- **Footer:** Regular, 10pt

---

## Alternative: Linear Fusion Diagram

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         HYBRID RAG FUSION                                    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   QUERY: "What projects improve soil health in tropical regions?"           │
│      │                                                                      │
│      ▼                                                                      │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │                         PARALLEL SEARCH                          │     │
│   ├──────────────────┬──────────────────┬────────────────────────────┤     │
│   │                  │                  │                            │     │
│   ▼                  ▼                  ▼                            │     │
│ ┌──────┐          ┌──────┐          ┌──────┐                        │     │
│ │Vector│          │Graph │          │Keyword│                        │     │
│ │Search│          │Query │          │Match │                        │     │
│ └──┬───┘          └──┬───┘          └──┬───┘                        │     │
│    │                 │                 │                             │     │
│    ▼                 ▼                 ▼                             │     │
│ ┌──────┐          ┌──────┐          ┌──────┐                        │     │
│ │Rank 1│          │Rank 1│          │Rank 1│                        │     │
│ │Rank 2│          │Rank 2│          │Rank 2│                        │     │
│ │Rank 3│          │Rank 3│          │Rank 3│                        │     │
│ │  ⋮   │          │  ⋮   │          │  ⋮   │                        │     │
│ └──┬───┘          └──┬───┘          └──┬───┘                        │     │
│    │                 │                 │                             │     │
│    └─────────────────┴─────────────────┘                            │     │
│                      │                                               │     │
│                      ▼                                               │     │
│              ┌───────────────┐                                      │     │
│              │ RECIPROCAL    │                                      │     │
│              │ RANK FUSION   │                                      │     │
│              │               │                                      │     │
│              │ Score = Σ 1   │                                      │     │
│              │        ─────  │                                      │     │
│              │        k+rank │                                      │     │
│              └───────┬───────┘                                      │     │
│                      │                                               │     │
│                      ▼                                               │     │
│              ┌───────────────┐                                      │     │
│              │ FINAL RANKED  │                                      │     │
│              │   RESULTS     │                                      │     │
│              │               │                                      │     │
│              │ 1. Brazil     │                                      │     │
│              │    forest...  │                                      │     │
│              │ 2. Kenya      │                                      │     │
│              │    agrofor... │                                      │     │
│              │ 3. Indonesia  │                                      │     │
│              │    peat...    │                                      │     │
│              └───────────────┘                                      │     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Key Message

**"Three search methods, combined by reciprocal rank fusion, deliver results that no single method could achieve alone."**

The diagram should emphasize:
1. **Complementary strengths** - Each method excels at different things
2. **Parallel execution** - All three run simultaneously
3. **Mathematical combination** - RRF is a principled fusion method
4. **Better results** - The combination outperforms any single approach
