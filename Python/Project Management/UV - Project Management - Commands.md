---
title: UV - Project Management - Commands
created: 2026-06-03
tags:
  - uv
  - commands
  - bash
  - best-practices
  - python
  - intermediate
---
[Managing Python Projects With UV - An All-in-One Solution](../../RealPython/Managing%20Python%20Projects%20With%20UV%20-%20An%20All-in-One%20Solution.md)

[UV Cheat Sheet](https://yonesuke.github.io/cheatsheet/cheatsheet_ruff.html)


| Commands                                                             | Description                                                                    | Use case                                                                                                              |
| :------------------------------------------------------------------- | :----------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------- |
| ==Initialize Project==                                               |                                                                                |                                                                                                                       |
| `uv init`                                                            | initialize project with a name                                                 | `uv init <project_name>`                                                                                              |
| `uv init . `                                                         | initialize current proejct as uv managed project                               | `uv init .`                                                                                                           |
| `uv init --python 3.14.5`                                            | initiate current project with python verson                                    | `uv init --python 3.14.5 .`                                                                                           |
| `uv init project_name --python 3.14.5`                               | initialize project with a name, and with specific python version               | when you need to initialize new project with structure and with specific python version.                              |
| ==Adding - Installing Packages==                                     |                                                                                |                                                                                                                       |
| `uv add <package_name>`                                              | add package to the current environment. if no environment, then it creates one | `uv add fastapi`                                                                                                      |
| `uv add pytest --dev`                                                | install dependencies for the development environment                           | `uv add --dev pytest ruff`                                                                                            |
| `uv add -r requirements.txt`                                         | Install dependencies from `requirements.txt`                                   |                                                                                                                       |
| ==Running Script - Project==                                         |                                                                                |                                                                                                                       |
| `uv run main.py`                                                     | Run `project file`                                                             |                                                                                                                       |
| `uv run app.py`                                                      | Run `single script file`                                                       |                                                                                                                       |
| `uv run --with ‘flask’ —-with ‘pandas’ —-with ‘requests’ app.py`     | Run `single app.py` file, with dependencies on the fly                         | it is used when yo not need to install and dependency and just need to run the file with all dependencies on the fly. |
| `uv add —-script app.py ‘pkg1’ ‘pkg2’ ‘pkg3’`<br><br>`uv run app.py` | Run `single script` with dependencies<br><br><br>then run the `script file`    | it is used when we do not need to install dependencies, but we decorate them on the `top of page`.                    |
| ==Updating Packages==                                                |                                                                                |                                                                                                                       |
| `uv sync`                                                            | sync all dependencies with project                                             | `uv sync`                                                                                                             |
| `uv sync --upgrade`                                                  | upgrade all dependencies in the project                                        | `uv sync --upgrade`                                                                                                   |
| `uv lock --upgrade`                                                  | Upgrade all in `lock` file                                                     |                                                                                                                       |
| ==Uninstall - Remove Package==                                       |                                                                                |                                                                                                                       |
| `uv remove package_name`                                             | remove or uninstall dependency from project and update `pyproject.tmol`        |                                                                                                                       |
| `uv remove —-script app.py ‘pkg1’ ‘pkg2’`                            | Remove `package` from the `script` file                                        |                                                                                                                       |

### Configuration - pyproject.toml

```toml
[project]

# ... standard project metadata ...

[tool.ruff]

# Target Python version (adjust to your project's needs)

target-version = "py310"

# Maximum line length (Ruff defaults to 88, similar to Black)

line-length = 88

[tool.ruff.lint]

# Enable rules:

# E: Pycodestyle errors

# F: Pyflakes

# I: isort (Import sorting)

# B: Flake8-bugbear (Potential bugs)

# UP: Pyupgrade (Upgrade syntax to newer Python versions)

# N: Pep8-naming

select = ["E", "F", "I", "B", "UP", "N"]

# Ignore specific rules if needed

ignore = []

# Allow unused variables when underscore-prefixed.

dummy-variable-rgx = "^(_+|(_+[a-zA-Z0-9_]*[a-zA-Z0-9]+?))$"

[tool.ruff.lint.isort]

# Organize imports settings

known-first-party = ["my_project"]

[tool.ruff.format]

# Like Black, use double quotes for strings.

quote-style = "double"

# Indent with spaces, rather than tabs.

indent-style = "space"

# Respect magic trailing commas.

skip-magic-trailing-comma = false

# Automatically detect the appropriate line ending.

line-ending = "auto"
```
