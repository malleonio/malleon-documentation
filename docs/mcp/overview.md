# Malleon MCP Server

The [MCP (Model Context Protocol)](https://modelcontextprotocol.io) server [`@malleon/mcp`](https://www.npmjs.com/package/@malleon/mcp) connects AI coding assistants (Cursor, Claude, and others) to Malleon Replay. Agents can list errors, inspect replays, upload reference builds, and verify fixes with the headless replay client.

**Package:** [npmjs.com/package/@malleon/mcp](https://www.npmjs.com/package/@malleon/mcp)

## Prerequisites

- **Node.js 18+**
- **Malleon account** with App ID and a JWT from the dashboard (**App Settings**)
- **[Malleon Replay Client](https://malleon.io/#/replay-client-download)** running locally on the default port (`9287`) if you use verification workflows (`verify_fix`)

## Run with npx

```bash
npx -y @malleon/mcp
```

Set `MALLEON_JWT` and `MALLEON_APP_ID` in the environment (see below).

## Cursor

Add to your project’s `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "malleon": {
      "command": "npx",
      "args": ["-y", "@malleon/mcp"],
      "env": {
        "MALLEON_JWT": "your-jwt-here",
        "MALLEON_APP_ID": "your-app-id-here"
      }
    }
  }
}
```

## Environment variables

| Variable | Required | Default | Description |
| -------- | -------- | ------- | ----------- |
| `MALLEON_JWT` | Yes | — | JWT from Malleon → App Settings |
| `MALLEON_APP_ID` | Yes | — | App ID from the dashboard |
| `MALLEON_SERVER_URL` | No | `https://malleon.io` | Replay server base URL |
| `MALLEON_TEST_RUNNER_URL` | No | `http://localhost:9287` | Local replay client URL |

## What agents can do

- **`find_healthy_sessions`** — Recent sessions with no errors and decent activity (regression-test candidates)
- **`list_errors`** — Recent or frequent errors with replay IDs
- **`diagnose_replay`** — Stack traces, console logs, DOM context, and request summaries for a replay
- **`create_reference_replay`** — Upload a build output directory as a reference replay for comparison
- **`verify_fix`** — Replay the original session against new code and report pass/fail

For full parameter tables, Claude Desktop / Claude Code examples, and step-by-step workflows, see the [malleon-mcp README](https://github.com/malleon-io/malleon-mcp/blob/main/README.md) on GitHub.
