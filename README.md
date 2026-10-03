# mcp-therapro

TheraPro MCP repository. Connects MCP clients (Claude Code, Claude Desktop, etc.) to the
TheraPro Freshdesk MCP server at `https://therapro.freshdesk.com/mcp`, using
[`mcp-remote`](https://www.npmjs.com/package/mcp-remote) as a stdio-to-HTTP bridge.

## Prerequisites

- Node.js 18+ (for `npx`)
- A Freshdesk API key for the `therapro` helpdesk

## Configuration

The API key is **never** stored in this repo. It's read from the `FRESHDESK_API_KEY`
environment variable.

### Claude Code

`.mcp.json` at the repo root is picked up automatically when you run `claude` in this
directory. Claude Code expands `${FRESHDESK_API_KEY}` from your environment:

```bash
export FRESHDESK_API_KEY='<API_KEY>'
claude
```

Run `/mcp` inside Claude Code to confirm `freshdesk-mcp` is connected.

### Claude Desktop

Copy the `freshdesk-mcp` entry from
[`config/claude_desktop_config.example.json`](config/claude_desktop_config.example.json)
into your `claude_desktop_config.json`, and replace `<API_KEY>` in the `env` block with
your key:

- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`

`mcp-remote` substitutes `${FRESHDESK_API_KEY}` in the header from that `env` block.
Restart Claude Desktop afterwards.

## Security

- Keep real keys out of git — `.env` is git-ignored; `.env.example` shows the shape.
- If a key is ever committed or shared, rotate it in Freshdesk (Profile settings → API key).
