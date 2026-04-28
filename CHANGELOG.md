# Changelog

All notable changes to this project are recorded here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [Unreleased]

### Added
- Governance files: SECURITY.md, AGENTS.md, CHANGELOG.md
- Security policy with responsible disclosure process
- AI agent development constraints for command execution safety
- Known vulnerability tracking (issue #106: command injection via unsanitized workingDir)

---

## [1.0.0] - 2025 Release

### Added
- MCP server implementation in TypeScript for Go language tools
- Go code analysis tools:
  - `go_find_dead_code`: Identify unused code in Go projects
  - `go_vet`: Run Go's static analyzer for suspicious code patterns
  - `go_format`: Format Go code according to standard style
  - `go_lint`: Run Go linting with golint
  - `go_test`: Execute Go tests and report results
  - `go_mod_tidy`: Clean up and organize Go module dependencies
- Example note-taking tools for MCP tool development patterns
- Comprehensive TypeScript type definitions for tool inputs and outputs
- Custom error handling with structured MCP error responses
- MCP Inspector integration for testing and debugging
- Full test suite with Vitest and coverage reporting
- CONTRIBUTING.md with developer guidelines
- CODE_OF_CONDUCT.md for community standards

### Features
- Strict TypeScript mode with explicit return types
- Output from Go tools passed directly to LLMs for analysis
- Test project (`cmd/example`) for validating tool functionality
- Biome linting and formatting for code quality
- Watch mode development with hot reload (bun run dev)
- Cross-platform support (Node.js 20.12+, Bun 1.3+)

## Version History

Documentation versioning aligns with software releases.

### Supported Versions

| Version | Release Date | Support Status | Notes |
|---------|--------------|---|---|
| 1.0.0   | 2025        | Active | Initial release with Go tools and MCP integration |

## Security & Governance

- See [SECURITY.md](SECURITY.md) for vulnerability reporting and security practices
- See [AGENTS.md](AGENTS.md) for AI agent development constraints
- Known issue: Command injection vulnerability via unsanitized `workingDir` (#106) — see SECURITY.md for details

---

**Last updated:** 2026-04-27
