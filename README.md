# MCP Golang

A Model Context Protocol (MCP) server that provides Go language tools for LLMs to analyze, test, and format Go code.

**Features:**
- Full set of Go code analysis tools (`go vet`, `go test`, `go fmt`, `golint`, `deadcode`, `go mod tidy`)
- TypeScript implementation with strict type checking
- Comprehensive error handling and validation
- Tool output passed directly to LLMs

## 🚀 Getting Started

- **Setup & Installation:** See [HUMANS.md](HUMANS.md)
- **Development & Constraints:** See [AGENTS.md](AGENTS.md)
- **Security & Reporting:** See [SECURITY.md](SECURITY.md)
- **Contributing:** See [CONTRIBUTING.md](CONTRIBUTING.md)
- **Changes:** See [CHANGELOG.md](CHANGELOG.md)

## Available Go Tools

- `go_analyze` — Comprehensive code analysis using golangci-lint (configurable severity, auto-fix)
- `go_fix` — Code cleanup: runs `go mod tidy`, `goimports`, and `gofumpt` in sequence
- `go_test` — Run Go tests with optional coverage reports, race detection, and benchmarks

All tools require an absolute `wd` (working directory) path parameter.

## License

MIT
