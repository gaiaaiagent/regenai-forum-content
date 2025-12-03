
---

## The Code Graph: From Documents to Implementation

While document knowledge tells us *what* Regen Network does, the code graph reveals *how* it does it. When an AI agent needs to understand credit retirement, it can trace from a concept in a forum post → through the `MsgRetire` message type → to the Keeper that handles it → to the exact function implementation on GitHub. This is the bridge between human-readable knowledge and machine-executable code.

The KOI MCP has evolved beyond document search into a full-stack technical assistant. Seven repositories are now indexed with deep code understanding, comprising **27,414 code entities**:

| Repository               | Description                           |
| ------------------------ | ------------------------------------- |
| **regen-ledger**         | The Cosmos SDK blockchain core        |
| **regen-web**            | TypeScript/React frontend application |
| **koi-sensors**          | KOI network sensor implementations    |
| **koi-processor**        | Knowledge processing pipeline         |
| **regen-koi-mcp**        | The MCP server you're using now       |
| **koi-research**         | Research and documentation            |
| **regen-data-standards** | JSON schemas for ecological data      |

### Understanding Entity Types

The code graph extracts typed entities using tree-sitter AST parsing—understanding code structure rather than treating it as plain text:

| Entity Type   | What It Represents                                                     |
| ------------- | ---------------------------------------------------------------------- |
| **Entity**    | General code constructs (variables, constants, types)                  |
| **Type**      | Type definitions and aliases                                           |
| **Interface** | Go interfaces and TypeScript interfaces                                |
| **Function**  | Standalone functions across all repos                                  |
| **Message**   | Cosmos SDK transaction message types (MsgCreateBatch, MsgRetire, etc.) |
| **Query**     | gRPC query handlers for reading blockchain state                       |
| **Event**     | Blockchain events emitted by transactions                              |
| **Keeper**    | Core module state managers (the heart of each Cosmos module)           |

The Cosmos SDK-specific types—**Keeper**, **Message**, **Query**, and **Event**—are particularly valuable. These are the architectural backbone of regen-ledger: Messages define what users can do, Keepers manage state, Queries expose data, and Events record what happened.

### The 3D Code Graph Visualization


![regen-koi-graph|690x336](upload://y5Hf3fxS5OrE5TLiiwjUpx5jAVa.jpeg)
*The interactive 3D code graph showing 1,000 sampled entities from the full 27,414-entity database. Colors indicate entity types: Functions (green), Interfaces (purple), Messages (orange), Keepers (blue). Clusters reveal module structure; hub nodes indicate core infrastructure.*

The visualization uses a force-directed graph algorithm where:

- **Clusters** indicate tightly coupled modules—entities defined in the same file or with related names appear spatially close
- **Hub nodes** with many connections are core infrastructure—the Keepers at the center of each module
- **Peripheral nodes** are specialized utilities—used in specific contexts, connected to fewer neighbors
- **Color coding** instantly distinguishes entity types, making architectural patterns visible at a glance

### How Relationships Are Discovered

The graph contains over **11,000 relationships** between entities, inferred through multiple strategies:

1. **Same-file relationships**: Entities defined in the same source file are likely related—a Keeper and its helper functions, a Message and its validation logic
2. **Naming conventions**: Cosmos SDK follows predictable patterns. `MsgCreateBatch` relates to `CreateBatch`, `QueryBalance` relates to `Balance`
3. **Call graph analysis**: Functions that call other functions create explicit dependency edges
4. **Import analysis**: Module imports reveal architectural dependencies

### Discovery Example: Understanding Credit Retirement

Here's how the code graph enables deep technical understanding:

1. **Search**: "What happens when credits are retired?"
2. **Graph query**: Find `MsgRetire` message type
3. **Trace relationship**: `MsgRetire` → handled by `Keeper.Retire()`
4. **View source**: Click through to `x/ecocredit/base/keeper/msg_retire.go` on GitHub
5. **Explore context**: See related functions in the same cluster—validation, event emission, state updates

This is structural intelligence that document search alone cannot efficiently provide. You're not just finding *mentions* of retirement—you're tracing the actual execution path through the codebase.

### Code Intelligence Tools

The new code graph tools make this exploration accessible through natural language:

- *"Which Keeper handles MsgCreateBatch in the ecocredit module?"*
- *"What functions call the credit retirement handler?"*
- *"Show me the tech stack for regen-ledger"*
- *"Search for validator setup documentation across all repos"*
- *"What events are emitted when a credit batch is created?"*

A future blog post will be dedicated to the Regen KOI Code Graph and how it's used to power the Regen Full-Stack agent. 

