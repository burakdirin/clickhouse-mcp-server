# Clickhouse MCP server
[![LightNow capabilities](https://lightnow.ai/badge/io.github.burakdirin/clickhouse-mcp-server)](https://lightnow.ai/servers/io.github.burakdirin/clickhouse-mcp-server)

A Clickhouse database MCP server project.

## Installation

You can install the package using `uv`:

```bash
uv pip install clickhouse-mcp-server
```

Or using `pip`:

```bash
pip install clickhouse-mcp-server
```

## Components

### Tools

The server provides two tools:
- `connect_database`: Connects to a specific Clickhouse database
  - `database` parameter: Name of the database to connect to (string)
  - Returns a confirmation message when connection is successful

- `execute_query`: Executes Clickhouse queries
  - `query` parameter: SQL query/queries to execute (string)
  - Returns query results in JSON format
  - Multiple queries can be sent separated by semicolons

## Configuration

The server uses the following environment variables:

- `CLICKHOUSE_HOST`: Clickhouse server address (default: "localhost")
- `CLICKHOUSE_USER`: Clickhouse username (default: "root") 
- `CLICKHOUSE_PASSWORD`: Clickhouse password (default: "")
- `CLICKHOUSE_DATABASE`: Initial database (optional)
- `CLICKHOUSE_READONLY`: Read-only mode (set to 1/true to enable, default: false)

## Quickstart

### Installation

#### Claude Desktop

MacOS: `~/Library/Application\ Support/Claude/claude_desktop_config.json`

Windows: `%APPDATA%/Claude/claude_desktop_config.json`

<details>
  <summary>Development/Unpublished Server Configuration</summary>

```json
{
  "mcpServers": {
    "clickhouse-mcp-server": {
      "command": "uv",
      "args": [
        "--directory",
        "/Users/burakdirin/Projects/clickhouse-mcp-server",
        "run",
        "clickhouse-mcp-server"
      ],
      "env": {
        "CLICKHOUSE_HOST": "localhost",
        "CLICKHOUSE_USER": "root",
        "CLICKHOUSE_PASSWORD": "password",
        "CLICKHOUSE_DATABASE": "[optional]",
        "CLICKHOUSE_READONLY": "true"
      }
    }
  }
}
```
</details>

<details>
  <summary>Published Server Configuration</summary>

```json
{
  "mcpServers": {
    "clickhouse-mcp-server": {
      "command": "uvx",
      "args": [
        "clickhouse-mcp-server"
      ],
      "env": {
        "CLICKHOUSE_HOST": "localhost",
        "CLICKHOUSE_USER": "root",
        "CLICKHOUSE_PASSWORD": "password",
        "CLICKHOUSE_DATABASE": "[optional]",
        "CLICKHOUSE_READONLY": "true"
      }
    }
  }
}
```
</details>

### Installing via Smithery

To install Clickhouse Database Integration Server for Claude Desktop automatically via [Smithery](https://smithery.ai/server/@burakdirin/clickhouse-mcp-server):

```bash
npx -y @smithery/cli install @burakdirin/clickhouse-mcp-server --client claude
```

## Development

### Building and Publishing

To prepare the package for distribution:

1. Sync dependencies and update lockfile:
```bash
uv sync
```

2. Build package distributions:
```bash
uv build
```

This will create source and wheel distributions in the `dist/` directory.

3. Publish to PyPI:
```bash
uv publish
```

Note: You'll need to set PyPI credentials via environment variables or command flags:
- Token: `--token` or `UV_PUBLISH_TOKEN`
- Or username/password: `--username`/`UV_PUBLISH_USERNAME` and `--password`/`UV_PUBLISH_PASSWORD`

### Debugging

Since MCP servers run over stdio, debugging can be challenging. For the best debugging
experience, we strongly recommend using the [MCP Inspector](https://github.com/modelcontextprotocol/inspector).

You can launch the MCP Inspector via [`npm`](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) with this command:

```bash
npx @modelcontextprotocol/inspector uv --directory /Users/burakdirin/Projects/clickhouse-mcp-server run clickhouse-mcp-server
```

Upon launching, the Inspector will display a URL that you can access in your browser to begin debugging.
