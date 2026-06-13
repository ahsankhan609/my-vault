---
title: Stop Installing Python on Your Laptop. Google Colab Changed How We Code Forever.
source: https://python.plainenglish.io/stop-installing-python-on-your-laptop-google-colab-changed-how-we-code-forever-f925ad4828e2
author:
  - "[[A. Rahman]]"
published: 2026-01-14
created: 2026-06-13
description: The nightmare is always the same. You want to learn Computational Science. You are excited. Then you open the …
tags:
  - google-colab
  - tools
---
## The nightmare is always the same. You want to learn Computational Science. You are excited.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*kEMHD245rwZ5TNEs)

Photo by Alexandru Acea on Unsplash

Then you open the installation tutorial.

Suddenly, your excitement is gone. You have spent 3 hours just “setting up your desk,” and you haven’t written a single line of code.

Remember the golden rule: **Human Time > Machine Time.**

If you are wasting your valuable hours fighting with a *local host* installation, you have lost the battle before it even started.

Luckily, there is a new way. A method adopted by top data scientists and engineers in Silicon Valley.

Forget the installation. Welcome to your new laboratory: **Google Colab**.

## What is Google Colab? (And Why It’s Our “Cheat Code”)

The gold standard for modern computing today is a format called **Jupyter Notebooks**.

This format is genius because it allows us to mix explanatory text, mathematical formulas, and executable code in a single interactive document.

**Google Colab** is essentially a Jupyter Notebook running in the *cloud*.

Imagine Google Docs, but for Python coding.

- No installation required.
- Free.
- Accessible from any browser.

This is the tangible realization of the efficiency philosophy. We remove technical barriers so we can focus strictly on the science.

## Tutorial: Your First Laboratory

Let’s prove how easy this is. Here are the “secret” features found in the documentation that make Notebooks much more powerful than just a standard calculator.

### Step 1: Open the Lab Doors

Open your browser and type [colab.new](http://colab.new/).

Boom. You have a ready-to-use Python environment. No boring setup.

### Step 2: Execute Your First Code

In the box (called a “Cell”), type this classic code:

```c
print("Hello Computational World")
```

Press Shift + Enter.

In a second, the result appears below it. It’s that simple.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*cZ8oYDpP9eLTjbUuywwmEg.png)

The output results in google collab

### Step 3: The “Magic” Commands (Pro Tip)

Many beginners don’t know that you can create text files directly from within the notebook without opening Notepad.

In Python notebooks, we use a special feature called the **File Magic** command. Try typing this in a new Colab cell:

```c
%%file simulation_data.txt
This is the content of my simulation file.
Initial velocity = 0
```

Press **Shift + Enter**.

The notebook will reply with Overwriting simulation\_data.txt.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*GZv3Zz3j2jph1AwQCWDfjA.png)

The output results

Congratulations, you just created a file on Google’s server without leaving your browser.

### Step 4: Accessing the Linux Terminal (!)

This is my favorite feature. We can talk directly to the Operating System (Shell) using the exclamation mark (`!`).

Type this:

```c
!cat simulation_data.txt
```

The result? The notebook will display the content of the file you just created.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*KSiNHiMCSzThczd16YlFNQ.png)

The output results

What does this mean?

It means Google Colab is not a toy. It is a full environment where you can execute shell commands. You can install additional libraries, download datasets, and run external Python scripts, all with a simple exclamation mark prefix.

## The Takeaway

Stop making things hard for yourself.

The world of *Computational Engineering* is difficult because of the math, not because of how you install Python.

Start today. Delete Anaconda from your laptop if it’s just eating up your RAM. Switch to Colab. Use the time you save to learn what really matters: Solving real-world problems.

Welcome to the era of *Zero-Setup Science*.

...

*What do you think? Are you Team “Local Host” or Team “Cloud”? Let me know in the comments!*

...

## Source & Further Reading

This article is inspired by the concepts found in **“Introduction to Python for Computational Science and Engineering”** by **Hans Fangohr**.

You can get the full book for free here:

[https://fangohr.github.io/introduction-to-python-for-computational-science-and-engineering/book.pdf](https://fangohr.github.io/introduction-to-python-for-computational-science-and-engineering/book.pdf)