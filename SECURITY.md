# Security Policy

## Reporting Security Vulnerabilities

**DO NOT** open a public GitHub issue for security vulnerabilities. Instead, please report them responsibly to:

**Email:** security@rethunk.tech  
**Response SLA:** We aim to respond to security reports within 24 hours.

When reporting a vulnerability, please include:
- Description of the vulnerability
- Affected component(s) and version(s)
- Steps to reproduce (if applicable)
- Potential impact
- Suggested fix (optional)

## Scope & Risk Profile

`rethunk-mcp-go` is a Model Context Protocol (MCP) server that executes Go language tools for code analysis. It has elevated security considerations due to command execution.

### Command Execution Risk
- **Critical:** This server executes Go CLI commands (`go vet`, `go fmt`, `go test`, `golint`, etc.) with user-supplied parameters
- Active vulnerability: #106 documents command injection via unsanitized `workingDir` parameter
- All tool inputs must be rigorously validated to prevent shell escape sequences
- Output from Go tools is passed directly to LLMs—malformed output could trigger LLM injection attacks

### Tool Input Validation
- **Required:** All file paths and command arguments must be validated and sanitized
- **Path traversal:** Restrict tool execution to intended project directories
- **Shell injection:** Never pass user input directly to shell commands; use safe escaping or argument arrays
- **Symbolic links:** Resolve and validate file paths to prevent directory escape

### MCP Server Security
- MCP allows remote tool invocation from Claude Code and other MCP clients
- Validate all tool invocations before executing Go commands
- Implement rate limiting to prevent abuse of compute-intensive tools (`go test`)
- Log all tool executions for audit trails

### Dependency Management
- Go runtime security updates must be monitored
- Node.js/TypeScript dependencies audited via `bun audit`
- Keep Go tools (`golint`, `deadcode`, etc.) up-to-date for security patches

## Security Practices

### Input Sanitization
- All file paths: validate against `.` (current directory) to prevent traversal
- Working directory: must be within project root, no parent directory access
- Tool arguments: use safe escaping (e.g., shell-escape library or argument arrays)
- Regular expressions: limit complexity to prevent ReDoS attacks

### Testing
- Fuzzing tests for command execution paths
- Path traversal test cases (e.g., `../../../etc/passwd`)
- Shell injection test cases (e.g., `; rm -rf /`, backticks, `$()`)
- Review test output for false positives in linting/formatting results

### Deployment
- Run MCP server with minimal privileges
- Restrict filesystem access to project directories only
- Use container/sandbox isolation for untrusted code analysis
- Monitor resource usage (CPU, memory) to detect abuse

## Supported Versions

Only the latest release receives security updates.

| Version | Supported |
|---------|-----------|
| Latest  | ✅ Yes    |
| Older   | ⚠️ Limited|

Please upgrade to the latest version for security patches.

## Known Vulnerabilities

### Active (Unfixed)
- **#106:** Command injection via unsanitized `workingDir` in `executeGoCommand` (Windows shell path)
  - Status: Under investigation
  - Workaround: Validate `workingDir` input before passing to tools
  - Patch ETA: TBD

## Third-Party Security

### Go Tools
- Executables: `go`, `golint`, `deadcode` (external dependencies, not packaged)
- Verify tool versions match official Go releases
- Monitor upstream for security advisories

### Node.js Dependencies
- Primary: MCP SDK, TypeScript, Bun build tools
- Run `bun audit` regularly; address critical and high-severity vulnerabilities

## Testing & Validation

- Test MCP server with malicious input before production deployment
- Validate path sanitization with edge cases (relative paths, symlinks, null bytes)
- Test shell injection payloads to confirm escaping works
- Verify output from Go tools does not contain exploitable patterns

## Incident Response

If a security vulnerability is discovered:

1. **Report immediately** to security@rethunk.tech (do not disclose publicly)
2. **Include reproduction steps** and affected version(s)
3. **Allow 24-48 hours** for initial response and triage
4. **Coordinate disclosure** timeline if patch is required
5. **Credit will be given** to the reporter (if desired)

## Contact

- **Security Issues:** security@rethunk.tech
- **General Support:** support@rethunk.tech
- **Website:** https://rethunk.tech

---

**Last updated:** 2026-04-27
