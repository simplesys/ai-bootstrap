# Agent Instructions

## Communication

- The repository owner describes requirements in Russian.
- Respond in Russian unless the user asks for another language.
- Keep responses concise.

## Documentation

- **Always use the AI-agent documentation and project context from `ai-docs/`**.
- Treat the documentation in `lang/ru` as the source of truth for describing all repository documents.
- All descriptions at the project root must be in English.
- If files in `lang/ru` change, translate those changes into English and update the corresponding files at the project root.
- Project-local skills are described in `lang/ru/SKILLS.md`; the English version is stored in `SKILLS.md`. If a request matches a local skill or its short name such as `/update-docs`, use that procedure only within this repository.
- Additional AI instructions will be placed in `ai-docs/`. Before starting a project task, check all instructions in that directory.
- Additional project documents will be placed in `docs/`.

## Repository Structure

- Scripts for local installation and applying settings for the documented libraries and skills will be placed in `scripts/`.
- Example configuration files will be placed in `examples/`.
- Repository-level AI instructions must be stored in `AGENTS.md`. `CLAUDE.md` must remain a symbolic link to `AGENTS.md`.

## Development Rules

- Prefer small, focused changes that match the existing repository structure.
- Do not overwrite user changes without explicit instruction.
- Before adding automation, document the expected command and required environment variables.
- **Changes made by a developer must not be replaced, deleted, or rolled back without explicit human permission.** Always request permission for those actions and describe exactly what you plan to do.
- If a task requires changing code that has already been changed by a developer, the agent must preserve those changes and make only the strictly necessary change.
- **When a developer changes code and tests fail because of that code, fix the tests, not the new code.** A failing test must not be used as a reason to undo code written by a developer.

### Keep Everything Simpler (KISS)

- Follow the rule "the simpler, the better" and "the best code, interface, or button is the one that does not exist." Code must solve the stated task and nothing more.
- Implement only what was explicitly requested: do not add unrequested capabilities, settings, or "flexibility for later."
- Do not handle errors that are unlikely in practice.
- If code can be rewritten so that it becomes smaller, rewrite it.
- Constantly evaluate whether your solution would look overcomplicated to an experienced developer. Is the code difficult to understand when reading it? If yes, simplify it.

### Apply DRY Correctly

- If code is duplicated in several places, it should be unified. Try to avoid duplication in code.
- At the same time, if several situations are expected to diverge later, duplication is allowed. For example, a shared implementation may be created for translation into other languages. If some languages require a special approach, it is acceptable to duplicate code to avoid overcomplicating the shared code with checks and branches that other languages do not need.

### Targeted Edits

- Write only what is needed for the request.
- Do not incidentally fix neighboring code, comments, or formatting when the task did not require it. Such improvements are allowed only in refactoring tasks.
- Do not touch working mechanisms.
- Always follow the style specified in the project. Even if you found a solution in another style, rewrite it in the project style.
- Remove unused code that is not related to the task only with the developer's permission.
- Remove only the code that became unnecessary as a result of your changes.

### Thoughtful Approach to Writing Code

- Do not act on guesses. Do not hide it if you do not fully understand something.
- Before writing code, do the following:

    1. Analyze the user's task.
    2. State the assumptions the solution will rely on.
    3. If you have doubts, ask. If there are several possible interpretations, list them all instead of choosing on your own.
    4. If you see a simpler path, say so.
    5. If the solution proposed by the human is not the best one, object with reasoning.
    6. If you encounter an unclear point, stop and clarify everything that is ambiguous.

### Focus on Measurable Results

- Define clear criteria for task completion. The development cycle continues until the goals are reached.
- Turn vague tasks into verifiable goals.
- For multi-step tasks, create a plan:

    Action 1 -> Check -> Testing

    Action 2 -> Check -> Testing

## CodeGraph

1. When working with code, including searching files or code, analyzing any part of the project, or diagnosing errors, use MCP CodeGraph.

2. If the data appears stale, use `codegraph_status`. Do not run `codegraph sync` while a watcher is active.

3. Start code exploration with `codegraph_explore`.
Use `codegraph_search` only to search for a symbol name.
Use `codegraph_node` to retrieve the full body of a symbol.
Use `codegraph_callers` and `codegraph_callees` to analyze relationships in code.
Use `codegraph_impact` before refactoring.

4. Do not reopen files whose source code CodeGraph has already found, except when editing is required, when checking uncommitted changes, or when a stale-index warning was received. Use `rg`, `sed`, and direct file reads only for formats unsupported by the index, exact text search, or other cases where CodeGraph is not sufficient.
