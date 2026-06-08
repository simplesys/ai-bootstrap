# CodeGraph

[Repository URL](https://github.com/colbymchenry/codegraph)

Description: an MCP for indexing files as a graph. After the tool is started, the AI agent spends fewer tokens searching for file information. The file index is stored locally in the project, which also speeds up search for the AI itself.

Global installation:

```bash
npm install -g @colbymchenry/codegraph
codegraph install --target=codex --location=global --yes
# Or
codegraph install --target=claude --location=global --yes
```

Project MCP initialization. Run the command in the project directory:

```bash
codegraph init -i
```

Then add [the following prompt](../examples/codeGraph/agents.md) to `AGENTS.md`.

Restart Codex and run `/mcp` in the new session: the CodeGraph server should be displayed.
Answer Always allow to all questions.

To update the index, use the command below, but when working with an agent this happens automatically and is usually not required.

```bash
codegraph sync
```

For the final Codex check after restarting it, you can send the following prompt:

```
MCP CodeGraph has been configured for Codex in this project. Check that you are now working with this MCP.
```

The response will include confirmation. If not, you can ask the AI to diagnose what is missing to complete the setup.
