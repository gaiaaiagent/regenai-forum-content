# Claude Code MCP Setup Tutorial: Complete Guide for Regen Network MCPs

## Introduction

This comprehensive tutorial will guide you through setting up Model Context Protocol (MCP) servers in Claude Code, with a specific focus on installing and configuring the four Regen Network MCPs. By the end of this guide, you'll understand the difference between project-scoped and global MCP installations, know how to verify your MCP servers are working correctly, and have practical examples for testing each server.

## What is MCP?

Model Context Protocol (MCP) is a standard protocol that allows Claude Code to connect to external tools and data sources, extending its capabilities beyond the built-in features. MCP servers can provide access to databases, APIs, file systems, and specialized services.

The Regen Network ecosystem provides four MCP servers:

1. **regen-koi-mcp** - Access to the KOI knowledge graph and semantic data
2. **regen-python-mcp** - Python-based Regen Network utilities
3. **regen** - Core Regen Ledger blockchain data access
4. **regen-registry-review-mcp** - Automated carbon credit project document review

## Prerequisites

Before starting, ensure you have the following tools installed on your system:

### 1. Node.js (v20 or later)

Node.js is required to run JavaScript-based MCP servers.

**Installation:**

- **macOS** (using Homebrew):
  ```bash
  brew install node
  ```

- **Linux** (Ubuntu/Debian):
  ```bash
  curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
  sudo apt-get install -y nodejs
  ```

- **Windows**:
  Download from [nodejs.org](https://nodejs.org/)

**Verify installation:**
```bash
node --version
npm --version
```

### 2. Python (3.10 or later)

Python is required for Python-based MCP servers.

**Verify installation:**
```bash
python --version
# or
python3 --version
```

### 3. uv (Python Package Manager)

`uv` is Astral's modern Python package manager, required for running Python MCP servers.

**Installation:**

- **macOS** (using Homebrew):
  ```bash
  brew install uv
  ```

- **Linux/Windows**:
  ```bash
  curl -LsSf https://astral.sh/uv/install.sh | sh
  ```

**Verify installation:**
```bash
uv --version
```

### 4. Git

Required for cloning MCP repositories.

**Verify installation:**
```bash
git --version
```

### 5. Claude Code

Ensure you have Claude Code installed. If not, follow the [official installation guide](https://claude.com/claude-code).

## Understanding MCP Configuration Scopes

Claude Code supports three different scopes for MCP configuration:

### 1. User Scope (Global)
- **Location**: `~/.claude.json`
- **Availability**: Available across all projects for your user account
- **Use Case**: Personal tools you want to use in every project
- **Version Control**: Not tracked in git
- **Command**: `claude mcp add <name> --scope user`

### 2. Project Scope (Team-Shared)
- **Location**: `.mcp.json` in project root
- **Availability**: Shared with everyone working on the project
- **Use Case**: Project-specific tools that your team needs
- **Version Control**: Tracked in git, shared with team
- **Command**: `claude mcp add <name> --scope project`

### 3. Local Scope (Project-Specific, Private)
- **Location**: `.claude/settings.local.json` in project root
- **Availability**: Available only to you in the current project
- **Use Case**: Personal development servers, experimental configs, sensitive credentials
- **Version Control**: Not tracked in git
- **Command**: `claude mcp add <name> --scope local` (default)

### Scope Priority

When servers with the same name exist at multiple scopes, Claude Code resolves conflicts using this priority:

**Local > Project > User**

This means local-scoped servers override project-scoped servers, which override user-scoped servers.

### Best Practices

**Use Project Scope When:**
- The MCP server is essential for the project's functionality
- You want to share the configuration with your team
- The configuration should be version-controlled
- You're setting up a standard development environment

**Use User Scope When:**
- You want a tool available across all your projects
- The tool is for personal productivity
- You don't want to clutter individual project configs

**Use Local Scope When:**
- You're experimenting with a new MCP server
- The configuration contains sensitive credentials (though environment variables are preferred)
- You want to override a project/user configuration temporarily

## Installation Methods: CLI vs Manual Configuration

There are two main approaches to installing MCP servers in Claude Code:

### Method 1: CLI Wizard (`claude mcp add`)

**Pros:**
- Quick setup for simple configurations
- Interactive prompts guide you through the process
- Good for testing and experimentation

**Cons:**
- Frustrating for complex configurations with many parameters
- Difficult to see all configurations at once
- Typos require restarting the entire process
- Hard to copy/paste complex configurations

**Example:**
```bash
claude mcp add github --scope user
```

### Method 2: Manual JSON Configuration (Recommended)

**Pros:**
- Full control over all configuration options
- Easy to edit and update configurations
- See all MCP servers at once
- Perfect for complex setups with multiple environment variables
- Easy to copy/paste and share configurations
- Better for automation and team sharing

**Cons:**
- Slightly steeper learning curve
- Requires understanding JSON syntax
- Must manually restart Claude Code after changes

**Example:**
```json
{
  "mcpServers": {
    "server-name": {
      "command": "node",
      "args": ["/path/to/server/index.js"],
      "env": {
        "VARIABLE": "value"
      },
      "description": "Server description"
    }
  }
}
```

### Recommendation

For the Regen Network MCPs, **manual JSON configuration is strongly recommended** because:
- The servers require multiple environment variables
- You need to specify absolute paths to the built server files
- It's easier to maintain and debug
- You can see all four MCP configurations at once

## Step-by-Step Installation: Regen Network MCPs

This guide uses the **project-scoped manual configuration method** for installing all four Regen MCPs.

### Step 1: Create Your Project Directory

Create a dedicated directory for your Regen MCP setup:

```bash
mkdir regen-mcps
cd regen-mcps
```

### Step 2: Clone the MCP Repositories

Clone all four Regen MCP repositories into a `mcps` subdirectory:

```bash
mkdir mcps
cd mcps

# Clone regen-koi-mcp (TypeScript/Node.js)
git clone https://github.com/gaiaaiagent/regen-koi-mcp.git

# Clone regen-python-mcp (Python)
git clone https://github.com/gaiaaiagent/regen-python-mcp.git

# Clone regen (TypeScript/Node.js)
git clone https://github.com/regen-network/mcp.git

# Clone regen-registry-review-mcp (Python)
git clone https://github.com/gaiaaiagent/regen-registry-review-mcp.git

cd ..
```

Your directory structure should now look like:
```
regen-mcps/
└── mcps/
    ├── regen-koi-mcp/
    ├── regen-python-mcp/
    ├── mcp/
    └── regen-registry-review-mcp/
```

### Step 3: Build the TypeScript/Node.js MCP Servers

Build the two Node.js-based MCP servers:

```bash
# Build regen-koi-mcp
cd mcps/regen-koi-mcp
npm install
npm run build
cd ../..

# Build regen (core MCP server)
cd mcps/mcp
npm install
npm run build
cd ../..
```

**Verify builds:**
```bash
# Check that the built files exist
ls mcps/regen-koi-mcp/dist/index.js
ls mcps/mcp/server/dist/index.js
```

### Step 4: Setup Python MCP Servers

Setup the two Python-based MCP servers using `uv`:

```bash
# Setup regen-python-mcp
cd mcps/regen-python-mcp
uv sync
cd ../..

# Setup regen-registry-review-mcp
cd mcps/regen-registry-review-mcp
uv sync

# Configure environment variables for registry-review
cp .env.example .env
# Edit .env to add your REGISTRY_REVIEW_ANTHROPIC_API_KEY
cd ../..
```

**Note:** The `regen-registry-review-mcp` requires an Anthropic API key for LLM-based document extraction. If you don't have one, you can still configure the server, but some features will be limited.

### Step 5: Enable Project-Scoped MCPs

Create the `.claude/settings.json` file to enable project-scoped MCP servers:

```bash
mkdir -p .claude
cat > .claude/settings.json << 'EOF'
{
  "enableAllProjectMcpServers": true
}
EOF
```

**Important:** Without this file, Claude Code will not load MCP servers from `.mcp.json`.

### Step 6: Create the MCP Configuration File

Create the `.mcp.json` file with configurations for all four Regen MCPs:

```bash
cat > .mcp.json << EOF
{
  "mcpServers": {
    "regen-koi": {
      "command": "node",
      "args": ["$(pwd)/mcps/regen-koi-mcp/dist/index.js"],
      "env": {
        "KOI_API_ENDPOINT": "https://regen.gaiaai.xyz/api/koi",
        "JENA_ENDPOINT": "https://regen.gaiaai.xyz/api/koi/fuseki/koi/sparql"
      },
      "description": "KOI Knowledge Graph MCP Server - Access to Regen's semantic knowledge base"
    },
    "regen-python": {
      "command": "uv",
      "args": [
        "run",
        "--directory",
        "$(pwd)/mcps/regen-python-mcp",
        "python",
        "main.py"
      ],
      "env": {
        "PYTHONPATH": "$(pwd)/mcps/regen-python-mcp/src",
        "REGEN_MCP_LOG_LEVEL": "INFO"
      },
      "description": "Regen Python MCP Server - Python utilities for Regen Network"
    },
    "regen": {
      "command": "node",
      "args": ["$(pwd)/mcps/mcp/server/dist/index.js"],
      "env": {
        "NODE_ENV": "production",
        "REGEN_RPC_ENDPOINT": "https://regen-rpc.publicnode.com:443"
      },
      "description": "Regen Network MCP Server - Access to Regen Ledger blockchain data"
    },
    "registry-review": {
      "command": "uv",
      "args": [
        "run",
        "--directory",
        "$(pwd)/mcps/regen-registry-review-mcp",
        "python",
        "-m",
        "registry_review_mcp.server"
      ],
      "env": {
        "REGISTRY_REVIEW_LLM_EXTRACTION_ENABLED": "true"
      },
      "description": "Registry Review MCP Server - Automated document review for carbon credit projects"
    }
  }
}
EOF
```

**Important Notes:**

1. The `$(pwd)` command expands to your current working directory, creating absolute paths
2. On Windows, use `%cd%` instead of `$(pwd)`, or manually replace with absolute paths
3. Each server has a unique name (`regen-koi`, `regen-python`, `regen`, `registry-review`)
4. Environment variables are specific to each server's requirements

### Step 7: Verify the Configuration

Before starting Claude Code, verify your configuration file is valid JSON:

```bash
# On Linux/macOS with Python
python3 -m json.tool .mcp.json

# Or use Node.js
node -e "JSON.parse(require('fs').readFileSync('.mcp.json', 'utf8'))"
```

If there are syntax errors, fix them before proceeding.

## Verifying MCP Servers Are Working

### Method 1: Using the `/mcp` Command (Primary Method)

The `/mcp` command in Claude Code displays the status of all configured MCP servers.

1. Start Claude Code from your project directory:
   ```bash
   cd regen-mcps
   claude
   ```

2. Type the `/mcp` command in the chat:
   ```
   /mcp
   ```

3. Claude Code will display the MCP Server Status:
   ```
   MCP Server Status:
   - regen-koi: connected
   - regen-python: connected
   - regen: connected
   - registry-review: connected
   ```

**Troubleshooting Disconnected Servers:**

If a server shows as "disconnected", try these steps:

1. **Check server installation:**
   ```bash
   # For Node.js servers
   ls -l mcps/regen-koi-mcp/dist/index.js
   ls -l mcps/mcp/server/dist/index.js

   # For Python servers
   cd mcps/regen-python-mcp && uv run python main.py --help
   cd mcps/regen-registry-review-mcp && uv run python -m registry_review_mcp.server --help
   ```

2. **Verify configuration paths:**
   ```bash
   cat .mcp.json | grep -A 3 "regen-koi"
   ```

3. **Check for path issues:**
   - Ensure paths are absolute (not relative)
   - On Windows, use forward slashes or escaped backslashes

4. **Restart Claude Code:**
   - Exit Claude Code completely
   - Start it again from the project directory

5. **Enable debug mode:**
   ```bash
   claude --mcp-debug
   ```

### Method 2: Using CLI Commands

You can also verify MCP servers using the `claude mcp` CLI commands:

```bash
# List all configured servers
claude mcp list

# Get details for a specific server
claude mcp get regen-koi

# Test a server connection
claude mcp get regen-python
```

### Method 3: Test with a Simple Prompt

Once all servers show as connected, test them with a simple prompt:

```
What MCP tools are available?
```

Claude should list the tools provided by each MCP server.

## Testing Each MCP Server

Now that your MCP servers are running, let's test each one with specific prompts.

### Testing regen-koi-mcp

The KOI MCP provides access to Regen Network's semantic knowledge graph.

**Test Prompt 1: Search the Knowledge Graph**
```
Use the KOI MCP to search for information about "carbon credits" in the knowledge graph.
```

**Test Prompt 2: Query Entities**
```
Query the KOI knowledge graph for entities related to ecological monitoring.
```

**Test Prompt 3: SPARQL Query**
```
Execute a SPARQL query on the KOI endpoint to find all projects in the knowledge graph.
```

**Expected Behavior:**
- The MCP should connect to the KOI API endpoint
- Return structured data about carbon credits, projects, or monitoring
- Show RDF/semantic data relationships

### Testing regen-python-mcp

The Python MCP provides utilities for interacting with Regen Network.

**Test Prompt 1: Network Information**
```
Use the regen-python MCP to get information about the Regen Network blockchain.
```

**Test Prompt 2: Data Validation**
```
Use the regen-python MCP to validate a Regen Network address format.
```

**Test Prompt 3: Utility Functions**
```
What utility functions are available in the regen-python MCP?
```

**Expected Behavior:**
- The MCP should execute Python functions
- Return formatted data about the network
- Provide validation and utility operations

### Testing regen (Core Ledger MCP)

The core Regen MCP provides direct access to Regen Ledger blockchain data.

**Test Prompt 1: Query Blockchain Data**
```
Use the regen MCP to query the latest block height on Regen Ledger.
```

**Test Prompt 2: Account Information**
```
Query the regen MCP for information about a specific Regen address (use an example address).
```

**Test Prompt 3: Ecosystem Credits**
```
Use the regen MCP to list available ecocredit classes on the Regen Ledger.
```

**Expected Behavior:**
- The MCP should connect to the Regen RPC endpoint
- Return blockchain data in JSON format
- Show current state of the ledger

### Testing regen-registry-review-mcp

The Registry Review MCP automates document review for carbon credit projects.

**Test Prompt 1: List Review Tools**
```
What document review capabilities does the registry-review MCP provide?
```

**Test Prompt 2: Document Analysis (if you have a sample document)**
```
Use the registry-review MCP to analyze a carbon credit project document for compliance.
```

**Test Prompt 3: Extraction Features**
```
What information can the registry-review MCP extract from project documents?
```

**Expected Behavior:**
- The MCP should describe its document review capabilities
- If LLM extraction is enabled, it can analyze documents
- Return structured data about project compliance

## Common Issues and Troubleshooting

### Issue 1: "Cannot connect to MCP server"

**Symptoms:**
- Server shows as "disconnected" in `/mcp`
- Error messages about connection failures

**Solutions:**

1. **Check Node.js/Python installation:**
   ```bash
   node --version
   python3 --version
   uv --version
   ```

2. **Verify paths in .mcp.json are absolute:**
   ```bash
   # Replace $(pwd) with actual absolute paths if needed
   sed -i 's|$(pwd)|'$(pwd)'|g' .mcp.json
   ```

3. **Check file permissions:**
   ```bash
   chmod +x mcps/regen-koi-mcp/dist/index.js
   chmod +x mcps/mcp/server/dist/index.js
   ```

4. **Windows-specific: Use full path to npx:**
   ```json
   {
     "command": "C:\\Program Files\\nodejs\\node.exe"
   }
   ```

### Issue 2: "spawn uv ENOENT" (macOS/Linux)

**Symptoms:**
- Python MCP servers fail to start
- Error message mentions "uv" not found

**Solutions:**

1. **Use absolute path to uv:**
   ```bash
   which uv  # Get the path
   ```

   Then update `.mcp.json`:
   ```json
   {
     "command": "/usr/local/bin/uv"  # or your actual path
   }
   ```

2. **Add uv to PATH:**
   ```bash
   export PATH="$HOME/.local/bin:$PATH"
   ```

### Issue 3: Python Package Conflicts

**Symptoms:**
- Python MCP servers fail with import errors
- Dependency version conflicts

**Solutions:**

1. **Recreate uv environment:**
   ```bash
   cd mcps/regen-python-mcp
   rm -rf .venv
   uv sync
   ```

2. **Check Python version:**
   ```bash
   python3 --version  # Must be 3.10+
   ```

### Issue 4: Configuration Not Loading

**Symptoms:**
- `/mcp` shows no servers
- Changes to `.mcp.json` don't take effect

**Solutions:**

1. **Verify `.claude/settings.json` exists:**
   ```bash
   cat .claude/settings.json
   ```

2. **Restart Claude Code completely:**
   - Don't just close the chat window
   - Quit the entire application
   - Restart from the project directory

3. **Check JSON syntax:**
   ```bash
   python3 -m json.tool .mcp.json
   ```

### Issue 5: Environment Variables Not Working

**Symptoms:**
- MCP server starts but can't connect to external services
- API errors or endpoint not found

**Solutions:**

1. **Verify environment variables in `.mcp.json`:**
   ```json
   {
     "env": {
       "KOI_API_ENDPOINT": "https://regen.gaiaai.xyz/api/koi"
     }
   }
   ```

2. **Check for typos in variable names**

3. **Test endpoints manually:**
   ```bash
   curl https://regen.gaiaai.xyz/api/koi
   ```

### Issue 6: MCP Servers Working but Claude Ignores Them

**Symptoms:**
- `/mcp` shows all servers as "connected"
- Claude doesn't use the MCP tools in responses

**Solutions:**

1. **Be explicit in your prompts:**
   - Bad: "Tell me about carbon credits"
   - Good: "Use the regen-koi MCP to search for carbon credits"

2. **Clear conversation context:**
   ```
   /clear
   ```

3. **Check server descriptions:**
   - Ensure descriptions in `.mcp.json` clearly explain what each server does

### Issue 7: Performance Issues / Slow Responses

**Symptoms:**
- MCP servers take a long time to respond
- Claude Code becomes unresponsive

**Solutions:**

1. **Check network connectivity:**
   ```bash
   ping regen.gaiaai.xyz
   ```

2. **Reduce logging verbosity:**
   ```json
   {
     "env": {
       "REGEN_MCP_LOG_LEVEL": "WARNING"  # Instead of INFO or DEBUG
     }
   }
   ```

3. **Use compact command if context is too large:**
   ```
   /compact
   ```

## Advanced Configuration

### Using npx for Node.js Servers (Alternative)

Instead of building servers locally, you can use `npx` to run them:

```json
{
  "mcpServers": {
    "example-server": {
      "command": "npx",
      "args": ["-y", "@package/server-name"]
    }
  }
}
```

**Note:** This downloads packages on-demand, which can be slower on first run.

### Debug Mode

Enable verbose logging for troubleshooting:

```bash
# Start Claude Code with debug flag
claude --mcp-debug

# Or set environment variable
export MCP_CLAUDE_DEBUG=true
claude
```

**Warning:** Disable debug mode for normal operation to avoid JSON parsing issues.

### Enterprise MCP Management

For organizations, Claude Code supports enterprise-managed MCP configurations in `managed-mcp.json`:

- Centralized control over which MCP servers employees can access
- Ability to prevent unauthorized MCP servers
- Option to disable MCP entirely if needed

### Timeout Configuration

Configure MCP server startup timeout:

```json
{
  "mcpServers": {
    "slow-server": {
      "command": "node",
      "args": ["server.js"],
      "env": {
        "MCP_TIMEOUT": "30000"
      }
    }
  }
}
```

## Security Best Practices

### 1. Protect Sensitive Credentials

- **Never commit API keys to `.mcp.json`**
- Use environment variables for secrets
- Add `.mcp.json` to `.gitignore` if it contains sensitive data
- Use local scope for personal credentials

### 2. Limit Filesystem Access

For MCP servers that access the filesystem:
- Only allowlist the specific project directory
- Start with read-only access
- Enable writes only when necessary

### 3. Review MCP Server Code

Before installing an MCP server:
- Review the source code on GitHub
- Check for suspicious network calls
- Verify the maintainer's reputation
- Read user reviews and issues

### 4. Use Denylist for Restrictions

In enterprise settings, use the denylist feature:
- Denylist takes absolute precedence over allowlist
- Block servers by name or command
- Applies to all scopes (user, project, local, enterprise)

## Managing Multiple Projects

### Strategy 1: User-Scoped for Common Tools

Install frequently used MCPs globally:

```bash
claude mcp add github --scope user
claude mcp add filesystem --scope user
```

### Strategy 2: Project-Scoped for Team Consistency

For each project, maintain a `.mcp.json` file:

```
project-a/
├── .mcp.json  # Project-specific MCPs
└── .claude/settings.json

project-b/
├── .mcp.json  # Different project MCPs
└── .claude/settings.json
```

### Strategy 3: Hybrid Approach (Recommended)

- Use **user scope** for general productivity tools
- Use **project scope** for project-specific tools like Regen MCPs
- Use **local scope** for experiments and personal overrides

## Useful Commands Reference

### MCP Management Commands

```bash
# List all configured MCP servers
claude mcp list

# Add a server (user scope)
claude mcp add <name> --scope user

# Add a server (project scope)
claude mcp add <name> --scope project

# Get details for a specific server
claude mcp get <name>

# Remove a server
claude mcp remove <name>

# Test a server
claude mcp get <name>
```

### Claude Code Commands

Inside Claude Code chat:

```
/mcp           # Show MCP server status
/clear         # Clear conversation context
/compact       # Compact conversation (keep summary)
/status        # Check conversation size
```

### Debug Commands

```bash
# Start with debug logging
claude --mcp-debug

# Check configuration syntax
python3 -m json.tool .mcp.json

# Test server independently
node mcps/regen-koi-mcp/dist/index.js
uv run --directory mcps/regen-python-mcp python main.py
```

## Migration Guide: Moving from User to Project Scope

If you initially configured MCPs in user scope and want to move them to project scope:

1. **Export current configuration:**
   ```bash
   # View user-scoped config
   cat ~/.claude.json
   ```

2. **Copy relevant server configurations to project `.mcp.json`:**
   ```bash
   # Create project config
   cat > .mcp.json << EOF
   {
     "mcpServers": {
       // Paste server configs here
     }
   }
   EOF
   ```

3. **Update paths to be project-relative:**
   - Change absolute paths to use `$(pwd)`
   - Or use relative paths from project root

4. **Enable project MCPs:**
   ```bash
   mkdir -p .claude
   echo '{"enableAllProjectMcpServers": true}' > .claude/settings.json
   ```

5. **Remove from user scope (optional):**
   ```bash
   claude mcp remove <name>
   ```

6. **Test the migration:**
   ```bash
   claude
   # Then type: /mcp
   ```

## Conclusion

You now have a complete setup of all four Regen Network MCP servers in Claude Code! This guide covered:

- Understanding MCP scopes (user, project, local)
- Choosing between CLI and manual configuration methods
- Installing and building all four Regen MCPs
- Verifying servers are working correctly
- Testing each MCP with specific prompts
- Troubleshooting common issues
- Security best practices

### Key Takeaways

1. **Use project scope** for team-shared, version-controlled MCP configurations
2. **Manual JSON configuration** provides the most flexibility and control
3. **The `/mcp` command** is your primary verification tool
4. **Be explicit in prompts** when you want Claude to use specific MCP tools
5. **Debug mode** (`--mcp-debug`) helps diagnose connection issues

### Next Steps

- Explore each MCP's capabilities in depth
- Create custom prompts for your specific use cases
- Contribute back to the Regen MCP repositories with improvements
- Share your configurations with the Regen community

### Additional Resources

- [Claude Code MCP Documentation](https://docs.claude.com/en/docs/claude-code/mcp)
- [Model Context Protocol Specification](https://modelcontextprotocol.io/)
- [Regen Network MCP Repository](https://github.com/regen-network/mcp)
- [KOI MCP Repository](https://github.com/gaiaaiagent/regen-koi-mcp)
- [Regen Python MCP Repository](https://github.com/gaiaaiagent/regen-python-mcp)
- [Registry Review MCP Repository](https://github.com/gaiaaiagent/regen-registry-review-mcp)

---

## Sources

This tutorial was researched and compiled using the following sources:

- [Connect Claude Code to tools via MCP - Claude Code Docs](https://code.claude.com/docs/en/mcp)
- [Configuring MCP Tools in Claude Code - The Better Way - Scott Spence](https://scottspence.com/posts/configuring-mcp-tools-in-claude-code)
- [Add MCP Servers to Claude Code - Setup & Configuration Guide | MCPcat](https://mcpcat.io/guides/adding-an-mcp-server-to-claude-code/)
- [Claude Code Configuration Guide | ClaudeLog](https://claudelog.com/configuration/)
- [Set Up MCP with Claude Code | SailPoint Developer Community](https://developer.sailpoint.com/docs/extensibility/mcp/integrations/claude-code/)
- [Ultimate Guide to Claude MCP Servers & Setup | 2025](https://generect.com/blog/claude-mcp/)
- [Adding MCP Servers in Claude Code | Mehmet Baykar](https://mehmetbaykar.com/posts/adding-mcp-servers-in-claude-code/)
- [Claude Code MCP Troubleshooting Guide: Common Issues & Expert Solutions | PixelNoir](https://pixelnoir.us/posts/claude-code-mcp-troubleshooting-guide-2025)
- [Claude Code Tips & Tricks: Setting Up MCP Servers](https://cloudartisan.com/posts/2025-04-12-adding-mcp-servers-claude-code/)
- [Claude Code MCP Complete Setup Guide: From Installation to Production Deployment 2025 | PixelNoir](https://pixelnoir.us/posts/claude-code-mcp-setup-guide-2025)
- [MCP Server Prompting: The Complete Guide For 2025 - Stainless MCP Portal](https://www.stainless.com/mcp/mcp-server-prompting-the-complete-guide-for-2025)
- [How to test MCP servers effectively (6 best practices)](https://www.merge.dev/blog/mcp-server-testing)
- [Troubleshooting Claude Code: Why MCP Prompts Fail & How to Fix](https://www.arsturn.com/blog/why-is-claude-ignoring-your-mcp-prompts-a-troubleshooting-guide)
