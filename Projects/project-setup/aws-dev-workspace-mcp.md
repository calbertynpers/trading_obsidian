# AWS Dev — Workspace MCP Config

> `.mcp.json` in the `aws_dev` workspace root
> This is the workspace-level MCP config for the AWS Deployment Framework project.

```json
{
  "mcpServers": {
    "trading_knowledge_base": {
      "command": "uvx",
      "args": ["--from", "obsidian-mcp-server", "obsidian-mcp"],
      "env": {
        "OBSIDIAN_VAULT_PATH": "/Users/clintalbertyn/Documents/obsidian/trading_knowledge_base"
      },
      "disabled": false,
      "autoApprove": [
        "obsidian_configure", "obsidian_list", "obsidian_search",
        "obsidian_daily", "obsidian_write", "obsidian_append",
        "obsidian_status", "obsidian_read"
      ]
    },
    "awslabs.core-mcp-server": {
      "command": "uvx",
      "args": ["awslabs.core-mcp-server@latest"],
      "env": { "FASTMCP_LOG_LEVEL": "ERROR" },
      "disabled": false,
      "autoApprove": []
    },
    "awslabs.aws-api-mcp-server_default": {
      "command": "uvx",
      "args": ["awslabs.aws-api-mcp-server@latest"],
      "env": { "AWS_REGION": "us-east-1", "AWS_PROFILE": "default" },
      "disabled": false,
      "autoApprove": ["call_aws", "suggest_aws_commands"]
    },
    "fetch": {
      "command": "uvx",
      "args": ["mcp-server-fetch"],
      "env": {},
      "disabled": false,
      "autoApprove": ["fetch"]
    }
  }
}
```

## When to use this config

Copy this to any workspace that needs:
- AWS infrastructure management (CloudFormation, EC2, RDS, Secrets Manager)
- Access to the trading knowledge base (tickets, service docs)
- URL fetching for documentation lookup

## Important

- `AWS_REGION` is set to `us-east-1` as the MCP default, but trading platform resources are in **`eu-north-1`**. Always specify `--region eu-north-1` in `call_aws` commands.
- The vault path uses lowercase `trading_knowledge_base` — ensure the path matches your local Obsidian vault location.
