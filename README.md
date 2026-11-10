# Mokxi MCP server

[![Mokxi MCP connector – tool definition quality and endpoint health on Glama](https://glama.ai/mcp/connectors/com.mokxi/mokxi/badges/score.svg)](https://glama.ai/mcp/connectors/com.mokxi/mokxi)

Ask your AI assistant for a circuit and get one that works.

Mokxi's remote MCP server lets Claude, ChatGPT, Cursor, VS Code and other MCP clients:
- pick a board and parts from Mokxi's catalog
- wire them and write the sketch
- check the circuit the way the Mokxi editor does
- hand back a link that opens and runs the project in the browser simulator at [mokxi.com](https://mokxi.com)

Boards: Arduino (Uno, Nano, Mega and more), ESP32 family, Raspberry Pi Pico and others.

- **Server URL:** `https://mokxi.com/mcp`
- **Transport:** Streamable HTTP
- **Auth:** OAuth (sign in to Mokxi when your client asks), or an API token sent as `Authorization: Bearer mkx_...`. Create a token at mokxi.com, Settings, API tokens.
- **Registry:** `com.mokxi/mcp` in the official MCP Registry

## Tools

| Tool | What it does |
| --- | --- |
| `get_project_format` | Describes the project format a client writes |
| `list_boards` | Lists the boards Mokxi simulates |
| `search_parts` | Searches the parts catalog |
| `get_part` | Gives a part's pins and details |
| `validate_project` | Checks a project the way the editor does |
| `create_project` | Returns a link that opens and runs the project in Mokxi |

## Install

**Claude (claude.ai and desktop):** Settings, Connectors, Add custom connector, URL `https://mokxi.com/mcp`, then sign in to Mokxi.

**Claude Code:**
```bash
claude mcp add --transport http mokxi https://mokxi.com/mcp
```

**Cursor** (`~/.cursor/mcp.json`):
```json
{ "mcpServers": { "mokxi": { "url": "https://mokxi.com/mcp", "headers": { "Authorization": "Bearer mkx_YOUR_TOKEN" } } } }
```

**VS Code** (`.vscode/mcp.json`):
```json
{ "servers": { "mokxi": { "type": "http", "url": "https://mokxi.com/mcp", "headers": { "Authorization": "Bearer mkx_YOUR_TOKEN" } } } }
```

## Try it

> Build me an ESP32 that reads a DHT22 and shows the temperature on an SSD1306 OLED, then give me the Mokxi link.

## About

Mokxi is a browser simulator for Arduino, ESP32 and Pico. You wire real parts, write real code and press Run. The server is hosted by Mokxi, and this repository holds its listing and setup docs. Help: [mokxi.com/help](https://mokxi.com/help).
