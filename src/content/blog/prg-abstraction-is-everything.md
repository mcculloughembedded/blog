---
title: Abstraction is Everything
author: David McCullough
pubDatetime: 2024-09-29T04:06:31Z
slug: Abstraction is Everything
featured: false
draft: false
tags:
    - programming
description:
    How abstraction can be applied to anything.
---

# A Computer Scientist's Definition of Abstraction
In the context of applying abstraction to anything and everything, I will be
using the definition of abstraction that is most commonly given in computer
science.

The [Nand2Tetris](https://www.nand2tetris.org/) course describes abstraction
as the separation of interface and implementation.
In this context, an interface describes what a module does, while the
implementation describes how the interface is realised.
Thus, abstraction is the process of disassociating what something does from
how it does it.

## Abstraction Manages Complexity
The idea of abstraction is fundamental to computer science.
Without it, it would be impossible to realise the complexity of modern
computing.

I present here a simple example of how abstraction can aid in understanding
complexity in a computer program.

Consider a point in 2D space
```c
struct point_t
{
    int x,
    int y,
};
```
We could move the object to the origin of that space by setting `x` and `y` to '0'.
```c
point_t position = {2,4};
// Move to origin
position.x = 0;
position.y = 0;
```
This requires two steps to understand how this fits into the overall program.
First, one must understand what setting `x` and `y` to '0' achieves, then
only can one consider how it relates to the context in which it is used.

A better way is to create a function
```c
void move_to_origin(point_t* t_point)
{
    t_point->x = 0;
    t_point->y = 0;
}
```
By doing this, we create an interface which abstracts away the implementation.
The step of understanding why `x` and `y` are set to zero is removed.
We are now free to think in terms of 'moving the point to the origin' instead
of worrying about the details of that operation.

There are other benefits to this, such as the [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) principle and an inherent
association with [TDD](https://www.agilealliance.org/glossary/tdd/).
These are out of scope for this post.

What is important is that by moving the implementation into a function, we have
created an interface that is distinct from that implementation.

# Abstraction is a Fundamental Concept
The importance of the example above cannot be overstated.
While it is simple, it demonstrates a number of non-obvious points.

## Layers of Abstraction
The main power of abstraction lies in being able to think at an appropriate
level for the problem at hand.

In the above example, having an appropriately named function allowed us to
think in terms of why moving the point to the origin is required, without
needing to consider how it should be moved there.

That is just one example of how abstraction is helpful.
We can build on that idea to create seemingly impossibly complex systems.

For example, we could build on our `point_t` implementation by creating a line.
A straight line is fully defined by only two points.
```c
struct line_t
{
    point_t p1,
    point_t p2,
};
```
From lines, we can build polygons.
We can connect polygons together to create arbitrary shapes.
At each level, we choose an appropriate level of abstraction.

For example, because we have created the abstract idea of a line, we can think
of a square as four lines of equal length, connected to each other at right
angles.
We don't have to consider the infinite number of points that make up the
square.
If we had to think of all the points that make up a square, we would be soon
be mentally overloaded, even when considering simple shapes like squares.

It's not difficult to see how this concept can (and is!) extended to create
otherwise unmanageably complex systems.
Think of modern computers.
They contain billions of transistors.
Without some way to manage that complexity, it would be impossible to
understand how they work.

## Abstraction Helps to Limit Scope
[Scope Creep](https://en.wikipedia.org/wiki/Scope_creep) is a serious problem.
Not just in software engineering, but in every project.

In [How to Take Smart Notes](https://www.goodreads.com/book/show/34507927-how-to-take-smart-notes), Sönke Ahrens says of the tools required to follow
the method, `"More is unnecessary. Less is impossible."`.
In my view, a project for which this can be said is a successful one.
It implies that the goals of the project are clear, and that they have been
achieved optimally.

But how do we know what is unnecessary and what is required?

One way is to use abstraction.
By worrying only about interfaces, we can create modules that work together
to achieve the project outcomes.
When we do this, we don't have to work on the implementation of the modules
right away.
The interfaces describe how the modules will interact.
We can use this information to decide which modules are really required.
The advantage of abstraction here is that we don't have to think about every
implementation all at once.
If we did, we would spend too much time on implementations and only find out
what we don't need once we have already done it.

It would be naive to think that thinking in this way will result in perfectly
optimal projects.
Of course not.
In the real world we change our minds because we never really know exactly
what we want.
Thinking in terms of interfaces is a strategy to help us understand our goals
before we do the bulk of the work.
In doing so, we can limit the scope of work to what matters.

The concept of thinking in terms of interfaces is more formally articulated by
the computer science concept of [Designing by Contract](https://en.wikipedia.org/wiki/Design_by_contract).

## Improve by Standardising
A contender for my favourite quote of all time comes from the book [Atomic Habits](https://www.goodreads.com/book/show/40121378-atomic-habits?from_search=true&from_srp=true&qid=7B7Rv4NntF&rank=1).
>You do not rise to the level of your goals. You fall to the level of your systems.

Over the weekend, I found another quote that complements this idea beautifully.
>We only improve when we standardise something.

This comes from the book [Building a Second Brain](https://www.goodreads.com/book/show/59616977-building-a-second-brain?ac=1&from_search=true&qid=Sd8ud1AeIO&rank=1).

To me, these two thoughts link to abstraction in a non-obvious way.
By creating interfaces, we begin to build a system.
An interface is nothing but a standardised way to interact with something.
The system of interfaces serves as a yard-stick against which it can be
compared to itself.
As the system grows, we continually fall to its level.
The standardisation of its interfaces allows us to understand what that level
is, and points to where and how it can be improved.

In contrast, an interfaceless system isn't really a system at all.
It is a highly coupled mess of implementations.
When it is time to improve it, the exposed implementations hide its flaws.

## Decoupling
A more obvious benefit to abstraction is the decoupling that it provides.
In the point example, if we decided we want the origin to be at `{1.62, 6.28}`,
we only need to make that change in the `move_to_origin()` function.
The code at the call site doesn't need to change.

This is only possible because the interface and the implementation are
completely separate.

# Abstraction is for Everyone
The view of abstraction presented so far is usually done in the context of
computer science.
Even when discussed outside of the field, it typically serves as an introduction
to the computer science application.

I'm flipping that on its head.

## Abstractions in Everyday Life
Abstraction is everywhere.
Even if you are not conscious of it, you are making use of interfaces without
considering their implementations.

Take a car for example.
The interface is the steering wheel, the gear lever, the pedals and the seat.
Do you need to understand how the engine works to be able to operate the car?
Obviously not.
People drive cars every day without this knowledge.
What's more, if the fuel injection system has a problem, you only require
knowledge of that specific sub-system, at its level of abstraction, to fix it.
That's a good thing, because very few people have intimate knowledge of every
aspect of a modern car.
This is no different from the computer science idea of abstraction.
Cars are designed like this in the same way computer programmers design their
software.

Likewise, the interface for a fridge is that it is an enclosed box with a door.
The inside of the box is cold.
The design contract between the fridge and you is that if you open the fridge
door, put something inside the fridge, and then close the door, that thing will
be cooled down.

## So What?
There are many cases where abstraction is implicit, but where we would do well
to consider it explicity.

For the most part, consciously thinking of abstraction in the fridge and car
examples is a little bit silly.
But what about when managing a project?
Or building a house?
Or writing a book?

In each of these examples, there are clear ways in which isolated modules can
be created by defining interfaces.
All the benefits discussed in this post still apply!

When managing a project, the project can be split into sub-projects.
The interface for each sub-project is its outcomes.
Sub-projects can be worked on in parallel, because every sub-project knows
what to expect from every other sub-project.
At some point, sub-projects can be combined to create another abstraction
layer.
The project is tracked by monitoring the interfaces between its sub-projects.

Likewise, a house can be defined as a collection of areas.
Each area has a purpose.
That is its interface.
The interface for an area costs nothing.
If time or money is short, the implementation does not need to be done for a
specific area.
It's interface can be left in place, thereby reducing the scope of the project,
while still allowing further expansion.

A book has a slightly more obvious connection to abstraction.
Books are normally comprised of chapters, or at the very least organised by
topic.
By knowing what each chapter or topic is about, an author is free to write any
chapter at any time.

# Use It!
I think the idea of explicity thinking about abstraction while doing common
tasks is powerful.

It is one way to create a system to which we can fall to and improve.
Abstraction is not limited to programmers.
Use it!
