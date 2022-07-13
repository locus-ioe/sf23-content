---
title: "Day 1: Introduction to Software Development"
date: 2022-07-10
tags: []
draft: false
weight: 1
---

## Resource link [here](https://drive.google.com/drive/folders/1O0afZJMpGJYTLkdT_6cYWCBW8pcGgjDM?usp=sharing)

# Software doesn't wear out

There is important distinction between other engineering products and software product, lets take an example of the hardware,As time passes, issues in hardware increase due to lot of reason like friction, radiation and physical damages but it is not the case in software. Software product should evolve with time, due to patches and bugfixes software becomes robust as time passes, this is to say, failure rate decreases. This is to say the software doesn’t wear out. Thus software should be developed not manufactured.

# Software crisis

In early days of computing, writing software was not taken as project, it was taken as a simple task, the task performed by some genius looking guys called "Programmers". But soon hardware evolved and so the requirements for the software, people started to dream for large software powered systems. But there were failures like software running over-budget, over-time, and low quality softwares.
In the late 1960s, it became clear that the development of software is different than manufacturing other products. In mid computing era people started to practice software development as a engineering problem, after that software development field has evolved as enginneering discipline, people started to develop software in large organized teams, created different softwares that help them organizie softwares they are writing, Version management, configuration management, release management tools were developed.Different tools are used at different stages of software development life cycle.

![](/attachments/sdlc-tools.png)

# “Millenium Bug” or “Y2K

{{< youtube kyZDa09U7gc >}}

When complicated computer programs were being written during the 1960s through the 1980s, computer engineers used a two-digit code for the year. The "19" was left out. Instead of the date reading 1970, it read 70. Engineers shortened the date because data storage in computers was costly and took up a lot of space. As the year 2000 approached, computer programmers realized that computers might not interpret 00 as 2000, but as 1900. Activities that were programmed on a daily or yearly basis would be damaged or flawed.

This explained that for the success of a project, coding is just a part and there are so many other steps to be carried out. That’s why it was realized that software engineering is important. Let’s discuss what is software engineering.

Moral : Software architech/engineer should me futuristic while designing the software systems

# Programming Paradigms

When you are brand new to programming, programming paradigms are not of much importance. But as you go up the stairs and start creating complex programs and software, it is vital to understand which programming paradigm is best suited for your project.

Paradigm can be understood as a model or framework of how a certain task is done. Programming languages are tools and not all tools are good for all jobs. Hence, we need programming paradigms.

## Procedural

- A large program is divided into smaller programs called procedures. The procedures are also called subprograms, subroutines, methods or functions
- Continues to be preferred choice for beginners
- Example: BASIC, C, FORTRAN

### Features of Procedural Code

- Procedural Programming is excellent for general-purpose programming
- The coded simplicity along with ease of implementation of compilers and interpreters
- A large variety of books and online course material available on tested algorithms, making it easier to learn.
- The source code is portable
- The code can be reused in different parts of the program, without the need to copy it
- The program flow can be tracked easily as it has a top-down approach.
  For example, to develop a simple Bank Account App procedurally:

1. Creating an account for an individual (account)
2. Getting an account to deposit or withdraw funds (getAccount, deposit, withdraw)
3. Transferring funds between two different accounts (transfer)
4. Recording all changes that occur with all accounts (accounts)

## Object-Oriented

- All real-world entities are represented by Classes. Objects are instances of classes. It is used to structure a software program into simple, reusable pieces of code blueprints (usually called classes), which are used to create individual instances of objects. There are many object-oriented programming languages including JavaScript, C++, Java, and Python.

- Example: Car example, Bank App Example

* A class (BankAccount) encapsulates a set of properties (constructor function) and behavior (class functions deposit, withdraw, and transfer) that can be used to instantiate an object of specific values (i.e: let john = new BankAccount(“John”)). This is typically used to model real-world objects.

## Functional

- Uses pure, high order functions to develop applications

- What is a pure function?
  Pure functions are those which take an argument list as an input and whose output is a return value. Now you may feel that all functions are pure as any function takes in values and returns a value.

* For example, if a function relies on the global variable or class member’s data, then it is not pure. And in such cases, the return value of that function is not entirely dependent on the list of arguments received as input

* Eg: Common LISP, Clojure, Erlang, Haskell

Difference between Functional and Procedural

- A functional language (ideally) allows you to write a mathematical function, i.e. a function that takes n arguments and returns a value. If the program is executed, this function is logically evaluated as needed.1

* A procedural language, on the other hand, performs a series of sequential steps. (There's a way of transforming sequential logic into functional logic called continuation passing style.)

* As a consequence, a purely functional program always yields the same value for an input, and the order of evaluation is not well-defined; which means that uncertain values like user input or random values are hard to model in purely functional languages.

# Programming vs scripting vs markup languages

- **Programming** - Compiler based languages which are developed from scratch that run independently as compared to the scripting languages. Example: C, C++, Java, Pascal, C#, VB, Basic, COBOL, etc

- **Scripting** - A scripting language is nothing but a programming language which does not require a clear compilation step. Scripting languages need to be interpreted (Scanning the code line by line, not like compiler in one go) instead of compiled. Low maintenance scripting languages are JavaScript, PHP, Ruby, Perl, VB Script, etc.
  With the modern hardware and compilation techniques, the line between scripting and programming languages is getting more and more blurry. Languages like Python sits in both the types because many coders use this language without a compilation step, but the central part of implementation needs a compilation, and only after that it can be run in the bytecode.

  **Markup Languages**: Markup languages are languages that are not in any way executed or used to perform actions but they are used to structure data, identify data or present data as the case may be. Eg. HTML, XML
  Note: CSS is a stylesheet language, describing the presentation of a markup language

# Operating systems

The operating system is a system program that serves as an interface between the computing system and the end-user. Windows Mac and linux are some popular operating systems. Basically an operating is a software program that manages and controls the execution of application programs, software resources and computer hardware. Eventually every thing that is programmed must run on some metal, so operating system is the software that provides environment for other software/programs to run on hardware.

Microsoft created the first window operating system in 1975. After introducing the Microsoft Windows OS, Bill Gates and Paul Allen had the vision to take personal computers to the next level. Therefore, they introduced the MS-DOS in 1981; however, it was very difficult for the person to understand its cryptic commands.And then, Windows released various operating systems.

Besides the Windows operating system, Apple is another popular operating system built in the 1980s, and this operating system was developed by Steve Jobs, a co-founder of Apple.

In 1969, a team of developers of Bell Labs started a project to make a common software for all the computers and named it as 'Unix'. It was simple and elegant, used 'C' language instead of assembly language and its code was recyclable. As it was recyclable, a part of its code now commonly called 'kernel' was used to develop the operating system and other functions and could be used on different systems. Also its source code was open source.

In 1991, Linus Torvalds a student at the university of Helsinki, Finland, thought to have a freely available academic version of Unix started writing its own code. Later this project became the Linux kernel. He wrote this program specially for his own PC as he wanted to use Unix 386 Intel computer but couldn't afford it. He did it on MINIX using GNU C compiler. GNU C compiler is still the main choice to compile Linux code but other compilers are also used like Intel C compiler.
He started it just for fun but ended up with such a large project. Firstly he wanted to name it as 'Freax' but later it became 'Linux'.

# Open Source - Brief History

# Notion - Note taking software

- Project Management and Note taking application
- Uses of Notion: schedule tasks, manage files, save documents, set reminders, keep agendas, and organize their work
- Has a myriad of facilities
- We will look into a few of them, but I advice you to explore it on your own

## Topics that will be covered (onsite)

- Land on a blank notion page
- Setting up your notion page
- Begin with a dashboard
- How to create a page within a page
- Talking about text types - Headings, texts
- Talking about block types - check lists, tables
- Making notes based on topics
- How to track your todos - Task Databases
- Mention about filtering, grouping, no need to explain

# Markdown

- Notion supports both Markdown and Latex
- Both Latex and Markdown are vast, but latex is way more complicated. Has a lot of facilities, but is more complicated, so we won’t talk about it now. Let’s talk a bit about markdown
- Markdown is the .md file that you see everywhere(Every GitHub repo asks you to make one, if you have used it)
- Markdown is widely used for documentation
- In fact this site's content that you are currently reading is also prepared using markdown

* We will be learning a few basic markdown syntax, for notion, also for your everyday documentation

Learn more about markdown [here](https://github.com/tchapi/markdown-cheatsheet)

# How to get help?

- Google is your best friend. Don't know how to google like pro? see the video.

{{< youtube cEBkvm0-rg0 >}}

- Our lord and savior: Stack Overflow Try to use stackoverflow early, Prefer stack overflow over other sites, can't stress this enough.

* Reddit ma there are various subreddits, subreddits for literally everything
  r/learnprogramming, r/askprogramming, r/Frontend, r/LearnPython, r/WebDev

* Youtubers - freeCodeCamp, CS Dojo, The Coding Train, Corey Schafer
* GitHub- different repos, code from all around the world, GitHub Students Pack (Show the site)

  Student Email - GitHub Student Developer Pack, Free Microsoft Office 365, Google Suite for Education, Notion Premium, Namecheap .me domain, Free Lucidchart Account, Free JetBrains Account, Amazon Prime Student
