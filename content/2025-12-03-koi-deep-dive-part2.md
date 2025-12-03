# KOI MCP Deep Dive - Part 2: Tutorial & Resources

This is **Part 2** of the Week 2 Regen AI update. See [Part 1](https://forum.regen.network/t/week-2-12-regen-ai-update-koi-mcp-deep-dive/XXX) for the full technical deep dive into how KOI works.

---

## The Birth of Automated Regenerative Media

Perhaps the most remarkable demonstration of KOI in action is the automated weekly podcast.

![regen_digest_podcast|690x327](upload://q0QJNISZrTmdkYRofypGusRiykS.png)
*Visit [digest.gaiaai.xyz](https://digest.gaiaai.xyz/) to experience the first AI-generated Regen Network podcast—a synthesis of each week's activity across the entire ecosystem.*

---

## Tutorial: Connect to the KOI Brain

Ready to tap into this knowledge network yourself? Here's how to connect the KOI MCP to your AI workflow.

### Option 1: Claude Code

The most powerful way to work with the Regen KOI MCP is directly in Claude Code.

![regen-koi-gpt-chat2|690x453](upload://kNpOY23nbx46rTVm4RlOTIg5XFj.jpeg)
![regen-koi-gpt-chat3|690x351](upload://vS8CFCoX5HskiAkQwbO2IzyCqCn.jpeg)
*Example queries and responses from the KOI MCP—showing how natural language questions return grounded, cited answers.*

1. Clone and build the Repository
```bash
cd
mkdir regen-koi-mcp
cd regen-koi-mcp
git clone https://github.com/gaiaaiagent/regen-koi-mcp.git
cd regen-koi-mcp
npm install
npm run build
cd ..
```

2. Connect with Claude Code (In `~/regen-koi-mcp`)
Place the following in `~/regen-koi-mcp/.mcp.json`. Replace `USER` with your username on your system.
```json
{
  "mcpServers": {
      "regen-koi": {
        "command": "node",
        "args": ["/home/USER/regen-koi-mcp/regen-koi-mcp/dist/index.js"],
        "env": {
          "KOI_API_ENDPOINT": "https://regen.gaiaai.xyz/api/koi",
          "JENA_ENDPOINT": "https://regen.gaiaai.xyz/api/koi/fuseki/koi/sparql"
        }
      },
    }
}
```

Place the following in `~/regen-koi-mcp/.claude/settings.json`
```json
{
  "enableAllProjectMcpServers": true
}
```

3. In your terminal open claude (In `~/regen-koi-mcp`)
```
claude

# In claude verify the mcp is connected.
/mcp
```

You should see the `regen-koi` server listed with its available tools (`search_knowledge`, `get_stats`, `generate_weekly_digest`, etc.).

4. Test it out
```
# In claude code
Please search the koi network for the notes on the latest governance discussions.
```


### Option 2: Regen KOI GPT

You can immediately access the Regen KOI Network via the Regen KOI GPT. Try it out!

![regen-koi-gpt|690x348](upload://wzUbJKuP8erjfwkrmnaFGCy111P.png)
*The Regen KOI GPT custom assistant—access the full knowledge base directly from ChatGPT.*

**[Launch Regen KOI GPT →](https://chatgpt.com/g/g-692f3c6bc5e48191b3d1721f4a8ccdec-regen-koi-gpt)**

### Option 3: Connect Via NPX

For Claude Desktop or other MCP-compatible clients, use the NPX package:

```bash
claude mcp add regen-koi npx regen-koi-mcp@latest
```

For detailed platform-specific instructions, see the [project README](https://github.com/gaiaaiagent/regen-koi-mcp).

### Using KOI Tools

Once connected, you have access to a powerful suite of tools that continue to expand:

**Knowledge Base Search**

| Tool | Description |
|------|-------------|
| `search_knowledge` | Hybrid semantic + graph search with date filtering |
| `get_stats` | Knowledge base statistics |
| `generate_weekly_digest` | Create curated weekly summaries |
| `get_notebooklm_export` | Export full content for NotebookLM (saves to file, 99% context reduction) |

**Code Knowledge Graph** *(New!)*

| Tool | Description |
|------|-------------|
| `query_code_graph` | Query relationships between Keepers, Messages, and Events |
| `search_github_docs` | Search across 5 indexed Regen GitHub repositories |
| `get_repo_overview` | Get structured overview of repository architecture |
| `get_tech_stack` | Understand languages, frameworks, and dependencies |

**Authentication** *(Team Members)*

| Tool | Description |
|------|-------------|
| `regen_koi_authenticate` | OAuth login for @regen.network email to access internal docs |


### Connecting Over API

For developers who want to integrate KOI directly into their applications, the knowledge base is accessible via a REST API. The base URL is:

```
https://regen.gaiaai.xyz/api/koi
```

For full API documentation, see the [API Endpoints Guide](https://github.com/gaiaaiagent/regen-koi-mcp/blob/main/docs/API_ENDPOINTS.md). An OpenAPI 3.1 schema is also available for integration with tools like Custom GPTs or API clients.

### Example Queries to Try

Once configured, try asking Claude:

**Knowledge Search:**
- *"What are the current governance proposals being discussed in Regen Network?"*
- *"Explain the Ecometric methodology for grassland carbon credits"*
- *"What happened in Regen Network over the past two weeks?"*

**Code Intelligence:**
- *"How does MsgCreateBatch work in the ecocredit module?"*
- *"What keepers handle credit retirement?"*
- *"Show me the structure of the basket module"*

**Digests & Exports:**
- *"Generate a weekly digest and save it to a file"*
- *"Get the full NotebookLM export with all forum posts"*

Each response comes grounded in verified knowledge, with citations you can follow to primary sources.

---

## Resources & Links

**Getting Started:**
- **Regen KOI GPT**: [Launch on ChatGPT](https://chatgpt.com/g/g-692f3c6bc5e48191b3d1721f4a8ccdec-regen-koi-gpt)
- **Regen KOI MCP**: [github.com/gaiaaiagent/regen-koi-mcp](https://github.com/gaiaaiagent/regen-koi-mcp)
- **KOI MCP User Guide**: [User Guide on GitHub](https://github.com/gaiaaiagent/regen-koi-mcp/blob/main/docs/USER_GUIDE.md)

**Weekly Digests:**
- **Podcast & Digests**: [digest.gaiaai.xyz](https://digest.gaiaai.xyz/)

**KOI Protocol:**
- **BlockScience**: [block.science](https://block.science/) — creators of the KOI specification
- **A Preview of the KOI-net Protocol**: [BlockScience Blog](https://blog.block.science/a-preview-of-the-koi-net-protocol/)
- **KOI Nodes as Neurons**: [BlockScience Blog](https://blog.block.science/koi-nodes-as-neurons/)
- **KOI-net Protocol Spec**: [github.com/BlockScience/koi-net](https://github.com/BlockScience/koi-net)

**Community:**
- **Tuesday Stand-up**: [Join us Tuesdays](https://calendar.google.com/calendar/u/0/embed?src=c_1250640b0093c1453ac648937f168c97e48175e7862fb02d38f45e0639df2b25@group.calendar.google.com) for live development updates
- **Previous Update**: [Week 1 - Announcing Regen AI](https://forum.regen.network/t/announcing-regen-ai/553)

---

*This is the second of 12 weekly updates documenting the development of Regen AI. The forum is our knowledge commons. Every discussion here feeds back into KOI, strengthening our collective intelligence.*
