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

- `go_find_dead_code` — Find unused code in Go projects
- `go_vet` — Run Go's static analyzer
- `go_format` — Format Go code
- `go_lint` — Run Go linting
- `go_test` — Run Go tests
- `go_mod_tidy` — Clean up Go module dependencies

## License

MIT
