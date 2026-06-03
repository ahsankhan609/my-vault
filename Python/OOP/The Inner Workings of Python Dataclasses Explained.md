---
title: The Inner Workings of Python Dataclasses Explained
source: https://jacobpadilla.com/writing/python-dataclass-internals
author:
  - "[[Jacob Padilla]]"
published: 2024-12-24
created: 2026-05-26
description: Discover how Python dataclasses work internally! Learn how to use __annotations__ and exec() to make our own dataclass decorator!
tags:
  - classes
  - dataclasses
---
Dataclasses in Python are pretty cool, but have you ever wondered how they work internally? In this article, I’m going to recreate a simple dataclass decorator to explain some of the key concepts behind this cool module!

## The Main Concepts

Dataclass decorators are pretty unique - instead of the decorator wrapping the class in another object, which is what a standard decorator would do, the dataclass decorator just uses the metadata from the user-defined class to create a few methods, adds those methods to the user-defined class, and then returns the same class that it received like this:

```python
def dataclass(cls):
    # Modify cls...
    return cls

@dataclass
class Example:
    Pass
```

The decorator is able to modify the user-defined class with the help of the `__annotations__` dunder attribute, which provides the metadata to the decorator, and `exec`, a function the dataclass module uses to create the new methods. Since these two Python features are the core of how a dataclass works, let’s go over them first:

`__annotations__` is a dictionary in Python that stores type hints for variables, attributes, and function arguments or return values within Python objects. The dataclass decorator uses it to inspect the user-defined fields in the class.

Here’s an example of how this works:

```python
class Example:
    name: str
    age: int

print(Example.__annotations__)
```

`__annotations__` will return a dictionary with the names of the variables and the type hints:

```python
{'name': str, 'age': int}
```

By the way, technically, the dataclass decorator uses the following line to get the annotations, but if you look at the code for `get_annotations` in the `inspect` module, it’s also using the `__annotations__` attribute.

```python
cls_annotations = inspect.get_annotations(cls)
```

Next, let’s look at the second feature dataclasses rely on: `exec`. This function takes code in the form of a string, such as “x = 1”, or in the case of dataclasses, whole function definitions, and turns them into Python objects.

Here’s a simple example that uses `exec` to execute a string of code that sets `x` equal to 1 and stores it in a custom namespace:

```python
namespace = {}
exec('x = 1', None, namespace)
print(namespace)  # Output: {'x': 1}
```

The dataclass uses the `exec` function to create the methods required for the class. In this article, I’ll go over `__init__`, `__setattr__` and `__delattr__` (for implementing the `frozen` argument), and finally, the `__repr__` dunder method. However, the actual dataclass uses `exec` to handle a lot of other options as well.

## First Version

Now that I’ve covered the main concepts behind the dataclass decorator, let’s make our first (bare-bones) version!

Throughout this article, I’ll be using this dataclass definition in the examples:

```python
@dataclass
class PersonInfo:
    first_name: str
    last_name: str
    age: int

person = PersonInfo(first_name='Michael', last_name='Scott', age=46)
```

The first thing that we need to do is define a decorator which will look like this:

```python
def dataclass(cls=None, /, *, init=True, frozen=False, repr=True):

    def wrap(cls):
        # We will be altering the class here
        return cls
  
    if cls is None:  # If we provide arguments to the dataclass decorator
        return wrap
      
    return wrap(cls)
```

This decorator will either return the `wrap` function or call `wrap` depending on whether the dataclass was created with or without arguments. If no arguments are provided to the decorator, the decorator is first called when Python passes the object being wrapped into it. In this case, the `cls` argument will **not** be `None`, and the decorator will return `wrap(cls)`, which simply returns the altered class (since `wrap` returns `cls`).

For example, a decorator with no arguments would look like this:

```python
@decorator
class Example:
    ...
```

And what Python ends up doing with the decorator is equivalent to the following line of code, which passes the object being wrapped into the decorator:

```python
Example = decorator(Example)
```

However, if there are arguments in the decorator, the dataclass function will be called, and then the actual decorator will be returned, which in our case is the `wrap` function. Python will then do the same thing as above and call `wrap` with the decorated class!

Back to making our dataclass decorator, in our first version, we are going to add an `__init__` method so that the class can actually accept the user-defined fields. Since the dataclass module uses `exec` to do this, we first need to create a string-based `__init__` function definition that we can then pass into `exec`.

To do this we will use the following code, which is basically just a simplified version of what the actual dataclass module is doing:

```python
def _create_fn(cls, name, func):
    ns = {}
    exec(func, None, ns)
    method = ns[name]
    setattr(cls, name, method)

def _init_fn(cls, fields):
    args = ', '.join(fields)

    lines = [f'self.{field} = {field}' for field in fields]
    body = '\n'.join(f'  {line}' for line in lines)

    txt = f'def __init__(self, {args}):\n{body}'

    _create_fn(cls, '__init__', txt)
```

`_create_fn` creates the function and then uses `setattr` to add the newly created method to the class `cls`. In terms of the `_init_fn`, this will generate the function definition from `fields`, which will be a list of user-defined fields in the dataclass.

For example, let’s say that `fields` is equal to `[“first_name”, “last_name”, “age”]`. The `txt` variable, which is sent to `_create_fn` and then passed into `exec`, would end up being:

```python
def __init__(self, first_name, last_name, age):
    self.first_name = first_name
    self.last_name = last_name
    self.age = age
```

Putting this code all together, we get our first version of the dataclass!

```python
def dataclass(cls=None, /, *, init=True, frozen=False, repr=True):

    def wrap(cls):
        fields = cls.__annotations__.keys()
  
        if init:
            _init_fn(cls, fields)
      
        return cls
  
    if cls is None:
        return wrap
    return wrap(cls)

def _create_fn(cls, name, func):
    ns = {}
    exec(func, None, ns)
    method = ns[name]
    setattr(cls, name, method)

def _init_fn(cls, fields):
    args = ', '.join(fields)

    lines = [fself.{field} = {field}' for field in fields]
    body = '\n'.join(f'  {line}' for line in lines)

    txt = f'def __init__(self, {args}):\n{body}'
    _create_fn(cls, '__init__', txt)
```

## The Frozen Argument

Now, let’s add the frozen option to our custom dataclass. In the regular dataclasss, this `frozen` argument lets us make the dataclass instances immutable, which can be very useful! All of these options basically just add more dunder methods to the class. In the case of the frozen option, we will need to add the `__setattr__` and `__delattr__` dunder methods since those are the two methods that are called when we either try to alter or delete an instance variable.

Before adding these two methods to our dataclass, let’s go over how `__setattr__` works (`__delattr__` is pretty much the same thing, but for deleting). When we try to set an instance variable by using a `.` and `=`. `__setattr__` will be called with two arguments: The name of the attribute we are trying to access and the value that we are trying to set it to.

In this example below, we’re just printing `hello` every time that we set an attribute and then using `super` to call the `__setattr__` method in the base class, which is `object`.

```python
from typing import Any

class Example:
    def __setattr__(self, name: str, val: Any) -> None:
        print('hello')
        super().__setattr__(name, val)

e = Example()
e.item = 1
e.item = 1
e.item = 1
```

Because we’re setting an attribute three times in the above example, “hello” is printed out 3 times:

```
hello
hello
Hello
```

To add these two dunder methods to our dataclass decorator, all we’re doing is checking if the `frozen` parameter was set to `True` and if it is, calling `_frozen_get_del_attr`. This creates two method definitions for the dunder methods that I just talked about, and whenever they are called, they just raise an exception.

The only problem now is how the `__init__` method will be able to create instance variables… After all, the `__init__` method also uses the class’s `__setattr__` method when setting instance variables (`self.name = val`). To solve this issue, we need to alter our dataclass’s `__init__` method to avoid setting instance variables directly with `self.name = val`. Instead, we need to force the `__init__` method to use the base `object.__setattr__` method when setting instance variables via the following line of code (one per field): `object.__setattr__(self, “name”, name)`.

```python
def dataclass(cls=None, /, *, init=True, frozen=False, repr=True):

    def wrap(cls):
        fields = cls.__annotations__.keys()
  
        if init:
            _init_fn(cls, fields)
      
        if frozen:
            _frozen_get_del_attr(cls, fields)
  
        return cls
  
    if cls is None:
        return wrap
    return wrap(cls)

def _create_fn(cls, name, func):
    ns = {}
    exec(func, None, ns)
    method = ns[name]
    setattr(cls, name, method)

def _init_fn(cls, fields):
    args = ', '.join(fields)

    lines = [f'object.__setattr__(self, "{field}", {field})' for field in fields]
    body = '\n'.join(f'  {line}' for line in lines)

    txt = f'def __init__(self, {args}):\n{body}'
    _create_fn(cls, '__init__', txt)

def _frozen_get_del_attr(cls, fields):
    setattr_txt = (
        'def __setattr__(self, name, val):\n'
        '    raise Exception(f"Cannot assign to field {name!r}")'
    )

    delattr_txt = (
        'def __delattr__(self, name):\n'
        '    raise Exception(f"Cannot delete field {name!r}")'
    )

    _create_fn(cls, '__setattr__', setattr_txt)
    _create_fn(cls, '__delattr__', delattr_txt)
      

@dataclass(frozen=True)
class PersonInfo:
    first_name: str
    last_name: str
    age: int

person = PersonInfo(first_name='Michael', last_name='Scott', age=46)
person.age = 47
```

Now, when we try to change an instance variable, we get this error:

```python
Exception: Cannot assign to field 'age'
```

## Adding a \_\_repr\_\_

The last method I want to add is `__repr__`, which prints out a class instance in an easy-to-read format. If you print out a regular dataclass, you get this type of output:

```python
person = PersonInfo(first_name='Michael', last_name='Scott', age=46)
print(person)  # Output: PersonInfo(first_name='Michael', last_name='Scott', age=46)
```

To get the same output in our dataclass, we just need to get all of the instance variables, which by default are stored in the instance’s `__dict__` attribute, and then format them with f-strings.

```python
def _repr_fn(cls, fields):
    txt = (
        "def __repr__(self):\n"
        "    fields = [f'{key}={val!r}' for key, val in self.__dict__.items()]\n"
        "    return f'{self.__class__.__name__}({\", \".join(fields)})'"
    )
    _create_fn(cls, '__repr__', txt)
```

The `!r` in the f-string is something that I actually learned about while reading through the dataclass module! It lets you call the `__repr__` method of each variable when turning the value into a string, which helps to format our output better!

With `_repr_fn` created, adding everything together, we get our final custom dataclass!

```python
def dataclass(cls=None, /, *, init=True, frozen=False, repr=True):

    def wrap(cls):
        fields = cls.__annotations__.keys()
  
        if init:
            _init_fn(cls, fields)
      
        if repr:
            _repr_fn(cls, fields)
  
        if frozen:
            _frozen_get_del_attr(cls, fields)
  
        return cls
  
    if cls is None:
        return wrap
    return wrap(cls)

def _create_fn(cls, name, func):
    ns = {}
    exec(func, None, ns)
    method = ns[name]
    setattr(cls, name, method)

def _init_fn(cls, fields):
    args = ', '.join(fields)

    lines = [f'object.__setattr__(self, "{field}", {field})' for field in fields]
    body = '\n'.join(f'  {line}' for line in lines)

    txt = f'def __init__(self, {args}):\n{body}'
    _create_fn(cls, '__init__', txt)

def _repr_fn(cls, fields):
    txt = (
        "def __repr__(self):\n"
        "    fields = [f'{key}={val!r}' for key, val in self.__dict__.items()]\n"
        "    return f'{self.__class__.__name__}({\", \".join(fields)})'"
    )
    _create_fn(cls, '__repr__', txt)

def _frozen_get_del_attr(cls, fields):
    setattr_txt = (
        'def __setattr__(self, name, val):\n'
        '    raise Exception(f"Cannot assign to field {name!r}")'
    )

    delattr_txt = (
        'def __delattr__(self, name):\n'
        '    raise Exception(f"Cannot delete field {name!r}")'
    )

    _create_fn(cls, '__setattr__', setattr_txt)
    _create_fn(cls, '__delattr__', delattr_txt)
      

@dataclass
class PersonInfo:
    first_name: str
    last_name: str
    age: int

person = PersonInfo(first_name='Michael', last_name='Scott', age=46)
```

And if we try to print out `person`, we get the same output as the standard dataclass:

```python
PersonInfo(first_name='Michael', last_name='Scott', age=46)
```

## Conclusion

Hopefully, this gives you a good idea of what the dataclass decorator is doing internally! Until writing this article, I had no idea that it was creating a function with `exec`! The actual dataclass has a lot more “method creation functions”, just like the ones in this example.

Lastly, I want to mention that while dataclasses are great, it may be better to use the Pydantic [dataclasses](https://docs.pydantic.dev/latest/concepts/dataclasses/) version (or, even better, their BaseModels) since their dataclass includes type validation. Their dataclass also uses the `__annotations__` attribute to get the specified fields, but unlike the built-in dataclass version, it uses the type hints in `__annotations__` for its type validation.