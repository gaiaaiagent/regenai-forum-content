# 5-Minute Flow Diagram Specification

**Purpose:** Show how knowledge travels from source to searchable in under 5 minutes
**Tool:** Canva, Figma, or similar
**Style:** Clean timeline with icons and timestamps

---

## Concept

A horizontal timeline showing a piece of knowledge (e.g., a forum post) traveling through the KOI system with timestamps at each stage.

---

## Visual Layout

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                    FROM POST TO SEARCHABLE IN 5 MINUTES                              │
│                    ─────────────────────────────────────────                         │
│                                                                                      │
│  ┌─────┐    ┌─────┐    ┌─────┐    ┌─────┐    ┌─────┐    ┌─────┐    ┌─────┐         │
│  │ 📝  │───►│ 👁️  │───►│ 🔀  │───►│ 🧮  │───►│ 💾  │───►│ 🔍  │───►│ 🤖  │         │
│  │     │    │     │    │     │    │     │    │     │    │     │    │     │         │
│  │POST │    │SENSE│    │ROUTE│    │EMBED│    │STORE│    │INDEX│    │QUERY│         │
│  └──┬──┘    └──┬──┘    └──┬──┘    └──┬──┘    └──┬──┘    └──┬──┘    └──┬──┘         │
│     │         │          │          │          │          │          │             │
│  ═══╪═════════╪══════════╪══════════╪══════════╪══════════╪══════════╪═════════    │
│     │         │          │          │          │          │          │             │
│   0:00      0:01       0:02       0:03       0:04       0:05       5:00+           │
│   ─────     ─────      ─────      ─────      ─────      ─────      ─────           │
│   Gregory   Discourse  KOI        BGE        PostgreSQL Hybrid     Claude          │
│   posts     Sensor     Coordinator Embeddings + pgvector RAG API   Desktop         │
│   proposal  detects    routes     generates   stores     indexes   AI answers      │
│             change     event      1024-dim    document   for       "What's new     │
│                                   vector                 search    in governance?" │
│                                                                                      │
│  ════════════════════════════════════════════════════════════════════════════════   │
│                              TOTAL TIME: < 5 MINUTES                                 │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

---

## Detailed Steps

### Step 1: POST (0:00)
- **Icon:** 📝 Document/pen
- **Actor:** Gregory (community member)
- **Action:** Posts governance proposal on forum.regen.network
- **Visual:** Speech bubble or forum icon

### Step 2: SENSE (0:01)
- **Icon:** 👁️ Eye or radar
- **Actor:** Discourse Sensor
- **Action:** Detects new topic, generates RID
- **Visual:** Sensor icon pulsing
- **RID shown:** `orn:discourse.forum.regen.network:topic/482`

### Step 3: ROUTE (+0:01)
- **Icon:** 🔀 Split arrows
- **Actor:** KOI Coordinator (port 8005)
- **Action:** Receives FUN event (NEW), routes to Event Bridge
- **Visual:** Central hub with routing arrows

### Step 4: EMBED (+0:01)
- **Icon:** 🧮 Calculator or neural network
- **Actor:** BGE Embeddings (port 8090)
- **Action:** Generates 1024-dimensional semantic vector
- **Visual:** Document transforming into vector representation

### Step 5: STORE (+0:01)
- **Icon:** 💾 Database cylinder
- **Actor:** PostgreSQL + pgvector (port 5432)
- **Action:** Stores text, metadata, and embedding
- **Visual:** Database with document entering

### Step 6: INDEX (+0:01)
- **Icon:** 🔍 Magnifying glass
- **Actor:** Hybrid RAG API (port 8301)
- **Action:** Document now discoverable via semantic search
- **Visual:** Search index updating

### Step 7: QUERY (5:00+)
- **Icon:** 🤖 Robot or Claude logo
- **Actor:** Claude Desktop via MCP
- **Action:** User asks "What's happening with credit class governance?"
- **Visual:** AI agent retrieving and citing the post

---

## Color Scheme

| Stage | Color | Meaning |
|-------|-------|---------|
| POST | Blue | Human input |
| SENSE | Green | Detection |
| ROUTE | Red | Central coordination |
| EMBED | Purple | Processing |
| STORE | Pink | Storage |
| INDEX | Cyan | Query-ready |
| QUERY | Orange | AI consumption |

---

## Typography

- **Title:** Bold, 24pt+
- **Stage labels:** Bold, 14pt
- **Timestamps:** Monospace, 12pt
- **Descriptions:** Regular, 11pt

---

## Annotations to Include

1. **RID callout:** Show the unique identifier format
2. **FUN event badge:** "NEW" event type
3. **Vector dimensions:** "1024-dim" label on embedding
4. **Port numbers:** Small badges at each service

---

## Alternative: Vertical Timeline

```
┌─────────────────────────────────────────┐
│     FROM POST TO SEARCHABLE             │
│         IN 5 MINUTES                    │
├─────────────────────────────────────────┤
│                                         │
│  0:00  ●═══ Gregory posts proposal      │
│        │                                │
│  0:01  ●═══ Discourse Sensor detects    │
│        │    RID: orn:discourse...       │
│        │                                │
│  0:02  ●═══ KOI Coordinator routes      │
│        │    Event: NEW                  │
│        │                                │
│  0:03  ●═══ BGE generates embedding     │
│        │    1024 dimensions             │
│        │                                │
│  0:04  ●═══ PostgreSQL stores           │
│        │                                │
│  0:05  ●═══ Hybrid RAG indexes          │
│        │                                │
│  5:00+ ●═══ Claude answers query        │
│             with citation               │
│                                         │
│  ═══════════════════════════════════    │
│      TOTAL: < 5 MINUTES                 │
└─────────────────────────────────────────┘
```

---

## Key Message

**"Knowledge flows through KOI like signals through a nervous system—fast, efficient, and traceable."**

The diagram should emphasize:
1. **Speed** - Under 5 minutes from post to searchable
2. **Traceability** - Every step is auditable
3. **Automation** - No human intervention needed
4. **Citation** - AI can cite the exact source
