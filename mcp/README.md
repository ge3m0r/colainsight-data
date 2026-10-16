# COLA Insight MCP server

COLA Insight provides a public, read-only Model Context Protocol server for source-linked Social Security COLA data and educational calculations.

## Connect

Use this remote Streamable HTTP endpoint:

```text
https://www.colainsight.com/mcp
```

No account or API key is required. A common client configuration shape is:

```json
{
  "mcpServers": {
    "cola-insight": {
      "url": "https://www.colainsight.com/mcp"
    }
  }
}
```

Client field names vary. Follow the current documentation for the client you use.

## Read-only tools

| Tool | Purpose |
|---|---|
| `get_current_cola` | Returns the latest tracked 2027 COLA status, rate, CPI-W observations, timestamp, and source links. |
| `calculate_benefit_change` | Estimates monthly and annual benefit changes from a current monthly benefit amount. |
| `get_cola_history` | Returns preserved forecast, formula-derived, and official snapshots in reverse chronological order. |
| `get_cola_sources` | Returns primary government sources and COLA Insight documentation links. |

The server also exposes the current machine-readable record as an MCP resource.

## Data and privacy boundaries

- The server does not provide any write, refresh, account, or payment capability.
- Do not send a name, Social Security number, health information, or other sensitive personal data.
- Benefit calculations are educational estimates. SSA calculation and rounding rules determine actual payments.
- `forecast`, `computed`, and `official` are different statuses and must not be presented as interchangeable.
- The endpoint is limited to 60 requests per IP address per minute. Cache results and avoid unnecessary polling.

## Verification and versioning

- Human-readable documentation: https://www.colainsight.com/mcp-server
- Official Registry record: https://registry.modelcontextprotocol.io/v0/servers/io.github.ge3m0r%2Fcola-insight/versions/1.0.1
- Runtime endpoint: https://www.colainsight.com/mcp
- Current metadata: [`server.json`](../server.json)

The production Cloudflare Worker implementation remains private. This repository publishes the connection metadata, data contract, reusable datasets, methodology, and documentation needed to inspect and cite the service without implying that the deployment source is open source.
