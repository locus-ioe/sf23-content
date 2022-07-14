---
title: "Day 2, 3 and 4: Git, debugging and Python Basics and Intermediate"
date: 2022-07-10
tags: ["git", "python", "code"]
authors: ["Aaditya Subedi"]
draft: false
weight: 2
---

## Resource Link [here](https://drive.google.com/drive/folders/1FUed1LDZk41Cpot32-GhbDDzBSbDTURI?usp=sharing)

# Python Guides

![Untitled](/attachments/Pythonlogo.png)
<img src="/attachments/Pythonlogo.png" width="200" height="100">

# What is Python?

Python is an interpreted, object-oriented, high-level, dynamically semantic programming language. It is particularly desirable for Rapid Application Development as well as for usage as a scripting or glue language to tie existing components together. Python's straightforward syntax prioritizes readability and makes it simple to learn, which lowers the cost of program maintenance. Python's support for modules and packages promotes the modularity and reuse of code in programs. For all popular platforms, the Python interpreter and the comprehensive standard library are freely distributable and available in source or binary form.

—— Extracted from [**here**](https://www.python.org/doc/essays/blurb/)

# History of Python!

In December 1989, Python’s creator Guido Van Rossum was looking for a hobby project to keep him occupied during the week around Christmas. He chose to call it Python. The language’s name isn’t about snakes, but about the popular British comedy troupe Monty Python (from the 1970s). Guido himself is a big fan of BBC’s TV Show – _Monty Python’s Flying Circus_. Being in a rather irreverent mood, he named the project ‘_Python_’

![**Guido van Rossum**](/attachments/guidovanrossum.png)

**Guido van Rossum**

# Why Python?

- Solves complex problems in **less time and fewer lines of code.**
- It can be used in **multi-purpose** jobs like AI/ML, Data Analysis, Software development, etc.
- It is a **High-level language**, so no need to worry about complex tasks such as memory management in C++.
- It is **Cross-Platform,** which means it can be run in different OS like Windows, macOS, and Linux.
- It has a **huge community,** so whenever you get stuck there is someone out there to help.
- It has a **large ecosystem** of libraries, frameworks, and tools. Whatever you want to do, it is likely that someone else has already done it there, since Python has been around for over 20 years and is still popular.

# Flavor of Python

Python ships in various flavors:

- **CPython-** Written in C, the most common implementation of Python
- **Jython-** Written in Java, compiles to bytecode
- **IronPython-** Implemented in C#, an extensibility layer to frameworks written in .NET
- **Brython-** Browser Python, runs in the browser
- **RubyPython-** Bridge between Python and Ruby interpreters
- **PyPy-** Implemented in Python
- **MicroPython-** Runs on a microcontroller

# Scope of Python

![Untitled](/attachments/scope_50.png)

![Untitled](/attachments/scope2_50.png)

# How is Python Code actually executed?

The Programming languages we use like C, C++, C#, and Python are all text-based languages that we humans understand, but computers do not understand them. They only understand machine codes (bunch of `0`s and `1`s like `0010100`, `1001010111000`). So if we have some code written in C, JAVA, Python, or any, we should convert them into machine code. That’s the job of a **compiler** or **interpreter.** A compiler or interpreter (combinly known as a **language processor** or **translator**) is a program that knows how to convert **C** (note I am taking the context of **C** only for now) into machine code. This machine code, however, is specific to the type of CPU of a computer(i.e machine code should be according to the architecture of the CPU, you will know about this in detail in a microprocessor course). That means if we compile a **C** code in Windows Machine, we can’t run it on macOS and vice versa. This is because they have different machine codes to do the same task, just like how people have different languages to talk about the same opinion.

However, Python just like Java, C# follows a different route to convert codes into machine code. This different route makes such languages platform-independent (technically: **cross-platform**).

Let’s take an example of translating python code into machine language using **CPython** (python interpreter written in C). CPython converts python code into something called “Python Byte code” instead of directly into machine code. Python Byte Code is then passed to something called Python Virtual Machine, which then converts byte code into platform-specific machine code and executes it.

Now onward, we will ship the Python byte code to different platforms, the python byte code is run on Python Virtual Machine irrespective of the platform, thus this makes Python cross-platform(or platform independent). However, the way Python Virtual Machine convert byte code into machine code is platform-specific.

## Above is all about the intro to Python.

To dive into the technical implementation of Python, we can find a bunch of resources online as it has a large community.

Official [Python docs](https://docs.python.org/3/) (GOAT resource, the official documentation of python, but it is too difficult to grasp for beginners).
No worry, I will suggest some beginner-friendly Python Getting Started materials online.

Video Resource: [Python - The Practical Guide](https://www.udemy.com/course/learn-python-by-building-a-blockchain-cryptocurrency/),
[Python Tutorial - Python Full Course for Beginners](https://www.youtube.com/watch?v=_uQrJ0TkZlc&t=2256s)

Textual Resource: [Geeks for geeks](https://www.geeksforgeeks.org/python-programming-language/)

Discussion forum: [StackOverflow](https://stackoverflow.com/) (Ask any question you wish to know here, there is more likely that your problem is already asked).

One of the Best Notes for refreshing the Python concept(for all levels), once you know the concept of Python is: [Python Notes for Professional](https://books.goalkicker.com/PythonBook/)

### Final Word for all beginners:

If you want to be a python geek, try to refer to as many articles and resources online until you can decode the [official python docs](https://docs.python.org/3/) and make them a primary source for your code reference.
