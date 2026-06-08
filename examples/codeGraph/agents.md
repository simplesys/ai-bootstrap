## CodeGraph

1. When working with code, including searching files or code, analyzing any part of the project, or diagnosing errors, use MCP CodeGraph.

2. If the data appears stale, use `codegraph_status`. Do not run `codegraph sync` while a watcher is active.

3. Start code exploration with `codegraph_explore`.
Use `codegraph_search` only to search for a symbol name.
Use `codegraph_node` to retrieve the full body of a symbol.
Use `codegraph_callers` and `codegraph_callees` to analyze relationships in code.
Use `codegraph_impact` before refactoring.

4. Do not reopen files whose source code CodeGraph has already found, except when editing is required, when checking uncommitted changes, or when a stale-index warning was received. Use `rg`, `sed`, and direct file reads only for formats unsupported by the index, exact text search, or other cases where CodeGraph is not sufficient.
