---
title: Document Your Python Code and Projects With ChatGPT
source: https://realpython.com/document-python-code-with-chatgpt/
author:
  - "[[Real Python]]"
published: 2023-11-08
created: 2026-05-29
description: Good documentation is a critical feature of any successful Python project. In practice, writing documentation is hard and can take a lot of time and effort. Nowadays, with tools like ChatGPT, you can quickly document your Python code and projects.
tags:
  - llm
  - github
  - tools
---
![Document Your Python Code and Projects With ChatGPT](https://realpython.com/cdn-cgi/image/width=1920,format=auto/https://files.realpython.com/media/Documenting-Your-Code-with-the-Help-of-ChatGPT_Watermarked.daa041e7ad32.jpg)

Having good **documentation** is a critical feature of any successful Python project. In practice, writing documentation is hard and can take a lot of time and effort, so some developers don’t like to do it. Luckily, with **large language models** (LLMs) and tools like **ChatGPT**, you can quickly document your Python code and projects.

In Python, you can document your code using **docstrings** and then take advantage of them to enrich the project’s **external documentation**. ChatGPT can be of great help in writing both docstrings and external documentation.

**In this tutorial, you’ll:**

- Build different ChatGPT prompts to generate Python **docstrings**
- Use different **styles** while generating docstrings with ChatGPT
- Add `doctest` **tests** and **usage examples** to Python docstrings
- Create **external documentation**, such as `README` files and tutorials, with ChatGPT

To get the most out of this tutorial, you should have a [ChatGPT account](https://realpython.com/chatgpt-coding-mentor-python/#set-up-your-chatgpt-coding-mentor) and know the basics of interacting with this tool using [prompt engineering](https://realpython.com/practical-prompt-engineering/). You should also know the basics of how to [document Python code](https://realpython.com/documenting-python-code/).

> [!warning] Warning
> **Get Your Code:** [Click here to download free sample code](https://realpython.com/bonus/document-python-code-with-chatgpt-code/) for documenting Python code with ChatGPT.

## Benefits of Using ChatGPT for Documenting Python Code

Having high-quality, up-to-date documentation is critical for any software project. Poor documentation can cause a project to fail or go unnoticed even if the codebase is well written and the project’s main idea is innovative and useful.

Writing good documentation takes considerable time and effort. That’s why using [large language models (LLMs)](https://en.wikipedia.org/wiki/Large_language_model) like [ChatGPT](https://realpython.com/chatgpt-coding-mentor-python/) can be a viable alternative for providing your projects and code with proper documentation.

> [!primary] Primary
> **Note:** Check out [Episode 174: Considering ChatGPT’s Technical Review of a Programming Book](https://realpython.com/podcasts/rpp/174/) of The Real Python Podcast for an interesting conversation about using ChatGPT to run a technical review on existing resources, such as books.

Some of the benefits of ChatGPT for documenting Python code include the following:

- **Increased productivity**: It allows automation of tasks related to code documentation and its maintenance, which saves you considerable time and effort.
- **Improved quality**: It helps ensure that your documentation is accurate, up-to-date, and comprehensive.
- **Enhanced user experience**: It can produce engaging and user-friendly documentation, leading to a better user experience.
- **Reduced costs**: It helps reduce the costs of creating and maintaining documentation.
- **Improved compliance**: It can help ensure that the documentation complies with standards and regulations, making it more consistent and professional.

With ChatGPT, you can generate cool documentation for your Python code in almost no time. In the following sections, you’ll learn the basics of using ChatGPT as an assistant for creating coherent docstrings and user-friendly external documentation for your Python projects.

## Effective ChatGPT Prompts for Writing Docstrings

The primary way to document Python code is through [docstrings](https://realpython.com/documenting-python-code/#docstrings-background). In Python, a **docstring** is typically a triple-quoted string that occupies the first line of [modules](https://realpython.com/python-modules-packages/), [functions](https://realpython.com/defining-your-own-python-function/), [classes](https://realpython.com/python-classes/), and [methods](https://realpython.com/python-classes/#providing-behavior-with-methods). This string has a special meaning for Python, which stores it in an attribute called `.__doc__`.

Many Python tools, including [code editors and IDEs](https://realpython.com/python-ides-code-editors-guide/), take advantage of docstrings to provide real-time help when you’re writing your code. Docstrings are also part of Python’s **built-in help system**, which you can access with the [`help()`](https://docs.python.org/3/library/functions.html#help) function:

```
>>> help(str)

Help on class str in module builtins:

class str(object)
 |  str(object='') -> str
 |  str(bytes_or_buffer[, encoding[, errors]]) -> str
 |
 |  Create a new string object from the given object. If encoding or
 |  errors is specified, then the object must expose a data buffer
 |  that will be decoded using the given encoding and error handler.
 |  Otherwise, returns the result of object.__str__() (if defined)
 |  or repr(object).
 |  encoding defaults to sys.getdefaultencoding().
 |  errors defaults to 'strict'.
 |
 |  Methods defined here:
 |
 |  __add__(self, value, /)
 |      Return self+value.
 |
 |  __contains__(self, key, /)
 |      Return key in self.
...
```

In this example, you call `help()` with the [`str`](https://realpython.com/python-strings/) class as an argument, and you get the class’s documentation page, which includes the class’s docstring:

```
>>> print(str.__doc__)
str(object='') -> str
str(bytes_or_buffer[, encoding[, errors]]) -> str

Create a new string object from the given object. If encoding or
errors is specified, then the object must expose a data buffer
that will be decoded using the given encoding and error handler.
Otherwise, returns the result of object.__str__() (if defined)
or repr(object).
encoding defaults to sys.getdefaultencoding().
errors defaults to 'strict'.
```

In this case, you get the class’s docstring by accessing the `.__doc__` attribute directly on the `str` class. As you can conclude, docstrings add a lot of value to your code. They’re the primary documentation that you and other Python developers will use to learn about any Python object.

You can also take advantage of your code’s docstrings when you’re building project documentation with a tool like [Sphinx](https://realpython.com/courses/python-sphinx/) or [MkDocs](https://realpython.com/python-project-documentation-with-mkdocs/). These tools have plugins and features that allow you to extract the docstrings and make them part of your project’s external documentation, which can save you a lot of time.

Python has well-established conventions for writing good docstrings. Package, module, class, method, and function docstrings all have specific goals and should follow specific guidelines. You can find these guidelines and conventions in [PEP 257](https://peps.python.org/pep-0257/).

> [!primary] Primary
> **Note:** To dive deeper into documenting Python projects, check out [Documenting Python Code: A Complete Guide](https://realpython.com/documenting-python-code/) and [How to Write Docstrings in Python](https://realpython.com/how-to-write-docstrings-in-python/).

Although PEP 257 provides a standard, you’ll actually find a healthy variety of docstring styles across the Python ecosystem. Here are a few common alternatives:

- [Google-style docstrings](https://google.github.io/styleguide/pyguide.html#38-comments-and-docstrings): This style comes from Google, and you’ll find many examples in the company’s open-source projects.
- [NumPy docstring standard](https://numpydoc.readthedocs.io/en/latest/format.html#docstring-standard): This style was developed for the NumPy library, and many other Python projects have adopted it.
- [reStructuredText (RST) or Sphinx docstring format](https://sphinx-rtd-tutorial.readthedocs.io/en/latest/docstrings.html#the-sphinx-docstring-format): This style is based on reStructuredText and comes from Sphinx, which is a useful tool for automating documentation creation.
- [Epytext style](http://epydoc.sourceforge.net/epytext.html): This is a lightweight markup language used to format docstrings, originally created by the [Epydoc](https://epydoc.sourceforge.net/) project.

Each style has its own conventions. Generally, you should choose one style and use it consistently throughout your Python project.

In practice, choosing a docstring style is mostly a matter of personal preference. However, you should also consider the specific needs of your project, including the following characteristics:

- **Your project’s complexity**: If you have a large and complex project, then you may benefit from the Sphinx or NumPy style, which allows for detailed documentation. In contrast, small projects may just require basic documentation, and something like PEP 257 or Google-style docstrings will be okay.
- **Your documentation tools**: If you use something like Sphinx or MkDocs to generate your project’s documentation, then you should use the style that has the best support in your tool of choice.

With this short background on docstrings in Python, you’re ready to start prompting ChatGPT to write some docstrings for you.

### Using the Target Code as Part of Your Prompts

The quickest way to create prompts for writing docstrings is to ==include the target code as part of the prompt itself==. Consider the following example, where you create a prompt for generating the ==docstring of a function== that adds two numbers together:

> **You:** Write a single-line docstring for the following function:
> 
> ```
> def add(a, b):
>     return a + b
> ```
> 
> **ChatGPT:**
> 
> ```
> def add(a, b):
>     """Return the sum of a and b."""
>     return a + b
> ```

In this prompt, you ask ChatGPT to write a single-line docstring for your function. The result is quite straightforward and readable. This type of docstring doesn’t provide detailed information about the [arguments](https://realpython.com/python-optional-arguments/) and the [return](https://realpython.com/python-return-statement/) value of your function.

You can make your prompt a bit more detailed and ask for a [[Documenting Python Code A Complete Guide#Docstring Types|specific document style]]. The following prompts make ChatGPT generate docstrings for your `add()` function using Google, NumPy, and Sphinx styles, respectively:

> **You:** Write a Google-style docstring for the following function:
> 
> ```
> def add(a, b):
>     return a + b
> ```
> 
> **ChatGPT:**
> 
> ```
> def add(a, b):
>     """Sum two numbers.
> 
>     Args:
>         a (int or float): The first number.
>         b (int or float): The second number.
> 
>     Returns:
>         int or float: The sum of the two numbers.
>     """
>     return a + b
> ```
> 
> **You:** Write a NumPy-style docstring for the following function:
> 
> ```
> def add(a, b):
>     return a + b
> ```
> 
> **ChatGPT:**
> 
> ```
> def add(a, b):
>     """
>     Sum two numbers.
> 
>     Parameters
>     ----------
>     a : int or float
>         The first number to be added.
>     b : int or float
>         The second number to be added.
> 
>     Returns
>     -------
>     int or float
>         The sum of a and b.
>     """
>     return a + b
> ```
> 
> **You:** Write a Sphinx-style docstring for the following function:
> 
> ```
> def add(a, b):
>     return a + b
> ```
> 
> **ChatGPT:**
> 
> ```
> def add(a, b):
>     """
>     Calculate the sum of two numbers.
> 
>     :param a: The first number.
>     :type a: int or float
>     :param b: The second number.
>     :type b: int or float
>     :return: The sum of the two numbers.
>     :rtype: int or float
>     """
>     return a + b
> ```

These three docstrings look more complete and polished than the single-line docstring that you saw before. When you add information about the specific style that you want to use, ChatGPT can generate complete docstrings for your function. Of course, the initial result may not be perfect, but it’s a good starting point.

> [!primary] Primary
> **Note:** ChatGPT is pretty good at formatting and styling docstrings. However, you should always cross-reference the corresponding documentation to make sure that the output is completely compliant with the selected style.

The most important point is that you’ve gotten complete docstrings by using a single, short sentence as a prompt. This is an incredible productivity boost for your project.

ChatGPT not only allows you to generate docstrings for functions. It can also take modules, classes, and so on. Here’s a short example of how to generate a docstring for a `Circle` class and its methods:

> **You:** Write NumPy-style docstrings for the following class and its methods:
> 
> ```
> class Circle:
>     def __init__(self, radius):
>         self.radius = radius
> 
>     def calculate_area(self):
>         return round(math.pi * self.radius ** 2, 2)
> ```
> 
> **ChatGPT:**
> 
> ```
> class Circle:
>     """
>     A Circle class to perform some circle-related operations.
> 
>     Parameters
>     ----------
>     radius : float
>         The radius of the circle.
> 
>     Attributes
>     ----------
>     radius : float
>         The radius of the circle.
> 
>     Methods
>     -------
>     calculate_area():
>         Calculates the area of the circle.
>     """
> 
>     def __init__(self, radius):
>         """
>         Constructs all the necessary attributes for the circle object.
> 
>         Parameters
>         ----------
>         radius : float
>             The radius of the circle.
>         """
>         self.radius = radius
> 
>     def calculate_area(self):
>         """
>         Calculate the area of the circle.
> 
>         Returns
>         -------
>         float
>             The area of the circle rounded to 2 decimal places.
>         """
>         return round(math.pi * self.radius ** 2, 2)
> ```

Wow! That was neat! With a single-sentence prompt, you’ve made ChatGPT generate NumPy-style docstrings for your class and all its methods. That’s a great addition to your codebase.

### Including Only Signatures in Your Prompts

Sometimes, you can’t use the target code as part of your prompts. This may be due to privacy requirements, or maybe you just want to keep your company’s code safe. In this scenario, you can create prompts that only use the [signature](https://en.wikipedia.org/wiki/Type_signature) of your classes, methods, and functions.

> [!primary] Primary
> **Note:** There are lots of ongoing lawsuits around ChatGPT’s use of data. In any case, you should check ChatGPT’s [terms of use](https://openai.com/policies/terms-of-use) to make sure the tool is right for you and that you’re using it correctly.

To understand how to create these types of prompts, consider the signature of a function that checks if a number falls within a given interval:

> **You:** Write a Google-style docstring for a function with the following signature:
> 
> ```
> def in_interval(number, start, end):
> ```
> 
> **ChatGPT:**
> 
> ```
> def in_interval(number, start, end):
>     """
>     Checks if a given number is within a specified interval.
> 
>     This function takes three arguments: a number, and the start
>     and end points of an interval.
>     It checks whether the given number falls within the specified
>     interval or not.
> 
>     Args:
>         number (int or float): The number to check.
>         start (int or float): The starting point of the interval.
>         end (int or float): The ending point of the interval.
> 
>     Returns:
>         bool: True if the given number falls within the interval,
>         False otherwise.
> 
>     Raises:
>         ValueError: If the start is larger than the end, or if
>         the number, start, or end are not numbers.
>     """
> ```

In this example, the function’s signature is the only context that you provide to ChatGPT. The LLM is smart enough to examine the function’s name and arguments and generate a suitable docstring for you. Note that having descriptive function and argument names is key in this kind of prompt. Otherwise, the output may not be good enough.

In most cases, adding [type hints](https://realpython.com/python-type-checking/) to the function’s signature will improve the quality of the generated docstring.

### Writing Prompts That Use No Code

You can also craft a prompt by just describing the input and output of your code or by providing a detailed description of what your code does. Again, these types of prompts are useful when you’re not allowed to upload your code as part of your prompt.

To illustrate, here’s a prompt that asks ChatGPT to write a docstring for a function that determines whether an integer number is prime:

> **You:** Write a Google-style docstring for a function that takes an integer as an argument and determines whether it’s a prime number.
> 
> **ChatGPT:**
> 
> ```
> def is_prime_number(n):
>     """
>     Determines if an input integer is a prime number.
> 
>     This function takes an integer as an argument and checks
>     whether it is a prime number. A prime number is a
>     positive natural number greater than 1 that has no positive
>     integer divisors other than 1 and itself.
> 
>     Args:
>         n (int): The integer to check.
> 
>     Returns:
>         bool: True if the input integer is a prime number,
>         False otherwise.
> 
>     Raises:
>         ValueError: If n is less than or equal to 1.
>     """
> ```

This docstring is quite complete and useful. It even includes an explanation of what a prime number is, which is great! You can tweak it further and polish a few details. However, you already have a great starting point.

### Asking for Tests and Usage Examples in Your Prompts

Usage examples are probably the most important part of good software documentation. Through code examples, your users can quickly understand how to use your code and how it works. Often, other developers will scan through your documentation until they find a code example.

So, adding usage examples to your docstrings is a big plus. With ChatGPT, providing usage examples is just a matter of including a short sentence in your prompts. Consider the following prompt and its output:

> **You:** Write a NumPy-style docstring for the following function. Add a section with usage examples as `doctest` tests:
> 
> ```
> def add(a, b):
>  return a + b
> ```
> 
> **ChatGPT:**
> 
> ```
> def add(a, b):
>  """
>  Add two numbers together.
> 
>  This function takes two numbers (either integers or floats)
>  as arguments and returns their sum.
> 
>  Parameters
>  ----------
>  a : int or float
>      The first number to add.
>  b : int or float
>      The second number to add.
> 
>  Returns
>  -------
>  int or float
>      The sum of the two input numbers.
> 
>  Examples
>  --------
>  >>> add(1, 2)
>  3
>  >>> add(5.5, 2.5)
>  8.0
>  >>> add(100, -50)
>  50
>  """
>  return a + b
> ```

The highlighted lines show the usage examples for your function. In the prompt, you instructed ChatGPT to use the [`doctest`](https://realpython.com/python-doctest/) test format for the examples. This will provide two important assets:

1. Usage examples
2. Basic tests for your code

That’s neat! You’ve gotten two benefits in one shot! Your documentation has cool usage examples for your user, and at the same time, it has tests that will help you make your code more robust. You can run these tests using the `doctest` command.

## External Documentation for Your Python Code

Up to this point, you’ve used ChatGPT to help you write docstrings for your Python code. Even though docstrings can be an important part of a project’s documentation, they may not be enough. There might be some aspects in your code that need deeper explanations and detailed examples.

So, if you want to have great documentation that improves users’ engagement with your project, then you need to create other external documentation, such as `README` files, tutorials, and how-to guides.

Creating this type of documentation will take more effort and time than creating docstrings for your code. Fortunately, ChatGPT can help you here too. In the following sections, you’ll explore the basics of using ChatGPT to create external documentation for your Python projects. To kick thing off, you’ll start with `README` files.

### Creating README Files

A `README` file is arguably the most basic piece of external documentation that you’ll ever create for any Python project. You’ll probably find many different recommendations about what to include in your `README` files. In general, the content of this file will depend on your specific project and its main goals.

> [!primary] Primary
> **Note:** To learn more about writing good `README` files, check out [How to write a great README for your GitHub project](https://dbader.org/blog/write-a-great-readme-for-your-github-project).

You can rely on ChatGPT when creating a `README` file for a given project. If you don’t have a clear idea of what to include in this type of file, then you can ask ChatGPT:

> **You:** What are the recommended guidelines for writing a `README` file?
> 
> **ChatGPT:** Writing a good `README` file is important to help users understand the purpose of your project, how to use it, and how to potentially contribute to it. Here are some common sections that are often included in a well-written `README` file:
> 
> 1. **Project Title**: A brief, catchy title at the beginning of the README.
> 2. **Project Description**: A couple of paragraphs describing the project, what it does, and its purpose.
> 3. **Installation and Getting Started**: Detailed instructions on how to install the project and any dependencies, how to set it up, and how to get it running. For a software project, include the necessary command lines.
> 4. **Usage Examples**: Show samples on how to use the project. Code snippets and screenshots can be very useful in this section.
> 5. **Contribution Guidelines**: If your project is open source and you’re accepting contributions, specify how to contribute and submit pull requests to your project. You might include code style preferences, automatic tests they should pass, and so forth.
> 6. **Licenses**: Note the project’s license type.
> 7. **Contact Information**: Provide your contact information or guidelines on how to get support.
> 8. **Credits and Acknowledgements**: Where necessary, give credit to related work or resources you have utilized.
> 
> Keep your `README` clear, concise, and informative. Remember, it is generally the first thing people will see when they visit your project, and it could greatly influence their decision to use or contribute to it.

Of course, this list isn’t complete or definitive. You may need some other sections depending on your specific project. However, the output provides a great starting point for a great `README` file.

Now, you can select the best structure for your file and then create specific prompts for ChatGPT to help you write each section. Start off with the title:

> **You:** Write five engaging titles for the `README` file of a Python project that provides basic math operations.
> 
> **ChatGPT:**
> 
> 1. “Welcome to PyBasicMath: Your One-Stop Solution for Basic Mathematical Operations in Python”
> 2. “PyBasicMath: Simplifying Complex Calculations with Basic Mathematical Functions”
> 3. “Math Made Easy with PyBasicMath: A Complete Python Package for Basic Calculations”
> 4. “Unleash the Power of Mathematics with PyBasicMath: Quick and Efficient Python Math Operations”
> 5. “PyBasicMath: Making Mathematics Approachable for Python Developers of All Levels”

This is a great list of title suggestions. You probably like some of them already, but you can also pick ideas from several of these suggestions and develop a great title yourself. Go ahead and try writing prompts for other sections. You’ll be surprised at how helpful ChatGPT can be.

As an exercise, you can go ahead and write specific prompts to generate the rest of the sections that ChatGPT suggested above.

Asking ChatGPT for help creating the `README` file piece by piece rather than asking it to generate the whole `README` file may be more convenient and effective because you can tweak the prompt to target a specific section.

### Generating Code Explanations

ChatGPT can generate a detailed explanation of how a piece of code works. This possibility opens a great opportunity for you to create external documentation. Here’s a prompt that asks the LLM to explain how a function works:

> **You:** Explain how the following function works:
> 
> ```
> def find_extremes(iterable):
>     data = tuple(iterable)
>     if len(data) == 0:
>         raise ValueError("input iterable must not be empty")
>     return min(data), max(data)
> ```
> 
> **ChatGPT:**
> 
> The `find_extremes(iterable)` function finds the smallest and largest values in an `iterable` such as a list, tuple, or any other Python iterable object. Here’s a step-by-step breakdown:
> 
> 1. `data = tuple(iterable)`: This line of code converts the input iterable into a tuple. Regardless of whether the input is a list, a set, or another type of iterable, by converting it into a tuple, it ensures that the data can be iterated through consistently in the next steps.
> 2. `if len(data) == 0: raise ValueError("input iterable must not be empty")`: If the length of the tuple `data` is zero (i.e., if the input iterable is empty), a `ValueError` exception is raised with the message “input iterable must not be empty”. This acts as a guard clause, preventing the function from proceeding with an empty iterable, which would cause the `min` and `max` functions to also raise a `ValueError`.
> 3. `return min(data), max(data)`: This line uses the built-in Python functions `min` and `max` to find the smallest and largest values in the iterable, respectively. These values are returned as a tuple.
> 
> If the function can compare elements within `data`, it determines the smallest and the largest values. If not (e.g., `iterable` is a complex object that doesn’t implement a comparison operation), the `min` and `max` functions will raise a `TypeError`.
> 
> Overall, this function takes any iterable and returns a tuple representing the smallest and largest values present in the iterable.

ChatGPT’s output is quite detailed and explains how the function works line by line. This piece of explanation will be a great addition to the external documentation of your project. You can use this explanation in a tutorial, a how-to guide, or even in a `README` file if that’s appropriate for the project at hand.

### Creating Usage Examples

You’ve already learned that ChatGPT can generate usage examples as part of your docstrings. It can also generate usage examples that you can then use in a tutorial, a how-to guide, or a `README` file:

> **You:** Write three usage examples for the following function. Add explanations to each example:
> 
> ```
> def is_divisible(a, b):
>     if not a % b:
>         return True
>     return False
> ```
> 
> **ChatGPT:**
> 
> The `is_divisible(a, b)` function checks whether one number (`a`) is completely divisible by another number (`b`). It uses the modulus operator (`%`), which returns the remainder of the division of `a` by `b`. If the remainder is 0, it indicates that `a` is completely divisible by `b`.
> 
> ```
> print(is_divisible(10, 5))  # Returns: True
> ```
> 
> In this example, the function is checking if `10` is divisible by `5`. Since `10` divided by `5` gives a quotient of `2` without any remainder, the function returns `True`.
> 
> ```
> print(is_divisible(17, 3))  # Returns: False
> ```
> 
> In this case, the function is checking if `17` is divisible by `3`. As `17` divided by `3` gives a quotient of `5` and a remainder of `2`, the function returns `False`.
> 
> ```
> print(is_divisible(36, 9))  # Returns: True
> ```
> 
> Here, the function checks whether `36` is divisible by `9`. As `36` divided by `9` gives a quotient of `4` with no remainder, the function returns `True`. It indicates that `36` is completely divisible by `9`.

Note that your prompt includes the specific number of examples that you want. It also asks for individual explanations. You can add more detailed instructions about other aspects of your code as well. For example, you can ask for specific edge cases, like when the second argument is `0`.

Detailed instructions will improve the quality of the generated output and direct the explanation toward specific and important behaviors of your code that can be useful for your users.

### Writing Tutorials and How-to Guides

Now that you’ve used ChatGPT to generate code explanations and usage examples, you can assemble them and develop a tutorial or a how-to guide for your code.

For example, say that you want to create a tutorial about using a Python library that performs basic math calculations. If you’ve used a single ChatGPT thread to generate the code examples and explanations for the library, then the chat has enough context to generate title suggestions, an outline, an introduction, and even a good conclusion.

Here’s a short prompt that asks ChatGPT to generate an outline for a tutorial:

> **You:** Write an outline for a tutorial on a Python library that performs basic math calculations.
> 
> **ChatGPT:**
> 
> Outline for Python Basic Math Library Tutorial
> 
> **Introduction**
> 
> 1. Brief Introduction for the Tutorial
> 2. Understanding the Importance of Mathematics in Programming
> 3. Introducing the Python Basic Math Library:
> 	- What is the Python Basic Math Library?
> 		- What functions does it include?
> 
> **Getting Started**
> 
> 1. Installing the Python Basic Math Library
> 2. Importing the Library into Your Python Project
> 
> **Deep Dive Into Basic Math Functions**
> 
> 1. Addition:
> 	- Syntax and Parameter Information
> 		- Hands-on Example
> 2. Subtraction:
> 	- Syntax and Parameter Information
> 		- Hands-on Example
> 3. Multiplication:
> 	- Syntax and Parameter Information
> 		- Hands-on Example
> 4. Division:
> 	- Syntax and Parameter Information
> 		- Hands-on Example
> 5. Modulus:
> 	- Syntax and Parameter Information
> 		- Hands-on Example
> 6. Power:
> 	- Syntax and Parameter Information
> 		- Hands-on Example
> 7. Square Root:
> 	- Syntax and Parameter Information
> 		- Hands-on Example
> 8. Rounding Numbers:
> 	- Syntax and Parameter Information
> 		- Hands-on Example
> 
> **Advanced Topics**
> 
> 1. Using Multiple Functions Together
> 2. Examples of Real-World Applications using Basic Math Library
> 3. Tracing Errors and Troubleshooting
> 
> **Summary and Next Steps**
> 
> 1. Recap of Key Topics Covered
> 2. Where to Go Next: Other Mathematical Libraries in Python
> 3. Closing Remarks and Encouragement
> 
> Throughout the tutorial, we will be using practical sessions, hands-on exercises, use cases, and quizzes to make the learning process interesting and engaging. By the end of this tutorial, you will be proficient in using the Python Basic Math Library for various math operations.

Now, you can write specific prompts for ChatGPT to generate content for each section. You can also insert the usage examples and the code explanations in the appropriate sections. Go ahead and give it a try!

As you can see, ChatGPT is a great companion when it comes to documenting Python projects. However, before publishing any of the generated content, make sure you vet it all for accuracy and quality.

## Conclusion

Now you know how to leverage the power of tools like ChatGPT to document your code with appropriate docstrings. You also learned how to quickly create external documentation for a Python project with the help of ChatGPT.

**In this tutorial, you’ve learned how to:**

- Write different ChatGPT prompts to generate Python **docstrings** efficiently
- Use different **styles** while generating docstrings with ChatGPT
- Ask ChatGPT to add **`doctest` tests** and **usage examples** to your docstrings
- Build **external documentation** for a Python project with ChatGPT

With these skills, you’re ready to start creating useful and engaging documentation for your Python code and projects.

> [!warning] Warning
> **Get Your Code:** [Click here to download free sample code](https://realpython.com/bonus/document-python-code-with-chatgpt-code/) for documenting Python code with ChatGPT.

🐍 Python Tricks 💌

Get a short & sweet **Python Trick** delivered to your inbox every couple of days. No spam ever. Unsubscribe any time. Curated by the Real Python team.

![Python Tricks Dictionary Merge](https://realpython.com/static/pytrick-dict-merge.4201a0125a5e.png)

About **Leodanis Pozo Ramos**

Leodanis is a self-taught Python developer, educator, and technical writer with over 10 years of experience.

[» More about Leodanis](https://realpython.com/team/lpozoramos/)

---
