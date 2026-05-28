---
title: "Python's filter(): Extract Values From Iterables"
source: https://realpython.com/python-filter-function/
author:
  - "[[Real Python]]"
published: 2021-06-09
created: 2026-05-26
description: In this step-by-step tutorial, you'll learn how Python's filter() works and how to use it effectively in your programs. You'll also learn how to use list comprehension and generator expressions to replace filter() and make your code more Pythonic.
tags:
  - intermediate
  - best-practices
---
![Python's filter(): Extract Values From Iterables](https://realpython.com/cdn-cgi/image/width=1920,format=auto/https://files.realpython.com/media/How-to-Use-Pythons-filter__Watermarked.4234700cc1c3.jpg)

### Python's filter(): Extract Values From Iterables

Python’s [`filter()`](https://docs.python.org/3/library/functions.html#filter) is a built-in function that allows you to process an iterable and extract those items that satisfy a given condition. This process is commonly known as a **filtering** operation. With `filter()`, you can apply a **filtering function** to an iterable and produce a new iterable with the items that satisfy the condition at hand. In Python, `filter()` is one of the tools you can use for [functional programming](https://realpython.com/python-functional-programming/).

**In this tutorial, you’ll learn how to:**

- Use Python’s **`filter()`** in your code
- Extract **needed values** from your iterables
- Combine `filter()` with other **functional tools**
- **Replace** `filter()` with more **Pythonic** tools

With this knowledge, you’ll be able to use `filter()` effectively in your code. Alternatively, you have the choice of using [list comprehensions](https://realpython.com/list-comprehension-python/) or [generator expressions](https://realpython.com/introduction-to-python-generators/#building-generators-with-generator-expressions) to write more [Pythonic](https://realpython.com/learning-paths/writing-pythonic-code/) and readable code.

To better understand `filter()`, it would be helpful for you to have some previous knowledge on [iterables](https://realpython.com/python-iterators-iterables/#getting-to-know-python-iterables), [`for` loops](https://realpython.com/python-for-loop/), [functions](https://realpython.com/defining-your-own-python-function/), and [`lambda` functions](https://realpython.com/python-lambda/).

> [!warning] Warning
> **Free Bonus:** [5 Thoughts On Python Mastery](https://realpython.com/bonus/python-mastery-course/), a free course for Python developers that shows you the roadmap and the mindset you’ll need to take your Python skills to the next level.

## Coding With Functional Style in Python

==**Functional programming**== is a paradigm that promotes using functions to perform almost every task in a program. A pure functional style relies on functions that don’t modify their input arguments and don’t change the program’s state. They just take a specific set of arguments and [return](https://realpython.com/python-return-statement/) the same result every time. These kinds of functions are known as [pure functions](https://en.wikipedia.org/wiki/Pure_function).

In functional programming, functions often operate on arrays of data, transform them, and produce new arrays with added features. There are three fundamental operations in functional programming:

1. [Mapping](https://en.wikipedia.org/wiki/Map_\(higher-order_function\)) applies a transformation function to an iterable and produces a new iterable of transformed items.
2. [Filtering](https://en.wikipedia.org/wiki/Filter_\(higher-order_function\)) applies a [predicate, or Boolean-valued, function](https://en.wikipedia.org/wiki/Boolean-valued_function) to an iterable and generates a new iterable containing the items that satisfy the [Boolean](https://realpython.com/python-boolean/) condition.
3. [Reducing](https://en.wikipedia.org/wiki/Fold_\(higher-order_function\)) applies a reduction function to an iterable and returns a single cumulative value.

Python [isn’t heavily influenced by functional languages](https://web.archive.org/web/20161104183819/http://python-history.blogspot.com.br/2009/04/origins-of-pythons-functional-features.html) but by [imperative](https://en.wikipedia.org/wiki/Imperative_programming) ones. However, it provides several features that allow you to use a functional style:

- [Anonymous functions](https://realpython.com/python-lambda/)
- A [`map()`](https://realpython.com/python-map-function/) function
- A [`filter()`](https://docs.python.org/3/library/functions.html#filter) function
- A [`reduce()`](https://realpython.com/python-reduce-function/) function

Functions in Python are [first-class objects](https://realpython.com/primer-on-python-decorators/#first-class-objects), which means that you can pass them around as you’d do with any other object. You can also use them as arguments and return values of other functions. Functions that accept other functions as arguments or that return functions (or both) are known as [higher-order functions](https://en.wikipedia.org/wiki/Higher-order_function), which are also a desirable feature in functional programming.

In this tutorial, you’ll learn about `filter()`. This built-in function is one of the more popular functional tools of Python.

## Understanding the Filtering Problem

Say you need to process a [list](https://realpython.com/python-list/) of [numbers](https://realpython.com/python-numbers/) and return a new list containing only those numbers greater than `0`. A quick way to approach this problem is to use a `for` loop like this:

```
>>> numbers = [-2, -1, 0, 1, 2]

>>> def extract_positive(numbers):
...     positive_numbers = []
...     for number in numbers:
...         if number > 0:  # Filtering condition
...             positive_numbers.append(number)
...     return positive_numbers
...

>>> extract_positive(numbers)
[1, 2]
```

The loop in `extract_positive()` iterates through `numbers` and stores every number greater than `0` in `positive_numbers`. The [conditional statement](https://realpython.com/python-conditional-statements/) *filters out* the negative numbers and `0`. This kind of functionality is known as a **filtering**.

Filtering operations consist of testing each value in an iterable with a [predicate](https://en.wikipedia.org/wiki/Predicate_\(mathematical_logic\)) function and retaining only those values for which the function produces a true result. Filtering operations are fairly common in programming, so most programming languages provide tools to approach them. In the next section, you’ll learn about Python’s way to filter iterables.

## Getting Started With Python’s filter()

Python provides a convenient built-in function, `filter()`, that abstracts out the logic behind filtering operations. Here’s its signature:

```
filter(function, iterable)
```

The first argument, `function`, must be a single-argument function. Typically, you provide a predicate (Boolean-valued) function to this argument. In other words, you provide a function that returns either `True` or `False` according to a specific condition.

This `function` plays the role of a **decision function**, also known as a **filtering function**, because it provides the criteria to filter out unwanted values from the input iterable and to keep those values that you want in the resulting iterable. Note that the term **unwanted values** refers to those values that evaluate to false when `filter()` processes them using `function`.

> [!primary] Primary
> **Note:** The first argument to `filter()` is a **function object**, which means that you need to pass a function without calling it with a pair of parentheses.

The second argument, `iterable`, can hold any Python iterable, such as a [list, tuple](https://realpython.com/python-lists-tuples/), or [set](https://realpython.com/python-sets/). It can also hold generator and iterator objects. An important point regarding `filter()` is that it accepts only one `iterable`.

To perform the filtering process, `filter()` applies `function` to every item of `iterable` in a loop. The result is an iterator that yields the values of `iterable` for which `function` returns a true value. The process doesn’t modify the original input iterable.

Since `filter()` is written in [C](https://github.com/python/cpython/blob/master/Python/bltinmodule.c) and is highly optimized, its internal implicit loop can be more efficient than a regular `for` loop regarding execution time. This efficiency is arguably the most important advantage of using the function in Python.

A second advantage of using `filter()` over a loop is that it returns a `filter` object, which is an iterator that yields values on demand, promoting a [lazy evaluation](https://en.wikipedia.org/wiki/Lazy_evaluation) strategy. Returning an iterator makes `filter()` more memory efficient than an equivalent `for` loop.

> [!primary] Primary
> **Note:** In Python 2.x, [`filter()`](https://docs.python.org/2/library/functions.html#filter) returns `list` objects. This behavior changed in [Python 3.x](https://docs.python.org/3/whatsnew/3.0.html#views-and-iterators-instead-of-lists). Now the function returns a `filter` object, which is an iterator that yields items on demand. Python iterators are well known to be memory efficient.

In your example about positive numbers, you can use `filter()` along with a convenient predicate function to extract the desired numbers. To code the predicate, you can use either a `lambda` or a user-defined function:

```
>>> numbers = [-2, -1, 0, 1, 2]

>>> # Using a lambda function
>>> positive_numbers = filter(lambda n: n > 0, numbers)
>>> positive_numbers
<filter object at 0x7f3632683610>
>>> list(positive_numbers)
[1, 2]

>>> # Using a user-defined function
>>> def is_positive(n):
...     return n > 0
...
>>> list(filter(is_positive, numbers))
[1, 2]
```

In the first example, you use a `lambda` function that provides the filtering functionality. The call to `filter()` applies that `lambda` function to every value in `numbers` and filters out the negative numbers and `0`. Since `filter()` returns an iterator, you need to call `list()` to consume the iterator and create the final list.

> [!primary] Primary
> **Note:** Since `filter()` is a built-in function, you don’t have to [import](https://realpython.com/python-import/) anything to be able to use it in your code.

In the second example, you write `is_positive()` to take a number as an argument and return `True` if the number is greater than `0`. Otherwise, it returns `False`. The call to `filter()` applies `is_positive()` to every value in `numbers`, filtering out the negative numbers. This solution is way more readable than its `lambda` equivalent.

In practice, `filter()` isn’t limited to Boolean functions such as those in the examples above. You can use other types of functions, and `filter()` will evaluate their return value for truthiness:

```
>>> def identity(x):
...     return x
...

>>> identity(42)
42

>>> objects = [0, 1, [], 4, 5, "", None, 8]
>>> list(filter(identity, objects))
[1, 4, 5, 8]
```

In this example, the filtering function, `identity()`, doesn’t return `True` or `False` explicitly but the same argument it takes. Since `0`, `[]`, `""`, and [`None`](https://realpython.com/null-in-python/) are falsy, `filter()` uses their **truth value** to filter them out. The final list contains only those values that are truthy in Python.

> [!primary] Primary
> **Note:** Python follows a set of rules to determine an object’s truth value.
> 
> For example, the following [objects are falsy](https://docs.python.org/3/library/stdtypes.html#truth-value-testing):
> 
> - Constants like [`None`](https://realpython.com/null-in-python/) and `False`
> - Numeric types with a zero value, like `0`, `0.0`, `0j`, [`Decimal(0)`](https://docs.python.org/3/library/decimal.html#decimal.Decimal), and [`Fraction(0, 1)`](https://docs.python.org/3/library/fractions.html#fractions.Fraction)
> - Empty sequences and collections, like `""`, `()`, `[]`, `{}`, [`set()`](https://realpython.com/python-sets/), and `range(0)`
> - Objects that implement [`__bool__()`](https://docs.python.org/3/reference/datamodel.html#object.__bool__) with a return value of `False` or [`__len__()`](https://docs.python.org/3/reference/datamodel.html#object.__len__) with a return value of `0`
> 
> Any other object will be considered truthy.

Finally, if you pass `None` to `function`, then `filter()` uses the **identity function** and yields all the elements of `iterable` that evaluate to `True`:

```
>>> objects = [0, 1, [], 4, 5, "", None, 8]

>>> list(filter(None, objects))
[1, 4, 5, 8]
```

In this case, `filter()` tests every item in the input iterable using the Python rules you saw before. Then it yields those items that evaluate to `True`.

So far, you’ve learned the basics of `filter()` and how it works. In the following sections, you’ll learn how to use `filter()` to process iterables and throw away unwanted values without a loop.

[Remove ads](https://realpython.com/account/join/)

## Filtering Iterables With filter()

The job of `filter()` is to apply a decision function to each value in an input iterable and return a new iterable with those items that pass the test. The following sections provide some practical examples so you can get up and running with `filter()`.

### Extracting Even Numbers

As a first example, say you need to process a list of integer numbers and build a new list containing the even numbers. Your first approach to this problem might be to use a `for` loop like this:

```
>>> numbers = [1, 3, 10, 45, 6, 50]

>>> def extract_even(numbers):
...     even_numbers = []
...     for number in numbers:
...         if number % 2 == 0:  # Filtering condition
...             even_numbers.append(number)
...     return even_numbers
...

>>> extract_even(numbers)
[10, 6, 50]
```

Here, `extract_even()` takes an iterable of integer numbers and returns a list containing only those that are even. The conditional statement plays the role of a filter that tests every number to find out if it’s even or not.

When you run into code like this, you can extract the filtering logic into a small predicate function and use it with `filter()`. This way, you can perform the same computation without using an explicit loop:

```
>>> numbers = [1, 3, 10, 45, 6, 50]

>>> def is_even(number):
...     return number % 2 == 0  # Filtering condition
...

>>> list(filter(is_even, numbers))
[10, 6, 50]
```

Here, `is_even()` takes an integer and returns `True` if it’s even and `False` otherwise. The call to `filter()` does the hard work and filters out the odd numbers. As a result, you get a list of the even numbers. This code is shorter and more efficient than its equivalent `for` loop.

### Finding Prime Numbers

Another interesting example might be to extract all the [prime numbers](https://en.wikipedia.org/wiki/Prime_number) in a given interval. To do that, you can start by coding a predicate function that takes an integer as an argument and returns `True` if the number is prime and `False` otherwise. Here’s how you can do that:

```
>>> import math

>>> def is_prime(n):
...     if n <= 1:
...         return False
...     for i in range(2, int(math.sqrt(n)) + 1):
...         if n % i == 0:
...             return False
...     return True
...

>>> is_prime(5)
True
>>> is_prime(12)
False
```

The filtering logic is now in `is_prime()`. The function iterates through the integers between `2` and the [square root](https://realpython.com/python-square-root-function/) of `n`. Inside the loop, the [conditional statement](https://realpython.com/python-conditional-statements/) checks if the current number is divisible by any other in the interval. If so, then the function returns `False` because the number isn’t prime. Otherwise, it returns `True` to signal that the input number is prime.

With `is_prime()` in place and tested, you can use `filter()` to extract prime numbers from an interval like this:

```
>>> list(filter(is_prime, range(1, 51)))
[2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47]
```

This call to `filter()` extracts all the prime numbers in the range between `1` and `50`. The algorithm used in `is_prime()` comes from Wikipedia’s article about [primality tests](https://en.wikipedia.org/wiki/Primality_test#Simple_methods). You can check out that article if you need more efficient approaches.

### Removing Outliers in a Sample

When you’re trying to [describe and summarize a sample of data](https://realpython.com/python-statistics/), you probably start by finding its mean, or average. The mean is a quite popular [central tendency](https://en.wikipedia.org/wiki/Central_tendency) measurement and is often the first approach to analyzing a dataset. It gives you a quick idea of the center, or **location**, of the data.

In some cases, the mean isn’t a good enough central tendency measure for a given sample. [Outliers](https://realpython.com/python-statistics/#outliers) are one of the elements that affect how accurate the mean is. Outliers are [data points](https://en.wikipedia.org/wiki/Data_point) that differ significantly from other observations in a sample or population. Other than that, there is no unique mathematical definition for them in statistics.

However, in [normally distributed](https://en.wikipedia.org/wiki/Normal_distribution) samples, outliers are often defined as data points that lie more than two [standard deviations](https://en.wikipedia.org/wiki/Standard_deviation) from the sample mean.

Now suppose you have a normally distributed sample with some outliers that are affecting the mean accuracy. You’ve studied the outliers, and you know they’re incorrect data points. Here’s how you can use a couple of functions from the [`statistics`](https://docs.python.org/3/library/statistics.html#module-statistics) module along with `filter()` to clean up your data:

```
>>> import statistics as st
>>> sample = [10, 8, 10, 8, 2, 7, 9, 3, 34, 9, 5, 9, 25]

>>> # The mean before removing outliers
>>> mean = st.mean(sample)
>>> mean
10.692307692307692

>>> stdev = st.stdev(sample)
>>> low = mean - 2 * stdev
>>> high = mean + 2 * stdev

>>> clean_sample = list(filter(lambda x: low <= x <= high, sample))
>>> clean_sample
[10, 8, 10, 8, 2, 7, 9, 3, 9, 5, 9, 25]

>>> # The mean after removing outliers
>>> st.mean(clean_sample)
8.75
```

In the highlighted line, the `lambda` function returns `True` if a given data point lies between the mean and two standard deviations. Otherwise, it returns `False`. When you filter the `sample` with this function, `34` is excluded. After this cleanup, the mean of the sample has a significantly different value.

[Remove ads](https://realpython.com/account/join/)

### Validating Python Identifiers

You can also use `filter()` with iterables containing nonnumeric data. For example, say you need to process a list of [strings](https://realpython.com/python-strings/) and extract those that are valid Python [identifiers](https://docs.python.org/3/reference/lexical_analysis.html#identifiers). After doing some research, you find out that Python’s [`str`](https://docs.python.org/3/library/stdtypes.html#str) provides a method called [`.isidentifier()`](https://docs.python.org/3/library/stdtypes.html#str.isidentifier) that can help you out with that validation.

Here’s how you can use `filter()` along with `str.isidentifier()` to quickly validate identifiers:

```
>>> words = ["variable", "file#", "header", "_non_public", "123Class"]

>>> list(filter(str.isidentifier, words))
['variable', 'header', '_non_public']
```

In this case, `filter()` runs `.isidentifier()` on every string in `words`. If the string is a valid Python identifier, then it’s included in the final result. Otherwise, the word is filtered out. Note that you need to use `str` to access `.isidentifier()` in the call to `filter()`.

> [!primary] Primary
> **Note:** Besides `.isidentifier()`, `str` provides a rich set of `.is*()` [methods](https://docs.python.org/3/library/stdtypes.html#string-methods) that can be useful for filtering iterables of strings.

Finally, an interesting exercise might be to take the example further and check if the identifier is also a [keyword](https://realpython.com/python-keywords/). Go ahead and give it a try! Hint: you can use [`.kwlist`](https://docs.python.org/3/library/keyword.html#keyword.kwlist) from the [`keyword`](https://docs.python.org/3/library/keyword.html#module-keyword) module.

### Finding Palindrome Words

An exercise that often arises when you’re getting familiar with Python strings is to find [palindrome words](https://en.wikipedia.org/wiki/Palindrome) in a list of strings. A palindrome word reads the same backward as forward. Typical examples are “madam” and “racecar.”

To solve this problem, you’ll start by coding a predicate function that takes a string and checks if it reads the same in both directions, backward and forward. Here’s a possible implementation:

```
>>> def is_palindrome(word):
...     reversed_word = "".join(reversed(word))
...     return word.lower() == reversed_word.lower()
...

>>> is_palindrome("Racecar")
True
>>> is_palindrome("Python")
False
```

In `is_palindrome()`, you first reverse the original `word` and store it in `reversed_word`. Then you return the result of comparing both words for equality. In this case, you use `.lower()` to prevent case-related differences. If you call the function with a palindrome word, then you get `True`. Otherwise, you get `False`.

You already have a working predicate function to identify palindrome words. Here’s how you can use `filter()` to do the hard work:

```
>>> words = ("filter", "Ana", "hello", "world", "madam", "racecar")

>>> list(filter(is_palindrome, words))
['Ana', 'madam', 'racecar']
```

Cool! Your combination of `filter()` and `is_palindrome()` works properly. It’s also concise, readable, and efficient. Good job!

## Combining filter() With Other Functional Tools

So far, you’ve learned how to use `filter()` to run different filtering operations on iterables. In practice, you can combine `filter()` with other functional tools to perform many different tasks on iterables without using explicit loops. In the next two sections, you’ll learn the basics of using `filter()` along with [`map()`](https://realpython.com/python-map-function/) and [`reduce()`](https://realpython.com/python-reduce-function/).

### The Square of Even Numbers: filter() and map()

Sometimes you need to take an iterable, process each of its items with a **transformation function**, and produce a new iterable with the resulting items. In that case, you can use `map()`. The function has the following signature:

```
map(function, iterable[, iterable1, ..., iterableN])
```

The arguments work like this:

1. **`function`** holds the transformation function. This function should take as many arguments as iterables you pass into `map()`.
2. **`iterable`** holds a Python iterable. Note that you can provide several iterables to `map()`, but that’s optional.

`map()` applies `function` to each item in `iterable` to transform it into a different value with additional features. Then `map()` yields each transformed item on demand.

To illustrate how you can use `filter()` along with `map()`, say you need to compute the square value of all the even numbers in a given list. In that case, you can use `filter()` to extract the even numbers and then `map()` to calculate the square values:

```
>>> numbers = [1, 3, 10, 45, 6, 50]

>>> def is_even(number):
...     return number % 2 == 0
...

>>> even_numbers = list(filter(is_even, numbers))
>>> even_numbers
[10, 6, 50]

>>> list(map(lambda n: n ** 2, even_numbers))
[100, 36, 2500]

>>> list(map(lambda n: n ** 2, filter(is_even, numbers)))
[100, 36, 2500]
```

First, you get the even numbers using `filter()` and `is_even()` just like you’ve done so far. Then you call `map()` with a `lambda` function that takes a number and returns its square value. The call to `map()` applies the `lambda` function to each number in `even_numbers`, so you get a list of square even numbers. The final example shows how to combine `filter()` and `map()` in a single expression.

[Remove ads](https://realpython.com/account/join/)

### The Sum of Even Numbers: filter() and reduce()

Another functional programming tool in Python is `reduce()`. Unlike `filter()` and `map()`, which are still built-in functions, `reduce()` was moved to the [`functools`](https://docs.python.org/3/library/functools.html#module-functools) module. This function is useful when you need to apply a function to an iterable and reduce it to a single cumulative value. This kind of operation is commonly known as a [reduction or folding](https://en.wikipedia.org/wiki/Fold_\(higher-order_function\)).

The signature of `reduce()` is like this:

```
reduce(function, iterable, initial)
```

Here’s what the arguments mean:

1. **`function`** holds any Python callable that accepts two arguments and returns a single value.
2. **`iterable`** holds any Python iterable.
3. **`initial`** holds a value that serves as a starting point for the first partial computation or reduction. It’s an optional argument.

A call to `reduce()` starts by applying `function` to the first two items in `iterable`. This way, it computes the first cumulative result, called an **accumulator**. Then `reduce()` uses the accumulator and the third item in `iterable` to compute the next cumulative result. The process continues until the function returns with a single value.

If you supply a value to `initial`, then `reduce()` runs the first partial computation using `initial` and the first item of `iterable`.

Here’s an example that combines `filter()` and `reduce()` to cumulatively calculate the total sum of all the even numbers in a list:

```
>>> from functools import reduce
>>> numbers = [1, 3, 10, 45, 6, 50]

>>> def is_even(number):
...     return number % 2 == 0
...

>>> even_numbers = list(filter(is_even, numbers))
>>> reduce(lambda a, b: a + b, even_numbers)
66

>>> reduce(lambda a, b: a + b, filter(is_even, numbers))
66
```

Here, the first call to `reduce()` computes the sum of all the even numbers that `filter()` provides. To do that, `reduce()` uses a `lambda` function that adds two numbers at a time.

The final example shows how to chain `filter()` and `reduce()` to produce the same result you got before.

## Filtering Iterables With filterfalse()

In [`itertools`](https://realpython.com/python-itertools/), you’ll find a function called [`filterfalse()`](https://docs.python.org/3/library/itertools.html#itertools.filterfalse) that does the inverse of `filter()`. It takes an iterable as argument and returns a new iterator that yields the items for which the decision function returns a false result. If you use `None` as the first argument to `filterfalse()`, then you get the items that are falsy.

The point of having the `filterfalse()` function is to promote **code reuse**. If you already have a decision function in place, then you can use it with `filterfalse()` to get the rejected items. This saves you from coding an inverse decision function.

In the following sections, you’ll code some examples that show how you can take advantage of `filterfalse()` to reuse existing decision functions and continue doing some filtering.

### Extracting Odd Numbers

You already coded a predicate function called `is_even()` to check if a number is even or not. With that function and the help of `filterfalse()`, you can build an iterator that yields odd numbers without having to code an `is_odd()` function:

```
>>> from itertools import filterfalse
>>> numbers = [1, 3, 10, 45, 6, 50]

>>> def is_even(number):
...     return number % 2 == 0
...

>>> list(filterfalse(is_even, numbers))
[1, 3, 45]
```

In this example, `filterfalse()` returns an iterator that yields the odd numbers from the input iterator. Note that the call to `filterfalse()` is straightforward and readable.

### Filtering Out NaN Values

Sometimes when you’re working with [floating-point arithmetic](https://en.wikipedia.org/wiki/Floating-point_arithmetic), you can face the issue of having [NaN (not a number)](https://en.wikipedia.org/wiki/NaN) values. For example, say you’re calculating the mean of a sample of data that contains NaN values. If you use Python’s `statistics` module for this computation, then you get the following result:

```
>>> import statistics as st

>>> sample = [10.1, 8.3, 10.4, 8.8, float("nan"), 7.2, float("nan")]
>>> st.mean(sample)
nan
```

In this example, the call to `mean()` returns `nan`, which isn’t the most informative value you can get. NaN values can have different origins. They can be due to invalid inputs, corrupted data, and so on. You should find the right strategy to deal with them in your applications. One alternative might be to remove them from your data.

The [`math` module](https://realpython.com/python-math-module/) provides a convenient function called [`isnan()`](https://docs.python.org/3/library/math.html#math.isnan) that can help you out with this problem. The function takes a number `x` as an argument and returns `True` if `x` is a NaN and `False` otherwise. You can use this function to provide the filtering criteria in a `filterfalse()` call:

```
>>> import math
>>> import statistics as st
>>> from itertools import filterfalse

>>> sample = [10.1, 8.3, 10.4, 8.8, float("nan"), 7.2, float("nan")]

>>> st.mean(filterfalse(math.isnan, sample))
8.96
```

Using `math.isnan()` along with `filterfalse()` allows you to exclude all the NaN values from the mean computation. Note that after the filtering, the call to `mean()` returns a value that provides a better description of your sample data.

## Coding With Pythonic Style

Even though `map()`, `filter()`, and `reduce()` have been around for a long time in the Python ecosystem, **list comprehensions** and **generator expressions** have become strong and Pythonic competitors in almost every use case.

The functionality these functions provide is almost always more explicitly expressed using a generator expression or a list comprehension. In the following two sections, you’ll learn how to replace a call to `filter()` with a list comprehension or a generator expression. This replacement will make your code more Pythonic.

### Replacing filter() With a List Comprehension

You can use the following pattern to quickly replace a call to `filter()` with an equivalent list comprehension:

```
# Generating a list with filter()
list(filter(function, iterable))

# Generating a list with a list comprehension
[item for item in iterable if function(item)]
```

In both cases, the final purpose is to create a list object. The list comprehension approach is more explicit than its equivalent `filter()` construct. A quick read through the comprehension reveals the iteration and also the filtering functionality in the `if` clause.

Using list comprehensions instead of `filter()` is probably the path most Python developers take nowadays. However, list comprehensions have some drawbacks compared to `filter()`. The most notable one is the lack of lazy evaluation. Also, when developers start reading code that uses `filter()`, they immediately know that the code is performing filtering operations. However, that’s not so evident in code that uses list comprehensions with the same goal.

A detail to notice when turning a `filter()` construct into a list comprehension is that if you pass `None` to the first argument of `filter()`, then the equivalent list comprehension looks like this:

```
# Generating a list with filter() and None
list(filter(None, iterable))

# Equivalent list comprehension
[item for item in iterable if item]
```

In this case, the `if` clause in the list comprehension tests `item` for its truth value. This test follows the standard Python rules about truth values you already saw.

Here’s an example of replacing `filter()` with a list comprehension to build a list of even numbers:

```
>>> numbers = [1, 3, 10, 45, 6, 50]

>>> # Filtering function
>>> def is_even(x):
...     return x % 2 == 0
...

>>> # Use filter()
>>> list(filter(is_even, numbers))
[10, 6, 50]

>>> # Use a list comprehension
>>> [number for number in numbers if is_even(number)]
[10, 6, 50]
```

In this example, you can see that the list comprehension variant is more explicit. It reads almost like plain English. The list comprehension solution also avoids having to call `list()` to build the final list.

[Remove ads](https://realpython.com/account/join/)

### Replacing filter() With a Generator Expression

The natural replacement for `filter()` is a **generator expression**. That’s because `filter()` returns an iterator that yields items on demand just like a generator expression does. Python iterators are known to be memory efficient. That’s why `filter()` now returns an iterator instead of a list.

Here’s how you can use generator expressions to write the example in the above section:

```
>>> numbers = [1, 3, 10, 45, 6, 50]

>>> # Filtering function
>>> def is_even(x):
...     return x % 2 == 0
...

>>> # Use filter()
>>> even_numbers = filter(is_even, numbers)
>>> even_numbers
<filter object at 0x7f58691de4c0>
>>> list(even_numbers)
[10, 6, 50]

>>> # Use a generator expression
>>> even_numbers = (number for number in numbers if is_even(number))
>>> even_numbers
<generator object <genexpr> at 0x7f586ade04a0>
>>> list(even_numbers)
[10, 6, 50]
```

A generator expression is as efficient as a call to `filter()` in terms of memory consumption. Both tools return iterators that yield items on demand. Using either one might be a question of taste, convenience, or style. So, you’re in charge!

## Conclusion

Python’s `filter()` allows you to perform **filtering** operations on iterables. This kind of operation consists of applying a **Boolean function** to the items in an iterable and keeping only those values for which the function returns a true result. In general, you can use `filter()` to process existing iterables and produce new iterables containing the values that you currently need.

**In this tutorial, you learned how to:**

- Work with Python’s **`filter()`**
- Use `filter()` to **process iterables** and keep the values you need
- Combine `filter()` with **`map()`** and **`reduce()`** to approach different problems
- Replace `filter()` with **list comprehensions** and **generator expressions**

With this new knowledge, you can now use `filter()` in your code to give it a [functional style](https://realpython.com/learning-paths/functional-programming/). You can also switch to a more Pythonic style and replace `filter()` with [list comprehensions](https://realpython.com/list-comprehension-python/) or [generator expressions](https://realpython.com/introduction-to-python-generators/#building-generators-with-generator-expressions).

🐍 Python Tricks 💌

Get a short & sweet **Python Trick** delivered to your inbox every couple of days. No spam ever. Unsubscribe any time. Curated by the Real Python team.

![Python Tricks Dictionary Merge](https://realpython.com/static/pytrick-dict-merge.4201a0125a5e.png)

About **Leodanis Pozo Ramos**

Leodanis is a self-taught Python developer, educator, and technical writer with over 10 years of experience.

[» More about Leodanis](https://realpython.com/team/lpozoramos/)

---

*Each tutorial at Real Python is created by a team of developers so that it meets our high quality standards. The team members who worked on this tutorial are:*[Joanna](https://realpython.com/team/jjablonski/)[Jacob](https://realpython.com/team/jschmitt/)

Master Real-World Python Skills With Unlimited Access to Real Python

![Locked learning resources](https://realpython.com/static/videos/lesson-locked.f5105cfd26db.svg)

**Join us and get access to thousands of tutorials, hands-on video courses, and a community of expert Pythonistas:**

Master Real-World Python Skills  
With Unlimited Access to Real Python

![Locked learning resources](https://realpython.com/static/videos/lesson-locked.f5105cfd26db.svg)

**Join us and get access to thousands of tutorials, hands-on video courses, and a community of expert Pythonistas:**

Keep Learning

Related Topics: [intermediate](https://realpython.com/tutorials/intermediate/) [best-practices](https://realpython.com/tutorials/best-practices/) [python](https://realpython.com/tutorials/python/)

Related Learning Paths:

- [Functional Programming With Python](https://realpython.com/learning-paths/functional-programming/?utm_source=realpython&utm_medium=web&utm_campaign=related-learning-path&utm_content=python-filter-function)

Related Courses:

- [Filtering Iterables With Python](https://realpython.com/courses/python-filter-function/?utm_source=realpython&utm_medium=web&utm_campaign=related-course&utm_content=python-filter-function)

Related Tutorials:

- [Python's reduce(): From Functional to Pythonic Style](https://realpython.com/python-reduce-function/?utm_source=realpython&utm_medium=web&utm_campaign=related-post&utm_content=python-filter-function)
- [Python's map(): Processing Iterables Without a Loop](https://realpython.com/python-map-function/?utm_source=realpython&utm_medium=web&utm_campaign=related-post&utm_content=python-filter-function)
- [How to Use Generators and yield in Python](https://realpython.com/introduction-to-python-generators/?utm_source=realpython&utm_medium=web&utm_campaign=related-post&utm_content=python-filter-function)
- [How to Join Strings in Python](https://realpython.com/python-join-string/?utm_source=realpython&utm_medium=web&utm_campaign=related-post&utm_content=python-filter-function)