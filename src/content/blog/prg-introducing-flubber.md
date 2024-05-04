---
title: Introducing Flubber
author: David McCullough
pubDatetime: 2024-04-20T04:00:00Z
slug: introducting-flubber
featured: false
draft: false
tags:
    - programming
description:
     A command line interface to automate the setup and execution of CppuTest tests.
---

It's been about a year since I was first introduced to the concept of [Test Driven Development](https://www.agilealliance.org/glossary/tdd/) (TDD).
That is a statement that I almost find unbelievable.
I've been through an entire engineering degree, with multiple courses on programming, and TDD was not even mentioned!

Since learning about the idea, I've only managed to apply it sporadically.
Day to day, I work with memory constrained embedded devices.
Almost all of the code has one or more hardware dependencies.
Couple that with deadline pressure and a work environment that does not mandate TDD, and you get an environment that is certainly not ideal for learning the practice.

On the occasion that I have steadfastly stuck to the idea of TDD, it has worked extremely well.

So what's the problem?
Why haven't I been using it all the time?

# The First Step is Difficult!
Imagine, like me, that you've been happily practicing what James Grenning calls [Debug Later Programming](http://blog.wingman-sw.com/physics-of-test-driven-development).
One day, someone shows you their TDD workflow.
You think, "Wow! That seems like a really good way to program."

Doing some research, you find a testing framework like [CppuTest](https://cpputest.github.io/).
The documentation looks good.
James has even written a [whole book](https://www.goodreads.com/book/show/9505798-test-driven-development-for-embedded-c?ac=1&from_search=true&qid=4V9GdD2QSO&rank=1) about it.

Time to write your first test!

But what's this?
The recommended [getting started](https://github.com/jwgrenning/cpputest-starter-project?tab=readme-ov-file) project is filled with [Bash](https://www.gnu.org/software/bash/), [Docker](https://www.docker.com/) and [Make](https://www.gnu.org/software/make/), and it only works on Linux![^james-is-not-an-idiot]
It's all the usual confusing and unintuitive tools that any C/C++ developer has fought with before.

The first step is difficult.

That's where Flubber comes in.

# What is Flubber?
Flubber is a cross-platorm[^is-it-really-cross-platform] command line interface (CLI) that automates the setup and execution of CppuTest tests.
It's like James' starter project, but it requires no knowledge of the underlying tools.

Flubber aims to be extensible.
If you have knowledge of the underlying tools, you should be able to tailor its behaviour to your liking.
If you don't, Flubber allows you to just write tests, without all the usual troubles!

# Getting Started
I recommend you read Flubber's readme.
Flubber' GitHub is the go-to source for everything, so I won't elaborate further here.

# Why?
Flubber was motivated by my desire to learn TDD.
I felt like the process of simply getting the test executor to run was getting in the way of that.

For me, it was too much mental overhead to get started.
Ironically, that triggered a much larger project.

I've been using Flubber to work through James' book, and I've integrated it into my profesional workflow.
Obviously, I'm not an expert in TDD.
Flubber is probably missing a few pieces of the puzzle, and overlooking others.
If anything, that's why I've decided to make it public.
I know that there is a host of people who are more proficient TDD'ers than I am.
Hopefully, Flubber will attract a few of them, and they can help improve it.

# What's with the Name?
Flubber is named after Ned Brainard's invention from the movie [The Absent Minded Professor](https://en.wikipedia.org/wiki/The_Absent-Minded_Professor).
I watched the [remake](https://en.wikipedia.org/wiki/Flubber_(film)) when I was a child, and for some reason it stuck.


[^james-is-not-an-idiot]: This isn't a hit on the starter project. Anyone already familiar with these tools will find it extremely useful. It's just that large parts of Bash and Make border on the esoteric.
[^is-it-really-cross-platform]: As of the time of writing, I am pretty much the only person who uses Flubber. Flubber is _supposed_ to be cross-platform, but I've only used it on Window.
