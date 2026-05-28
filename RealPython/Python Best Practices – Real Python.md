---
title: Python Best Practices – Real Python
source: https://realpython.com/ref/best-practices/project-layout/
author:
  - "[[Real Python]]"
published:
created: 2026-05-26
description: Guidelines and best practices for effectively structuring and organizing your Python projects.
tags:
  - "#best-practices"
---
## project layout

Once your code grows beyond a single file, how you organize it starts to matter a lot. A clear, predictable **project layout** facilitates codebase navigation and helps you understand how pieces fit together. It also allows you and other collaborators to make informed decisions about where to place new code or resources.

In contrast, a messy layout slows everyone down and often leads to tangled imports, duplicated logic, and code that’s hard to test.

In most Python projects, you can distinguish between two general types of layouts:

1. **`src/` layout:** The source code is organized within the `src/` directory. This layout is well suited for library code that will be packaged and distributed to others, and for larger projects. It helps ensure your tests import the installed package instead of the local working directory, avoiding common import errors.
2. **Flat layout:** The source code package or packages live at the root level alongside other files like `README.md` or `pyproject.toml`. This layout can work well for quick scripts, but it’s prone to accidentally importing the wrong files and can become messy as a project grows.

Modern Python projects typically follow a small set of common layout patterns. At the top level, you usually have a project root directory that contains everything related to the project, including metadata, configuration files, source code, and other resources.

Here are some commonly used layout components you’ll encounter in Python projects:

| File/Directory | Purpose |
| --- | --- |
| `src/`   (`src/` layout) | Contains the project’s Python code |
| `project_package_name/`   (Flat layout) | Contains the project’s Python code and is often named after your project |
| `tests/` | Contains unit tests for the project’s code |
| `README.md` | Provides an overview of the project, installation instructions, basic usage examples, and similar |
| `LICENSE` | Holds a legal document defining the terms under which the project can be used and distributed |
| `pyproject.toml` | Provides a centralized configuration file that holds metadata, dependencies, build system information, tool-specific settings, and similar |
| `docs/` | Contains detailed user and developer documentation (optional) |
| `bin/` or `scripts/` | Contains executable scripts that import and call functions from your main package (optional) |

When laying out Python projects, you can summarize the best practices as follows:

- **Use a clear top-level structure:** At the root of your project, keep the most important files that describe and configure the project: `pyproject.toml`, `README.md`, `LICENSE`, and configuration files for tools and continuous integration (CI). Group code into directories instead of leaving many Python files in the root directory. This practice makes the project easier to scan and understand at a glance.
- **Put importable code in a package and avoid a large collection of top-level modules:** Organize your application or library code into a proper [package](https://realpython.com/ref/glossary/package/) with subpackages or [modules](https://realpython.com/ref/glossary/module/) that reflect logical domains, such as `core`, `api`, `models`, and so on. Avoid large modules where unrelated functions pile up over time. A well-structured package hierarchy improves reuse, discoverability, and testability.
- **Choose wisely between a `src/` or flat layout:** For packages intended to be installed, published, or reused, consider the `src/` layout, which separates source code from other components and prevents issues with imports. For relatively small projects and basic scripts, you can opt for the flat layout.
- **Keep tests in a dedicated `tests/` directory:** Place your unit tests in a top-level `tests/` directory that loosely mirrors your package structure. This separation keeps your repository clean and makes it easier to exclude tests from distributions while still making it easy to run the tests.
- **Separate layers such as interface, domain, and persistence in larger applications:** Within your source packages, clearly define boundaries between the user-facing layer, such as [command-line interfaces (CLIs)](https://realpython.com/ref/glossary/command-line-interface/), [text-based user interfaces (TUIs)](https://realpython.com/python-textual/), [graphical user interfaces (GUIs)](https://realpython.com/ref/glossary/graphical-user-interface/), or web frontends, and the domain or business logic. Keep persistence code that deals with databases, the file system, or external services separate as well.

To see the impact of layout on clarity, compare these two small projects.

🔴 **Avoid this:**

```
project_name/
├── doc_index.html
├── doc_source.txt
├── LICENSE
├── main.py
├── module1.py
├── module2.py
├── pyproject.toml
├── README.md
├── test_module1.py
├── test_module2.py
└── tests_init.py
```

In this layout, it’s not clear what the main entry point is, where the core business logic lives, or how tests relate to the code. Everything sits on the same level, which makes imports fragile and encourages “grab bag” modules like `utils.py` that accumulate unrelated functionality.

✅ **Favor this:**

Use the `src/` layout:

```
project_name/
├── bin/                  # Optional
│   └── project_name
├── docs/                 # Optional
│   ├── index.html
│   └── source.txt
├── src/
│   └── project_name/
│       ├── __init__.py
│       ├── __main__.py
│       ├── module1.py
│       └── module2.py
├── tests/
│   ├── __init__.py
│   ├── test_module1.py
│   └── test_module2.py
├── LICENSE
├── README.md
└── pyproject.toml
```

Or use the flat layout:

```
project_name/
├── bin/                  # Optional
│   └── project_name
├── docs/                 # Optional
│   ├── index.html
│   └── source.txt
├── project_name/
│   ├── __init__.py
│   ├── __main__.py
│   ├── module1.py
│   └── module2.py
├── tests/
│   ├── __init__.py
│   ├── test_module1.py
│   └── test_module2.py
├── LICENSE
├── pyproject.toml
└── README.md
```

In these layouts, a quick glance at the root directory reveals critical information about the project’s structure. You’ll quickly discover configuration files, [`README.md`](https://realpython.com/readme-python-project/), the project’s license, the source code, the tests, and other details.