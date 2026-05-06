# Project Setup — Reference Configs

This folder contains reference configurations for the trading platform projects. Other projects can pull these files to set up their local environment with the correct MCP servers, steering rules, and agent instructions.

## Contents

| File | Purpose |
|------|---------|
| [[Projects/project-setup/kiro-mcp-user-level\|kiro-mcp-user-level]] | User-level Kiro MCP config (`~/.kiro/settings/mcp.json`) — all available MCP servers |
| [[Projects/project-setup/aws-dev-workspace-mcp\|aws-dev-workspace-mcp]] | Workspace-level MCP config for the AWS deployment framework project |
| [[Projects/project-setup/aws-dev-claude-md\|aws-dev-claude-md]] | CLAUDE.md for the AWS deployment framework project |
| [[Projects/project-setup/aws-dev-steering\|aws-dev-steering]] | Steering file for the AWS deployment framework |

## How to use

When setting up a new project that needs AWS deployment support:

1. Copy the relevant MCP servers from the user-level config
2. Reference the AWS steering doc for naming/tagging conventions
3. Use the CLAUDE.md as a template for project-specific agent instructions
4. Add the `trading_knowledgebase` MCP server to access tickets and docs

## MCP Servers by Category

### Always needed (all projects)
- `trading_knowledgebase` — Obsidian vault access
- `fetch` — URL fetching

### AWS projects
- `awslabs.aws-api-mcp-server_default` — AWS CLI via MCP
- `awslabs.core-mcp-server` — AWS documentation search
- `aws-knowledge-mcp-server` — AWS knowledge base

### Trading-specific
- `binance-data-collector` — Market data MCP
- `binance-position-tools` — Position management MCP
- `tradingview-mcp` — TradingView analysis
- `coingecko-scanner` — CoinGecko FTP/Long scanning
