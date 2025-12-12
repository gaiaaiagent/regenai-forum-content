# Connecting ChatGPT Custom GPTs to MCP Servers: Architecture, Best Practices, and Limitations

**Research Date:** December 9, 2025
**Prepared by:** Claude Code Agent
**Purpose:** Blog post research on GPT-MCP integration approaches

---

## Executive Summary

This report investigates how ChatGPT Custom GPTs can connect to Model Context Protocol (MCP) servers, comparing the architectural approaches between GPT Custom Actions (API proxy method) and native MCP access (Claude Code method). The research reveals significant architectural differences, performance trade-offs, and practical limitations when connecting GPTs to MCP infrastructure.

Key findings:
- GPTs require an HTTP REST API wrapper/proxy to access MCP servers (cannot use native JSON-RPC/stdio)
- Direct MCP protocol access (Claude Code) offers superior performance, state management, and tool discovery
- GPT hallucinations can be significantly reduced through careful system instruction design
- The Regen KOI GPT demonstrates both the potential and pitfalls of GPT-based MCP access

---

## 1. How ChatGPT Custom GPTs Work with External APIs

### 1.1 GPT Actions Overview

GPT Actions empower ChatGPT users to interact with external applications via RESTful API calls using natural language. They convert natural language text into the JSON schema required for an API call. At their core, GPT Actions leverage Function Calling to:

1. Decide which API call is relevant to the user's question
2. Generate the JSON input necessary for the API call
3. Execute the API call using the third party app's authentication

**Source:** [OpenAI GPT Actions Documentation](https://platform.openai.com/docs/actions/introduction)

### 1.2 Architecture: GPT Builder Custom Actions

Custom GPTs allow developers to:
- Describe the schema of an API call via OpenAPI specification
- Configure authentication mechanisms (API key, OAuth 2.0, or none)
- Add custom instructions to guide the GPT's behavior
- Attach knowledge files for additional context

The GPT acts as a bridge between user's natural language questions and the API layer, abstracting away the complexity of API calls from end users.

**Source:** [How To Build Custom GPTs - CometAPI](https://www.cometapi.com/how-to-build-custom-gpts/)

### 1.3 New Development: ChatGPT Apps (October 2025)

In October 2025, OpenAI introduced the Apps SDK, allowing developers to build apps that run directly inside ChatGPT conversations. This represents an evolution beyond simple Custom Actions:

**GPTs (Custom Actions):**
- Text-based responses via OpenAPI integration
- Instruction-first assistant over knowledge base
- Limited to API call patterns

**Apps:**
- Authenticated actions with embedded UI components
- In-chat discovery and visual workflows
- More complex multi-step interactions

Launch partners included Booking.com, Canva, Coursera, Expedia, Figma, Spotify, and Zillow.

**Source:** [Apps in ChatGPT vs Custom GPTs](https://skywork.ai/blog/apps-in-chatgpt-vs-custom-gpts-gpt-apps-2025-comparison/)

---

## 2. Creating Custom Actions in GPT Builder

### 2.1 OpenAPI Schema Requirements

For GPT Actions, OpenAPI schemas define the functionality of each action. The schema must include:

**Core Components:**
- OpenAPI version (3.0 or later)
- API title and description
- Server URL(s)
- Paths (endpoints) with operations

**Per-Operation Details:**
- `operationId` - Unique identifier ChatGPT uses to call the action
- Description - Helps the model understand when to use this action
- Parameters - Query, path, header, or body parameters
- Request/response schemas
- Authentication configuration

**Example Structure:**
```json
{
  "openapi": "3.0.0",
  "info": {
    "title": "Regen KOI API",
    "version": "1.0.0"
  },
  "servers": [
    {
      "url": "https://regen.gaiaai.xyz/api/koi"
    }
  ],
  "paths": {
    "/query": {
      "post": {
        "operationId": "searchKOI",
        "description": "Search Regen Network knowledge base",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "query": {"type": "string"},
                  "limit": {"type": "integer"}
                }
              }
            }
          }
        }
      }
    }
  }
}
```

**Tools for Schema Creation:**
- OpenAI's "Actions GPT" - can generate schemas from API documentation
- Swagger Editor - for validation
- OpenAPI Action Builder GPT - specialized schema generator

**Sources:**
- [Creating OpenAPI Schemas for Custom GPTs - BYU](https://genai.byu.edu/creating-openapi-schemas-for-custom-gpts)
- [GPT Actions Library - OpenAI Cookbook](https://cookbook.openai.com/examples/chatgpt/gpt_actions_library/.gpt_action_getting_started)

### 2.2 Authentication Methods

GPT Actions support three authentication mechanisms:

**1. No Authentication**
- For public, read-only endpoints
- No credentials required

**2. API Key Authentication**
- Stored server-side by OpenAI
- Automatically injected into requests
- Can be header-based or custom

**3. OAuth 2.0**
- User signs in through authorization server
- ChatGPT performs Authorization Code flow with PKCE
- Access token attached to subsequent requests as `Authorization: Bearer <token>`

**Important Security Note:** When using OAuth with MCP servers, the server must validate tokens server-side:
- Verify signature using JWKS
- Check issuer, audience, expiry
- Enforce required scopes
- ChatGPT does NOT support client credentials or service account flows

**Sources:**
- [GPT Action Authentication - OpenAI](https://platform.openai.com/docs/actions/authentication)
- [How to Add Authentication to MCP-Powered ChatGPT App - Stytch](https://stytch.com/blog/guide-to-authentication-for-the-openai-apps-sdk/)

### 2.3 Limitations of Custom Actions

**Technical Constraints:**
- 8,000 character limit on custom instructions
- 512 MB limit per knowledge file upload
- Multiple file uploads can cause errors
- Text files work better than JSON/structured formats
- Cannot pass images through actions (including DALL-E generated or user-uploaded)

**Workflow Limitations:**
- Cannot combine multiple Custom GPTs in a single conversation
- Lack robust step-chaining for complex workflows
- No persistent memory across long tasks
- Limited context retention during extended conversations

**Integration Challenges:**
- No native support for tools like Slack or Salesforce (must wire manually)
- Each function requires separate custom Action definition
- Cannot directly call other GPTs or combine their capabilities

**Sources:**
- [Custom GPT Actions Limits - OpenAI Community](https://community.openai.com/t/custom-gpt-actions-limits/493329)
- [Why You Should Not Build Custom GPT with Actions](https://sivi.ai/blog/why-you-should-not-build-custom-gpt-with-actions-chatgpt-plugin)

---

## 3. The Regen KOI GPT: A Case Study in Hallucination

### 3.1 How the Regen KOI GPT Works

The Regen KOI GPT (available at https://chatgpt.com/g/g-67605ebed10c8191a1e91dfbf63e1ade-regen-koi) is configured to access the Regen KOI (Knowledge Organization Infrastructure) via Custom Actions. It queries:

- **KOI API**: Knowledge base search at `https://regen.gaiaai.xyz/api/koi`
- **Regen Ledger Data**: Blockchain credit information
- **Registry Metadata**: Project and methodology documentation

### 3.2 Documented Hallucination Incidents

Based on internal testing documented in `/docs/other/2025-12-09-koi-gpt-hallucination.md`, the Regen KOI GPT exhibited several severe hallucination patterns:

**Incident 1: Fabricated Credit Data**
- **Query:** "What is the total number of credits live on Regen Ledger?"
- **First Response:** Provided detailed table with 11 credit classes, specific issuance numbers, hectares, and dollar values
- **Problem:** Data included credit classes with completely fabricated issuance numbers
- **Example:** Claimed Kulshan Carbon Trust issued ~410,000 tCO2e when actual on-chain issuance was only 372 tCO2e

**Incident 2: Invalid Data Sources**
- **Claim:** "Data verified via Regen Ledger Explorer at `regen.aneka.io`"
- **Reality:** This explorer domain does not exist
- **Impact:** All "verified" batch numbers and transaction hashes were fabricated

**Incident 3: Missing Credit Classes**
- **First Query:** Returned 5 carbon-focused credit classes
- **Correction Needed:** User had to explicitly request ERA Brazil, Terrasos, SeaTrees Marine Biodiversity, and Kulshan Biochar
- **Root Cause:** GPT queried KOI with carbon-centric keywords, missing biodiversity/marine classifications

**Incident 4: Conflating Registry vs Ledger Data**
- **Confusion:** Mixed off-chain Registry protocols (approved but not issued) with on-chain Ledger issuances
- **Initially Claimed:** ERA Brazil and Terrasos were "off-chain only"
- **Actual Status:** Both credit classes were live on-chain since August 2025
- **Problem:** GPT accessed outdated KOI index snapshot from May 2025

### 3.3 Why the GPT Hallucinated

**Root Causes Identified:**

1. **Data Namespace Confusion**
   - KOI indexes multiple sources: Ledger (on-chain), Registry (off-chain), GitHub, forums
   - GPT query defaulted to Ledger namespace, excluding Registry-only protocols
   - Biodiversity credits stored under different schema fields (`credit_protocol` vs `credit_class`)

2. **Index Lag**
   - KOI syncs every few months from Ledger API
   - GPT accessed May 2025 snapshot, missing August 2025 on-chain updates
   - New credit classes appeared on Registry before KOI index updated

3. **Lack of On-Chain Verification**
   - GPT cannot directly query Regen Ledger gRPC/RPC endpoints
   - Relies entirely on KOI's cached/indexed data
   - No ability to verify issuance numbers against blockchain state

4. **Confidence in Fabricated Details**
   - LLMs generate plausible-sounding specific numbers (batch IDs, transaction hashes)
   - GPT presented estimated/projected figures as "verified on-chain data"
   - Cited non-existent explorers with authoritative tone

**Source:** Internal documentation at `/home/ygg/Workspace/RegenAI/regenai-forum-content/docs/other/2025-12-09-koi-gpt-hallucination.md`

### 3.4 Corrected Data (After Multiple Iterations)

After several correction rounds and explicit verification requests, the GPT eventually provided accurate data:

**Actual Regen Ledger Stats (December 2025):**
- Total Credits Issued: 1,039,069
- Currently Tradable: 525,655
- Retired: 106,413
- Total Credit Classes: 13 (not 11)
- Total Land Managed: ~560,000 hectares
- Estimated Market Value: $8.6-9.8M USD

**Accurate Credit Classes:**
- C01: CarbonPlus Grasslands (4,539 credits)
- C02: Urban Forest Carbon (33,028 credits)
- C03: Toucan VCS Bridged (522,530 credits)
- C05: Kulshan Biochar (23 credits - NOT 410,000)
- C06: Ecometric Soil Carbon (69,943 credits)
- BT01: Terrasos Biodiversity (30,233 credits)
- USS01: ERA Brazil Jaguar Habitat (77,988 credits)
- MBS01: SeaTrees Marine Biodiversity (300,000 credits)
- KSH01: Sheep Grazing Stewardship (786 credits)

**Source:** `/home/ygg/Workspace/RegenAI/regenai-forum-content/docs/other/2025-12-09-KOI-MCP-usage.md`

---

## 4. Best Practices for GPT System Instructions to Prevent Hallucination

### 4.1 Explicit Uncertainty Instructions

**Key Principle:** Tell the AI what to do when it doesn't know.

**Recommended Instructions:**
```
If you don't know an answer, don't infer anything or make up answers.
Just tell the user you don't know the answer.

When uncertain or lacking sufficient information to provide an accurate answer:
- Say "I'm not sure" or "I don't have enough information to answer that"
- Explain specifically what information is missing or unclear
- Never provide speculative or fabricated information
```

**Source:** [How To Stop ChatGPT Hallucinations - God of Prompt](https://www.godofprompt.ai/blog/stop-chatgpt-hallucinations)

### 4.2 Ground Responses to Provided Sources

**Force Source Citation:**
```
You MUST cite sources for all factual claims.

When providing data:
1. Reference the specific API endpoint or document used
2. Include timestamps for time-sensitive information
3. Distinguish between verified data and estimates
4. If data comes from a cache or index, state the index date

Example format:
"According to the Regen Ledger query executed on [timestamp],
credit class C01 has issued 4,539 credits (source: /api/ledger/batches)."
```

**Grounded Answer Approach:**
```
Use ONLY the sources provided. Do not use your training data to answer questions.

If the provided sources don't contain the answer:
- State "The provided sources do not contain this information"
- Do NOT attempt to fill gaps with general knowledge
- Suggest alternative sources or queries the user could try
```

**Source:** [How to Reduce Hallucinations in ChatGPT - OpenAI Community](https://community.openai.com/t/how-to-reduce-hallucinations-in-chatgpt-responses-to-data-queries/900796)

### 4.3 Custom Instructions Framework

ChatGPT's custom instructions act as persistent ground rules for every conversation. Structure them with:

**Components:**
1. **Task** - What the GPT should do
2. **Context** - What data sources are available
3. **Expectations** - Accuracy requirements, citation standards
4. **Output Format** - How to structure responses

**Example Custom Instructions for Data-Heavy GPTs:**
```
ROLE: You are a Regen Network data assistant with access to the KOI API.

DATA SOURCES:
- KOI API: Cached/indexed data (may be outdated)
- You DO NOT have direct blockchain access
- You CANNOT verify on-chain state in real-time

ACCURACY REQUIREMENTS:
1. Always state the data source and timestamp
2. Distinguish "API returned" vs "estimated" vs "unknown"
3. If asked for on-chain verification you cannot provide, say so explicitly
4. When providing numbers, include confidence qualifiers:
   - "KOI API reports..." (for cached data)
   - "Estimated based on..." (for projections)
   - "Cannot verify - would require direct chain query"

PROHIBITED:
- DO NOT cite explorers or tools you cannot access
- DO NOT present estimates as verified facts
- DO NOT fabricate transaction hashes, batch IDs, or URLs
- DO NOT fill gaps with plausible-sounding specifics

OUTPUT FORMAT:
- Always include "Data Source" and "Last Updated" sections
- Clearly separate verified facts from estimates
- Provide confidence levels for numerical data
```

**Source:** [Prevent ChatGPT Hallucinations with Custom Instructions - Flux+Form](https://flux-form.com/marketing-ai-training/prevent-chatgpt-hallucinations/)

### 4.4 Retrieval-Augmented Generation (RAG) Best Practices

For GPTs connected to external knowledge bases:

**Knowledge Base Quality:**
- Curate and regularly update the knowledge base
- Remove outdated or conflicting information
- Version control documentation

**Query Design:**
- Use specific, scoped queries rather than broad searches
- Implement filters for data recency
- Return metadata with results (timestamp, source, confidence)

**Response Validation:**
- Implement server-side validation of GPT queries
- Log all API calls for audit trails
- Rate-limit to prevent runaway hallucination loops

**Limitation:** RAG does not guarantee factual accuracy, but usually reduces hallucinations when properly implemented.

**Sources:**
- [ChatGPT Hallucinations Expert Guide - Intellectual Lead](https://intellectualead.com/chatgpt-hallucinations-guide/)
- [AI Hallucination: Compare Popular LLMs - AIM](https://research.aimultiple.com/ai-hallucination/)

### 4.5 Model Performance Context (2025)

**Current State of Hallucinations:**
- GPT-5 responses are ~45% less likely to contain factual errors than GPT-4o
- With reasoning enabled, GPT-5 is ~80% less likely to hallucinate than o3
- However, hallucinations remain a fundamental challenge for ALL LLMs
- Non-zero hallucination risk exists on every model and release

**Expert Consensus:**
"Many experts have stated that hallucinations cannot be fixed or removed from LLMs. However, there are many strategies to mitigate hallucinations, including Prompt Engineering."

**Recommendation:** Assume non-zero hallucination risk. Use mitigation strategies to reduce edit time, not to skip editorial review.

**Source:** [Why Language Models Hallucinate - OpenAI](https://openai.com/index/why-language-models-hallucinate/)

---

## 5. Architecture: Connecting GPTs to MCP Servers via API Proxy

### 5.1 The GPT-to-MCP Architecture

Since GPTs can only communicate via HTTP REST APIs (not native MCP protocol), connecting a GPT to an MCP server requires an intermediary API layer:

```
┌─────────────────────────────────────────────┐
│  ChatGPT Custom GPT                         │
│  - Receives user query in natural language │
│  - Converts to API call via OpenAPI schema │
└──────────────────┬──────────────────────────┘
                   │ HTTP POST
                   │ (REST API with JSON payload)
                   ▼
┌─────────────────────────────────────────────┐
│  API Proxy / Wrapper Layer                  │
│  - Translates REST requests to MCP format  │
│  - Converts MCP responses to REST JSON     │
│  - Handles authentication                  │
└──────────────────┬──────────────────────────┘
                   │ JSON-RPC over HTTP/SSE
                   │ (or stdio for local)
                   ▼
┌─────────────────────────────────────────────┐
│  MCP Server                                 │
│  - Executes tools (query_code_graph, etc.) │
│  - Accesses resources (files, databases)   │
│  - Manages state and context               │
└──────────────────┬──────────────────────────┘
                   │ Backend connections
                   ▼
┌─────────────────────────────────────────────┐
│  Data Sources                               │
│  - PostgreSQL + Apache AGE (graph)         │
│  - Vector databases (embeddings)           │
│  - Blockchain RPC (Regen Ledger)           │
│  - File systems, APIs, etc.                │
└─────────────────────────────────────────────┘
```

### 5.2 The API Proxy Layer

**Required Components:**

1. **OpenAPI Specification** - Defines REST endpoints the GPT can call
2. **HTTP Server** - Receives GPT requests (typically Express.js, FastAPI, etc.)
3. **Request Translator** - Converts REST JSON to MCP JSON-RPC format
4. **MCP Client** - Communicates with MCP server via native protocol
5. **Response Translator** - Converts MCP responses back to REST JSON

**Example: Regen KOI API Proxy**

The Regen KOI system exposes HTTP endpoints that wrap MCP functionality:

```
POST https://regen.gaiaai.xyz/api/koi/query
→ Wraps MCP tool: search_koi
→ Returns: JSON response

POST https://regen.gaiaai.xyz/api/koi/graph
→ Wraps MCP tool: query_code_graph
→ Returns: JSON response
```

Each endpoint translates the HTTP request into an MCP JSON-RPC call and returns formatted results.

### 5.3 Why REST API Wrapping is Suboptimal

The consensus in 2025 is that simply wrapping REST APIs with MCP (or vice versa) is architecturally problematic:

**Design Philosophy Mismatch:**
- REST APIs are designed for manipulating data states (CRUD operations)
- MCP/AI agents are designed to execute actions and achieve goals
- REST focuses on resource-centric nouns (GET /users)
- MCP focuses on action-oriented verbs (run_analysis)

**Limitations of REST Wrappers:**
- Forces agents to think in terms of HTTP verbs instead of capabilities
- Doesn't provide true "tools" - just different ways to perform CRUD
- Limits what agents can reliably and effectively accomplish
- Adds unnecessary translation overhead

**Quote from Industry Analysis:**
"Many common implementations simply create an MCP wrapper over existing API services. This is a suboptimal design choice. Forcing MCP to simply be a passthrough or a light translation layer for REST APIs means you are not providing the agent with true 'tools' in the sense of capabilities, but rather with a slightly different way to perform CRUD operations."

**Sources:**
- [MCP is not REST API](https://leehanchung.github.io/blogs/2025/05/17/mcp-is-not-rest-api/)
- [MCP vs API: Understanding Their Relationship](https://www.merge.dev/blog/api-vs-mcp)

### 5.4 When REST Wrappers Are Acceptable

Despite the architectural concerns, REST API wrappers for MCP can be pragmatic:

**Acceptable Use Cases:**
- Rapid prototyping and proof-of-concept
- Legacy integration where rebuilding native MCP is costly
- Public-facing APIs where HTTP/REST is a requirement
- Simple query/response patterns without complex state

**Best Practices When Using Wrappers:**
- Map GET requests to MCP resources (data retrieval)
- Map POST/PUT/DELETE to MCP tools (actions)
- Design based on operation purpose, not just HTTP method
- Include proper error handling and timeout management
- Document the wrapper's limitations clearly

**Quote:**
"Many AI integrations today do just use regular REST APIs, and that works fine! The reason to be interested in MCP is to make integration easier and more standardized as AI capabilities grow. It's about reducing friction."

**Source:** [What is MCP and AI Agents?](https://tallyfy.com/mcp-agents-rest-apis/)

---

## 6. Direct MCP Access: The Claude Code Approach

### 6.1 Native MCP Protocol Architecture

Claude Code connects directly to MCP servers using the native protocol, without HTTP intermediaries:

```
┌─────────────────────────────────────────────┐
│  Claude Code (MCP Client)                   │
│  - Desktop application                      │
│  - Native MCP protocol support              │
└──────────────────┬──────────────────────────┘
                   │ JSON-RPC 2.0
                   │ Transport: stdio OR HTTP/SSE
                   ▼
┌─────────────────────────────────────────────┐
│  MCP Server(s)                              │
│  - Multiple servers can be configured       │
│  - Direct tool/resource exposure            │
│  - Stateful sessions with capabilities      │
└──────────────────┬──────────────────────────┘
                   │ Direct backend access
                   ▼
┌─────────────────────────────────────────────┐
│  Data Sources (Direct Access)               │
│  - File systems (stdio transport)           │
│  - Databases (local or networked)           │
│  - APIs (with authentication)               │
└─────────────────────────────────────────────┘
```

### 6.2 Transport Methods

MCP supports multiple transport mechanisms, chosen based on deployment:

**1. stdio (Standard Input/Output)**
- **Use Case:** Local processes on the same machine
- **Advantages:**
  - Direct system access
  - No network overhead
  - Ideal for filesystem operations, local scripts
- **How It Works:** MCP server runs as subprocess, communicates via stdin/stdout
- **Example:** Claude Code → local filesystem MCP server

**2. HTTP with Server-Sent Events (SSE)**
- **Use Case:** Remote/cloud-based MCP servers
- **Advantages:**
  - Works across networks
  - Supports streaming responses
  - Most widely supported for cloud services
- **How It Works:** HTTP for requests, SSE for server-to-client streaming
- **Example:** Claude Code → hosted Regen KOI MCP server

**3. WebSocket (Less Common)**
- **Use Case:** Bidirectional real-time communication
- **Advantages:** Full duplex communication
- **Disadvantages:** Less standardized in MCP ecosystem

**Sources:**
- [Connect Claude Code to Tools via MCP](https://code.claude.com/docs/en/mcp)
- [MCP Specification](https://modelcontextprotocol.io/specification/2025-06-18)

### 6.3 Protocol Communication

MCP uses JSON-RPC 2.0 for all communication:

**Client-Server Handshake:**
1. Client initiates connection
2. Server and client exchange capabilities
3. Agreement on protocol version, supported features
4. Session established with shared context

**Message Types:**
- **Requests:** Client asks server to execute action (tools) or retrieve data (resources)
- **Responses:** Server returns results or errors
- **Notifications:** One-way messages (progress updates, logging)

**Example Tool Call:**
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "query_code_graph",
    "arguments": {
      "query_type": "list_repos"
    }
  }
}
```

**Response:**
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "content": [
      {
        "type": "text",
        "text": "{\"repositories\": [\"regen-ledger\", \"regen-web\"]}"
      }
    ]
  }
}
```

**Source:** [MCP fundamentals - Medium](https://medium.com/@kednaik/mcp-fundamentals-using-claude-client-and-mcp-to-generate-code-file-f9522acbe585)

### 6.4 Capability Negotiation

MCP's handshake includes capability negotiation:

**Server Capabilities:**
- Tools available (with schemas)
- Resources accessible (file paths, database connections)
- Prompts supported (pre-defined query templates)
- Experimental features enabled

**Client Capabilities:**
- Sampling (can request LLM completions via server)
- Roots (file system roots accessible to server)

This negotiation ensures both sides know what operations are supported, preventing errors from incompatible features.

**Source:** [Claude MCP Integration Deep Dive](https://claudecode.io/guides/mcp-integration)

### 6.5 Dynamic Tool Discovery

When Claude Code connects to an MCP server:

1. **Automatic Discovery:** Claude automatically learns available tools and resources
2. **Schema Understanding:** Each tool includes JSON schema defining parameters
3. **Intelligent Selection:** Claude determines when to use each tool based on user query
4. **No Hard-Coding:** Tools can be added/modified without Claude updates

**Example from Regen KOI MCP:**
- `search_koi` - Vector + hybrid search across knowledge base
- `query_code_graph` - Graph queries over 26,768 code entities
- `query_ledger` - Direct Regen blockchain state queries
- `semantic_scholar_search` - Academic paper search

Claude Code automatically knows about all these tools and their parameters through the MCP protocol.

**Source:** [Claude Code MCP Integration Architecture](https://www.walturn.com/insights/claude-mcp-a-new-standard-for-ai-integration)

### 6.6 State Management

MCP supports stateful sessions:

**Session State:**
- Maintained across multiple interactions
- Context persists (conversation history, loaded resources)
- Server can track progress on long-running operations

**Comparison to REST:**
- REST is stateless - each request is independent
- MCP can maintain conversation context
- Reduces payload size (no need to resend full history)
- Server can optimize based on session state

**Example:** A chatbot using MCP retains conversation history across API calls. With REST, history must be embedded in every request.

**Source:** [MCP vs Traditional APIs](https://treblle.com/blog/mcp-vs-traditional-apis-differences)

---

## 7. Performance Comparison: API Proxy vs Native MCP

### 7.1 JSON-RPC Performance Advantages

**Single Endpoint Design:**
- JSON-RPC uses one endpoint (e.g., `/rpc`) for all methods
- REST requires multiple endpoints (`/users`, `/posts`, `/comments`)
- Simpler routing, reduced HTTP overhead

**Native Batching:**
- JSON-RPC supports batch requests (multiple operations in one HTTP call)
- REST requires separate requests for each operation
- Reduces network round-trips significantly

**Action-Oriented Design:**
- JSON-RPC: Named methods like `run_analysis()`
- REST: Navigate to resource URLs like `GET /analysis/results`
- JSON-RPC mirrors how AI agents think (actions, not data nouns)

**Quote:**
"MCP chose JSON-RPC because its lightweight, single-endpoint design ensures fast and efficient communication for real-time AI tasks. It supports batch requests, allowing multiple operations in one call."

**Source:** [Why MCP Uses JSON-RPC Instead of REST or gRPC](https://glama.ai/blog/2025-08-13-why-mcp-uses-json-rpc-instead-of-rest-or-g-rpc)

### 7.2 stdio vs HTTP Performance

**stdio Transport (Local):**
- Zero network latency
- Direct process-to-process communication via pipes
- Ideal for file operations, local databases, system tools
- Used when MCP server runs on same machine as client

**HTTP/SSE Transport (Remote):**
- Network latency added
- Requires HTTP request/response cycle
- Additional overhead: TLS, headers, connection management
- Necessary for cloud-hosted services

**Performance Impact:**
- stdio can be 10-100x faster for local operations
- HTTP adds ~10-100ms baseline latency per request
- For high-frequency operations (code analysis, file searching), stdio is vastly superior

**Source:** [JSON-RPC vs REST for distributed platform APIs](https://dev.to/radixdlt/json-rpc-vs-rest-for-distributed-platform-apis-3n0m)

### 7.3 Real-World Performance: gRPC Comparison

While MCP uses JSON-RPC (not gRPC), gRPC performance data provides context:

**gRPC Benchmarks (2025):**
- Can outperform REST by up to 7x in microservice architectures
- Messages 60-80% smaller than JSON
- Microsoft: "gRPC can be up to 8x faster than JSON serialization"

**JSON-RPC Position:**
- Not as fast as gRPC (binary Protocol Buffers)
- Faster than traditional REST due to batching, single endpoint
- More readable/debuggable than binary protocols
- Better platform compatibility than gRPC

**Quote:**
"JSON-RPC strikes the right balance: it's structured without being overly complex, readable without sacrificing flexibility, and versatile across platforms."

**Source:** [gRPC vs REST: Key Similarities and Differences](https://blog.dreamfactory.com/grpc-vs-rest-how-does-grpc-compare-with-traditional-rest-apis)

### 7.4 The API Proxy Overhead

When using an API proxy to connect GPT to MCP:

**Added Latency Layers:**
1. GPT function calling decision (100-500ms)
2. GPT → Proxy HTTP request (10-50ms network)
3. Proxy translation REST→JSON-RPC (1-10ms)
4. Proxy → MCP HTTP/stdio request (10-100ms)
5. MCP tool execution (variable: 10ms-10s+)
6. MCP → Proxy response (10-100ms)
7. Proxy translation JSON-RPC→REST (1-10ms)
8. Proxy → GPT HTTP response (10-50ms)
9. GPT response generation (500ms-5s)

**Total Overhead:** ~650ms-6+ seconds (excluding tool execution time)

**Claude Code Native MCP:**
1. Claude tool selection (100-500ms)
2. Claude → MCP JSON-RPC via stdio (1-10ms local) or HTTP (10-100ms remote)
3. MCP tool execution (variable)
4. MCP → Claude response (1-100ms)
5. Claude response generation (500ms-5s)

**Total Overhead:** ~600ms-5.6s (excluding tool execution)

**Difference:** API proxy adds ~50ms-400ms per request, plus translation complexity and potential bugs.

### 7.5 Data Freshness Issues

**GPT with API Proxy:**
- Queries cached/indexed data in KOI
- KOI index updated monthly or quarterly
- No direct blockchain access
- Data can be 1-3 months stale

**Claude Code with Native MCP:**
- Can query live blockchain RPC endpoints
- Real-time data from databases
- Direct file system access
- Data freshness limited only by source update frequency

**Example from Regen KOI Testing:**
- GPT (May 2025): Reported 5 carbon credit classes
- Actual (August 2025): 13 credit classes on-chain
- 3-month data lag caused hallucinations

---

## 8. Limitations of GPT Compared to Claude Code for MCP Usage

### 8.1 Protocol Constraints

| Feature | ChatGPT Custom GPT | Claude Code |
|---------|-------------------|-------------|
| **MCP Protocol** | No native support | Native JSON-RPC 2.0 |
| **Transport** | HTTP REST only | stdio, HTTP/SSE, WebSocket |
| **Tool Discovery** | Manual OpenAPI schema | Automatic via MCP handshake |
| **State Management** | Stateless (or manual) | Stateful sessions |
| **Batching** | Not supported | Native batch requests |
| **Real-time Streaming** | Limited | SSE streaming support |

### 8.2 Integration Complexity

**ChatGPT Custom GPT:**
- Requires OpenAPI schema (100-1000+ lines of YAML/JSON)
- Manual schema updates when API changes
- Each function = separate schema definition
- Authentication configuration per-GPT
- No built-in library of integrations

**Claude Code:**
- Connects to pre-built MCP servers (community ecosystem)
- Automatic tool discovery via protocol
- Authentication handled at MCP server level
- Thousands of community MCP servers available
- One MCP server = potentially dozens of tools

**Quote from Industry Analysis:**
"Custom GPT Actions have no native support for tools like Slack or Salesforce—everything has to be wired manually. Need to connect to a tool like Slack? You have to build a custom Action for every single function you need."

**Source:** [Custom GPT Actions in 2025](https://www.lindy.ai/blog/custom-gpt-actions)

### 8.3 Reliability and Context Management

**GPT Limitations:**
- 8,000 character instruction limit
- Context window shared with conversation
- Can forget earlier instructions in long conversations
- No persistent memory across sessions (unless manually implemented)
- Prone to hallucination when data is ambiguous

**Claude Code Advantages:**
- System prompts don't count against context
- MCP server maintains state across interactions
- Tools can access persistent storage
- Explicit "I don't know" behavior when uncertain
- Better at multi-step reasoning tasks

**Quote:**
"During a long conversation or a complex task, GPTs can forget earlier instructions or lose important context. This lack of reliability is a deal-breaker for any process that has to run the same way every single time."

**Source:** [The Potential and Limitations of OpenAI's Custom GPTs](https://www.leojkwan.com/openai-and-custom-chat-gpts/)

### 8.4 Workflow Capabilities

**GPT Workflow Limitations:**
- Cannot combine multiple GPTs in one conversation
- Limited step-chaining for complex tasks
- No native task orchestration
- Cannot trigger workflows based on conditions

**Claude Code with MCP:**
- Can use multiple MCP servers simultaneously
- Tools can call other tools (with user approval)
- Supports complex multi-step workflows
- Conditional logic via tool execution

**Example Scenario:**
**Task:** "Analyze Regen Ledger data, create a report, and post to Slack"

**GPT Approach:**
1. Call Regen API → get data
2. User copies data manually
3. User asks GPT to format report
4. User manually posts to Slack (or uses separate Slack GPT)

**Claude Code Approach:**
1. Query Regen MCP server → get data
2. Use filesystem MCP → write report
3. Use Slack MCP → post automatically
4. All in one conversation flow

### 8.5 Security and Access Control

**GPT Considerations:**
- All custom instructions visible to users
- API keys stored by OpenAI
- OAuth tokens managed by OpenAI
- Limited control over token scopes
- No support for client credentials flow

**Claude Code with MCP:**
- MCP servers run locally or on private infrastructure
- Credentials never sent to Anthropic
- Full control over authentication mechanisms
- Support for all OAuth flows
- Can use mTLS, service accounts, etc.

**Security Trade-off:**
- GPT: Simpler setup, but less control
- Claude Code: More configuration, but full security control

**Source:** [OpenAI Authentication in 2025](https://www.datastudios.org/post/openai-authentication-in-2025-api-keys-service-accounts-and-secure-token-flows-for-developers-and)

### 8.6 Cost and Scalability

**GPT Usage:**
- Requires ChatGPT Plus subscription ($20/month per user)
- API calls from GPT to external services count against rate limits
- No control over GPT infrastructure scaling

**Claude Code with MCP:**
- Can run entirely locally (zero runtime cost)
- Self-hosted MCP servers scale independently
- Pay only for Claude API usage (if using cloud)
- Full control over infrastructure costs

**Enterprise Consideration:**
For organizations, self-hosted MCP infrastructure with Claude Code provides better cost predictability and data sovereignty.

### 8.7 Developer Experience

**GPT Custom Actions:**
- Web-based configuration (no code required for basic setup)
- OpenAPI schema can be complex to write/maintain
- Limited debugging tools
- No local testing without deploying

**Claude Code with MCP:**
- Code-based configuration (TypeScript, Python, etc.)
- Rich debugging via stdio logs
- Local testing before deployment
- Strong community ecosystem and examples

**Developer Preference (2025):**
Developers building complex integrations prefer MCP's code-first approach. Non-technical users prefer GPT's web interface.

---

## 9. Summary and Recommendations

### 9.1 Key Findings

**Architecture Differences:**
1. **GPTs require HTTP REST API proxy** to access MCP functionality - cannot use native protocol
2. **Claude Code uses native MCP protocol** (JSON-RPC via stdio or HTTP/SSE) - direct, low-latency access
3. **API proxy adds complexity:** translation layers, latency, debugging challenges
4. **REST wrappers are suboptimal** but pragmatic for legacy integration

**Hallucination Mitigation:**
1. **Explicit uncertainty instructions** reduce confident fabrication
2. **Source citation requirements** improve accountability
3. **Custom instructions framework** establishes persistent guidelines
4. **RAG with quality curation** reduces but doesn't eliminate hallucinations
5. **Non-zero hallucination risk** exists on all LLMs - editorial review mandatory

**Performance Impact:**
1. **JSON-RPC is faster than REST** for AI agent interactions (batching, single endpoint)
2. **stdio transport is vastly faster** than HTTP for local operations
3. **API proxy overhead:** ~50-400ms per request
4. **Data freshness:** Direct MCP access provides real-time data vs. cached/indexed

**Practical Limitations:**
1. **GPT technical constraints:** 8K instruction limit, no image passing, limited batching
2. **GPT workflow limits:** No multi-GPT composition, poor step-chaining
3. **GPT integration complexity:** Manual schema creation, no auto-discovery
4. **Claude Code advantages:** Native protocol, better context, multiple MCP servers

### 9.2 Use Case Recommendations

**Use ChatGPT Custom GPT When:**
- Simple query/response patterns (no complex workflows)
- Public-facing chatbot on website
- Non-technical users need web interface setup
- Integration with existing REST APIs already deployed
- Low-frequency usage (cost not a concern)
- Security requirements met by OpenAI's infrastructure

**Use Claude Code with Native MCP When:**
- Complex multi-step workflows required
- High performance / low latency critical
- Local filesystem or database access needed
- Multiple data sources must be orchestrated
- Data sovereignty / on-premise deployment required
- Developer team available for MCP server development
- High-frequency usage makes cost optimization important

### 9.3 Best Practices for GPT-MCP Integration

If you must use GPT with MCP via API proxy:

**1. API Proxy Design:**
- Implement rate limiting to prevent runaway costs
- Log all requests/responses for debugging
- Add request validation before forwarding to MCP
- Include timeout handling for long-running operations
- Return structured errors with clear messages

**2. OpenAPI Schema:**
- Keep descriptions concise but specific
- Include examples for complex parameters
- Use enums to constrain inputs where possible
- Version your API and document breaking changes

**3. System Instructions:**
- Force source citation on every response
- Require confidence qualifiers ("estimated", "verified", "unknown")
- Prohibit fabrication of specific identifiers (URLs, IDs, hashes)
- Instruct to say "I don't know" when uncertain
- Include data freshness warnings

**4. Error Handling:**
- Return clear error messages (not generic 500s)
- Distinguish between proxy errors vs. MCP errors vs. data errors
- Provide user-friendly suggestions for resolution

**5. Monitoring:**
- Track hallucination incidents and patterns
- Monitor API proxy latency separately from MCP latency
- Alert on unusual error rates or timeout patterns
- Regularly audit GPT responses against source data

### 9.4 The Regen KOI GPT Lessons

**What Went Wrong:**
- GPT presented cached data as "live on-chain verified" without caveats
- Fabricated explorer URLs and transaction hashes when uncertain
- Did not indicate data staleness (3-month lag)
- Mixed Registry (off-chain) with Ledger (on-chain) namespaces

**What Could Improve It:**
- System instructions requiring explicit data source + timestamp
- Prohibition on citing tools the GPT cannot access
- Automatic freshness warnings on cached data
- Clearer distinction between "KOI reports" vs. "blockchain state"
- Fallback to "cannot verify - requires direct chain query" when appropriate

**Broader Lesson:**
GPTs work well for broad knowledge questions but struggle with precision data queries requiring verification. For financial/blockchain data, native MCP access (Claude Code) is more reliable.

### 9.5 Future Outlook

**Industry Trends (2025):**
- MCP adoption accelerating (OpenAI, Google DeepMind, Microsoft all adopting)
- Growing MCP server ecosystem (thousands of community servers)
- Movement toward native protocol support in more AI tools
- Security standards maturing (OAuth 2.1, proper token validation)

**GPT Evolution:**
- OpenAI Apps SDK may eventually support MCP natively
- GPT-5 / GPT-6 hallucination rates improving but never zero
- Possible convergence: OpenAI adopting MCP as official integration standard

**Recommendation:**
Organizations building AI integrations should:
1. Design for MCP-native architecture
2. Use REST wrappers only as temporary/legacy bridge
3. Invest in MCP server development skills
4. Plan for eventual native MCP support across all platforms

---

## 10. Sources

### ChatGPT Custom GPTs and External APIs
- [How To Build Custom GPTs - CometAPI](https://www.cometapi.com/how-to-build-custom-gpts/)
- [Custom GPT Actions in 2025 - Lindy](https://www.lindy.ai/blog/custom-gpt-actions)
- [GPT Actions - OpenAI API](https://platform.openai.com/docs/actions/introduction)
- [OpenAI Apps SDK: How Developers Bring Services Into ChatGPT](https://skywork.ai/blog/openai-apps-sdk-chatgpt-integration/)
- [How to Connect OpenAI GPTs to APIs - Superface](https://superface.ai/blog/how-to-connect-openai-gpts-to-apis)
- [Apps in ChatGPT vs Custom GPTs 2025](https://skywork.ai/blog/apps-in-chatgpt-vs-custom-gpts-gpt-apps-2025-comparison/)

### GPT Builder Custom Actions and OpenAPI
- [Creating OpenAPI Schemas for Custom GPTs - BYU](https://genai.byu.edu/creating-openapi-schemas-for-custom-gpts)
- [Mastering Custom GPT Actions Tutorial - Lilys.ai](https://lilys.ai/notes/en/custom-gpts-20251030/mastering-custom-gpt-actions-tutorial)
- [GPT Actions Library - OpenAI Cookbook](https://cookbook.openai.com/examples/chatgpt/gpt_actions_library/.gpt_action_getting_started)
- [Build Custom GPT using GPT Actions - Medium](https://medium.com/@ruchi.awasthi63/build-custom-gpt-using-gpt-actions-complete-guide-7436b402bba0)

### GPT System Instructions and Hallucination Prevention
- [How To Stop ChatGPT Hallucinations - God of Prompt](https://www.godofprompt.ai/blog/stop-chatgpt-hallucinations)
- [How to Reduce Hallucinations in ChatGPT - OpenAI Community](https://community.openai.com/t/how-to-reduce-hallucinations-in-chatgpt-responses-to-data-queries/900796)
- [ChatGPT Hallucinations Expert Guide - Intellectual Lead](https://intellectualead.com/chatgpt-hallucinations-guide/)
- [How to Stop ChatGPT from Hallucinating - Social Intents](https://help.socialintents.com/article/203-how-to-stop-chatgpt-from-hallucinating-and-making-things-up)
- [AI Hallucination: Compare Popular LLMs - AIM](https://research.aimultiple.com/ai-hallucination/)
- [Prevent ChatGPT Hallucinations with Custom Instructions - Flux+Form](https://flux-form.com/marketing-ai-training/prevent-chatgpt-hallucinations/)
- [Why Language Models Hallucinate - OpenAI](https://openai.com/index/why-language-models-hallucinate/)

### Model Context Protocol (MCP)
- [Model Context Protocol - Wikipedia](https://en.wikipedia.org/wiki/Model_Context_Protocol)
- [MCP Specification](https://modelcontextprotocol.io/specification/2025-06-18)
- [What Is the Model Context Protocol (MCP) - Descope](https://www.descope.com/learn/post/mcp)
- [Model Context Protocol (MCP): A Guide - DataCamp](https://www.datacamp.com/tutorial/mcp-model-context-protocol)
- [Introducing Model Context Protocol in Copilot Studio - Microsoft](https://www.microsoft.com/en-us/microsoft-copilot/blog/copilot-studio/introducing-model-context-protocol-mcp-in-copilot-studio-simplified-integration-with-ai-apps-and-agents/)

### MCP vs REST API Comparison
- [MCP is not REST API](https://leehanchung.github.io/blogs/2025/05/17/mcp-is-not-rest-api/)
- [MCP vs API: Understanding Their Relationship](https://www.merge.dev/blog/api-vs-mcp)
- [From REST API to MCP Server - Stainless](https://www.stainless.com/mcp/from-rest-api-to-mcp-server)
- [How does Model Context Protocol (MCP) differ from REST, GraphQL, or gRPC?](https://milvus.io/ai-quick-reference/how-does-model-context-protocol-mcp-differ-from-rest-graphql-or-grpc-apis)
- [What is MCP and AI agents?](https://tallyfy.com/mcp-agents-rest-apis/)
- [MCP vs. Traditional APIs - Treblle](https://treblle.com/blog/mcp-vs-traditional-apis-differences)
- [MCP vs APIs: What's the Difference? - Apidog](https://apidog.com/blog/mcp-vs-api/)

### Claude Code MCP Integration
- [Connect Claude Code to Tools via MCP](https://code.claude.com/docs/en/mcp)
- [Claude MCP: A New Standard for AI Integration - Walturn](https://www.walturn.com/insights/claude-mcp-a-new-standard-for-ai-integration)
- [Code Execution with MCP - Anthropic Engineering](https://www.anthropic.com/engineering/code-execution-with-mcp)
- [Claude Code MCP Integration Deep Dive](https://claudecode.io/guides/mcp-integration)
- [Claude MCP: The Complete Guide for Enterprises](https://www.unleash.so/post/claude-mcp-the-complete-guide-to-model-context-protocol-integration-and-enterprise-security)
- [MCP Fundamentals - Medium](https://medium.com/@kednaik/mcp-fundamentals-using-claude-client-and-mcp-to-generate-code-file-f9522acbe585)

### GPT Custom Actions Limitations
- [Custom GPT Actions in 2025 - Lindy](https://www.lindy.ai/blog/custom-gpt-actions)
- [GPTs vs Actions vs Plugins - eesel AI](https://www.eesel.ai/blog/gpts-vs-actions-vs-plugins)
- [Why You Should Not Build Custom GPT with Actions](https://sivi.ai/blog/why-you-should-not-build-custom-gpt-with-actions-chatgpt-plugin)
- [Custom GPT Actions Limits - OpenAI Community](https://community.openai.com/t/custom-gpt-actions-limits/493329)
- [The Potential and Limitations of OpenAI's Custom GPTs](https://www.leojkwan.com/openai-and-custom-chat-gpts/)

### Authentication and Security
- [GPT Action Authentication - OpenAI](https://platform.openai.com/docs/actions/authentication)
- [How to Add Authentication to MCP-Powered ChatGPT App - Stytch](https://stytch.com/blog/guide-to-authentication-for-the-openai-apps-sdk/)
- [OpenAI Authentication in 2025](https://www.datastudios.org/post/openai-authentication-in-2025-api-keys-service-accounts-and-secure-token-flows-for-developers-and)

### JSON-RPC vs REST Performance
- [Why MCP Uses JSON-RPC Instead of REST or gRPC - Glama](https://glama.ai/blog/2025-08-13-why-mcp-uses-json-rpc-instead-of-rest-or-g-rpc)
- [Pros and Cons of JSON-RPC and REST APIs - Crypto APIs](https://cryptoapis.io/blog/151-pros-and-cons-of-json-rpc-and-rest-apis-protocols)
- [gRPC vs. REST - DreamFactory](https://blog.dreamfactory.com/grpc-vs-rest-how-does-grpc-compare-with-traditional-rest-apis)
- [JSON-RPC vs REST for distributed platform APIs - DEV](https://dev.to/radixdlt/json-rpc-vs-rest-for-distributed-platform-apis-3n0m)
- [RPC vs REST: A Comprehensive Comparison - Medium](https://medium.com/@utkarshshukla.author/rpc-vs-rest-a-comprehensive-comparison-88d0c7e13687)

---

**Report End**

*This research was conducted to support blog post development on GPT-MCP integration patterns and best practices for the Regen AI community.*
