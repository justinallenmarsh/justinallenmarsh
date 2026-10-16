# One command-line interface for people and automation

[TangoTube CLI](https://github.com/justinallenmarsh/tangotube-cli) is a Go interface to the TangoTube catalogue and personal library. A dancer can use it in a terminal; a script or coding agent can use the same capabilities programmatically.

## Different consumers, explicit contracts

A person searching for a performance benefits from readable results and links. A script needs a stable structure, predictable errors, and no unexpected interactive prompts. The CLI writes readable output at a terminal and JSON when piped. Agent mode explicitly requests structured output and avoids prompts or opening a browser.

The public documentation defines the JSON envelope and exit codes. These are part of the interface: automation should not need to parse a table intended for a person or infer success from a friendly sentence.

## Authentication follows the operation

Public search requires no account. Actions on a personal library, such as likes and playlists, require login. This makes the first useful command available before account setup while keeping personal operations authenticated.

The CLI also exposes an MCP interface. Keeping its tool behavior aligned with the commands matters because a capability should have consistent meaning across both entry points. The repository includes MCP parity tests alongside command tests.

## Examples that lead to useful work

The getting-started path begins with a search rather than configuration. The documentation then moves from finding a performance to inspecting it, creating a practice clip, and saving it to a library. A diagnostic command, `tt doctor`, checks the installation, connection, sign-in, and coding-agent setup.

The terminal animation is optional. It is a product detail; structured command results remain the integration contract.

## Evidence

- [CLI contract](https://github.com/justinallenmarsh/tangotube-cli/blob/cd2ead3fcdc6b3794d7c6d729895087d13410411/docs/cli.md).
- [Agent and MCP documentation](https://github.com/justinallenmarsh/tangotube-cli/blob/cd2ead3fcdc6b3794d7c6d729895087d13410411/docs/agents.md).
- [Output tests](https://github.com/justinallenmarsh/tangotube-cli/blob/cd2ead3fcdc6b3794d7c6d729895087d13410411/internal/output/output_test.go).
- [MCP parity tests](https://github.com/justinallenmarsh/tangotube-cli/blob/cd2ead3fcdc6b3794d7c6d729895087d13410411/internal/commands/mcp_parity_test.go).
- [End-to-end tests](https://github.com/justinallenmarsh/tangotube-cli/tree/cd2ead3fcdc6b3794d7c6d729895087d13410411/e2e).
