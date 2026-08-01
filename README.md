# agent-web-search-mcp

Standalone [Model Context Protocol](https://modelcontextprotocol.io) (MCP) server for the
[**agent-web-search**](https://github.com/blueewhitee/agent-web-search) API.

A thin stdio wrapper — it just calls the API over HTTP and formats results for any
MCP-compatible agent (Claude Desktop, Cursor, Pi, etc.).

> This package is a **client of** the `agent-web-search` engine, not the engine itself.
> You need a running instance of the engine (see below) before the MCP can do anything.

---

## Install

```bash
uv tool install git+https://github.com/blueewhitee/agent-web-search-mcp
```

## Configure your MCP client

Add this to your MCP config (e.g. `~/.pi/agent/mcp.json` for Pi,
`claude_desktop_config.json` for Claude Desktop):

```json
{
  "mcpServers": {
    "agent-web-search": {
      "command": "agent-web-search-mcp",
      "env": {
        "AGENT_WEB_SEARCH_API_URL": "http://localhost:8000"
      }
    }
  }
}
```

`AGENT_WEB_SEARCH_API_URL` defaults to `http://localhost:8000` — set it to wherever your
engine is reachable.

## What you get

A single tool, `web_search`, that:
- routes the query to the engine's intent detector (code / news / general),
- fetches + extracts + ranks results,
- returns ranked chunks with scores and source URLs.

## Requirements

- A running `agent-web-search` engine (the FastAPI service from the
  [agent-web-search](https://github.com/blueewhitee/agent-web-search) repo).
  Easiest path: clone that repo and `docker compose up`.
- Python ≥ 3.12.

## Development

```bash
git clone https://github.com/blueewhitee/agent-web-search-mcp
cd agent-web-search-mcp
uv tool install --editable .
```

The `agent-web-search-mcp` command will then reflect local changes on restart.

## License

MIT (same as the engine).
