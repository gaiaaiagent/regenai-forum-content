# Eliza AI Agents: Architecture, Integration, and Regen Network Possibilities

**Research Report**
Date: December 9, 2025
Focus: ElizaOS Framework and Regen AI Integration

---

## Executive Summary

ElizaOS is an open-source TypeScript framework developed by ai16z for building autonomous AI agents with persistent personalities and modular capabilities. The framework has emerged as a leading platform for creating Web3-native AI agents, with growing adoption across blockchain ecosystems. This report examines ElizaOS architecture, its integration capabilities with external data sources through the Model Context Protocol (MCP), and the current state and future possibilities of Regen Network's AI agent ecosystem.

Key findings:
- ElizaOS provides a comprehensive plugin architecture for extending agent capabilities
- The framework supports MCP integration, enabling standardized access to external data sources
- Regen Network has partnered with Gaia AI to launch Regen AI, a full-stack ecosystem of intelligent agents
- Regen Network is developing MCP infrastructure for planetary intelligence
- Integration opportunities exist for ElizaOS agents to access Regen's ecological data and registry systems

---

## 1. What is ElizaOS?

### 1.1 Overview

ElizaOS is a TypeScript framework for building AI agents that can think, learn, and act autonomously. It enables developers to create agents with unique, persistent personalities, equip them with plugins to interact with the world, and allow them to work toward their goals independently.

Launched in 2024 by ai16z (a leading venture capital firm), ElizaOS is described as "a scalable, modular, and open-source AI agent framework designed to thrive in both Web2 and Web3 ecosystems." The framework is truly open source - every line of code is open source, and users can extend it through plugins, contribute to the core, and share with the community.

### 1.2 Key Features

**Multi-Agent Architecture**: Designed from the ground up for creating and orchestrating groups of specialized agents. ElizaOS leverages Worlds (server/workspace) and Rooms (channel/DMs) so each agent keeps its own context yet can signal others, enabling delegation, consensus, and load-balancing out of the box.

**Model Agnostic**: Supports all major AI models, including:
- OpenAI
- Anthropic (Claude)
- Google Gemini
- Meta Llama
- Grok
- Local models via Ollama

**Rich Connectivity**: Out-of-the-box connectors for popular platforms:
- Discord
- Telegram
- Twitter/X
- Farcaster
- Other social media and communication platforms

**Scalable Knowledge**: Supports both RAG-based and direct knowledge processing. Maintains stateful interactions and context across conversations.

**Plugin Architecture**: Every capability—model provider, vector store, social network, custom action—arrives as an npm plugin. You can hot-swap at runtime, stay clear of vendor lock-in, and keep the core lightweight.

### 1.3 Capabilities

Agents built with ElizaOS can:
- Trade on-chain and interact with smart contracts
- Manage social media accounts
- Create and publish content
- Analyze data from various sources
- Interact with any API, blockchain, website, or repository
- Read and write blockchain data
- Make autonomous decisions toward their goals

### 1.4 Market Impact

As of December 2025, Web3 hosts approximately 10,000 AI agents, collectively earning millions of dollars each week from on-chain activities. VanEck expects upward of 1 million AI agents to populate blockchain networks by the end of 2025. The ELIZA framework powers AI16Z by creating and managing autonomous AI agents optimized for diverse markets.

### 1.5 Recent Developments

**ElizaOS v2**: The framework recently released version 2 with significant architectural improvements:
- Unified message bus and simplified client architecture
- Unified Agent wallet system
- Adoption of registry and override model for the model system
- Enhanced extensible and generic core framework
- Updated community plugins
- Achievement of 100% test coverage

The new architecture is more modular and unified, with clearer interactions between different components, providing a better foundation for future expansion.

**Stanford Partnership**: Eliza Labs has partnered with Stanford University's Future of Digital Currency Initiative to research how AI agents can improve Web3. Commencing in 2025, research priorities include:
- Developing new frameworks for how autonomous agents establish and verify trust within digital currency networks
- Investigating how agents interact and coordinate in economic contexts
- Tackling fundamental questions about how AI agents can establish trust, coordinate actions, and make decisions within decentralized financial systems

---

## 2. ElizaOS Architecture

### 2.1 Core Components

#### Runtime System
The Runtime (src/runtime.ts) acts as the control tower for AI agents, serving as the central coordination layer for:
- Message processing
- Memory management
- State composition
- Action execution
- Integration with AI models and external services

Like a conductor leading an orchestra, the Runtime ensures all parts work together harmoniously.

#### Message Flow
When someone interacts with an agent, the following process occurs:

1. **Client** receives the message and forwards it to the Runtime
2. **Runtime** processes it with the character file configuration
3. **Runtime** loads relevant memories and knowledge
4. **Runtime** uses actions and evaluators to determine how to respond
5. **Providers** supply additional context
6. **Runtime** generates a response using the AI model
7. **Runtime** stores new memories
8. **Client** sends the response back to the user

#### Memory System
The framework implements specialized memory systems:

- **Memory Manager** (src/memory.ts): Acts like a personal diary helping agents remember information across interactions
- **Cache System** (src/cache.ts): Creates shortcuts for frequently accessed information, making agents respond faster and more efficiently

### 2.2 Core Concepts

**Agents**: The autonomous entities that can think, learn, and act. Each agent has its own personality, goals, and capabilities.

**Character Files**: Configuration files that define an agent's personality, knowledge base, and behavioral patterns. These files allow for consistent, persistent agent personalities.

**Providers**: Modules that supply real-time information to agents by integrating external APIs, managing temporal awareness, and providing system status updates to help agents make better decisions.

**Actions**: Represent the core capabilities of an AI agent - the things it can actually do. An action is defined by:
- **Name**: The unique identifier used to reference the action
- **Description**: Used to inform the agent when this action should be invoked
- **Handler**: The code that actually executes the action logic
- **Validator**: Determines if the action is valid to be called given the current context

The handler receives the agent runtime, the triggering message, the current state, and a callback function to send messages back to the user.

**Evaluators**: Run after each agent action, allowing the agent to reflect on what happened and potentially trigger additional actions. They are a key component in creating agents that can learn and adapt. Evaluators work in close conjunction with providers - often an evaluator will extract some insight that a provider will then inject into future context.

### 2.3 Plugin Architecture

The Eliza framework implements a flexible plugin architecture that enables modular extension of AI agent capabilities while maintaining system stability and coherence. Everything in Eliza is a plugin - including services, adapters, actions, evaluators, and providers. This approach ensures consistent behavior and better extensibility.

#### Plugin Structure

A basic plugin includes:

```typescript
import { Plugin, Action, Evaluator, Provider } from "@elizaos/core";

const myCustomPlugin: Plugin = {
  name: "my-custom-plugin",
  description: "Adds custom functionality",
  actions: [ /* custom actions */ ],
  evaluators: [ /* custom evaluators */ ],
  providers: [ /* custom providers */ ],
  services: [ /* custom services */ ],
};
```

Plugins can define:
- **Actions**: Custom capabilities the agent can perform
- **Evaluators**: Logic for analyzing and learning from actions
- **Providers**: Sources of contextual information
- **Services**: Background processes and integrations

### 2.4 Multi-Agent Coordination

ElizaOS leverages Worlds (server/workspace) and Rooms (channel/DMs) architecture:
- Each agent maintains its own context
- Agents can signal and communicate with other agents
- Enables delegation, consensus, and load-balancing
- Supports collaborative problem-solving among specialized agents

---

## 3. Connecting ElizaOS to External Data Sources

### 3.1 Integration Methods

ElizaOS supports multiple approaches for connecting to external data sources and APIs:

#### 3.1.1 Providers
Providers supply real-time information to agents by integrating external APIs. They implement a `get()` method which accepts runtime configuration, message context, and current state. For example, an EVM wallet provider fetches wallet details like address, balance, and chain information to expose blockchain functionality to agents.

#### 3.1.2 Custom Actions
You can extend Eliza with custom actions that fetch real-time data. This pattern can be adapted for any external API—e-commerce product lookups, weather forecasts, or dynamic knowledge bases. The action's handler function can make API calls and process the results.

#### 3.1.3 External Systems Support
Eliza can utilize:
- API endpoints
- Event streams
- Webhooks
- Database connectors
- Service meshes

Development tools incorporate SDKs, plugin architectures, testing frameworks, debugging tools, and deployment pipelines.

#### 3.1.4 Blockchain and Web3 Integration
ElizaOS offers rich connectivity with blockchain networks:
- Built-in support for EVM-compatible chains
- Cosmos/IBC integration capabilities
- Solana and other L1 blockchain support
- With Chainlink's CCIP and oracle network, agents can connect to trusted, real-world data

### 3.2 Model Context Protocol (MCP) Integration

The Model Context Protocol (MCP) is an open protocol developed by Anthropic that enables seamless integration between LLM applications and external data sources and tools. It provides a standardized way to connect LLMs with the context they need.

#### 3.2.1 Why MCP Matters for ElizaOS

Developers creating agents with ElizaOS often face challenges integrating external data sources, especially:
- Dynamic crypto market data
- Social media insights
- Diverse API authentication and formatting
- Data availability issues

With MCP, Eliza agents can seamlessly access a rich agents-as-a-service ecosystem — from token analytics to web search, as simple as a few lines of code.

#### 3.2.2 MCP Integration Options

**Official ElizaOS MCP Plugin (by Fleek Platform)**

Available as `@fleek-platform/eliza-plugin-mcp`, this plugin integrates the Model Context Protocol with ElizaOS, allowing agents to:
- Connect to multiple MCP servers simultaneously
- Access different capabilities from each server
- Use resources (context and data for the agent to reference)
- Execute tools provided by MCP servers
- Leverage prompts for common operations

MCP supports two types of servers:
- **stdio**: Standard input/output based servers
- **sse**: Server-sent events based servers

**MCPAgentAI Integration**

MCPAgentAI offers seamless integration with ElizaOS through a Python SDK designed to simplify interactions with MCP servers. It provides:
- Easy-to-use interface for connecting to MCP servers
- Reading resources from MCP servers
- Calling tools via MCP
- Two integration approaches:
  1. Embedded Eliza functionality (without running the full Eliza Framework)
  2. Full ElizaOS integration with MCP capabilities

**Native MCP Support**

The ElizaOS community has been working on implementing native Model Context Protocol (MCP) support to enable:
- Standardized context state handling
- Efficient context updates
- Cross-model compatibility
- Consistent context management across different models and systems

#### 3.2.3 MCP Architecture

The MCP architecture is straightforward:
- **MCP Servers**: Expose data and capabilities through a standardized protocol
- **MCP Clients**: AI applications that connect to these servers
- **Standardized Communication**: Both sides follow the MCP specification for interoperability

Developers can either:
1. Build MCP servers to expose their data sources
2. Build MCP clients (like ElizaOS agents) to consume data from existing servers

---

## 4. Regen Network and AI Agents

### 4.1 Regen Network Overview

Regen Network is a blockchain-based platform for issuing, trading, and governing science-backed ecological credits to power regenerative economies and climate solutions. It empowers communities to coordinate, fund, and verify regenerative action at scale.

#### Core Technology

**Regen Ledger**: A blockchain application for ecological assets and data claims built on top of Cosmos SDK and Tendermint Core. The ledger provides infrastructure for:
- Proof-of-Stake blockchain network governed by a community dedicated to planetary regeneration
- Ecological assets and verification of claims
- Science-backed ecological credits

**Network Statistics** (as of 2025):
- 75 validators
- 20,000+ wallet holders
- 42 major projects building on Regen Ledger

#### Integration with Broader Ecosystem

Regen Network integrates into the cryptocurrency ecosystem through:

**IBC (Inter-Blockchain Communication)**: The Regen Ledger is built using the Cosmos SDK, the most popular proof-of-stake-based blockchain development framework globally. IBC transfers provided by the Cosmos Hub allow sovereign blockchains to transfer data and digital assets or tokens from one chain to another.

**Key Partners**: Regen Network is onboarding partners including:
- Moss.Earth
- Open Earth Foundation
- Earthbanc
- ERA Brazil
- Shamba Protocol
- Terra Genesis International

### 4.2 Regen AI: The Agent Ecosystem

#### Partnership with Gaia AI

Gaia AI and Regen Network have officially partnered to launch **Regen AI**, a joint initiative to catalyze the regenerative finance (ReFi) movement using advanced AI systems.

**Vision**: A full-stack ecosystem of intelligent agents serving the regenerative economy. The vision is to merge AI with the wisdom of ecological and human systems – creating a "legibility layer" for climate data, ecological credits, and on-the-ground narratives.

#### How Regen AI Works

Gaia AI is training agents on Regen Network's rich public dataset, including:
- On-chain registry data and methodologies
- Real-time credit supply and pricing
- Project metadata
- Ecological State Protocols (ESPs)
- Biodiversity, soil organic carbon, biomass, and other ecological data

These agents act as tireless assistants and storytellers, supporting:
- Ecological coordination
- Verification processes
- Knowledge-sharing in real time
- Community engagement and education

**Platform Deployment**: Regen AI agents are deployed across:
- X (Twitter)
- Telegram
- Discord
- Farcaster

The agents serve as friendly guides in the ReFi community – answering questions, spreading awareness, and connecting participants across the globe.

#### Agent Archetypes

Four key agent archetypes form the pillars of regenerative intelligence:

1. **Narrator**: Weaves compelling eco-stories from ecological data
2. **Advocate**: Champions projects and policies in the regenerative space
3. **Politician**: Assists with governance and decision-making
4. **Voice of Nature**: Channels data from the earth into proposals and insights

#### Development Timeline

**Phase 2** (November 2025 - January 2026):
- Weekly updates being shared with the community
- Core MCP infrastructure for planetary intelligence being developed
- Integration with Regen Network's data ecosystem

#### Ecosystem Alliance

This partnership represents more than a product integration – it's a deep, multi-faceted ecosystem alliance grounded in:
- Shared regenerative mission
- Token alignment between projects
- Applied intelligence for ecological outcomes
- Gaia AI's cutting-edge agentic AI technology and community infrastructure
- Regen's established ecosystem for high-integrity ecological credit origination

### 4.3 Regen Network's Data Infrastructure

#### Regen Data Standards

Regen Network is developing a set of open-source data standards and tools to enable the global community to:
- Collect ecological data
- Verify ecological claims
- Analyze environmental impact
- Create a new global ecological data commons

**Goal**: Enable the world to understand and regenerate the ecological systems that support life on Earth.

#### Regen Data Tools

**Regenscan**: An ecological data explorer for credits and claims registered on the Regen Network blockchain. It serves as a public interface for exploring:
- Ecological credits
- Project data
- Claim verification
- On-chain ecological state

**Regen Data Stream**: Represents a significant milestone in realizing Regen's vision of a collaborative, interoperable platform for environmental crediting. It provides:
- Flexible, transparent tool for real-time data management
- User-friendly interface for project tracking
- Revolutionizing environmental project tracking
- Seamless integration with the Regen Registry

**Ecological State Protocols (ESPs)**: Examples include:
- Biodiversity assessments
- Above Ground Biomass (AGB)
- Soil Organic Carbon (SOC)
- Net Primary Productivity (NPP)
- Water Quality metrics
- Pollinator Density
- Many more environmental indicators

#### MCP Server Development

Regen Network maintains an "mcp" repository on their GitHub organization (regen-network/mcp), indicating active development of MCP infrastructure. While specific implementation details are still emerging, this suggests Regen is building an MCP server to expose ecological data to AI systems.

This would enable AI tools (including ElizaOS agents) to access:
- Carbon credits data
- Biodiversity information
- Ecological state protocols
- Registry information
- Project metadata
- Real-time environmental data

---

## 5. How ElizaOS Agents Can Use Regen MCPs

### 5.1 Integration Architecture

An ElizaOS agent can integrate with Regen Network's MCP servers using the following architecture:

```
ElizaOS Agent
    ↓
ElizaOS MCP Plugin (@fleek-platform/eliza-plugin-mcp)
    ↓
MCP Client Connection
    ↓
Regen Network MCP Server
    ↓
Regen Ledger / Registry / Data APIs
```

### 5.2 Potential Use Cases

#### 5.2.1 Ecological Credit Analysis Agent

An ElizaOS agent could:
- Query available ecological credits from the Regen Registry
- Analyze credit pricing and supply trends
- Provide investment recommendations based on ecological impact
- Monitor specific project performance
- Alert users to new credit issuances

**Required MCP Resources**:
- Credit inventory data
- Pricing history
- Project metadata
- Methodology documentation

#### 5.2.2 Project Verification Agent

An agent specialized in verification could:
- Access Ecological State Protocol data
- Compare claimed impacts against verified measurements
- Identify discrepancies or concerns
- Generate verification reports
- Track verification status across multiple projects

**Required MCP Resources**:
- ESP measurement data
- Historical project claims
- Verification records
- Methodology requirements

#### 5.2.3 Community Education Agent

A conversational agent deployed on social media could:
- Answer questions about specific ecological credits
- Explain regenerative finance concepts
- Share stories about successful projects
- Connect users with relevant resources
- Promote awareness of ecological initiatives

**Required MCP Resources**:
- Project descriptions and narratives
- Credit methodology explanations
- Educational content library
- Community forum data

#### 5.2.4 Governance Agent

An agent supporting Regen Network governance could:
- Monitor governance proposals
- Analyze proposal impacts on ecological outcomes
- Summarize complex governance decisions
- Notify stakeholders of voting deadlines
- Provide voting recommendations based on regenerative principles

**Required MCP Resources**:
- Governance proposal data
- Voting records
- Stakeholder information
- Policy documentation

#### 5.2.5 Data Integration Agent

A technical agent could:
- Aggregate data from multiple Ecological State Protocols
- Normalize measurements across different methodologies
- Identify correlations between ecological indicators
- Generate synthetic insights from combined datasets
- Export data for external analysis

**Required MCP Resources**:
- All ESP data feeds
- Metadata and schemas
- Historical measurements
- Cross-protocol mappings

### 5.3 Implementation Approach

To build an ElizaOS agent that uses Regen MCPs:

#### Step 1: Install Dependencies
```bash
npm install @elizaos/core @fleek-platform/eliza-plugin-mcp
```

#### Step 2: Configure MCP Servers
Create a configuration file specifying the Regen MCP server(s):

```typescript
const mcpConfig = {
  servers: {
    "regen-registry": {
      type: "stdio", // or "sse" depending on implementation
      endpoint: "https://mcp.regen.network/registry",
      // Additional configuration
    },
    "regen-data": {
      type: "stdio",
      endpoint: "https://mcp.regen.network/data",
    }
  }
};
```

#### Step 3: Create Custom Actions

Develop ElizaOS actions that leverage MCP resources:

```typescript
const queryCreditsAction: Action = {
  name: "QUERY_ECOLOGICAL_CREDITS",
  description: "Query available ecological credits from Regen Registry",

  validate: async (runtime, message, state) => {
    // Validation logic
    return true;
  },

  handler: async (runtime, message, state, callback) => {
    // Use MCP plugin to access Regen data
    const mcpPlugin = runtime.getPlugin("mcp");
    const credits = await mcpPlugin.getResource("regen-registry", "credits");

    // Process and respond
    await callback({
      text: `Found ${credits.length} ecological credits...`,
      data: credits
    });
  }
};
```

#### Step 4: Create Providers

Develop providers that inject Regen data into agent context:

```typescript
const regenContextProvider: Provider = {
  name: "regen-context",

  get: async (runtime, message, state) => {
    const mcpPlugin = runtime.getPlugin("mcp");

    // Fetch relevant context
    const activeProjects = await mcpPlugin.getResource(
      "regen-registry",
      "active-projects"
    );

    return {
      activeProjectCount: activeProjects.length,
      recentProjects: activeProjects.slice(0, 5),
      // Additional context
    };
  }
};
```

#### Step 5: Configure Agent Character

Define the agent's personality and knowledge:

```typescript
const regenAgentCharacter = {
  name: "RegenAdvisor",
  description: "An AI agent specialized in ecological credits and regenerative finance",
  modelProvider: "anthropic",
  plugins: [
    "@elizaos/plugin-bootstrap",
    "@fleek-platform/eliza-plugin-mcp",
    "custom-regen-plugin"
  ],
  settings: {
    mcpServers: mcpConfig
  },
  bio: [
    "Expert in Regen Network ecological credits",
    "Knowledgeable about carbon markets and biodiversity",
    "Committed to planetary regeneration"
  ]
};
```

### 5.4 Advantages of MCP Integration

**Standardization**: MCP provides a consistent interface for accessing Regen data, regardless of underlying implementation changes.

**Separation of Concerns**: The agent logic remains separate from data access logic, improving maintainability.

**Multiple Data Sources**: A single agent can access multiple MCP servers (Registry, Data Stream, ESPs) simultaneously.

**Real-time Updates**: MCP servers can provide live data feeds, ensuring agents have current information.

**Scalability**: As Regen Network expands its data offerings, new MCP resources can be added without changing agent code.

### 5.5 Challenges and Considerations

**Data Complexity**: Ecological data can be complex and nuanced. Agents must be carefully designed to interpret this data correctly.

**Authentication**: Access to some Regen data may require authentication or permissions. MCP integration must handle this securely.

**Rate Limiting**: Public MCP servers may have rate limits. Agents should implement appropriate caching and throttling.

**Data Freshness**: Different types of ecological data update at different intervals. Agents should be aware of data currency.

**Interpretation**: Agents providing ecological insights must be trained to avoid misrepresenting scientific data or making unfounded claims.

---

## 6. Requirements for Running ElizaOS Locally

### 6.1 System Requirements

**Hardware**:
- Minimum 2GB RAM (4GB recommended)
- 20GB available storage
- Modern CPU (any recent processor sufficient)

**Operating System**:
- Ubuntu or Debian (recommended for production)
- macOS
- Windows with WSL 2 (required for Windows users)

**Software**:
- Node.js version 23+ (specifically 23.3.0 recommended)
- Package manager: npm, pnpm, or bun

### 6.2 Installation Process

#### Option 1: Using ElizaOS CLI (Recommended)

1. Install bun (if not already installed):
```bash
curl -fsSL https://bun.sh/install | bash
```

2. Install ElizaOS CLI globally:
```bash
bun install -g @elizaos/cli
```

3. Verify installation:
```bash
elizaos --version
```

4. Create a new project with interactive setup:
```bash
elizaos create my-first-agent
```

The CLI will guide you through selecting:
- Database type (pglite requires no setup)
- Model provider (OpenAI, Anthropic, etc.)
- Platform integrations (Discord, Telegram, etc.)

#### Option 2: Manual Installation

1. Clone the repository:
```bash
git clone https://github.com/elizaOS/eliza.git
cd eliza
```

2. Install dependencies:
```bash
pnpm install --no-frozen-lockfile
```

3. Build the project:
```bash
pnpm build
```

### 6.3 Required API Keys

The specific API keys needed depend on which features you plan to use:

#### Core AI Model Providers (Choose at least one):

**OpenAI**:
```
OPENAI_API_KEY=sk-your-key-here
```
Required for OpenAI GPT models (GPT-4, GPT-3.5, etc.)

**Anthropic**:
```
ANTHROPIC_API_KEY=your-key-here
```
Required for Claude models (Opus, Sonnet, Haiku)

**Google Gemini**:
```
GOOGLE_GENERATIVE_AI_API_KEY=your-key-here
```
Required for Gemini models

**Together.ai**:
```
TOGETHER_API_KEY=your-key-here
```
Required for Together.ai hosted models

**Alternative: No API Key Required**:
- **Gaianet**: A public node with several AI models that doesn't require any API key
- **Ollama**: For local models, install Ollama and run models locally without API keys

#### Platform Integrations (Optional):

**Discord Bot**:
```
DISCORD_APPLICATION_ID=your-app-id
DISCORD_API_TOKEN=your-bot-token
```

**Telegram Bot**:
```
TELEGRAM_BOT_TOKEN=your-bot-token
```

**Twitter/X**:
```
TWITTER_API_KEY=your-key
TWITTER_API_SECRET=your-secret
TWITTER_ACCESS_TOKEN=your-token
TWITTER_ACCESS_SECRET=your-secret
```

#### Blockchain Integrations (Optional):

**EVM Chains**:
```
EVM_PRIVATE_KEY=your-private-key
SEPOLIA_RPC_URL=https://sepolia.infura.io/v3/your-key
# Or other EVM RPC endpoints
```

**Cosmos/Regen Network**:
```
COSMOS_CHAIN_ID=regen-1
COSMOS_RPC_URL=https://rpc.regen.network
COSMOS_PRIVATE_KEY=your-private-key
```

### 6.4 Configuration

Create a `.env` file in your project root with the necessary keys:

```env
# AI Model Provider (choose one or more)
OPENAI_API_KEY=sk-your-key
ANTHROPIC_API_KEY=your-key

# Optional: Platform Integrations
DISCORD_APPLICATION_ID=your-id
DISCORD_API_TOKEN=your-token

# Optional: Blockchain
EVM_PRIVATE_KEY=your-key
SEPOLIA_RPC_URL=your-rpc-url

# Optional: Database
# (pglite requires no configuration)
```

### 6.5 Running the Agent

#### Development Mode:
```bash
elizaos dev
# or
pnpm dev
```

#### Production Mode:
```bash
elizaos start
# or
pnpm start
```

### 6.6 Core Packages

The ElizaOS ecosystem includes several key packages:

- **@elizaos/server**: The Express.js backend that runs your agents and exposes the API
- **@elizaos/client**: The React-based web UI for managing and interacting with your agents
- **@elizaos/cli**: The central tool for scaffolding, running, and managing your projects
- **@elizaos/plugin-bootstrap**: The mandatory core plugin that handles message processing and basic agent actions

### 6.7 Local Models Alternative

For users who want to avoid API costs or work offline:

1. Install Ollama:
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

2. Download a model:
```bash
ollama pull llama3.1
```

3. Configure your character file:
```json
{
  "modelProvider": "ollama",
  "settings": {
    "model": "llama3.1"
  }
}
```

4. Set environment variables:
```env
OLLAMA_HOST=http://localhost:11434
```

---

## 7. Future Possibilities: Eliza + Regen Integration

### 7.1 Near-Term Opportunities (2025-2026)

#### 7.1.1 Registry Explorer Agent

**Purpose**: Help users discover and understand ecological credits in the Regen Registry.

**Capabilities**:
- Natural language queries about specific credits
- Comparison of different credit types
- Explanation of methodologies in accessible language
- Price tracking and notifications
- Portfolio management for credit buyers

**Technical Approach**:
- ElizaOS agent with MCP integration to Regen Registry
- Custom actions for credit queries
- Providers for market data
- Deployed on Discord, Telegram, and web interface

#### 7.1.2 Ecological Data Analyst

**Purpose**: Make complex ecological data accessible and actionable.

**Capabilities**:
- Analyze trends across Ecological State Protocols
- Generate reports on project performance
- Identify correlations between different environmental indicators
- Visualize data through generated charts and summaries
- Alert users to significant changes

**Technical Approach**:
- Integration with multiple Regen Data MCP servers
- Custom evaluators for data analysis
- Chart generation actions
- Scheduled monitoring and reporting

#### 7.1.3 Project Storyteller

**Purpose**: Bring ecological projects to life through compelling narratives.

**Capabilities**:
- Generate project summaries from registry data
- Create social media content highlighting impact
- Translate scientific data into accessible stories
- Share before/after comparisons
- Celebrate project milestones

**Technical Approach**:
- Content generation using advanced language models
- Integration with Regen project metadata
- Multi-platform publishing (Twitter, Medium, etc.)
- Image generation for visual storytelling

#### 7.1.4 Community Governance Assistant

**Purpose**: Increase participation in Regen Network governance.

**Capabilities**:
- Summarize governance proposals in plain language
- Notify users of relevant proposals
- Explain voting options and implications
- Track governance outcomes
- Provide voting recommendations aligned with regenerative principles

**Technical Approach**:
- Integration with Regen Ledger governance module
- Natural language processing for proposal analysis
- Multi-channel notifications
- Voting delegation support

### 7.2 Medium-Term Innovations (2026-2027)

#### 7.2.1 Autonomous Credit Traders

**Purpose**: Automated trading of ecological credits based on impact goals.

**Capabilities**:
- Execute trades based on predefined strategies
- Optimize portfolios for impact and returns
- Implement dollar-cost averaging for credit acquisition
- Rebalance holdings based on market conditions
- Report on impact achieved through purchases

**Technical Approach**:
- Full blockchain integration with Regen Ledger
- Smart contract interactions for DEX trading
- Risk management evaluators
- Real-time market monitoring
- Secure wallet management

#### 7.2.2 Cross-Chain Regenerative Finance Hub

**Purpose**: Bridge Regen Network with other blockchain ecosystems.

**Capabilities**:
- Transfer credits across chains via IBC
- Provide liquidity on multiple DEXs
- Arbitrage opportunities for credit pricing
- Cross-chain governance participation
- Unified view of multi-chain holdings

**Technical Approach**:
- Cosmos IBC integration
- Multi-chain wallet support
- Cross-chain messaging protocols
- Integration with Cosmos Hub and other IBC chains
- Support for Ethereum bridges (IBC Eureka)

#### 7.2.3 Verification Oracle Agents

**Purpose**: Automate parts of the ecological verification process.

**Capabilities**:
- Monitor remote sensing data feeds
- Compare claimed outcomes against satellite imagery
- Flag discrepancies for human review
- Track verification milestones
- Generate preliminary verification reports

**Technical Approach**:
- Integration with Earth observation APIs
- Machine learning models for change detection
- Chainlink oracle integration for trusted data
- Multi-signature verification workflows
- Human-in-the-loop for final approval

#### 7.2.4 Regenerative Project Discovery Engine

**Purpose**: Match funders with high-impact ecological projects.

**Capabilities**:
- Analyze project proposals and methodologies
- Score projects based on impact potential
- Match projects with funder preferences
- Track historical project performance
- Recommend diversified project portfolios

**Technical Approach**:
- Natural language processing of project documents
- Machine learning for impact prediction
- Integration with Regen Registry and external databases
- Recommendation engine algorithms
- User preference learning

### 7.3 Long-Term Vision (2027+)

#### 7.3.1 Planetary Intelligence Network

**Purpose**: A distributed network of specialized agents working together for planetary regeneration.

**Components**:
- **Monitoring Agents**: Continuously track ecological indicators globally
- **Analysis Agents**: Process and interpret environmental data
- **Coordination Agents**: Facilitate collaboration between projects and stakeholders
- **Funding Agents**: Optimize capital allocation for maximum impact
- **Verification Agents**: Ensure integrity of ecological claims
- **Governance Agents**: Facilitate decentralized decision-making
- **Education Agents**: Spread knowledge and build capacity

**Architecture**:
- ElizaOS multi-agent coordination
- Shared knowledge base across agent network
- Specialized agents for different ecological domains
- Inter-agent communication protocols
- Collective intelligence emergence

#### 7.3.2 Autonomous Ecological Asset Management

**Purpose**: Fully automated management of ecological asset portfolios.

**Capabilities**:
- Dynamic portfolio rebalancing
- Automated staking and DeFi participation
- Tax-loss harvesting for carbon credits
- Yield optimization across ReFi protocols
- Automated reporting and compliance
- Multi-generational impact planning

**Technical Approach**:
- Advanced DeFi integrations
- Multi-chain asset management
- Sophisticated risk modeling
- AI-driven strategy optimization
- Regulatory compliance automation

#### 7.3.3 Bioregional Coordination DAOs

**Purpose**: AI agents as core infrastructure for bioregional governance.

**Capabilities**:
- Coordinate restoration efforts across watersheds
- Optimize resource allocation within bioregions
- Facilitate multi-stakeholder decision-making
- Track ecological health at bioregional scale
- Bridge local knowledge with global markets
- Enable nested governance structures

**Technical Approach**:
- Geographic information system integration
- Multi-level governance protocols
- Stakeholder representation mechanisms
- Ecological boundary modeling
- Cultural knowledge preservation

#### 7.3.4 Regenerative Economy Operating System

**Purpose**: ElizaOS agents as foundational infrastructure for the regenerative economy.

**Capabilities**:
- Automate routine transactions in regenerative markets
- Provide universal access to ecological information
- Enable micro-transactions for ecological services
- Coordinate global supply chains for regenerative products
- Track full lifecycle impacts of economic activities
- Facilitate emergence of new regenerative business models

**Technical Approach**:
- Integration with all major ReFi protocols
- Interoperability standards for regenerative data
- Micro-payment infrastructure
- Supply chain transparency protocols
- Impact accounting standards

### 7.4 Technical Enablers for Future Integration

#### 7.4.1 Enhanced MCP Capabilities

**Standardized Ecological Data Schemas**: Development of MCP resource schemas specifically for ecological data types (carbon, biodiversity, water, soil, etc.)

**Real-time Data Streams**: MCP servers providing live updates from IoT sensors, satellite feeds, and verification systems

**Federated MCP Networks**: Multiple organizations providing complementary MCP servers that agents can query collectively

**Semantic Interoperability**: Ontologies and knowledge graphs enabling agents to understand relationships between different ecological concepts

#### 7.4.2 Agent Specialization Framework

**Domain-Specific Training**: Fine-tuned models for ecological concepts, ReFi terminology, and regenerative principles

**Multi-Agent Protocols**: Standardized communication patterns for agents to collaborate on complex tasks

**Reputation Systems**: Track record of agent decisions and recommendations for trust building

**Capability Discovery**: Agents advertising their capabilities and discovering complementary agents

#### 7.4.3 Blockchain Infrastructure Improvements

**IBC Eureka Adoption**: Expanded connectivity between Cosmos chains and Ethereum for broader DeFi integration

**Layer 2 Scaling**: Reduced transaction costs for micro-transactions and frequent agent operations

**Privacy Preserving Computation**: Zero-knowledge proofs for sensitive ecological or business data

**Decentralized Storage**: IPFS/Arweave integration for storing agent knowledge and ecological datasets

#### 7.4.4 Verification and Trust Infrastructure

**Cryptographic Attestations**: Agents signing their outputs for auditability

**Multi-Signature Workflows**: Human oversight for high-stakes decisions

**Transparent Decision-Making**: Explainable AI for agent reasoning

**Dispute Resolution**: Mechanisms for challenging and reviewing agent actions

### 7.5 Ecosystem Development Needs

#### For Successful Integration:

**Regen Network Side**:
- Complete MCP server implementation for registry and data access
- Document MCP resource schemas and API specifications
- Provide sandbox/testnet environments for agent development
- Establish agent guidelines and best practices
- Create agent developer program with support and incentives

**ElizaOS Side**:
- Continued improvement of MCP plugin capabilities
- Cosmos/Tendermint blockchain integration enhancements
- Educational resources for building ReFi agents
- Example agents demonstrating Regen integration
- Community of practice for regenerative AI agents

**Community**:
- Developers building specialized Regen agents
- Ecological experts validating agent outputs
- Funders supporting agent development
- Projects testing and deploying agents
- Governance participation in agent standards

---

## 8. Conclusion

ElizaOS represents a powerful, flexible framework for building autonomous AI agents, with strong support for Web3 integration and extensibility through its plugin architecture. The Model Context Protocol provides a standardized bridge between these agents and external data sources, making it an ideal integration point for Regen Network's ecological data.

Regen Network's partnership with Gaia AI to develop Regen AI demonstrates a clear vision for leveraging AI agents to advance the regenerative economy. The development of MCP infrastructure for planetary intelligence is a crucial step toward making Regen's rich ecological data accessible to AI systems.

The combination of ElizaOS's multi-agent capabilities with Regen Network's comprehensive ecological data infrastructure creates unprecedented opportunities for:

- **Democratizing Access**: Making complex ecological data understandable and actionable for everyone
- **Automating Coordination**: Reducing friction in regenerative markets and verification processes
- **Scaling Impact**: Enabling more efficient allocation of capital toward regenerative projects
- **Building Trust**: Providing transparent, verifiable information about ecological outcomes
- **Fostering Innovation**: Creating a platform for countless new regenerative applications

### Key Takeaways:

1. **ElizaOS is production-ready**: The framework is mature, well-documented, and actively maintained with a growing community

2. **MCP integration is available**: The ElizaOS MCP plugin provides the technical foundation for connecting to Regen data

3. **Regen is building infrastructure**: Active development of MCP servers and agent partnerships demonstrates commitment

4. **Near-term opportunities are clear**: Specific use cases like registry exploration and data analysis are immediately buildable

5. **Long-term vision is transformative**: The potential for agent-mediated planetary regeneration is profound

### Recommendations:

**For Developers**:
- Start experimenting with ElizaOS and the MCP plugin
- Monitor Regen Network's MCP repository for updates
- Join the Regen AI community to collaborate on agent development
- Build proof-of-concept agents demonstrating specific use cases

**For Regen Network**:
- Prioritize MCP server documentation and developer experience
- Create reference implementations of common agent patterns
- Establish standards and guidelines for agent behavior
- Foster a community of practice around regenerative AI

**For the Ecosystem**:
- Support projects building at the intersection of AI and ReFi
- Participate in governance discussions about agent standards
- Share knowledge and learnings across the community
- Stay committed to the regenerative mission while embracing technological innovation

The convergence of ElizaOS, MCP, and Regen Network represents a significant opportunity to accelerate planetary regeneration through intelligent automation. By making ecological data accessible to AI agents and empowering those agents to act in service of regeneration, we can create new possibilities for coordinating human and natural systems at the scale required by the climate crisis.

---

## Sources

### ElizaOS Framework
- [GitHub - elizaOS/eliza](https://github.com/elizaOS/eliza)
- [ElizaOS Documentation](https://docs.elizaos.ai)
- [ElizaOS Official Website](https://elizaos.ai/)
- [Eliza: A Web3 friendly AI Agent Operating System (arXiv)](https://arxiv.org/html/2501.06781v1)
- [Overview | eliza](https://elizaos.github.io/eliza/docs/core/overview/)
- [Introduction to Eliza](https://elizaos.github.io/eliza/docs/intro)
- [ai16z Unveils ElizaOS: The Path to Autonomous AI Agents](https://www.ainvest.com/news/ai16z-unveils-elizaos-path-to-autonomous-ai-agents-25021010b867fc71b073b28a/)
- [Create AI Agents with ai16z Eliza | Medium](https://medium.com/ai-dev-tips/create-ai-agents-with-ai16z-in-15-minutes-639751e6ea69)

### ElizaOS Architecture
- [Reading Notes of ElizaOS [2] | Medium](https://kvutien-yes.medium.com/reading-notes-of-elizaos-c29ac050555c)
- [ai16z's AI Agent framework Eliza V2 is released](https://followin.io/en/feed/15159830)
- [Transform Your Projects with Eliza: The Multi-Agent AI Framework](https://www.blockydevs.com/blog/transform-your-projects-with-eliza-the-multi-agent-ai-framework)

### ElizaOS and Stanford Partnership
- [ai16z's Eliza Labs, Stanford clinch AI research partnership](https://cointelegraph.com/news/ai16z-stanfod-ai-research-partnership)
- [a16z and Eliza Labs partner with Stanford | Medium](https://medium.com/@leonmorales1590/a16z-and-eliza-labs-partner-with-stanford-to-boost-ai-research-115fa5d42632)

### MCP Integration
- [Fleek | Introducing the Eliza MCP Plugin](https://resources.fleek.xyz/blog/announcements/fleek-eliza-mcp-plugin/)
- [GitHub - fleek-platform/eliza-plugin-mcp](https://github.com/fleek-platform/eliza-plugin-mcp)
- [@fleek-platform/eliza-plugin-mcp - npm](https://www.npmjs.com/package/@fleek-platform/eliza-plugin-mcp)
- [Add Model Context Protocol (MCP) Support · Issue #844](https://github.com/elizaOS/eliza/issues/844)
- [How to Connect ElizaOS with Heurist Mesh MCP | Medium](https://heuristai.medium.com/how-to-connect-elizaos-with-heurist-mesh-mcp-336fcce19250)

### ElizaOS Setup and Configuration
- [Deploying ElizaOS to Production | eliza](https://elizaos.github.io/eliza/docs/guides/remote-deployment/)
- [eliza/docs/docs/guides/configuration.md](https://github.com/elizaOS/eliza/blob/main/docs/docs/guides/configuration.md)
- [How to Build Web3-Enabled AI Agents with Eliza | Quicknode](https://www.quicknode.com/guides/ai/how-to-setup-an-ai-agent-with-eliza-ai16z-framework)
- [Build Your Own AI Agent in Minutes with Eliza | DEV](https://dev.to/nodeshiftcloud/build-your-own-ai-agent-in-minutes-with-eliza-a-complete-guide-263l)
- [Frequently Asked Questions | eliza](https://eliza.how/docs/faq)

### Plugin Development
- [Eliza Plugin Development Guide | Flow](https://developers.flow.com/blockchain-development-tutorials/use-AI-to-build-on-flow/agents/eliza/build-plugin)
- [Local Development Guide | eliza](https://elizaos.github.io/eliza/docs/guides/local-development/)
- [Advanced Usage Guide | eliza](https://elizaos.github.io/eliza/docs/guides/advanced/)
- [Part 2: Deep Dive into Actions, Providers, and Evaluators](https://elizaos.github.io/eliza/community/ai-dev-school/part2/)
- [Plugins | eliza](https://eliza.how/docs/core/plugins)

### Regen Network
- [Regen Network](https://www.regen.network/)
- [GitHub - regen-network/regen-ledger](https://github.com/regen-network/regen-ledger)
- [Regen Ledger Documentation](https://docs.regen.network/)
- [Overview | Regen Ledger Documentation](https://docs.regen.network/ledger/)
- [Regen Network - P2P Foundation](https://wiki.p2pfoundation.net/Regen_Network)

### Regen AI
- [Announcing Regen AI - Paragraph](https://paragraph.com/@gaiaai/regenai)
- [Announcing Regen AI - Regen Forum](https://forum.regen.network/t/announcing-regen-ai/553)
- [Regen AI: Agent for Planetary Regeneration](https://smartvillage.ca/2025/02/01/regenai/)
- [Regen AI](https://www.regen-ai.org/)

### Regen Data Infrastructure
- [Regen Data Standards](https://framework.regen.network/)
- [Regen Dataset Explorer](https://regenscan.com/)
- [Regen Data Stream | Medium](https://medium.com/regen-network/regen-data-stream-revolutionizing-environmental-project-tracking-1998de748dc9)
- [Ecological State Protocols | Medium](https://medium.com/regen-network/ecological-state-protocols-1c7e97dadeae)

### Cosmos and IBC
- [What is Cosmos IBC?](https://supra.com/academy/cosmos-ibc/)
- [Cosmos: The Epicenter Of On-Chain AI](https://x.com/cosmos/status/1924784265843376160)
- [IBC - Ecosystem - Cosmos](https://cosmos.network/ibc)
- [Deep Dive into Cosmos IBC Protocol](https://blog.bcas.io/deep-dive-cosmos-inter-blockchain-communication-protocol)
- [GitHub - cosmos/ibc-go](https://github.com/cosmos/ibc-go)
- [Top Projects in the Cosmos Ecosystem to Watch in 2025](https://www.kucoin.com/learn/crypto/top-cosmos-ecosystem-projects-to-watch)

---

**Report compiled:** December 9, 2025
**For:** Regen AI Integration Research
**Framework versions:** ElizaOS v2, Regen Ledger (current)
