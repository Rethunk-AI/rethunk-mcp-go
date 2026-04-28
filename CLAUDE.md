# Claude Code entrypoint

Go language tools for code analysis via MCP. See [AGENTS.md](AGENTS.md) for full agent onboarding.

## Quick Setup

```bash
go build -o build/mcp-go .
go test ./...
go vet ./...
```

## Development Workflow

- **MCP first:** Use MCP git tools
- **Commit early:** Logical chunks after each change
- **Tests:** `go test ./...` validates tool implementations
- **Linting:** `go vet ./...` before committing

## Key Files

- `src/tools/goTools.ts` — Go CLI tool wrappers
- `src/tools/noteTools.ts` — Example tools
- `cmd/example/` — Test Go project

See [AGENTS.md](AGENTS.md) for critical constraints on tool wrappers and command execution.

---

**Last updated:** 2026-04-27
