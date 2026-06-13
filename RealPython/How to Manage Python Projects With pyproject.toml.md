---
title: How to Manage Python Projects With pyproject.toml
source: https://realpython.com/python-pyproject-toml/
author:
  - "[[Real Python]]"
published: 2025-02-19
created: 2026-05-26
description: Learn how to manage Python projects with the pyproject.toml configuration file. In this tutorial, you'll explore key use cases of the pyproject.toml file, including configuring your build, installing your package locally, managing dependencies, and publishing your package to PyPI.
tags:
  - "#intermediate"
  - tools
---
![How to Manage Python Projects With pyproject.toml](https://realpython.com/cdn-cgi/image/width=1920,format=auto/https://files.realpython.com/media/How-to-Set-Up-a-pyproject.toml-File-for-Your-Python-Project_Watermarked.51dc34160c1d.jpg)

## How to Manage Python Projects With pyproject.toml

The `pyproject.toml` file simplifies Python project configuration by unifying package setup, managing dependencies, and streamlining builds. In this tutorial, you’ll learn how it can improve your day-to-day Python setup by exploring its key use cases, like configuring your build system, installing packages locally, handling dependencies, and publishing to [PyPI](https://realpython.com/ref/glossary/pypi/).

**By the end of this tutorial, you’ll understand that:**

- `pyproject.toml` is **a key component** for defining a Python project’s build system, specifying requirements and the build backend.
- **Dependencies and optional dependencies** can be managed directly within the `pyproject.toml` file or combined with the traditional `requirements.txt`.
- **Scripts for command-line execution** are defined in the `[project.scripts]` section, allowing you to automate common tasks.
- **Dynamic metadata** in `pyproject.toml` enables flexible project configuration, with attributes like version being resolved at build time.
- The Python packaging ecosystem includes various tools that leverage `pyproject.toml` for **project management**, enhancing collaboration, flexibility, and configurability.

To get the most out of this tutorial, you should be familiar with the [basics of Python](https://realpython.com/tutorials/basics/). You should know how to [import modules](https://realpython.com/python-import/) and install [packages](https://realpython.com/python-modules-packages/) with [pip](https://realpython.com/what-is-pip/). You should also be able to navigate the [terminal](https://realpython.com/terminal-commands/) and understand how to create [virtual environments](https://realpython.com/python-virtual-environments-a-primer/).

The `pyproject.toml` package configuration file is the *relatively* new (circa 2016) standard in the Python ecosystem, intended to unify package configuration. It’s also supported by many major tools for managing your Python projects. Some of the project management tools that support the `pyproject.toml` file are [pip](https://pip.pypa.io/en/stable/), [Setuptools](https://setuptools.pypa.io/en/latest/), [Poetry](https://python-poetry.org/), [Flit](https://flit.pypa.io/en/stable/), [`pip-tools`](https://github.com/jazzband/pip-tools), [Hatch](https://hatch.pypa.io/latest/), [PDM](https://pdm-project.org/en/latest/), and [uv](https://realpython.com/python-uv/).

The `pyproject.toml` file is a configuration file written in the [TOML](https://realpython.com/python-toml/) syntax. For many Python project management needs, a minimal `pyproject.toml` file doesn’t have to contain a lot of information:

TOML `pyproject.toml`

```
[project]
name = "a-sample-project"
version = "1.0.0"
```

Different tools have different requirements, but the name and version of your project are [officially](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/#basic-information) the only required fields in the `[project]` table. Typically, you’ll want to include more fields, but if you only want to include a minimal `pyproject.toml` file, then that’s all you’ll need to get started. Just include this file at the root of your project.

To understand more about why using a `pyproject.toml` file may be useful, you’ll explore a sample CLI application to show you how the `pyproject.toml` file fits into a standard project workflow.

> [!warning] Warning
> **Get Your Code:** [Click here to download the free sample code](https://realpython.com/bonus/python-pyproject-toml-code/) you’ll use to learn how to manage Python projects with pyproject.toml.

==**Take the Quiz:**== Test your knowledge with our interactive “How to Manage Python Projects With pyproject.toml” quiz. You’ll receive a score upon completion to help you track your learning progress:

---

[![How to Manage Python Projects With pyproject.toml](https://realpython.com/cdn-cgi/image/width=1920,format=auto/https://files.realpython.com/media/How-to-Set-Up-a-pyproject.toml-File-for-Your-Python-Project_Watermarked.51dc34160c1d.jpg)](https://realpython.com/quizzes/python-pyproject-toml/)

**Interactive Quiz**

[How to Manage Python Projects With pyproject.toml](https://realpython.com/quizzes/python-pyproject-toml/)

In this quiz, you'll test your understanding of Python's pyproject.toml file, which simplifies Python project configuration by unifying package setup, managing dependencies, and streamlining builds.

## Setting Up a Python Project With pyproject.toml

The example project you’ll work with in this tutorial is inspired by the classic [`cowsay`](https://en.wikipedia.org/wiki/Cowsay) program. The example project is called `snakesay` and—once installed—you can run it with the `ssay` command:

```
$ ssay Hello, World!

 _______________
( Hello, World! )
 ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
  \
   \    ___
    \  (o o)
        \_/ \
         λ \ \
           _\ \_
          (_____)_
         (________)=Oo°
```

As you can see, the program takes a string argument and echoes it back with a bit of [ASCII art](https://en.wikipedia.org/wiki/ASCII_art).

The structure of the example project follows a popular pattern for Python projects:

```
snakesay-project/    ← The project root
│
├── snakesay/        ← The main module of this project
│   ├── __init__.py
│   ├── __main__.py  ← The entry point to snakesay
│   └── snake.py     ← The core of the program
│
├── .gitignore
├── LICENSE
├── pyproject.toml   ← What this tutorial is about
└── README.md
```

The directory `snakesay-project` is the **root** location of your project. The main **package**, where most of the code goes, is the `snakesay` directory.

> [!primary] Primary
> **Note:** A popular and often recommended project layout is the `src` layout:
> 
> ```
> snakesay-project/
> │
> ├── src/
> │   └── snakesay/
> │       ├── __init__.py
> │       ├── __main__.py
> │       └── snake.py
> ...
> ```
> 
> This layout has two key advantages: it makes the location of the source code more explicit and helps avoid some of the issues that can arise with more complex configurations, especially with testing.

At the root level of the project, you’ve got the star of this tutorial, the `pyproject.toml` file. In this project, the `pyproject.toml` file currently contains the following content:

TOML `pyproject.toml`

```
[build-system]
requires = ["setuptools"]
build-backend = "setuptools.build_meta"

[project]
name = "snakesay"
version = "1.0.0"

[project.scripts]
ssay = "snakesay.__main__:main"

[tool.setuptools.packages.find]
where = ["."]
```

As the tutorial progresses, you’ll examine what all this means in more detail. You’ll also expand this `pyproject.toml` to include more tables and fields. As it stands, this `pyproject.toml` file includes:

- The **`[build-system]`** table: Specifies what’s needed to **build** the project. The `requires` key lists the required packages, and the `build-backend` key defines the module used for the build process.
- The **`[project]`** table: Contains essential **project metadata** and has plenty of optional fields, some of which you’ll explore later in this tutorial.
- The **`[project.scripts]`** table: Allows you to define one or several **executable commands** to be able to call your application from the command line. In this case, it’s `ssay`, but it can be anything you like.
- The **`[tools.setuptools.packages.find]`** table: Tells your build-system, Setuptools, where to find packages in your project. In this case, it’s just the root directory.

With this `pyproject.toml` file, you’ve already defined all the configuration you need to build and run your project.

The `[tools.setuptools.packages.find]` table isn’t required since the value of `["."]` is the default. Even though it’s the default, sometimes Setuptools can’t find other modules in the project root, and explicitly setting the `where` key can help with this.

Setuptools has various defaults for [package discovery](https://setuptools.pypa.io/en/latest/userguide/quickstart.html#package-discovery), which include the current project layout and the `src` layout.

If you want to customize the package discovery defaults, then bear in mind that the `[tools.setuptools.packages.find]` table is [Setuptools-specific](https://setuptools.pypa.io/en/latest/userguide/pyproject_config.html#setuptools-specific-configuration), and other build tools will have different tables and fields to configure the build process.

Why Setuptools in the first place? [Setuptools is the fallback](https://pip.pypa.io/en/stable/reference/build-system/pyproject-toml/#fallback-behaviour) build system when using `pip` if you don’t include the `[build-system]` table. So it’s a good choice for a build backend if you’re not sure what to use. It’s been a default build system for Python for a long time, and it’s well supported by the Python packaging ecosystem.

> [!primary] Primary
> **Note:** Setuptools and `pip`, though ubiquitous, aren’t officially part of the Python standard library. They’re separate projects maintained by the Python Packaging Authority (PyPA), which is a separate organization from the Python Software Foundation (PSF).
> 
> You’ll explore the Python packaging ecosystem more in the [Understanding the Context of `pyproject.toml` in Python Packaging](#understanding-the-context-of-pyprojecttoml-in-python-packaging) section.

The **build backend** of Setuptools is `setuptools.build_meta`. This is a Python module that **implements** the build backend [interface](https://realpython.com/python-interface/), as defined in [PEP 517](https://peps.python.org/pep-0517/).

Most of the code in the `snakesay` example project isn’t relevant to this tutorial, as you’re just interested in the `pyproject.toml` file. You can still download the source code of this project, if you’re interested. One relevant file is the **entry point**, which determines how your project behaves once installed:

Python `__main__.py`

```
import sys
from snakesay import snake

def main():
    snake.say(" ".join(sys.argv[1:]))

if __name__ == "__main__":
    main()
```

All this file does is join the **command-line arguments** into a string and use them to call the `say()` function in the `snake` module.

If you don’t install this project, then to call your `snakesay` program you’ll need to navigate to the `snakesay-project` directory and execute the following command:

```
$ python -m snakesay Hello, World!

 _______________
( Hello, World! )
 ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
  \
   \    ___
    \  (o o)
        \_/ \
         λ \ \
           _\ \_
          (_____)_
         (________)=Oo°
```

The `-m` flag tells the Python executable to treat the following argument as the **dotted path** to the module.

> [!primary] Primary
> **Note:** The dotted path isn’t the file path, but the way you’d refer to the module if you were importing it. For example, if the project was more complex than it is, and the target module was a few levels deep, you could have a dotted path of `snakesay.cli.entry`.

Since you’re calling the directory `snakesay` *as a module*, it runs the `__main__.py` file in that directory. If the directory didn’t have a `__main__.py`, then it couldn’t be directly executed as you’ve done above.

To set up the project so that you can call it from the command line with just a `ssay` command—as it’s configured to do in the `pyproject.toml` file—you’ll need to **install** the project.

[Remove ads](https://realpython.com/account/join/)

## Understanding Why You Should Install Your Python Project

One of the main reasons you’d want to install your package right off the bat is to take full advantage of the **import system**. Installing your project is generally the recommended way to work with Python projects and comes with other benefits that you’ll see later in the tutorial.

If you don’t install your project, then your project is **coupled** to its location on your **file system**. This may seem fine at first, but it’s often the root of much confusion when working with Python imports.

For example, you may think that you can just run the `__main__.py` file directly as a script:

```
$ python snakesay/__main__.py Hello, World!
Traceback (most recent call last):
  ...
  snakesay-project/snakesay/__main__.py", line 2, in <module>
    from snakesay import snake
ModuleNotFoundError: No module named 'snakesay'
```

As you can see, there are issues when importing. The key to understanding the problem is in understanding the [module search path](https://realpython.com/python-import/#pythons-import-path). When you try to import something in Python, such as `import math`, the Python interpreter looks in the module search path.

There are various locations in the module search path. If you run a Python *file* as a script, so with no `-m` flag, then the script location is added to the module search path. If you run a Python *module* with the `-m` flag, then the *module itself* is added to the search path.

To be able to `import snakesay`, there needs to be a `snakesay` module in the search path. In the example above, when you run the `__main__.py` file as a script, there’s no `snakesay` module in that directory so you get a `ModuleNotFoundError`.

> [!primary] Primary
> **Note:** Don’t be tempted to modify the module search path directly!
> 
> The module search path can be accessed at runtime at `sys.path`. Any path in the `PYTHONPATH` environment variable, if it exists, will also be added to the module search path.
> 
> Since you *can* modify the search path directly, many have done so—but this is a path fraught with trouble! You should almost never mess with the Python module search path manually. It just leads to headaches because you’re working against the grain of the Python import system.

Now that you understand some of the reasons *why* you’d want to install your project, you’ll see *how* to do that next.

## Installing Your pyproject.toml Project With pip

To install your project with [`pip`](https://realpython.com/what-is-pip/), first navigate to the `snakesay-project` directory and optionally create a [virtual environment](https://realpython.com/python-virtual-environments-a-primer/) there. Once ready, you can install your project:

```
$ (venv) python -m pip install -e .
Obtaining file:///home/realpython/snakesay-project
  Installing build dependencies ... done
  Checking if build backend supports build_editable ... done
  Getting requirements to build editable ... done
  Preparing editable metadata (pyproject.toml) ... done
Building wheels for collected packages: snakesay
  Building editable for snakesay (pyproject.toml) ... done
  Created wheel for snakesay: filename=snakesay-1.0.0-0.editable-py3-none-any.whl size=2909 sha256=f529244d56218345229cf6c7ec3992f56d6353f2fb54f22e9dd1012fb53114ef
  Stored in directory: /tmp/pip-ephem-wheel-cache-cg4dk_ud/wheels/ee/e7/78/f4cc6c30d6a4477b502f5bd0902c40950d7f17c47022392a55
Successfully built snakesay
Installing collected packages: snakesay
Successfully installed snakesay-1.0.0
```

That’s it—you’ve successfully installed your package locally. You’re now ready to take full advantage of Python’s powerful import system. Now you can rely on the `snakesay` module always being available wherever in the file system you happen to be. So, in the same way that you can always `import math` from wherever you are, now you’ll be able to `import snakesay` from wherever, too.

Try running the `__main__.py` file directly now, as you did before it was installed, and it should work! Also, if `snakesay` is installed correctly in the active Python interpreter, then you’ll be able to start a REPL session from anywhere in the file system and always be able to `import snakesay`.

This isn’t only handy for executing your program, but it’s also very useful for making your imports consistent in your project. Instead of resorting to relative imports—which can get hard to maintain—absolute imports will work predictably now. So, even if you’re deeply nested within the `snakesay` module, or you’re in a completely different module, you can always `from snakesay import snake` without issues.

As you may have noticed, the command used to install the project included the `-e` flag to instruct `pip` to install the package as an [editable install](https://realpython.com/what-is-pip/#installing-packages-in-editable-mode-to-ease-development).

An editable install means that if you edit the source code of the package, then you won’t need to reinstall the package to see those changes when you run the program. If you want to install an established project and don’t foresee any changes, then you can omit this flag.

There’s one thing to keep in mind with an editable install. If any changes are made to the `pyproject.toml` file itself, then you’ll often need to reinstall the package. This is because the `pyproject.toml` file is used to configure the build process, and if you change the fundamental configuration of the project, then you’ll need to completely rebuild the package.

> [!primary] Primary
> **Note:** If you’ve done an editable install, then you’ll now see a new `snakesay.egg-info` directory in the `snakesay-project` directory. This contains some project metadata associated with your installation. You can consider the `.egg-info` directory an installation **artifact** which you shouldn’t track with version control. If you do a *non* -editable install, then `pip` stores this metadata elsewhere.
> 
> The egg in `.egg-info` is a reference to the [egg format](https://setuptools.pypa.io/en/latest/deprecated/python_eggs.html), which was a way to distribute Python packages before the [wheel](https://realpython.com/python-wheels/) format was introduced. Although the wheel format is now the primary standard for Python package distribution, the `.egg-info` directory is still used by Setuptools to store metadata about the package in an editable installation. It’s somewhat of a relic from earlier days.

`pip` manages the overall installation process, ensuring that **dependencies** like Setuptools are available. Setuptools handles the build process, which involves finding packages, configuring metadata, creating links for editable mode, and setting up entry point scripts. Both tools leverage the `pyproject.toml` file to configure the process.

Another great thing about installing your project is that you can now run the `ssay` command from the command line. In the next section, you’ll see how the `pyproject.toml` file is used to configure scripts.

[Remove ads](https://realpython.com/account/join/)

## Using pyproject.toml to Configure Scripts

With the `snakesay` package installed, you’ll see that you can now call the command from the command line directly with the `ssay` command:

```
$ (venv) ssay "I'm installed!"

 _________________
( I'm insstalled! )
 ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
  \
   \    ___
    \  (o o)
        \_/ \
         λ \ \
           _\ \_
          (_____)_
         (________)=Oo°
```

You have this command available from the command line because the `pyproject.toml` file defines a section, which your build backend reads to create **executable commands**:

TOML `pyproject.toml`

```
...

[project.scripts]
ssay = "snakesay.__main__:main"

...
```

The `[project.scripts]` table has one entry with a key of `ssay` and a value of `"snakesay.__main__:main"`. With this information, your build backend will create an executable command to run the `main()` function in the `__main__` submodule of `snakesay`, which you just installed.

These values can be customized to whatever you want, and you can add as many as you want, as long as they point to a [Python callable](https://realpython.com/python-callable-instances/), such as a [function](https://realpython.com/defining-your-own-python-function/). You just need to make sure the target callable is a **procedure** —it shouldn’t take arguments.

You’ll typically want to automate certain common tasks in your project. Maybe that will involve easy commands for formatting, linting and [testing](https://realpython.com/pytest-python-testing/). While there are many tools that automate all or parts of this process for you, you can leverage the `pyproject.toml` file for quite a lot. Anything you can do in a Python function, you can attach a script to. So, with some imagination, there’s little that you couldn’t do.

> [!primary] Primary
> **Note:** The `[project.scripts]` table is currently limited to calling a Python function and doesn’t support arbitrary shell commands, like JavaScript’s `package.json` does.
> 
> If you want to run a script on your machine and aren’t too concerned about making things cross-platform or reproducible across different machines, then often a basic shell command is all you need. You can use the [`subprocess` module](https://realpython.com/python-subprocess/) to do this:
> 
> Python `scripts/scripts.py`
> 
> ```
> import subprocess
> 
> def run_command(command):
>     subprocess.run(["powershell", "-Command", command])
> 
> def task():
>     run_command("black && isort")
> ```
> 
> Python `scripts/scripts.py`
> 
> ```
> import subprocess
> 
> def run_command(command):
>     subprocess.run(["sh", "-c", command])
> 
> def task():
>     run_command("black && isort")
> ```
> 
> With this basic code set up, all you’d need to do is wrap your command in a Python function, like the `task()` function above, and reference it from your `pyproject.toml` file.
> 
> There’s extensive Python tooling available for this type of task management, such as [Invoke](https://www.pyinvoke.org/), which is a powerful and flexible tool inspired by classics such as [GNU Make](https://www.gnu.org/software/make/). [Poetry](https://realpython.com/dependency-management-python-poetry/) has a section in the `pyproject.toml` file to run shell scripts or Python functions. If you only need script running for formatting, linting and testing, specialized tools for automating these types of task exist, like [tox](https://tox.wiki/), which also leverages the `pyproject.toml` file.

At this stage, you might be pining after a single solution for project management, but the truth is that you’ll have to decide on a set of tools that works for you, and there’s always going to be a bit of a learning curve. You’ll explore why this is so in a bit, but for now, you’ll explore how to manage dependencies with the `pyproject.toml` file.

## Managing Dependencies With a pyproject.toml File

If all you need is to migrate from a basic [`requirements.txt` file](https://realpython.com/what-is-pip/#using-requirements-files), then you’ll be able to replace that with `pyproject.toml`. As you’ve seen, `pip` and Setuptools are almost always available as part of a default Python installation. These tools can take care of most dependency management tasks together with the `pyproject.toml` file, leaving you with one single file to manage your project.

Take the current state of the example project `snakesay`, which doesn’t have any dependencies. Imagine that you wanted to enhance the project with some fancy terminal magic with a library like [Rich](https://realpython.com/python-rich-package/). Since you foresee working on this longer than a few minutes, you may want to add in a some development tools, such as [Black](https://black.readthedocs.io/en/stable/) and [isort](https://pycqa.github.io/isort/):

```
...

[project]
name = "snakesay"
version = "1.0.0"
+dependencies = ["rich"]

+[project.optional-dependencies]
+dev = ["black", "isort"]

...
```

As you can see, you’ve added a list with one item in the `dependencies` key of the `[project]` table. In the `[project.optional-dependencies]` table, you’ve added a `dev` key with a list of two more dependencies. In this case, these dependencies are only needed if you’re developing the project. Note that the `dev` key is arbitrary—you can call it anything you like.

Now, if you install your project with `pip`, the Rich library will automatically be installed as part of the regular installation. Nice! If you want to install the optional dependencies too, then you can call:

```
$ python -m pip install -e ".[dev]"
```

Appending `[dev]` to the directory with the `pyproject.toml` file will include the optional dependencies you’ve specified under `dev`, along with the core dependencies specified in the `[project]` table. Very nice!

> [!primary] Primary
> **Note:** You can also [fine-tune requirement specifications](https://realpython.com/what-is-pip/#fine-tuning-requirements) as you would in a `requirements.txt` file. For example, if certain features of your project require at least a specific version of your dependencies, then you can specify that in the `pyproject.toml` file:
> 
> ```
> ...
> 
> [project]
> name = "snakesay"
> version = "1.0.0"
> +dependencies = ["rich>=13.9.0"]
> 
> [project.optional-dependencies]
> +dev = ["black>=24.1.0", "isort>=5.13.0"]
> 
> ...
> ```
> 
> This uses the greater than or equals to operator (`<=`) to specify that the packages installed should be higher than the specified version.
> 
> You can also use these symbols to specify a version for the build system, like Setuptools:
> 
> ```
> [build-system]
> +requires = ["setuptools>=75.3.0"]
> build-backend = "setuptools.build_meta"
> 
> ...
> ```
> 
> Specifying versions for your dependencies is just one way to ensure that your project is reproducible across different systems.

If you’re not ready to give up your `requirements.txt` file just yet, don’t worry! You can still use a traditional `requirements.txt` file and reference that file from `pyproject.toml`:

```
...

[project]
name = "snakesay"
version = "1.0.0"
+dynamic = ["dependencies", "optional-dependencies"]

[tool.setuptools.dynamic]
+dependencies = { file = ["requirements.txt"] }
+optional-dependencies.dev = { file = ["requirements-dev.txt"] }

...
```

With this setup, all you’d need is a couple of files at the root of your project to define the requirements:

```
# requirements.txt

rich

# requirements-dev.txt

black
isort
```

Then, when you install your project, the dependencies will be read from the `requirements.txt` and `requirements-dev.txt` files.

> [!primary] Primary
> **Note**: Using an external `requirements.txt` file showcases the ability to specify [dynamic metadata](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/#static-vs-dynamic-metadata). You can specify many attributes in the `[project]` table as dynamic, such as the `version`:
> 
> ```
> ...
> 
> [project]
> name = "snakesay"
> -version = "1.0.0"
> +dynamic = ["version"]
> 
> [tool.setuptools.dynamic]
> +version = {attr = "snakesay.__version__"}
> ...
> ```
> 
> In this example, the `version` key is set to be dynamic, and the value is read from the `__version__` attribute of the `snakesay` module. To make this work, you’d need to add a `__version__` attribute to the `__init__.py` file of the `snakesay` module:
> 
> Python `snakesay/__init__.py`
> 
> ```
> """A CLI program that echoes a string with a bit of ASCII art."""
> 
> __version__ = "1.0.0"
> ```
> 
> With that, you can now specify the version of your project in the `__init__.py` file, and it will be read from there when you install your project.
> 
> When a field is dynamic, it’s the [build backend’s responsibility](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/#static-vs-dynamic-metadata) to resolve the field. Setuptools uses the `[tool.setuptools.dynamic]` table to specify how to [resolve dynamic fields](https://setuptools.pypa.io/en/latest/userguide/pyproject_config.html#dynamic-metadata).

You’ve already set your dependency versions to be compatible with a specific version, but if you wanted to take another step towards ensuring reproducibility, you could use a **lock file**.

There’s a proposal for a standard lock file in [PEP 751](https://peps.python.org/pep-0751/), but it’s not yet been accepted. If you need a lock file right now, then perhaps the most straightforward way is to use `pip-tools`, which has some instructions on how it recommends [structuring requirements with `pyproject.toml`](https://pip-tools.readthedocs.io/en/stable/#requirements-from-pyproject-toml), as you’ve done with dynamic fields above.

To see some of the lively debate around standards in Python when it comes to how to specify dependencies in `pyproject.toml` file, check out the forum thread [Development Dependencies In `pyproject.toml`](https://discuss.python.org/t/development-dependencies-in-pyproject-toml/26149/14).

If you’ve been slightly overwhelmed by the number of tools and standards in the Python packaging ecosystem, you’re not alone. In the next section, you’ll explore the context of the `pyproject.toml` file in Python packaging.

[Remove ads](https://realpython.com/account/join/)

## Understanding the Context of pyproject.toml in Python Packaging

Having spent some time in the Python ecosystem, you’ve probably noticed that there are a few tools and workflows out there to pick and choose from. This can put a lot of people off. It’s natural to want [one universal standard](https://xkcd.com/927/).

To understand why Python is the way it is, it can be helpful to understand the context in which Python has evolved. So, in this section, you’ll get an overview of how Python packaging has developed, and why the `pyproject.toml` file is a step in the right direction.

Python was conceived by [Guido van Rossum](https://en.wikipedia.org/wiki/Guido_van_Rossum) at the tail end of the 1980s, during a time when the [World Wide Web](https://en.wikipedia.org/wiki/World_Wide_Web) hadn’t yet opened to the public. In these times, packaging wasn’t as much as a concern as it is today. Back then, developers often shared code by emailing files or physically passing around disks within the office. Not many would have imagined how the web would revolutionize society.

[When designing Python](https://python-history.blogspot.com/2009/01/pythons-design-philosophy.html), Guido van Rossum adopted the [Unix philosophy](https://en.wikipedia.org/wiki/Unix_philosophy) as a practical and time-saving approach. This philosophy embraces developing tools that tackle specific, often simple, tasks. These tools work well in isolation but can also be combined to solve more complex problems.

So, perhaps it’s no surprise that many Python packaging tools have evolved to reflect the Unix philosophy. There are tools for each packaging sub-task, and you can mix and match them to suit your needs.

The first build system for Python was `distutils`, which was included with Python from version 1.6 in the year 2000. It was the defacto **build system** for Python for four years.

In 2003, the [Python Package Index (PyPI)](https://realpython.com/ref/glossary/pypi/) was introduced to provide a central repository for Python packages. This was a big step forward for Python packaging, as it would eventually become the central location for developers to share their packages.

Perhaps with the rise of PyPI and the internet in general, the limitations of `distutils` were becoming obvious, such as rudimentary dependency management and tedious configuration. The **Setuptools** project was introduced in 2004 to address these limitations, eventually becoming the default build system.

**`pip`** was introduced in 2008 as a **package installer** for Python. It was designed to be a replacement for `easy_install`, which was the default package installer for Setuptools. `pip` was designed to be more user-friendly and to have a more consistent interface.

In 2011, the Python Packaging Authority (PyPA) was formed to take over the maintenance of key packaging tools like `pip` and Setuptools. PyPA has since brought various [other tools](https://packaging.python.org/en/latest/key_projects/#pypa-projects) under its umbrella.

While Setuptools was a big improvement over `distutils`, it still had limitations. As Python adoption grew, so did the special requirements of building and distributing Python packages. Over time, various tools emerged to address these limitations, some of which you’ll explore in the next section. That said, it was often difficult to switch between tools, as each tool had its own configuration format.

The `pyproject.toml` file was introduced to provide a single **configuration file** that could be used to specify build system configuration in an explicit way. It allows you to switch out the build backend entirely without having to completely rewrite your configuration. Its status as a project configuration file also makes it a convenient place to specify other project metadata and tool configuration.

> [!primary] Primary
> **Note:** To get into some of the nitty gritty details of Python’s packaging history and future direction, check out some of the [Python Packaging PEPs](https://peps.python.org/topic/packaging/).

Software development in general tends to progress this way. Often, you only get to fully know the problem after trying to solve it for a while. As society and development practices evolve, so must the tools being used.

Python’s ecosystem is robust in part because of the many tools that have been developed to solve specific problems. When the problem space evolves rapidly, it’s often easier to create new tools to solve these emerging challenges rather than trying to retrofit old, monolithic ones.

In the next section, you’ll explore a selection of the many tools that have survived the test of time and which also leverage the `pyproject.toml` file.

## Using Tools That Leverage the pyproject.toml File

There are now several tools to enhance specific areas of your project management, many of which can leverage the `pyproject.toml` file. In this section, you’ll explore some of these tools.

For advanced dependency management, you can use `pip-tools`, which is a set of utilities to manage and lock dependencies. It was originally based on the `requirements.txt` file, but can also be configured to leverage the `pyproject.toml`. This is a PyPA project, so it’s a good choice if you want to stay within the official PyPA ecosystem.

For automating testing and script running, you can use `tox`. This tool can leverage the `pyproject.toml` file to configure its behavior. Typically, this involves using a special table within the `pyproject.toml` file. For example, `tox` uses the `[tool.tox]` table to define its settings:

TOML `pyproject.toml`

```
[tool.tox]
requires = ["tox>=4.19"]
env_list = ["3.13", "3.12", "type"]
```

This table specifies that `tox` should use version 4.19 or higher, and that it should run the `3.13`, `3.12`, and `type` environments.

This `[tool.<TOOL>]` format is also leveraged to configure other tools not directly related to building. For example, development tools like Black and isort:

TOML `pyproject.toml`

```
...

[tool.black]
line-length = 88

[tool.isort]
profile = "black"
...
```

To see more tools that leverage the `pyproject.toml` file, you can check out the [Awesome pyproject.toml](https://github.com/carlosperate/awesome-pyproject) repository which lists tools that support the `pyproject.toml` file.

Even though having choice between small tools is great, there are some tools that attempt to be one-stop solutions for managing Python projects. These tools aim to simplify the process of managing Python projects and provide a more unified experience. They even provide their own build backend. Some of these tools include:

- [Hatch](https://hatch.pypa.io/latest/) (PyPA project)
- [PDM](https://pdm-project.org/)
- [Poetry](https://python-poetry.org/)
- [uv](https://docs.astral.sh/uv/)

These tools take care of all steps of the development process such as creating a new project, managing dependencies, managing environments, building, and publishing.

The tools listed here use the `pyproject.toml` file for configuration. So even if you don’t want to fully commit, by leveraging the `pyproject.toml` file you can try out these tools now or later without having to fully rewrite your configuration.

Another tool worthy of mention is another PyPA project: [Flit](https://flit.pypa.io/en/stable/). Flit is a minimal and easy-to-use project manager that has straightforward commands to build, install, and publish your package, but isn’t as all-encompassing as something like Poetry.

As you can see, there are many tools available to manage your Python project. The `pyproject.toml` file is a key part of all the tools mentioned in this section, providing a standard way to configure your project and making it easier to switch between tools.

[Remove ads](https://realpython.com/account/join/)

## Building and Distributing Your pyproject.toml Python Project

When it comes time to distribute your Python project, `pyproject.toml` plays a very important role. After all, the `pyproject.toml` file was initially adopted to configure the build process, and it’s the build process that creates the package that you distribute.

For distribution to [PyPI](https://pypi.org/), or any other package index, you’ll want to add some more fields to your `pyproject.toml` file to [configure your package for distribution](https://realpython.com/pypi-publish-python-package/#configure-your-package). These fields will help users understand what your package is about, who maintains it, and how to install it. In some cases, certain fields will also determine how your package is distributed:

TOML `pyproject.toml`

```
[build-system]
requires = ["setuptools"]
build-backend = "setuptools.build_meta"

[project]
name = "snakesay"
version = "1.0.0"
dependencies = ["rich"]
 = [{name = "Jin Doe", email = "jindoe@example.com"}]
keywords = ["CLI", "ASCII Art"]
license = "MIT"
readme = "README.md"
requires-python = ">=3.9"
classifiers = [
    "Development Status :: 3 - Alpha",
    "Intended Audience :: Developers",
    "License :: OSI Approved :: MIT License",
    "Programming Language :: Python :: 3.9",
    "Programming Language :: Python :: 3.10",
    "Programming Language :: Python :: 3.11",
    "Programming Language :: Python :: 3.12",
    "Programming Language :: Python :: 3.13",
    "Topic :: Software Development :: Libraries :: Python Modules",
]

[project.optional-dependencies]
dev = ["black", "isort", "build", "twine"]

[project.scripts]
ssay = "snakesay.__main__:main"

[tool.setuptools.packages.find]
where = ["."]
```

As you can see, there are a few new fields in the `[project]` table. All of these are useful to help users understand your package and to help package indexes categorize your package. The [`classifiers` field](https://pypi.org/classifiers/) is particularly important, as it helps package indices categorize your package.

PyPI even supports a `"Private :: Do Not Upload"` classifier, which will prevent your package from being uploaded to PyPI if you or someone on your team accidentally tries to upload it.

Also, note the inclusion of two new dependencies in the `[project.optional-dependencies]` table. These are [build](https://build.pypa.io/en/stable/) and [Twine](https://twine.readthedocs.io/en/stable/). Both of these are PyPA projects that are the recommended tools for building and uploading packages to PyPI.

The build project provides a build front end that makes it straightforward to build your package, creating both source distributions and wheel distributions. Being a front end, it doesn’t actually build your package, but it provides a consistent interface to build backends like Setuptools.

> [!primary] Primary
> **Note:** A Python build normally results in a couple of formats. Typically, you’ll get a **source distribution** (sdist), and a [wheel](https://realpython.com/python-wheels/), which can be uploaded to the Python Package Index (PyPI) for distribution.
> 
> A source distribution is a minimal standard format for your source code and metadata that make it easy for distribution. Often, it’s essentially a compressed version of your code. A wheel, on the other hand, is a pre-built binary format that simplifies installation. It doesn’t require building on the end user’s machine and can often be faster to install and more secure.
> 
> Wheels are especially useful if your package has [compiled](https://en.wikipedia.org/wiki/Compiler) components in other languages, as they can include these components in the wheel. For example, [NumPy](https://numpy.org/) has components in [C](https://en.wikipedia.org/wiki/C_\(programming_language\)), so distributing it as a wheel precludes the need to compile these components on the end user’s machine.
> 
> Wheels are the recommended format for distribution, though source distributions are still useful for some. Users may want to customize the package for particular build requirements, special environments, or if they want to compile the components themselves.

You’ve configured your project for distribution. To actually build your distributable package with Setuptools and build, you can run the following command:

```
$ python -m build
* Creating isolated environment: venv+pip...
* Installing packages in isolated environment:
  - setuptools
* Getting build dependencies for sdist...
...
* Building wheel from sdist
* Creating isolated environment: venv+pip...
* Installing packages in isolated environment:
  - setuptools
* Getting build dependencies for wheel...
...
Successfully built snakesay-1.0.0.tar.gz and snakesay-1.0.0-py3-none-any.whl
```

You’ll see that a `dist` directory has been created with both a source distribution and a wheel distribution.

> [!primary] Primary
> **Note:** Please don’t pollute the main PyPI instance with test packages!
> 
> If you want to test out uploading packages to PyPI, you can use the [Test PyPI](https://packaging.python.org/guides/using-testpypi/) instance. This is a separate instance of PyPI that you can use to test out uploading packages without affecting the main PyPI instance.

To [upload your package](https://realpython.com/pypi-publish-python-package/#upload-your-package) to PyPI you’ll be using Twine. To upload with Twine, you can run the following command:

```
$ python -m twine upload dist/*
```

This command will upload all the distributions in the `dist` directory to PyPI. You’ll be prompted to enter your PyPI username and password, though this behavior can be [configured](https://twine.readthedocs.io/en/stable/#configuration).

Twine is agnostic to `pyproject.toml` or any other build configuration file as Twine’s only focus is uploading distributions to the PyPI. That is, Twine doesn’t care how you build your package, it just uploads it. Since `pyproject.toml` is used to configure the build process, Twine doesn’t need to know about it.

Congratulations, you’ve managed an entire project lifecycle using only the `pyproject.toml` file to configure it. In the final section, you’ll take a look at the full `pyproject.toml` file example.

## Understanding a Full pyproject.toml Example

Here’s a full example of a `pyproject.toml` file that includes all the fields you’ve seen in this tutorial—plus a few more:

TOML `pyproject.toml`

```
[build-system]
requires = ["setuptools>=75.3.0"]
build-backend = "setuptools.build_meta"

[project]
name = "snakesay"
dependencies = ["rich>=13.9.0"]
 = [{name = "Jin Doe", email = "jindoe@example.com"}]
keywords = ["CLI", "ASCII Art"]
readme = {file = "README.md", content-type = "text/markdown"}
requires-python = ">=3.9"
classifiers = [
    "Development Status :: 3 - Alpha",
    "Intended Audience :: Developers",
    "License :: OSI Approved :: MIT License",
    "Programming Language :: Python :: 3",
    "Programming Language :: Python :: 3.9",
    "Programming Language :: Python :: 3.10",
    "Programming Language :: Python :: 3.11",
    "Programming Language :: Python :: 3.12",
    "Programming Language :: Python :: 3.13",
]
dynamic = ["version"]

[project.urls]
Repository = "https://github.com/me/spam.git"
Issues = "https://github.com/me/spam/issues"

[project.optional-dependencies]
dev = ["black>=24.1.0", "isort>=5.13.0", "build", "twine"]

[project.scripts]
ssay = "snakesay.__main__:main"

[tool.setuptools.packages.find]
where = ["."]

[tool.setuptools.dynamic]
version = {attr = "snakesay.__version__"}

[tool.black]
line-length = 88

[tool.isort]
profile = "black"
```

Feel free to use this example as a starting point for your own projects. You can also check out other project templates such as [Cookiecutter PyPackage](https://github.com/audreyfeldroy/cookiecutter-pypackage) for more inspiration on how to structure your project with `pyproject.toml`.

## Conclusion

In this tutorial, you’ve learned how to manage Python projects with the `pyproject.toml` file. Along the way, you’ve:

- Learned the purpose of the `pyproject.toml` file in Python projects
- Discovered how to **structure** a project with `pyproject.toml`
- **Installed** a project with `pip` using the `pyproject.toml` file
- Configured **executable commands** in the `[project.scripts]` table
- Managed **dependencies** in the `[project]` table
- Added **dynamic metadata** to make your project more flexible
- Included important information for **distribution** in the `[project]` table
- Gained insight into the Python packaging ecosystem including some history and context

With this knowledge, you’re well on your way to managing Python projects with `pyproject.toml` and simplifying your Python project management workflow.

> [!warning] Warning
> **Get Your Code:** [Click here to download the free sample code](https://realpython.com/bonus/python-pyproject-toml-code/) you’ll use to learn how to manage Python projects with pyproject.toml.

## Frequently Asked Questions

Now that you have some experience with using `pyproject.toml` in Python, you can use the questions and answers below to check your understanding and recap what you’ve learned.

These FAQs are related to the most important concepts you’ve covered in this tutorial. Click the *Show/Hide* toggle beside each question to reveal the answer.

You use a `pyproject.toml` file to configure Python projects, specifying build systems, dependencies, and project metadata in a standardized format.

You create a `pyproject.toml` file by placing it at the root of your project and including necessary configuration tables, such as `[build-system]` and `[project]`.

You structure a Python project with a root directory containing essential files like `pyproject.toml`, source code directories, and optional files like `README` and `LICENSE`.

You should include build system requirements, project metadata, dependencies, and optional configurations for scripts and additional tools in your `pyproject.toml` file.

You use `pyproject.toml` for comprehensive project configuration, including dependencies, whereas `requirements.txt` lists only the dependencies.

---

🐍 Python Tricks 💌

Get a short & sweet **Python Trick** delivered to your inbox every couple of days. No spam ever. Unsubscribe any time. Curated by the Real Python team.

![Python Tricks Dictionary Merge](https://realpython.com/static/pytrick-dict-merge.4201a0125a5e.png)

About **Ian Currie**

Ian is a Python nerd who relies on it for work and much enjoyment.

[» More about Ian](https://realpython.com/team/icurrie/)

---

Keep Learning

Related Topics: [intermediate](https://realpython.com/tutorials/intermediate/) [tools](https://realpython.com/tutorials/tools/)

Related Courses:

- [Everyday Project Packaging With pyproject.toml](https://realpython.com/courses/packaging-with-pyproject-toml/?utm_source=realpython&utm_medium=web&utm_campaign=related-course&utm_content=python-pyproject-toml)

Related Tutorials:

- [[Managing Python Projects With UV - An All-in-One Solution]]
- [Python and TOML: Read, Write, and Configure with tomllib](https://realpython.com/python-toml/?utm_source=realpython&utm_medium=web&utm_campaign=related-post&utm_content=python-pyproject-toml)
- [Managing Multiple Python Versions With pyenv](https://realpython.com/intro-to-pyenv/?utm_source=realpython&utm_medium=web&utm_campaign=related-post&utm_content=python-pyproject-toml)
- [Python's pathlib Module: Taming the File System](https://realpython.com/python-pathlib/?utm_source=realpython&utm_medium=web&utm_campaign=related-post&utm_content=python-pyproject-toml)
- [Data Classes in Python (Guide)](https://realpython.com/python-data-classes/?utm_source=realpython&utm_medium=web&utm_campaign=related-post&utm_content=python-pyproject-toml)