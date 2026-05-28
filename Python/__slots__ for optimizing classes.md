---
title: __slots__ for optimizing classes
source: https://www.pythonmorsels.com/__slots__/
author:
  - "[[Trey Hunner]]"
published: 2025-11-05
created: 2026-05-26
description: Most Python objects store their attributes in a __dict__ dictionary. Modules and classes always use __dict__, but not everything does.
tags:
  - "#classes"
  - best-practices
---
[using __slots__ for optimizing classes](https://www.youtube.com/watch?v=D1VQkJFb8yw&source_ve_path=MjM4NTE&embeds_referring_euri=https%3A%2F%2Fwww.pythonmorsels.com%2F)

Let's talk about how to **optimize the memory usage and the attribute lookup time** of our Python classes.

## How are class attributes stored by default?

Here we have a class called `Point` in a `points.py` file:

```
class Point:
    def __init__(self, x, y, z):
        (self.x, self.y, self.z) = (x, y, z)

def point_path_from_file(filename):
    with open(filename) as lines:
        return [
            Point(*map(float, point_line.split()))
            for point_line in lines
        ]
```

And here's an instance of this `Point` class:

```
>>> p = Point(1, 2, 3)
```

Normally, classes store their attributes in a [dictionary](https://www.pythonmorsels.com/using-dictionaries-in-python/) called `__dict__`.

```
>>> p.__dict__
{'x': 1, 'y': 2, 'z': 3}
```

We have a class here where every instance has `x`, `y`, and `z` attributes. But we could add other attributes to any instance of this `Point` class, and another key-value pair will appear in this [`__dict__`](https://www.pythonmorsels.com/where-are-attributes-stored/) dictionary.

For example if we add a `w` attribute:

```
>>> p.w = 4
```

Our `__dict__` dictionary will now have a `w` attribute:

```
>>> p.__dict__
{'x': 1, 'y': 2, 'z': 3, 'w': 4}
```

This is how classes work *by default*; classes work this way **unless you use `__slots__`**.

## Using \_\_slots\_\_ to restrict class attributes

To use `__slots__`, we need to define a `__slots__` attribute on our class that points to a **tuple of strings** that represent **valid attributes names** for each instance of our class.

Let's add `__slots__` to our `Point` class:

```
class Point:
    __slots__ = ('x', 'y', 'z')

    def __init__(self, x, y, z):
        (self.x, self.y, self.z) = (x, y, z)
```

This instance of our `Point` class has an `x` attribute (just as before):

```
>>> p = Point(1, 2, 3)
>>> p.x
1
```

We can change the value of this attribute (just as before):

```
>>> p.x = 10
>>> p.x
10
```

But if we try to make a new attribute (an attribute that isn't `x`, `y`, or `z`) we'll get an `AttributeError`:

```
>>> p.w = 4
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'Point' object has no attribute 'w'
```

We get an `AttributeError` because each instance of this class **no longer has a `__dict__` dictionary** where it stores its attributes:

```
>>> p.__dict__
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'Point' object has no attribute '__dict__'
```

Instead, `__slots__` uses something kind of like a fixed-width list (or like a mutable tuple) to store specifically three attributes: `x`, `y`, and `z`. So because we're using `__slots__`, **we can't expand the number of attributes** that are on each instance of this class.

## Why use \_\_slots\_\_?

Why would you ever use `__slots__` in your class?

In some cases, you might use `__slots__` to restrict which attributes are on your class: you might want to **disallow assigning arbitrary attributes** that shouldn't be on instances of your class. But that's a little bit unusual; it's not *usually* the reason we use `__slots__` in Python.

Typically, we use `__slots__` to **save memory** or **save time**.

Using `__slots__` can save memory because each instance of your class **won't use a dictionary** to store its attributes. Instead, each of your class instances will **use a more efficient data structure to store its attributes**; one that can't be arbitrarily expanded, but does know how to store exactly the attributes that are expected on your class.

The other reason you might use `__slots__` is to **save time with attribute lookups**. Attribute lookups take a little bit less time with `__slots__` because each attribute access **doesn't need to do a dictionary key lookup** (which requires a small computation under the hood).

## Saving memory usage with \_\_slots\_\_

Alongside our `Point` class, we have a `point_path_from_file` function in our `points.py` file:

```
class Point:
    __slots__ = ('x', 'y', 'z')

    def __init__(self, x, y, z):
        (self.x, self.y, self.z) = (x, y, z)

def point_path_from_file(filename):
    with open(filename) as lines:
        return [
            Point(*map(float, point_line.split()))
            for point_line in lines
        ]
```

We're going to write a command-line program, `point_stats.py`, that will call our `point_path_from_file` function (from our `points` module):

```
import points

path = points.point_path_from_file('point_path.txt')

x_total = y_total = z_total = 0
for p in path:
    x_total += p.x
    y_total += p.y
    z_total += p.z

average = (x_total/len(path), y_total/len(path), z_total/len(path))
print(f"Mean of values: {average}")
```

Our `point_path_from_file` function **makes a new `Point` object** out of each line in a give file:

```
def point_path_from_file(filename):
    with open(filename) as lines:
        return [
            Point(*map(float, point_line.split()))
            for point_line in lines
        ]
```

And our command-line script averages the `x`, `y`, and `z` values of all those `Point` objects and then prints out the mean of values.

If we run this program against a really big file ([this 55MB `point_path.txt` file](https://gist.github.com/treyhunner/20a47f3cf13f5b5a1ac93e603b116d2b#file-point_path-txt)) it's going to take a while.

```
$ python3 point_stats.py
Mean of values: (-1490.5125363997097, -631.0342665916223, -2989.753194999186)
```

That output takes about N seconds when running this program in its current form.

Our `point_path.txt` has a million lines in it. So we're making a million instances of the `Point` class, and we're storing them the list (pointed to by our `path` variable):

```
path = points.point_path_from_file('point_path.txt')
```

## Memory usage comparison with and without \_\_slots\_\_

If we wanted to see how much memory our program takes up, we could add some code in our command-line program to print out the maximum memory usage for our Python program:

```
import points
import resource

path = points.point_path_from_file('point_path.txt')

x_total = y_total = z_total = 0
for p in path:
    x_total += p.x
    y_total += p.y
    z_total += p.z

average = (x_total/len(path), y_total/len(path), z_total/len(path))
print(f"Mean of values: {average}")

usage = resource.getrusage(resource.RUSAGE_SELF).ru_maxrss
print(f"Memory usage: {usage:,}")
```

This strategy for printing out memory usage is a little bit fuzzy and it doesn't always work exactly right, but it's a pretty decent start:

```
import resource

# ...

usage = resource.getrusage(resource.RUSAGE_SELF).ru_maxrss
print(f"Memory usage: {usage:,}")
```

Running our program now tells us we're using a 176,328 bytes at maximum within our Python process:

```
$ python3 point_stats_with_mem.py
Mean of values: (-1490.5125363997097, -631.0342665916223, -2989.753194999186)
Memory usage: 176,328
```

Now let's modify our `points` module, and change our `Point` class to remove `__slots__`:

```
class Point:
    def __init__(self, x, y, z):
        (self.x, self.y, self.z) = (x, y, z)
```

If we run our code again, we'll see that it takes up *more* memory, because it needs to **store a `__dict__` dictionary for every instance** of our `Point` class:

```
$ python3 point_stats_with_mem.py
Mean of values: (-1490.5125363997097, -631.0342665916223, -2989.753194999186)
Memory usage: 271,660
```

Without `__slots__` our program takes 271,000 bytes which is more than the previous 176,328 bytes.

## Summary

If you want to make instances of your Python class **more memory-efficient** and a little bit **faster for attribute lookups** you might consider adding `__slots__` to your class. Although doing so is only recommended if you have thousands of instances of your class or if you're doing a ton of attribute lookups in your code.

Now it's your turn! 🚀

We don't learn by reading or watching. **We learn by doing.** That means writing Python code.

Practice this topic by working on these **related Python exercises**.

[**Month**: Class representing a month and year](https://www.pythonmorsels.com/exercises/e1ba106369e24029b5723a855ae5c735/) [**Vector**: Class representing 3-dimensional vector](https://www.pythonmorsels.com/exercises/ced757b8a1bd400bb983aa8a2eb0e8fe/) [**make\_class**: Class factory function](https://www.pythonmorsels.com/exercises/50135c189dec4c7e8288722fcd017a8e/)

✕

↑

A Python Tip Every Week

Need to **fill-in gaps** in your **Python skills**? I send weekly emails designed to do just that.

Click to open IoC report  
with VirusTotal Augment