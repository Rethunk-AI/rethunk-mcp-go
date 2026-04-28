# AGENTS — rethunk-mcp-go

MCP server for Go language analysis: static analysis, testing, linting, formatting via `go vet`, `go test`, `golint`, `go fmt`, and related tools.

## Repository Purpose

- **Users:** LLMs (Claude Code, ChatGPT) analyzing and improving Go codebases
- **AI Agents:** Tool orchestration and error handling for Go toolchain commands
- **Maintainers:** Go/TypeScript compatibility, security patch management

## Contents

```
src/
├── tools/
│   ├── goTools.ts          Go CLI tool wrappers (vet, test, fmt, lint, mod)
│   └── noteTools.ts        Example note-taking tools
├── types/                  TypeScript interfaces for tool I/O
├── errors/                 Custom MCP error classes
└── index.ts                MCP server entrypoint

cmd/
└── example/                Go test project for tool validation

package.json               Bun build & npm/ts config
README.md                  User documentation
SECURITY.md                Vulnerability reporting & input validation
CONTRIBUTING.md            Developer guidelines
```

## Usage

```bash
bun install
bun run build              # Compile TypeScript → JavaScript
bun run start              # Start MCP server (stdio or HTTP)
bun run dev                # Watch mode for development
bun run test               # Run TypeScript tests
bun run lint               # Run Biome linter/formatter
```

## 🚨 CRITICAL AI CONSTRAINT

**Modifications to command execution paths MUST NOT be made autonomously by AI agents without human review.**

- ✅ **Agents MAY:** fix typos, update docs, improve error messages, refactor non-critical code
- ❌ **Agents MUST NOT:** modify `executeGoCommand`, argument parsing, path resolution, or shell escaping logic without explicit human approval

Reason: `executeGoCommand` directly invokes shell commands with user-supplied input. Unreviewed changes could:
- Introduce shell injection vulnerabilities
- Enable directory traversal attacks
- Expose sensitive file contents via Go tool output
- Allow arbitrary code execution on the server

All changes to command execution require:
1. GitHub pull request for visibility
2. Security review focusing on input validation and shell escaping
3. Explicit approval before merge
4. Test with malicious input payloads before deployment

AI agents that modify command execution without human approval should have their edits rejected immediately.

## Technology

- **Language:** TypeScript (compiled to JavaScript, runs on Node.js via Bun)
- **Runtime:** Node.js 20.12+ or Bun 1.3+
- **External Tools:** Go 1.18+, golint, deadcode, standard Go toolchain
- **MCP SDK:** @modelcontextprotocol/sdk (for tool definitions and transport)

## Design Rationale

- **Tool Wrappers:** Each Go CLI tool (`go vet`, `go test`, etc.) is wrapped as an MCP tool so LLMs can invoke it directly
- **Error Handling:** Tool stderr and non-zero exits are captured and formatted for LLM interpretation
- **No Shell Parsing:** Tool output is passed as-is to prevent LLM injection; edge cases documented

## Constraints

- **Go required:** Assumes Go 1.18+ is installed and `go` binary is in PATH
- **External tools required:** `golint`, `deadcode` must be installed separately
- **Relative paths only:** Tools operate on relative paths within project directory (no absolute paths)
- **No network access:** Tools assume local file-only access; no remote module loading

## Getting Help

- **Security issues:** See [SECURITY.md](SECURITY.md) for responsible disclosure
- **Command injection:** Issue #106 documents unsanitized path handling; see SECURITY.md for mitigation
- **Tool errors:** Check README for prerequisites and installation instructions
- **Agent onboarding:** This file documents what agents should know before making changes

---

**Last updated:** 2026-04-27
