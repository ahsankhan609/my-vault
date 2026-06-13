---
title: "Learning Rust Made Me a Better Python Developer"
source: "https://belderbos.dev/blog/rust-made-me-a-better-python-developer/"
author:
  - "[[Bob Belderbos]]"
published: 2026-03-23
created: 2026-06-07
description: "Rust's ownership model, Result type, and exhaustive matching changed how I write Python. Here are the patterns that transferred."
tags:
  - "clippings"
---
You might be writing Python that silently mutates data it shouldn't, swallows exceptions it shouldn't, and relies on type annotations as suggestions rather than contracts. Not because you're careless, because Python lets you.

Rust doesn't. And six months of having a compiler refuse to let me move on changed how I write Python in ways no linter had managed before.

## Rust Is Already in Your Stack

You're probably using Rust without knowing it. Polars is the faster Pandas alternative. Ruff replaced flake8, isort, and black in a single tool. [Uv](https://belderbos.dev/blog/modern-python-tooling-uv-ruff-ty/) now handles virtual environments, package installation, and Python versions, replacing five separate tools.

Then there's Pydantic. Version 2 rebuilt its validation core in Rust and became 17 times faster. You still write Python. You still `uv add pydantic`. But the performance-critical path runs compiled Rust code.

Python for orchestration, Rust for speed. That's why the two languages aren't competitors. They're partners. PyO3 makes it straightforward to write Rust that exposes a Python API. You don't need to learn Rust to benefit from these tools, but understanding what's happening underneath changes how you think about your own code.

## Ownership Taught Me Data Flow

In Python, you pass objects around without thinking about who owns them. A function can receive a list, mutate it, and the caller's data changes. Nobody asked permission.

```python
def process_items(items: list[str]) -> list[str]:
    items.append("extra")  # mutates the caller's list
    return items
```

In Rust, you have to be explicit about this. Does the function borrow the data or take ownership? Can it mutate? The compiler won't let you leave this ambiguous.

Now when I write Python, I ask myself more often: does this function own the right to mutate the caller's data? The answer is usually no. So I return a new list instead of mutating the input:

```python
def process_items(items: list[str]) -> list[str]:
    return [*items, "extra"]  # returns a new list
```

This eliminates an entire class of bugs where mutation leaks across function boundaries.

## Result Types Taught Me Error Handling

Python lets you ignore exceptions. A function can raise anything at any time, and if you don't catch it, your program might crash at runtime. Thinking about failure paths upfront comes down to your experience and discipline.

Rust's `Result<T, E>` makes the choice explicit: this function can succeed with `T` or fail with `E`. You must handle both before the compiler lets you proceed.

I can't port `Result` to Python literally, but the mindset transfers. Instead of:

```python
def get_user(user_id: int) -> User:
    response = client.get(f"/users/{user_id}")
    return User(**response.json())  # what if this fails?
```

I now make failure explicit in the return type:

```python
def get_user(user_id: int) -> User | None:
    response = client.get(f"/users/{user_id}")
    if response.status_code == 404:
        return None
    response.raise_for_status()
    return User(**response.json())
```

## The Compiler Won't Let You Move On

Rust's compiler is famously strict, but because of that, also famously helpful. "Fighting the borrow checker" is a phrase you commonly hear from people learning Rust. But this "fight" teaches you so much: about data flow, lifetimes, who is responsible for what.

In Python, a type checker warning is a suggestion. You can ignore it and ship. In Rust, the code doesn't compile. There's no "I'll fix that later." That changes your relationship with tooling. After months of a compiler that refuses to let you proceed with a half-understood problem, you stop treating `ty` diagnostics as optional. Your Python toolchain becomes an approximation of Rust's compiler feedback loop.

## Pattern Matching Taught Me to Think in Cases

Rust's `match` is exhaustive. You handle every variant of an enum, or it won't compile. Add a new variant six months later? The compiler finds every `match` that needs updating.

Python has `match` since 3.10, but it doesn't enforce exhaustiveness. You can leave out a case and nothing warns you. Rust taught me to ask: what are all the states this can be in? Am I handling each one?

This applies beyond `match` statements. Kobzol's article ["Writing Python like it's Rust"](https://kobzol.github.io/rust/python/2023/05/20/writing-python-like-its-rust.html) captures it well: model your states explicitly, make invalid states unrepresentable. Use small named types instead of `dict[str, Any]`. Prefer `Header | Payload | Trailer` over a string field that could be anything. We can do all of this in Python, but Rust's compiler trains the instinct.

## You Don't Need Rust to Apply This

Python's type system can approximate a lot of this. Advanced type hints, `Protocol`, `TypeVar`, union types, `match` statements. Pair those with a type checker (`ty` or `mypy`), and you catch a lot of what Rust catches at compile time.

But there's a difference between knowing you *should* handle edge cases and having a compiler that *forces you* to do so. Rust builds that reflex. You develop a new instinct for Python.

## The AI Angle

When you direct an AI to write code, vague thinking produces vague output. "Add error handling" gets you something that compiles and looks reasonable but silently swallows the failure cases you didn't think to name. Rust trains you to think about those cases upfront and that precision transfers directly to how you prompt and how you review what comes back.

Rust trains that precision. Ownership, explicit errors, exhaustive matching. These aren't Rust-specific concepts, they're a way of thinking about what your code is actually doing. Once that thinking is a reflex, your AI prompts get tighter, your reviews of AI output get sharper, and you catch the places where the model glossed over a failure path.

## Key Takeaways

- Ownership thinking prevents mutation bugs. Ask "who owns this data?" before mutating it.
- Model failure in the return type. `User | None` communicates more than a docstring that says "may raise."
- Treat your toolchain as a compiler. `ty` warnings aren't suggestions if you stop treating them that way.
- Think in cases. If a value has three states, handle three states.
- You don't need to write Rust at work. The mindset transfer alone is worth the investment.

## Resources

I documented my early Rust learning journey at [rsbit.es](https://rsbit.es/).

Try the [intro exercises on the Rust Platform](https://rustplatform.com/) to get a feel for the language.

Related Pybites Podcast episodes:

- [#169: Bridging Python and Rust: An Interview with PyO3 Maintainer David Hewitt](https://www.youtube.com/watch?v=P47JUMSQagU)
- [#218: Why Python developers are learning Rust](https://www.youtube.com/watch?v=-5uLLBvWK5Q)

---

Rust doesn't replace Python for me, but learning it gave me a stricter lens to look at Python through. Same language, fewer surprises.