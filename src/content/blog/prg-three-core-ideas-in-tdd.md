---
title: Three Core Ideas in TDD
author: David McCullough
pubDatetime: 2024-05-12T04:00:00Z
slug: three-core-ideas-in-tdd
featured: false
draft: false
tags:
    - programming
description:
     Discussing three high level ideas in Test Driven Development.
---

In the last few weeks, I've been taking learning Test Driven Development (TDD) more seriously.
I've been working through [James Grenning's TDD book](https://www.goodreads.com/book/show/9505798-test-driven-development-for-embedded-c?ac=1&from_search=true&qid=zCn4Oaq2WF&rank=1).

A really good exercise for practice is to implement a circular buffer.
A circular buffer has no hardware dependencies, and its implementation has many boundary conditions to consider.
Looking around to see how others have approached the problem, I have noticed that quite a few implementations do the wrong thing.
James has a [blog post](http://blog.wingman-sw.com/tdd-guided-by-zombies) where he walks through his own implementation.
By using this and his book as a reference, I have identified three high level ideas that are central to TDD.

* TDD is a system.
* The test's are right!
* TDD both tests and drives the interface.

# TDD is a System
One of my favourite quotes comes from the book [Atomic Habits](https://www.goodreads.com/book/show/40121378-atomic-habits?from_search=true&from_srp=true&qid=qitMwPfBEb&rank=1) by James Clear.
The quote goes something like this:

>We don't rise to the level of our goals. We fall to the level of our systems.

Following this idea has significant implications on how one approaches things.
It implies that to achieve one's goals, one should create systems that make it impossible to _not_ achieve them.

This is exactly what TDD is for programming.
It is a set of guidelines that can be followed almost blindly to get you from nothing to working code.

I think this is what I like most about the idea of TDD.
When I sit down to code, I don't have to think much about what to do next.
I just follow the [TDD Cycle](https://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html).

The process doesn't change day to day.
It doesn't depend on how I am feeling.
It is always the same.

```
write a test -> make it pass -> refactor -> repeat
```

TDD achieves this by encouraging the programmer to take the smallest steps possible.
The TDD Cycle is so short that it does not have room for variation.
To me, this is the underlying reason why TDD works.

Of course, TDD isn't magic!
The programmer still has to think.
The TDD Cycle must be followed correctly and the programmer has to learn how to write good tests.
The system of TDD is a skill.

# The Test's Are Right!
In the first chapter of his TDD book, James stresses two points:

1. The tests are right
2. Do the simplest thing that could possibly work

If you are interested in TDD, applied to embedded systems or not, I highly recommend reading James' blog post about implementing a circular buffer.
James's circular buffer walk-through highlights these two points by showing them off in practice.
At various stages of his implementation, he hard-codes values in his production code to make his tests pass.
To a non-TDD'er, this feels completely wrong.

At every stage, James does the simplest thing that could possibly work.
In doing so, he proves that his production code does what the _current_ set of tests describes.
This what 'the tests are right' means and it is an _extremely_ important point.
Tests are useless if they fail silently, or worse; pass when they should fail.
By always taking the smallest next step, the risk of writing a poor test, or writing tests that don't cover all the behaviour, is minimised.

To someone learning TDD, this can be easier said than done.
It's not how programming is traditionally taught.

In my experience, the difficult bit is choosing what the simplest thing to do is.
Every line of code is a choice.
The wrong choice can lead you down the incorrect path.
Robert C. Martin talks about a method for deciding what to do next in [this blog post](https://blog.cleancoder.com/uncle-bob/2013/05/27/TheTransformationPriorityPremise.html).
I don't think that the level of detail introduced by The Transformation Priority Premise is practical.
What is does, however, is create a general feeling for what change to make next.

Robert's post is a much better discussion of the topic than I could ever write.
There is no need for me to go over it here.
I would, however, like to highlight one point that he makes.

>As the tests get more specific, the code gets more generic.

This is another nugget of gold in the TDD philosophy.
I went over James' circular buffer implementation again, but this time with this idea in the back of mind.
It's really interesting to be aware of how with each new test, the production code becomes more and more complete and practical.
All the while, 'the tests are right'.
James describes this as 'closing a vice around the production code'.


# TDD Both Tests and Drives the Interface
Tip [#66](https://pragprog.com/tips/) from The Pragmatic Programmer says that 'testing is not about finding bugs'.
In the discussion of this tip, The Pragmatic Programmer says that writing tests is a design feedback mechanism that comes with the bonus of having a comprehensive description of the production code.
The main value in unit testing is not the testing itself, but the way in which it shapes the code.

For me, this has been an extremely obvious outcome of practicing TDD.
Every time I have slowed down and forced myself to write a test for even (what seems to be) the most obvious thing, I have ended up with better code.

TDD results in a clearer separation of responsibilities between code modules.
This is something that embedded developers tend to say is not practical.
In my experience, working in an environment where every byte counts, I've found the opposite to be true.
When I don't apply TDD, my code quickly becomes a mess of highly coupled modules.
With TDD, there is no choice but to stand back, think about what each module is responsible for, and create clear separation between them.
If you apply TDD, you have to do this.
If you don't, writing tests becomes a nightmare.

The main complaint with decoupling modules in embedded systems is that it uses more code space.
This simply isn't true.
Well written code can be decoupled _and_ small.
TDD is the system that, if applied correctly, can make that happen.

The net result of applying TDD is better, more decoupled, and easier to change interfaces([Tip #14](https://pragprog.com/tips/)).

When I first tried TDD in a real world scenario, I fell for what is probably the most common TDD trap.
I tested the internal implementation of my code.
This not only makes the tests fragile, it also takes away the benefit of having the tests drive the interface.
When I started testing outcomes and not implementations, I found I would regularly stop and consider if the interface was sensible.
I did this because the tests forced me to consider what role the bit of code under test was playing.
The tests drove the interface.

Tests drive the interface by forcing the programmer to use it at every step.
In doing so, the programmer gets direct and immediate feedback on its design.

When I compare my non-TDD code to my TDD code, this point is painfully obvious.
It doesn't take more than a quick scan to see that the TDD code is more logical and better organised.

# Conclusion
Good programming isn't easy.
We need systems to help us make it easier.
TDD is one of those systems.

The power of TDD is obvious.
Like any tool, it must be used properly.

It's easy to get caught up in the details of TDD.
For the new practitioner, there can be a lot of them!

These three points are the ideas on which TDD is built.
With each application of TDD, one must remember to occasionally step back and consider the high level purpose of the method.
