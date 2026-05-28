---
title: Python Standard Library – Real Python
source: https://realpython.com/ref/stdlib/functools/
author:
  - "[[Real Python]]"
published: 2026-05-15
created: 2026-05-26
description: Provides higher-order functions and operations on callable objects.
tags:
  - "#glossary"
---
## functools

The Python **`functools`** [module](https://realpython.com/ref/glossary/module/) provides [higher-order functions](https://realpython.com/ref/glossary/higher-order-function/) and tools for working with [callable](https://realpython.com/ref/glossary/callable/) objects.

This module allows you to work with [functions](https://realpython.com/ref/glossary/function/) in a [functional programming](https://realpython.com/ref/glossary/functional-programming/) style, offering utilities that modify or extend the behavior of functions and [methods](https://realpython.com/ref/glossary/method/) in Python.

Here’s an example:

```
Explain
>>> import functools

>>> double = functools.partial(lambda x, y: x * y, y=2)
>>> double(5)
10
```

## Key Features

- Provides tools for creating partial functions
- Supports function memoization with `lru_cache`
- Offers decorators for method caching
- Includes utilities for comparing and ordering

## Frequently Used Classes and Functions

| Object | Type | Description |
| --- | --- | --- |
| [`functools.partial`](https://docs.python.org/3/library/functools.html#functools.partial) | Function | Returns a new callable object that behaves like the original function with specified arguments |
| [`@functools.lru_cache`](https://docs.python.org/3/library/functools.html#functools.lru_cache) | Decorator | Caches function calls with a Least Recently Used (LRU) cache strategy |
| [`functools.reduce()`](https://docs.python.org/3/library/functools.html#functools.reduce) | Function | Performs a cumulative computation on a sequence of elements |
| [`@functools.singledispatch`](https://docs.python.org/3/library/functools.html#functools.singledispatch) | Decorator | Transforms a function into a [single-dispatch](https://docs.python.org/3/glossary.html#term-single-dispatch) [generic function](https://docs.python.org/3/glossary.html#term-generic-function). |

## Examples

Create a partial function that computes powers of `3`:

```
>>> from functools import partial

>>> cube = partial(lambda x, y: x**y, y=3)
>>> cube(4)
64
```

Use `reduce()` to compute the product of a list:

```
>>> from functools import reduce
>>> reduce(lambda x, y: x * y, [1, 2, 3, 4])
24
```

## Common Use Cases

- Creating functions with fixed arguments for repeated use
- Optimizing recursive functions with caching
- Transforming comparison functions for sorting
- Performing cumulative operations on data collections

## Real-World Example

Suppose you have a [recursive](https://realpython.com/ref/glossary/recursion/) function that calculates Fibonacci numbers, and you want to optimize it by using caching to avoid redundant calculations:

```
>>> from functools import lru_cache

>>> @lru_cache(maxsize=128)
... def fibonacci(n):
...     if n < 2:
...         return n
...     return fibonacci(n-1) + fibonacci(n-2)
...

>>> fibonacci(100)
354224848179261915075
```

Here, the `@lru_cache` decorator significantly improves the performance of the Fibonacci function by storing the results of previously computed values, avoiding the need to recompute them.