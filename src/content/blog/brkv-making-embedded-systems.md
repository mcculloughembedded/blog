---
title: Review-Making Embedded Systems
author: David McCullough
pubDatetime: 2024-08-09T04:06:31Z
slug: review-making-embedded-systems
featured: false
draft: false
tags:
    - book-review
description:
    My review of the book Making Embedded Systems by Elecia White.
---

# TLDR;
[Making Embedded Systems](https://www.goodreads.com/book/show/12533344-making-embedded-systems?ac=1&from_search=true&qid=Oixkmzy2hm&rank=1) is an excellent introduction and overview to the world of embedded software.
It focuses on the methods and systems that an embedded software engineer is likely to use on a day to day basis.

_Making Embedded Systems_ is a must read for anyone making the transition from hobbyist to professional, and a good book to have on the shelf for those who already have some experience.

According to my [book rating system](https://mcculloughembedded.com/posts/my-book-rating-system/), I give _Making Embedded Systems_ 4 stars.
It is written and constructed well, and covers the fundamentals of embedded software development clearly.


# A Misleading Subtitle
I originally picked out _Making Embedded Systems_ because I was looking for a book that related common software design patterns to bare-metal programming.
There are plenty of 'design pattern' books, but (as far as I know) none that are written from the perspective of a programmer who has to be aware of serious memory contraints.
A lot of these books will tell you that good design is good design.
They argue that a well designed interface will naturally lead to more optimised code size; or that maintainability always wins the war between itself and code size.

This simply isn't true.
There are applications (which I have and am working on!) where the features that make the product competitive simply won't fit without packing all the bytes together at the cost of a well defined interface.
I wanted a book written by somebody who has been on both sides of the valley, and who can express the tradeoffs of employing typical software advice in tiny embedded microcontrollers.

The full title of _Making Embedded Systems_ is _Making Embedded Systems: Design Patterns for Great Software_.
That made me think _Making Embedded Systems_ was exactly was I was looking for.

It wasn't.

There is a fair amount of discussion on software design patterns, but I wouldn't venture to say that design patterns are the focus of the book.
Rather, the focus is on a way of thinking that every embedded software engineer has or will experience.

# So What Do You Get?
Like many young embedded software engineers in 2024, I got my first taste of microcontrollers through the [Arduino](https://www.arduino.cc/) platform.
Arduino left me wanting more.
In particular, I wanted to know how the obviously simplified lines of code I was writing resulted in an LED blinking, or a motor vibrating.

Arduino is intentionally simple.
It is designed to be a gentle introduction to the world of microcontrollers.
That's because the world of microcontrollers can get very complicated, very quickly.

_Making Embedded Systems_ is like a field manual for writing embedded software.
It outlines the usual traps and how to avoid them.
It tells you how to find the information you need.
It explains how to manage the inevitable conflict between you, the people who designed the hardware and the sales team who want the product to cure cancer.
_Making Embedded Systems_ is not just about writing software.
It is about taking an embedded product through its development cycle successfully.

When I started work as an embedded firmware engineer, I was given the task of writing a driver for a [DRV2605](https://www.ti.com/product/DRV2605?bm-verify=AAQAAAAJ_____w9SzgpIq-ynjr_o7CWLeuU86KtfOM3ejayuav1GKIJPldBYuNKjiK7HEs5WgSKlcOBcuCq8Uk6MrVMnDxYsM-l2m_wnEgarMWRo_TVfOqAcdfDQOJ1hsOd9dzffrdz1j0nmZbV8HIhyBQjXCvHdrl1gx05Z6vn_uRfanW44wojtY_mITJr9KvVs4oOSUd8JfRSpqEarzPJnKSwsOqp7dIMofsa7dVPylURotxlTKfex87DkpWhoT0tn8G10Tc_fIckC2Ym1tpOAh_ejhznv9Y5JMHOLQCXcD5g-d2IRWov_Hfw) haptics IC.
The code would be for internal use only, so it didn't have to be production ready.
The company already had some existing code for their chosen STM32 microcontroller.
All I had to do was write the interface for the DRV2605.
I saw the task as an opportunity to learn.
I had been dropped into an environment filled with people who had been writing code for microcontrollers for years, and I had access to all of it.

I found myself a copy of the datasheet and reference manual of the microcontroller I was using and, in between the DRV2605 code, I dived into the I2C driver code I had been given by a colleague.
Unfortunately, my youthful optimism was not enough to gain several years of embedded programming experience in one week.
I struggled my way through pages and pages of confusing terms and hundreds of lines of strange C code.
Ultimately, the project had to come to an end and I hadn't learnt much about the STM32 I was working with.

As I started becoming more involved in the company's production firmware, it became more and more obvious how naive I was to think that I could completely understand the intricacies of an STM32 in one week.

Looking back on that experience, _Making Embedded Systems_ would have been an extremely useful resource.
It wouldn't have made my learning easy, but it would have given it some direction.
I think that describes the target audience of the book extremely well.
_Making Embedded Systems_ is clearly aimed at newcomers to the field.
It is the bridge that spans the gap between `DigitalWrite(Pin4, HIGH)` and the 1000 page reference manuals of the underlying microcontroller.
Said another way, it wouldn't be useful for someone with no experience, nor would it be useful for someone who has been involved in a production emdedded firmware project.
It's usefulness is mostly limited to the people in between.

# You've Probably Already Done It
Unfortunately, since _Making Embedded Systems_ is only an overview of common experiences and ideas in embedded systems, anyone who has done a few years of embedded programming will have first hand experience of the bulk of its contents.

Since my DRV2605 days, I have read almost all the documentation for the [MSP430](https://www.ti.com/microcontrollers-mcus-processors/msp430-microcontrollers/overview.html) platform.
I have written state machines, fought with the idiosyncrasies of timers and both created and solved bugs caused by underflow and overflow.
I have implemented and analysed a [CORDIC](https://en.wikipedia.org/wiki/CORDIC) arctan algorithm, and studied the maths behind an integer only square root implementation.
For the most part, I've worked without a debugger, debugging by toggling IOs in strategic places or outputting binary coded decimal debug codes on them.
I've dived into the linker scripts of production firmware, and worked with the company's hardware team to write and test the product's deep sleep code.
I've scratched for literally bytes of code space to fit another feature in, or to fix a bug on existing firmware.

With the exception of Chapter 10 (Building Connected Devices), I have first hand experience of almost everything covered in the book.
A lot of that experience came through failure.
_Making Embedded Systems_ would certainly have helped to avoid a lot of the mistakes I have made along the way.
The point here is that I am definitely not an expert in the field of bare metal programming, and yet I have already encountered, thought about, and solved or implemented most of the topics covered in the book.

# Some (arguably) Bad Humour
There are a few jokes splattered throughout _Making Embedded Systems_.
Personally, I did not resonate with the humour.
I would have prefered the text to remain formal and direct.

Humour is, however, subjective.
I can understand why the jokes were included, especially given the target audience.
The embedded systems world can be quite intimidating.
Perhaps, for those to whom the humour is their style and who are encountering the topics for the first time, the humour may make the content less daunting.

# Conclusion
The software industry expects its engineers to learn on the job.
Arguably, failing (when done with the right attitude) is one of the most effective methods of learning.
Nevertheless, it is never an enjoyable experience to fail when it matters.
_Making Embedded Systems_ would probably help an inexperienced embedded engineer to avoid some of the more common sources of error.

_Making Embedded Systems_ is a guidebook for embedded software engineers.
It probably isn't going to make you write better software.
There simply isn't enough detail for that.
What it does do, however, is be a resource that can serve as the starting point to not just be a better programmer, but a better engineer.

Despite having already had experience of almost everything in the book, I will be keeping it on my bookshelf as a kind of field guide for my professional work.
I think it is an excellent resource for someone transitioning into the professional embedded systems world, and a useful resource for those who have already spent some time in it.

Ultimately, you become a better engineer by doing.
In my view, _Making Embedded Systems_ does not give enough detail to enable 'doing'.
I wouldn't recommend it as a primary learning resource, but it is worth having around.
