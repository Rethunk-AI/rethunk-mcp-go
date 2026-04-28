# Setup & Operations

User-facing setup, installation, and configuration guides.

## Prerequisites

- [Bun](https://bun.sh/) 1.3 or later (install and scripts)
- Node.js 20.12 or later (LTS recommended)
- Go 1.18 or later
- The following Go tools installed:
  - `golint`: `go install golang.org/x/lint/golint@latest`
  - `deadcode`: `go install github.com/remyoudompheng/go-misc/deadcode@latest`

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/Rethunk-AI/rethunk-mcp-go.git
   cd rethunk-mcp-go
   ```

2. Install dependencies:
   ```bash
   bun install
   ```

3. Build and run the server:
   ```bash
   bun run build
   bun run start
   ```

## Development

- Watch mode (TypeScript compiler): `bun run dev`
- Lint and format: `bun run lint`
- Fix linting issues: `bun run lint:fix`
- Run tests: `bun run test`

## Testing with MCP Inspector

For standalone testing, use the MCP Inspector tool:

```bash
bun run inspector
```

This opens an interactive session where you can test your MCP tools.

## Using with Cursor or Claude Desktop

To integrate this MCP server with Cursor or Claude Desktop, add this configuration to your MCP settings:

```json
{
  "mcpServers": {
    "mcp-golang": {
      "command": "node",
      "args": ["/path/to/rethunk-mcp-go/build/index.js"],
      "enabled": true
    }
  }
}
```

Replace `/path/to/rethunk-mcp-go` with your actual installation path.

Available tools in Cursor/Claude Desktop:
- `mcp_go_find_dead_code`
- `mcp_go_vet`
- `mcp_go_format`
- `mcp_go_lint`
- `mcp_go_test`
- `mcp_go_mod_tidy`

---

See [AGENTS.md](AGENTS.md) for developer onboarding and constraints on command execution.
