# ai-bootstrap

This repository contains a base structure for preparing a developer environment for effective work with AI agents.

## Documentation Translations

[Russian](lang/ru/README.md)

To translate Russian documentation into English, the project provides a Codex skill named `updocs`: write `updocs` in the Codex console, and the AI will check changes in `lang/ru`, translate them, and update the English version of the files.

If you write the message as `updocs --en`, the reverse process will run. Changes in the English documentation will be translated into Russian, and the documentation in `lang/ru` will be updated.

## Repository Structure

- `AGENTS.md` - primary instructions for Codex and other AI agents.
- `CLAUDE.md` - symlink to `AGENTS.md` for Anthropic AI.
- `SKILLS.md` - local repeatable project skills, including `/update-docs`.
- `ai-docs/` - AI instructions and repository documentation.
- `docs/` - additional repository documentation.
- `scripts/` - installation and setup scripts.
- `examples/` - example configuration files.
- `lang/` - translations of project documentation into other languages.

## MCP and Other Additions for AI Agents

[CodeGraph](docs/codeGraph.md)
