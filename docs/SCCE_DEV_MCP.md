# SCCE Developer MCP

Local developer MCP server for bounded repository and trace inspection.

## Build

```powershell
pnpm install --frozen-lockfile
pnpm mcp:build
```

## Start

- `pnpm mcp:start`
- `pnpm mcp:dev` for watch mode

## Codex registration

Use an absolute script path for a global registration so the server can start when
Codex is opened from another directory:

```powershell
codex mcp add scce-dev -- node <absolute-repository-path>\tools\scce-dev-mcp\dist\index.js
codex mcp list
```

Equivalent `config.toml`:

```toml
[mcp_servers.scce-dev]
command = "node"
args = ["<absolute-repository-path>/tools/scce-dev-mcp/dist/index.js"]
cwd = "<absolute-repository-path>"
```

Restart the Codex client after changing MCP configuration. The server uses standard
MCP stdio and treats its configured working directory as the repository root.

## Tools

- `repo_shape`, `repo_files`, `repo_search`, `repo_symbol`, `repo_callsites`
- `repo_routes`, `repo_deps`, `repo_deadcode`
- `git_changed`, `git_diff_summary`
- `test_run`, `test_failures`
- `pg_schema`, `pg_explain`
- `scce_trace_list`, `scce_trace_read`, `scce_answer_trace`

## Scope

- Results are bounded and structured for low-token diagnosis.
- The server is read/diagnostic oriented and does not expose arbitrary shell execution.
- MCP success does not substitute for the validation command appropriate to a change.
