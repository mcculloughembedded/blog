---
title: Nand2Tetris for Non-Programmers
author: David McCullough
pubDatetime: 2024-10-13T04:06:31Z
slug: nand2tetris-for-non-programmers
featured: false
draft: false
description:
    Learning how to manage complexity by building a general purpose computer.
---

I don't put any effort into advertising this blog.
I also don't have any idea how many people read it.
I purposefully have not set up any site traffic analytics.
That's not what it's about.

As a consequence, I imagine there aren't many returning readers,
and that most readers are programmers; specifically embedded firmware
developers.
Generally, my posts are written with the embedded firmware developer in mind.
This post is a slight deviation from that.

In the past, I have found random posts on personal blogs like this one to be
extremely useful.
I hope that someone will be inspired to take on the Nand2Tetris course
because of this post; and that they will find some use in having done so.

# What is Nand2Tetris?
[Nand2Tetris](https://www.nand2tetris.org/) is a well thought out (and free!)
course that takes you through the fundamentals of computer architecture by
building a general purpose computer from elementary components.

The course is split into two parts.
Part one consists of five hardware development projects, each of which builds
on its predecessor.
The final project culminates in a functioning general purpose computer, capable
of running complex programs like the classic [Tetris](https://en.wikipedia.org/wiki/Tetris) game.

The second part of the project progresses through the development of the
software required to code and then run such programs.

What makes Nand2Tetris unique, is that it is written with everyone in mind.
The authors do not assume any prior knowledge.
Despite this, they manage to strike a wonderful balance between letting
students figure out things for themselves and offering explanation and hints.

Although the second half of the course can be done by someone with no
programming experience, it is much better suited to someone with some
knowledge of computer science.
It is in the hardware development part of the course that I believe anyone can
find value.

Here's why.

# Managing Complexity
Complexity arises when something has many interconnected parts.
A complex system is not necessarily difficult to understand; although the word
'complex' is sometimes used to mean this.

By this definition, a general purpose computer is obviously a complex system.
Programmers understand this because they have to manipulate the system.
In doing so, they have to understand and deal with many of its components.
Non-programmers understand this because the system performs complicated tasks
such as retrieving information from the internet.
The nature of these non trivial tasks obviously necessitates complexity.

Nand2Tetris offers insight into how we have been able to manage and improve
these complex systems.
Complexity is not limited to general purpose computers.
It is everywhere.
Any skilled worker must be able to manage it.
That is one part of their job that makes them skilled.

The point here is that while Nand2Tetris is an excellent resource for
understanding the fundamentals of computer architecture, it is also an
excellent resource for anyone who needs to manage complex systems.
The fact that it is presented in an accessible way is what makes it worth
doing for anyone learning how to manage complexity.
Nand2Tetris is an extremely practical experience of modular and testable
design.
The ideas presented can be applied to any composite system.

## Interfaces
The secret to managing complexity is _interfaces_.
Interfaces are a method of effecting _abstraction_.
I wrote in more detail about abstraction in [this](https://mcculloughembedded.com/posts/Abstraction%20is%20Everything/) post.

The idea is that there are many benefits to separating what something does from
how it does it.
Extending this idea allows us to create and manage arbitrarily complex
systems by creating _layers of abstraction_.
The Nand2Tetris course places huge importance on this idea.
In every project, the _interface_ of the components being built are presented
before their _implementation_.
The text first defines the 'what' and the 'why', and then tackles the 'how'.
Every project starts with an explicit reminder that interface and
implementation are completely separate.
At the end of every project, there is some commentary on how the project fits
into the end goal of building a general purpose computer.
The next project always adds a layer of abstraction onto its predecessor,
until finally a general purpose computer is effected.
When I finished the last project, I reflected on the course.
At no point did I feel like I had faced an unmanageable problem; yet the task
of building a general purpose computer was extremely daunting at the start of
project one.
What better way is there to understand the power of abstraction than by
using it?


## Testing
Complex systems are often complicated.
A complicated system needs to be tested.
This has obvious benefits in computer science but is also applicable in other
fields.
Again, I refer you to my [post on abstraction](https://mcculloughembedded.com/posts/Abstraction%20is%20Everything/).

Every project in the Nand2Tetris course comes with a set of test scripts to
help you verify that your implementation effects its interface.
There's an interesting point that I missed when I spoke about
[how abstraction limits scope](https://mcculloughembedded.com/posts/Abstraction%20is%20Everything/#abstraction-helps-to-limit-scope).
The limiting of scope is what makes a system testable.
Taken as a whole, a complex system seems impossibly difficult to test.
However, at each layer of abstraction the scope of functionality is limited.
It becomes much clearer what to test and how to test it.

The inclusion of test scripts for each project is a form of [TDD](https://www.agilealliance.org/glossary/tdd/).
Every component has an interface, described both by its definition and by the
test scripts.

There are two valuable general lessons here.
1. If you can't verify that something does what it is supposed to do, use more
   abstraction!
2. By thinking first about how we can verify what we are doing before we think
   about how to do it, we ensure that we are thinking at the appropriate level
   of abstraction, and that our implementation does only what it needs to and
   nothing more.

In short, for any given system, Nand2Tetris teaches how to realise the
statement:[^smart-notes]

>More is unnecessary. Less is impossible.

_and_ make
sure the system works.

# What I do, I Understand
Every chapter of Nand2Tetris begins with a quote.
The very first chapter's quote is:

> What I hear I forget; What I see I remember; What I do, I understand.

This is where Nand2Tetris shines.
The course is structured in a way that forces you to manage complexity by
creating a complex thing.
It does this in a guided way, yet somehow never feels like the answer is
given to you for nothing.
By doing the Nand2Tetris course, you don't hear about general purpose computers
and abstraction; nor will you only read about them; you will understand them by
doing.

Earlier this week, I served as a [rubber duck](https://rubberduckdebugging.com/) for a colleague at work.
He was trying to do some difficult things requiring a deep understanding of the
MSP430's Application Binary Interface (ABI).
A while back, I spent some time going through the documentation for the ABI
and tried to relate it to the assembly generated by the compiler.
My colleague had reached a point where he could isolate the part of the ABI
that he was interested in, and see how the compiler and linker were
interacting.
After talking me through what he was doing, some parts of the ABI that I had
read before suddenly became very obvious.
I had previously seen them, and therefore only remembered them.
Just by observing him doing, I understood better.

The takeaway is that complexity cannot be faked.
Moreover, often complexity is something that is not easily mimicked in a
consequence free environment.
It is impossible to replicate the complexity created by a company full of
hard-working people.
This is why Nand2Tetris is so valuable.
It is a rare resource in which managing complexity is taught in an educational
and practical setting.

# Advanced Magic
The third of [Clarke's Three Laws](https://en.wikipedia.org/wiki/Clarke%27s_three_laws) states that
"Any sufficiently advanced technology is indistinguishable from magic".

I hope that someone reads this post, is inspired to do the Nand2Tetris course,
and in doing so understands the Nand2Tetris author's extension of this law.

>Any sufficiently advanced magic is indistinguishable from hard work, behind
the scenes.

Do the Nand2Tetris course, and learn how to create advanced magic!

[^smart-notes]: Sönke Ahrens, [How to Take Smart Notes](https://www.goodreads.com/book/show/34507927-how-to-take-smart-notes)
