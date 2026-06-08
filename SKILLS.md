# Project-Local Skills

This file describes repeatable project tasks. Use these instructions only within this repository.

## `updocs`: Synchronizing Documentation Between `lang/ru` and English Files

Short name: `updocs`.

Invocation variants:

- `updocs` - update English-language files based on `lang/ru`;
- `updocs --en` - update files in `lang/ru` based on the corresponding English-language files.

Use this skill when the user asks to update translations, synchronize documentation, or update files in one language version based on another.

Goal: without a flag, treat files in `lang/ru` as the source of truth and update the corresponding English-language files. With the `--en` flag, treat English-language files as the source of truth and update the corresponding files in `lang/ru`.

Workflow:

1. Determine the operating mode:
   - without the `--en` flag, the source is `lang/ru` and the target is the corresponding English-language files;
   - with the `--en` flag, the source is English-language files and the target is the corresponding files in `lang/ru`.
2. For mode without `--en`, find all current files in `lang/ru`.
3. Determine the corresponding English path:
   - `lang/ru/README.md` -> `README.md`;
   - `lang/ru/AGENTS.md` -> `AGENTS.md`;
   - `lang/ru/<path>` -> `<path>`, for example `lang/ru/examples/README.md` -> `examples/README.md`.
4. For `--en` mode, find all current English-language files that have a defined direct counterpart in `lang/ru`, and apply the reverse mapping:
   - `README.md` -> `lang/ru/README.md`;
   - `AGENTS.md` -> `lang/ru/AGENTS.md`;
   - `<path>` -> `lang/ru/<path>`, for example `examples/README.md` -> `lang/ru/examples/README.md`.
5. If the corresponding target file is missing, create it.
6. Translate the content into the target file's language while preserving Markdown structure, lists, links, paths, and meaning.
7. Do not delete or change the source files of the selected mode unless the user explicitly asks for it.
8. Do not touch user changes outside files that are direct counterparts of the source files in the selected mode.
9. After editing without `--en`, check that no accidental Cyrillic remains outside `lang/ru`:

   ```bash
   rg -n '\p{Cyrillic}' --glob '!lang/ru/**' .
   ```

10. In the final response, list the updated files and state that tests were not run if the changes were documentation-only.
