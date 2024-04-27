---
title: Custom Mechanical Keyboard Part One
author: David McCullough
pubDatetime: 2024-04-20T04:00:00Z
slug: custom-mechanical-keyboard-part-one
featured: false
draft: false
tags:
    - project
description:
     How I designed and built my own keyboard; and why it only has 34 keys!
---

I'm typing this post using a 34 key keyboard that I designed and built from scratch.
Everything is custom, from the key positions, to the case, right through to the keymap.

If you'd like an overview of the project, check out it's GitHub repository.

This is the first in a series of posts that will walk through the design process, culminating in the final build and my thoughts on using the keyboard as a daily driver.
In this post, I'll discuss how I got into custom keyboards, and we'll come up with a high level plan for the build.


# Deciding to Build a Keyboard
Shoes. Yes.<br/>
Shoes.

That's how I ended up building my own keyboard.
Specifically, barefoot shoes.
If you've never been into the world of barefoot shoes, you may be thinking, "How can there be such a thing as a barefoot shoe?".
It's a reasonable thing to think, and part of the reason I was interested in them.

This isn't about barefoot shoes, but if you'd like to know more, there are plenty of articles and videos about the topic.
I've particuarly enjoyed the [Barefoot Strength](https://www.youtube.com/@barefootstrength) YouTube channel, and I can recommend reading [Born to Run](https://www.goodreads.com/book/show/6289283-born-to-run?ac=1&from_search=true&qid=KUJgmqtudr&rank=1) by Christopher McDougall.

I was led from barefoot shoes to keyboards by a one video from [Ben Vallack](https://www.youtube.com/@BenVallack).
Ben's channel is varied, but there was a time when he was focused on building and experimenting with keyboards.
He was interested in using as few keys as possible, eventually settling (if I remember correctly), on an 18 key layout on which he could type at 80 words per minute.

I'm not interested in minimising the number of keys, but Ben's videos did get me thinking about different keyboard layouts.
I did some research, and found that the popular alternatives to [QWERTY](https://en.wikipedia.org/wiki/QWERTY) are [Dvorak](https://en.wikipedia.org/wiki/Dvorak_keyboard_layout), [Workman](https://workmanlayout.org/) and [Colemak Mod DH](https://colemakmods.github.io/mod-dh/).
Each of these optimises the letter placements for a different metric.

# Picking a Layout
I very quickly settled on Colemak Mod DH.
I highly recommend reading the rationale behind each layout.
It makes for very interesting reading.

In the end, I liked that the Colemak optimisation is focused on [same finger bigrams](https://colemakmods.github.io/mod-dh/compare.html).
Really though, I could've picked any one of the three.

There are plenty of other alternative layouts, each promising to be better than the others.
Having used Colemak for over a year, I am absolutely convinced that it is better than QWERTY and I don't think I will ever go back.
I'm certain that other layouts have very real, and just as relevant advantages.
When it comes to keyboard alternative layouts, there is no such thing as 'the best', only 'different'.

With my choice made, I used [Komonad](https://github.com/kmonad/kmonad) to remap my standard 65% staggered keyboard.
For a while, this was enough.

# Where did all the keys go?
The YouTube algorithm is relentless.
Now that it knew I had some interest in alternatives keyboards, it began to promote stranger and more esoteric keyboard designs.
After a while, I gave in and purchased a [Corne](https://github.com/foostan/crkbd) keyboard kit.

I used it at home for a while, but I never liked having a pre-made development board plugged into the main printed circuit board (PCB).
I have a little bit of experience with PCB layout, and it didn't seem too difficult to make a custom board.

# Custom PCB
Having decided to make my own board, I settled down for another round of research.

During my research, I stumbled across the [Clog V3](https://github.com/smores56/clog-v3).
You can see a picture of it on [Sam's site](https://sammohr.dev/keyboards).
I really like how the Clog V3 keyboard looks.
It oozes minimalism.
It is the keyboard manifestation of 'function over form'.

Aethestically, it was obvious that I wanted my keyboard to look the Clog V3, but with all the electronics hidden away.

# Wrapping Up
It's silly, but I chose a 34 keyboard layout because I thought it looked good.
Everything else required justification or is a happy accident.

In the next post, we'll define the key positions, and begin the schematic for the layout.
