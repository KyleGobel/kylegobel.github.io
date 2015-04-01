---
layout: post
title: Mono Embedding API Part 1
---

This post will walkthrough obtaining mono, and building it on Windows using any
edition of Visual Studio.

###Get the Mono Embedding API

Before we can start with the embedding API we'll need Mono itself.

Andreia Gaita ([Shana](https://github.com/shana))  has made a fork of mono with
some fixes to the embedding api, you can find her fork on [github](https://github.com/shana/mono).

I also have the same fork of mono, with the project files upgraded to VC++ 2013,
which can be found [here](https://github.com/kylegobel/mono).

So clone one of these repos, and switch to the ``embedding`` branch.

###Building Mono

Once your repo is cloned open it up in Visual Studio.

Before building mono, we'll have to build **genmdesc** first.  It can found in the
tools directory.

![Mono Project Structure](/images/buildFirst.png)

Right click and choose build.  Once that's finished we can build mono.

If all goes well we should have some output in our ``mono/msvc/Win32/bin`` folder.

Copy these files to a safe place, we'll need them later.

![Mono Build Output](/images/monoOutput.png)
