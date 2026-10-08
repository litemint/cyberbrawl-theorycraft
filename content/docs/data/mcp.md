+++
title = "MCP for AI agents"
short = "MCP Server"
weight = 3
date = "2026-10-08"
tags = ["mcp", "api", "ai"]
ShowToc = false
+++

Source: [github.com/xbid-ai/cyberbrawl-mcp](https://github.com/xbid-ai/cyberbrawl-mcp)

Cyberbrawl has a [Model Context Protocol](https://modelcontextprotocol.io) server, so AI agents can read the market prices as a tool: Claude, Cursor, VS Code, LangChain or your own agent. It serves the same data as [Market Prices](/docs/data/api/#market-prices), sourced from the Stellar DEX, over stdio or HTTP.

![Claude asking for Cyberbrawl prices](https://raw.githubusercontent.com/xbid-ai/cyberbrawl-mcp/master/claude-mcp.gif)

## How to use it

```bash
git clone https://github.com/xbid-ai/cyberbrawl-mcp
cd cyberbrawl-mcp
npm install
```

For Claude (Desktop or Code), Cursor or VS Code, add the server to the MCP config file, stdio transport:

```json
{
  "mcpServers": {
    "cyberbrawl": {
      "command": "node",
      "args": ["path/to/cyberbrawl-mcp/index.js"],
      "env": { "MCP_STDIO": "1" }
    }
  }
}
```

Then just ask: *"What is the CREDIT ask price in XLM right now?"*

For anything else, `npm start` runs the HTTP transport on `http://localhost:3000/mcp` (`PORT` and `MCP_PATH` to change it):

```bash
curl -sS -X POST http://localhost:3000/mcp -H "Content-Type: application/json" -H "Accept: application/json, text/event-stream" --data '{ "jsonrpc":"2.0","id":"1","method":"tools/call","params":{"name":"get_prices","arguments":{"markets":["USDC","XLM"],"limit":100,"offset":0}} }'
```

## The tool

`get_prices` returns the quotes of the game assets, filtered by market.

| Argument | Values | Default |
|---|---|---|
| `markets` | `"ALL"`, one of `XLM`, `USDC`, `CREDIT`, `KALE`, or an array of them | `"ALL"` |
| `limit` | 0 to 1000 rows | 10 |
| `offset` | first row to return | 0 |

Each row is a [Market Prices](/docs/data/api/#market-prices) quote: `ask` is the best price to buy one unit now, `bid` the best price to sell one, each with the path of hops the trade goes through.

```json
{
  "timestamp": "2026-10-08T17:32:06.040Z",
  "markets": "XLM",
  "rows": [
    {
      "asset": { "code": "CREDIT", "issuer": "GBAKUWF2HTJ325PH6VATZQ3UNTK2AGTATR43U52WQCYJ25JNSCF5OFUN" },
      "market": { "code": "XLM", "issuer": "native" },
      "prices": {
        "ask": { "price": "0.0002214", "path": [ { "asset_type": "credit_alphanum4", "asset_code": "SGM", "asset_issuer": "GAPNO…" }, { "asset_type": "credit_alphanum12", "asset_code": "DasKapital", "asset_issuer": "GBJEI…" } ] },
        "bid": { "price": "0.0002226", "path": [ { "asset_type": "credit_alphanum12", "asset_code": "yUSDC", "asset_issuer": "GDGTV…" }, { "asset_type": "credit_alphanum4", "asset_code": "USDC", "asset_issuer": "GA5ZS…" } ] }
      },
      "updated": "2026-10-08T17:31:41.541Z"
    }
  ]
}
```

Prices are cached for 20 seconds (`CACHE_TTL` in ms). The server is MIT, experimental and provided as-is.
