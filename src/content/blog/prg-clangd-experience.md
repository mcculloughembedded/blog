---
title: My Experience with clangd
author: David McCullough
pubDatetime: 2022-06-06T04:06:31Z
slug: my-experience-with-clangd
featured: false
draft: true 
tags: 
    - programming 
    - ready
description:
    My experience with clangd in embedded systems.
---

# What is clangd?
[clangd](https://clangd.llvm.org/) is a language server that provides smart editor features such as go-to-definition and code completion.
On it's own, it's a command line utility that isn't very useful.
Pair it with your favourite editor however, and you get a big part of the 'I' in 'IDE'(Integrated Development Environment).

# Background
I've been experimenting with [Neovim](https://neovim.io/) for a little while now.
Having finally gotten to a point where I have a configuration that I am able to maintain and extend myself (thanks [typecraft](https://www.youtube.com/watch?v=zHTeCSVAFNY&list=PLsz00TDipIffreIaUNk64KxTIkQaGguqn)!), I set about trying to tailor my setup to embedded development.

Like many developers, I'm coming from [VSCode](https://code.visualstudio.com/), where [Microsoft's C/C++ extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools) generally 'just works'.
I've never had an issue with VSCode, but even a brief look at Neovim is enough to see how powerful it can be.

For C/C++, clangd is to Neovim what [Intellisense](https://code.visualstudio.com/docs/editor/intellisense) is to VSCode[^clangd-vs-intellisense].
Therefore, to use Neovim for C/C++ development, one has to configure clangd.

# clangd Configuration
clangd requires at least one configuration file to understand your code base.
For anyone coming from VSCode, this is the equivalent of the [c_cpp_properties.json](https://code.visualstudio.com/docs/cpp/c-cpp-properties-schema-reference) file.

In clangd's case, there are three kinds of configuration files.

* compile_flags.txt
* .clangd
* compile_commands.json

The configuration files tell clangd how each source file is compiled.
clangd uses the configuration files to make the connections between the source files.
It's possible to use both _.clangd_ and _compile_commands.json_ in one project. 
In that configuration, _.clangd_ is used to specify global options for clangd, and _compile_commands.json_ is used to describe the compile flags for each source file.

When invoked on a certain file, clangd searches for the configuration files in the parent directory of the file.
The implication is that by default, all paths in the configuration files are relative to the current file.
The exception is the `directory` field in _compile_commands.json_.
This must be an absolute path.
However, the paths passed to the `arguments` field can be relative to the current file on which clangd is operating on.

Generally, _compile_commands.json_ is preferred, and overrides _.clangd_, which overrides _compile_flags.txt_.
The recommended place to put the configuration files is in the root of your project.

For the remainder of this post, we'll work with a project directory called 'clangd-config' that has the following structure:
```
clangd-config
│ clangd-configuration-file
├─inc
│  other.h 
└─src
   main.c
   other.c
```
clangd-configuration-file is either _compile_flags.txt_, _.clangd_ or _compile_commands.json_.

# Trying to Write the Configuration Files
In my case, I was locked into a pre-defined project structure and a custom toolchain.
That meant I had to mold the configuration files to my existing setup.

_compile_commands.json_ requires one entry for every file in the project.
It is usually automatically generated using another tool such as [Bear](https://github.com/rizsotto/Bear) or [CMake](https://cmake.org/).
I wanted to avoid using _compile_commands.json_ because I didn't think I could use any of the existing tools to create it.
My project structure is fixed, and all files compile with the same options.
It seemed that this is the ideal case for a _.clangd_ style configuration.

## .clangd
My first attempt was to place a _.clangd_ file in the root of my project.
I didn't realise that the paths must be relative to the source files.
I listed all the paths relative to the root of my project.
Of course, nothing worked!

I thought it may have to do with the indentation, or maybe the line endings.
After far too much time debugging, I gave up on _.clangd_ and tried _compile_flags.txt_.

I did eventually return to _.clang_ to see if I could get it to work.

For the project structure shown above, _.clangd_ might look something like this:
```yaml
CompileFlags:
    Add: [-std=c99, -I../inc]
    Compiler: clang++
```
The `Add` field is the list of compile flags that are passed to the compiler when building each source file.
Of course, you should add all the compile flags for your project to the list.

Note how the path for the `-I` flag moves up one directory.
It's relative to each source file, _not_ the location of _.clangd_.

If, for example, we added another .c file under `src/some-other-folder/`, clangd features wouldn't work completely.
For `main.c`, clangd would find _.clangd_ and `other.h`.
All of clangd's features would work for things declared in `other.h`.
For the new file, clangd would find _.clangd_ but would look in `src/inc/` for `other.h`, since the path is relative to the file being operated on.
Obviously, clangd would fail to find `other.h`, and anything in our new .c file using things from `other.h` would not be included in clangd's analysis.

This severely limits the use of a _.clangd_ file for specifying compile flags.
Effectively, all .c and .cpp files must be in the same directory.


## compile_flags.txt
_compile_flags.txt_ is a simplified version of _.clangd_. 
Both files let you specify the compile flags that are applied globally for every source file, but _.clangd_ has some extra options that change the behaviour of clangd.

Somehow I lucked into a working configuration.
I thought I had solved it!
Finally, a fully functioning Neovim setup for embedded systems!
It had taken far longer than it probably should have, but it was working!

Except, it wasn't.
Enter _background indexing_.

As a brief detour before discussing background indexing, here is the _compile_flags.txt_ file for our example project.
```
-std=c99
-I../inc 
```
Again, take note of the relative path for the `/inc` directory.
_compile_flags.txt_ suffers from similar problems as _.clangd_, for the same reasons.
It should only be used for extremely simple projects.

## Background Indexing
It turns out clangd builds an index containing information about every file for which it analyses.
The index is how clangd knows where to go to when you invoke go-to-definition, or what options to recommend in the autocompletion list.

Unfortunately, clangd only builds the entire index straight away if _compile_commands.json_ is used.
This means that if _.clangd_ or _compile_flags.txt_ is used to configure clangd, each source file has to be opened before any of clangd's fancy features are enabled for it.
That means things like go-to-definition and autocomplete don't work properly until the relevant files have been opened at least once.

Therefore, I couldn't get away with using only _.clangd_ or _compile_flags.txt_.
I needed to use _compile_commands.json_.

## compile_commands.json
There is absolutely no way a _compile_commands.json_ file can be managed manually.
One way or another, there must be something that generates it automatically.

In my case, it was relatively easy to write a [Python](https://www.python.org/) script that I could run as part of my project's build command.

It almost worked.

With my automatically generated _compile_commands.json_, clangd built it's index right away.
At first glance it seemed that everything was working well.
Soon, however, the cracks began to show, and before long they had split any hope of getting clangd to work into thousands of useless pieces.

A _compile_commands.json_ for our example project would look like this:
```json
[
    { 
        "directory": "/home/user/clang-config/src",
        "arguments": ["clang++", "-std=c99", "-I../inc", "-o", "-c", "main.o", "main.c"],
        "file": "main.c"
    },
    { 
        "directory": "/home/user/clang-config/src",
        "arguments": ["clang++", "-std=c99", "-I../inc", "-o", "-c", "other.o", "other.c"],
        "file": "other.c"
    },
]
```

I'm still not sure exactly why my custom made _compile_commands.json_ doesn't work.

One thing I don't like about the [_compile_commands.json_ format](https://clang.llvm.org/docs/JSONCompilationDatabase.html) is that the `directory` field must contain an absolute path. 
I think it would be better if this could be relative to the directory in which _compile_commands.json_ is stored.

# The Curse of the Embedded Compiler
clangd accepts the same arguments as the clang compiler, and interprets your source code as if it were compiled by clang.
If your actual compiler is not clang, clangd tries to find the equivalent clang flags, and uses those to work its magic.

If you're compiling for [X86](https://en.wikipedia.org/wiki/X86), or using a popular embedded compiler such as [ARM GCC](https://developer.arm.com/downloads/-/gnu-rm), this mostly works out.

However, if you're like me, you're not working with one of the hugely popular, and often open, compilers.
You're working with a compiler made for a microcontroller that the clangd developers might mention to each other once a decade.
clangd isn't able to translate your compile flags to the clang equivalent.
As a result, it spits out a bunch of false errors.

## query-driver
clangd does have a [--query-driver](https://releases.llvm.org/10.0.0/tools/clang/tools/extra/docs/clangd/Configuration.html) option.
As a last attempt, I added the flag and the path to my compiler in my Neovim config.

Whatever my compiler returned is not what clangd requires, and clangd failed to start.

# An Unexpected Breakthrough
A few weeks after giving up on clangd, I was casually looking around to see if there is an Intellisense integration for Neovim.
I stumbled across this [Reddit post](https://www.reddit.com/r/neovim/comments/17rhvtl/guide_how_to_use_clangd_cc_lsp_in_any_project/).

It was relatively easy to adapt the idea to my project.
A couple of [Bash](https://www.gnu.org/software/bash/) scripts later, and clangd was integrated into my toolchain and working properly for the first time!
I've been using my Neovim setup with clangd exclusively at work in the last few weeks.
There are a few false positives but in general everything is working extremely well.

I'm not sure why my attempt at generating a _compile_commands.json_ failed.
The CMake version creates a `/cmake` folder which stores the project's information.
That makes it difficult to compare it to my 'manual' method.


# Why Does Intellisense Work?
After struggling with clangd for so long, I wanted to know why Intellisense has been working so well for me thus far. 
I didn't spend too much time researching this, but from what I understand Intellisense analyses the raw text of the source files, while clangd analyses the project's theoretical build outputs.
Theoretically, the clangd analysis should be better.
Of course, whatever is being analysed must be 'clangd compatible'.

Intellisense works _most_ of the time.
I've found it tends to struggle with namespaces in C++, which makes sense given its text based analysis.
It has the advantage of being extremely easy to configure.
I've spent days fiddling with clangd, but I had Intellisense up and running in an hour or two.

I'm no expert on either Intellisense or clangd, so don't take the comments in this section as the absolute truth.

# The clangd Documentation
I've found the documentation for clangd to be lacking.
It feels scattered and at times incomplete.

It's strange because the [LLVM](https://llvm.org/) project is huge.
I think my struggles were born out of a number of problems.
The documentation is only one of them.

Looking back, I was trying to do things that the clangd developers would probably consider non-standard.
With that said, I wasted a lot of time debugging things that could have been avoided with clearer documentation.
If the documentation was more structured, better written and had more examples, I'm sure I would have spent far less time chasing ghosts.

Some of my problems could have been avoided if I had read more carefully, but I am still inclined to shift the blame onto the clangd documentation.
It felt clumsy and difficult to navigate.
Answers weren't where I thought they would be, and oftentimes the content only partially answered my questions.

In the end, it wasn't the official documentation that helped me to get it working.
In fact, most of the useful tips, hints, and information was found in various random posts scattered around the internet.

I spend a lot of time reading documentation.
Good documentation is a friction-less experience.
It not only walks you through the most common use cases of whatever it documents, it also provides an easily navigate-able reference for more complex use cases.
In my opinion, the clangd documentation doesn't do that.

I'm a big fan of the [Diataxis](https://diataxis.fr/) theory of documentation. 
It follows a system that is designed to avoid the problems that I feel the clangd documentation has.
Perhaps the LLVM project could consider Diataxis as a way to improve their documentation.

# Conclusion
This was a frustrating and time consuming experience.
In the end, I was able to get things working well.

I haven't use clangd long enough to see if it is really better than Intellisense.
However, I can already see that it does the job at least as well.

The main benefit is that I am now able to use Neovim for my embedded development at work.
This certainly wouldn't have been worth it if I was sticking with VSCode.
My day to day development experience is undoubtably better in Neovim.
I wouldn't be able to use Neovim at all if I hadn't struggled through this process.
For that reason alone, it was a worthwhile struggle.

In future, I will make sure so use CMake to set up my toolchain where possible.
That way, I can benefit from all of CMake's features directly, including it's ability to generate the _compile_commands.json_ configuration file.

[^clangd-vs-intellisense]: That's not quite the full story, but it's close enough for this post.
