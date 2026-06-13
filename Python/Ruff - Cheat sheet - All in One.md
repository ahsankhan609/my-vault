---
title: Ruff - Cheat sheet - All in One
created: 2026-12-05
tags:
  - python
  - pydantic
  - lecture
  - tools
  - commands
---
**Add Ruff to your project.**

```bash
uv add --dev ruff
```

[Installing Ruff from Official Source](https://docs.astral.sh/ruff/installation/)

| ==Check Files and fix errors== |                                                                  |                                                                                                          |
| ------------------------------ | ---------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| `ruff check .`                 | scan the current folder with all py files for errors             | [https://docs.astral.sh/ruff/linter/#rule-selection](https://docs.astral.sh/ruff/linter/#rule-selection) |
| `ruff check <file.py>`         | scan specific file for errors                                    | [https://docs.astral.sh/ruff/linter/#rule-selection](https://docs.astral.sh/ruff/linter/#rule-selection) |
| `ruff check . —fix`            | fix all erros in the current folder with all py files for errors | [https://docs.astral.sh/ruff/linter/#rule-selection](https://docs.astral.sh/ruff/linter/#rule-selection) |
| ==Format Files==               |                                                                  |                                                                                                          |
| `ruff format`                  | Format all files in the current directory.                       | [https://docs.astral.sh/ruff/formatter/](https://docs.astral.sh/ruff/formatter/)                         |
| `ruff format <file.py>`        | Format a single file                                             | [https://docs.astral.sh/ruff/formatter/](https://docs.astral.sh/ruff/formatter/)                         |
| ==All settings==               |                                                                  |                                                                                                          |
| All settings                   |                                                                  | [https://docs.astral.sh/ruff/settings/](https://docs.astral.sh/ruff/settings/)                           |
