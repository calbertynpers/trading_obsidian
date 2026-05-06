# Kiro MCP — User-Level Config

> `~/.kiro/settings/mcp.json`
> This is the global MCP config shared across all Kiro workspaces. Workspace-level configs override these.

```json
{
  "mcpServers": {
    "fetch": {
      "command": "/Users/clintalbertyn/.local/bin/uvx",
      "args": ["mcp-server-fetch"],
      "env": {},
      "disabled": false,
      "autoApprove": ["fetch"]
    },
    "coingecko-scanner": {
      "command": "/Users/clintalbertyn/Documents/repos/hummer_m1/.venv/bin/python3",
      "args": ["-m", "coingecko_scanner"],
      "env": {
        "COINGECKO_API_KEY": "<redacted>",
        "PYTHONPATH": "/Users/clintalbertyn/Documents/repos/hummer_m1/coingecko-scanner"
      },
      "disabled": true,
      "autoApprove": ["ftp_scan", "ftp_assess", "ftp_scan_status", "long_scan", "long_assess"]
    },
    "aws-knowledge-mcp-server": {
      "command": "uvx",
      "args": ["mcp-proxy", "--transport", "streamablehttp", "https://knowledge-mcp.global.api.aws"],
      "disabled": false,
      "autoApprove": ["aws___search_documentation", "aws___read_documentation"]
    },
    "awslabs.aws-api-mcp-server_default": {
      "command": "uvx",
      "args": ["awslabs.aws-api-mcp-server@latest"],
      "env": { "AWS_REGION": "us-east-1", "AWS_PROFILE": "default" },
      "disabled": false,
      "autoApprove": ["call_aws"]
    },
    "awslabs.aws-api-mcp-server_prod": {
      "command": "uvx",
      "args": ["awslabs.aws-api-mcp-server@latest"],
      "env": { "AWS_REGION": "us-east-1", "AWS_PROFILE": "prod" },
      "disabled": true,
      "autoApprove": ["call_aws"]
    },
    "awslabs.aws-api-mcp-server_staging": {
      "command": "uvx",
      "args": ["awslabs.aws-api-mcp-server@latest"],
      "env": { "AWS_REGION": "us-east-1", "AWS_PROFILE": "staging" },
      "disabled": true,
      "autoApprove": ["call_aws", "suggest_aws_commands"]
    },
    "awslabs.core-mcp-server": {
      "command": "uvx",
      "args": ["awslabs.core-mcp-server@latest"],
      "env": { "FASTMCP_LOG_LEVEL": "ERROR" },
      "disabled": true,
      "autoApprove": []
    },
    "awslabs.amazon-bedrock-agentcore-mcp-server": {
      "command": "uvx",
      "args": ["awslabs.amazon-bedrock-agentcore-mcp-server@latest"],
      "env": { "FASTMCP_LOG_LEVEL": "ERROR" },
      "disabled": true,
      "autoApprove": ["search_agentcore_docs", "fetch_agentcore_doc", "manage_agentcore_gateway"]
    },
    "trading_knowledgebase": {
      "command": "uvx",
      "args": ["--from", "obsidian-mcp-server", "obsidian-mcp"],
      "env": { "OBSIDIAN_VAULT_PATH": "/Users/clintalbertyn/Documents/obsidian/Trading_KnowledgeBase" },
      "autoApprove": ["obsidian_status", "obsidian_list", "obsidian_configure", "obsidian_write", "obsidian_read", "obsidian_append", "obsidian_search", "obsidian_daily"],
      "disabled": false
    },
    "tradingview-mcp": {
      "command": "uv",
      "args": ["tool", "run", "--from", "git+https://github.com/atilaahmettaner/tradingview-mcp.git", "tradingview-mcp"],
      "disabled": false,
      "autoApprove": ["coin_analysis", "volume_confirmation_analysis", "volume_breakout_scanner", "smart_volume_scanner", "multi_timeframe_analysis", "market_sentiment", "yahoo_price", "bollinger_scan", "top_gainers", "top_losers", "rating_filter", "financial_news", "market_snapshot", "combined_analysis", "multi_agent_analysis", "backtest_strategy"]
    },
    "binance-data-collector": {
      "command": "/Users/clintalbertyn/binance_data_service/.venv/bin/python",
      "args": ["-m", "binance_data_collector.mcp_server"],
      "cwd": "/Users/clintalbertyn/binance_data_service",
      "disabled": true,
      "autoApprove": ["get_snapshot", "get_history", "collector_status", "get_metrics"]
    },
    "binance-position-tools": {
      "command": "/Users/clintalbertyn/binance_data_service/.venv/bin/python",
      "args": ["-m", "binance_data_collector.position_mcp_server"],
      "cwd": "/Users/clintalbertyn/binance_data_service",
      "env": {
        "BINANCE_API_KEY": "<redacted>",
        "BINANCE_SECRET_KEY": "<redacted>"
      },
      "disabled": true,
      "autoApprove": ["get_positions", "get_trading_readiness", "set_leverage", "place_market_order", "place_limit_order", "place_stop_order", "get_open_orders", "cancel_all_orders", "cancel_order", "get_order_history", "get_income_history"]
    }
  }
}
```

## Notes

- API keys and secrets are redacted — pull from Secrets Manager or local env
- `disabled: true` servers are available but not active by default — enable per-workspace as needed
- The `AWS_REGION` defaults to `us-east-1` but trading platform resources are in `eu-north-1` — always specify `--region eu-north-1` in commands
