# Claude Code MCP Setup

# Connecting The Regen MCPs

1. Create a working directory:

```bash
mkdir regen-mcps
cd regen-mcps

```

1. Clone the MCP repos

```bash
mkdir mcps
git clone <https://github.com/regen-network/mcp.git> mcps/mcp
git clone <https://github.com/gaiaaiagent/regen-koi-mcp.git> mcps/regen-koi-mcp
git clone <https://github.com/gaiaaiagent/regen-python-mcp.git> mcps/regen-python-mcp

```

1. Build the MCP servers

```bash
# Build regen mcp
cd mcps/mcp
npm install
npm run build

# Build regen-koi-mcp
cd ../regen-koi-mcp
npm install
npm run build

# Return to project root
cd ../..

```

1. Enable MCPs in `.claude/settings.json`

```bash
mkdir -p .claude
cat > .claude/settings.json << 'EOF'
{
  "enableAllProjectMcpServers": true
}
EOF

```

1. Add MCP configuration to `.mcp.json`

From your `regen-mcps` directory, run:

```bash
cat > .mcp.json << EOF
{
  "mcpServers": {
    "regen-koi": {
      "command": "node",
      "args": ["$(pwd)/mcps/regen-koi-mcp/dist/index.js"],
      "env": {
        "KOI_API_ENDPOINT": "<https://regen.gaiaai.xyz/api/koi>",
        "JENA_ENDPOINT": "<https://regen.gaiaai.xyz/api/koi/fuseki/koi/sparql>"
      }
    },
    "regen-network": {
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
      }
    },
    "regen": {
      "command": "node",
      "args": ["$(pwd)/mcps/mcp/server/dist/index.js"],
      "env": {
        "NODE_ENV": "production"
      },
      "description": "Regen Network MCP Server - Access to Regen Ledger blockchain data"
    }
  }
}
EOF

```

Note: The `$(pwd)` will expand to your current working directory, creating absolute paths specific to your system.

1. Start Claude Code

```bash
claude
> /mcp

```

The MCP servers should now be available.

# Connecting The Regen MCPs (Including Registry Review)

1. Create a working directory:

```bash
mkdir regen-mcps
cd regen-mcps

```

1. Clone the MCP repos

```bash
mkdir mcps
git clone https://github.com/regen-network/mcp.git mcps/mcp
git clone https://github.com/gaiaaiagent/regen-koi-mcp.git> mcps/regen-koi-mcp
git clone https://github.com/gaiaaiagent/regen-python-mcp.git mcps/regen-python-mcp
git clone https://github.com/gaiaaiagent/regen-registry-review-mcp.git mcps/regen-registry-review-mcp

```

1. Build the MCP servers

```bash
# Build regen mcp
cd mcps/mcp
npm install
npm run build

# Build regen-koi-mcp
cd ../regen-koi-mcp
npm install
npm run build

# Setup regen-registry-review-mcp
cd ../regen-registry-review-mcp
uv sync
cp .env.example .env
# Edit .env to add your REGISTRY_REVIEW_ANTHROPIC_API_KEY

# Return to project root
cd ../..

```

1. Enable MCPs in `.claude/settings.json`

```bash
mkdir -p .claude
cat > .claude/settings.json << 'EOF'
{
  "enableAllProjectMcpServers": true
}
EOF

```

1. Add MCP configuration to `.mcp.json`

From your `regen-mcps` directory, run:

```bash
cat > .mcp.json << EOF
{
  "mcpServers": {
    "regen-koi": {
      "command": "node",
      "args": ["$(pwd)/mcps/regen-koi-mcp/dist/index.js"],
      "env": {
        "KOI_API_ENDPOINT": "<https://regen.gaiaai.xyz/api/koi>",
        "JENA_ENDPOINT": "<https://regen.gaiaai.xyz/api/koi/fuseki/koi/sparql>"
      }
    },
    "regen-network": {
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
      }
    },
    "regen": {
      "command": "node",
      "args": ["$(pwd)/mcps/mcp/server/dist/index.js"],
      "env": {
        "NODE_ENV": "production"
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

Note: The `$(pwd)` will expand to your current working directory, creating absolute paths specific to your system.

1. Start Claude Code

```bash
claude
> /mcp

```

The MCP servers should now be available.
