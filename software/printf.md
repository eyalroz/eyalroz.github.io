---
layout: page
title: Software
---

## printf() and friends... yes, really :-)

When we learn C programming for the first time, we often have the idea that "hey, I could implement that myself!" - about those library features that don't require OS-specific voodoo (like terminal emulation and such). This is especially true case for string-related functions, like `strcpy()`, or `strcat()` or `atoi()` and `atof()`. And then there's `printf()` (and its family: `sprintf()`, `vsprintf()`, `snprintf()` etc.). This is a bit more hefty, but we tend to think of its implementation as just some busy-work that someone has saved us the trouble of doing.

Well, that's absolutely not the case. First, an innovative implementation of (parts of) `printf()` can very well [land you](https://dl.acm.org/doi/abs/10.1145/249069.231397) a [well-cited](https://hal.archives-ouvertes.fr/hal-01227877) [paper](https://www.ampl.com/REFS/rounding.pdf) - because efficient and optimal conversion of a base-2 floating-point value into a base-10 value is quite challenging; and even more so if you want to use the inaccurate floating-point operations different kinds of hardware provide you with.

Still, one would ask - why both at all? Surely this is a solved problem, right? Who needs your custom `printf`-functions implementations, when the standard C library is available basically everywhere? Well, again, this is a misconception: Many platforms for which you may compile code _do not_ actually have a C library for you to use. The hardware would simply not support it. Only some of it, parts of it, are usable - and are often unavailable. In these cases, a stand-alone implementation of `printf()` is often called for. 

A particular example is GPU programming: You _can_ use `printf()` in GPU code, but you _don't_ have `sprintf()` available, neither in OpenCL nor CUDA; and `printf()` itself is missing some of its standard-library functionality. This which explains my motivation of getting into the "`printf()` business".

A larger category of use cases is small embedded systems: microcontrollers and extremely-low-resource CPUs. For these scenarios, even if a C library could be ported - it would be unusable: Way too much code. Programs intended for such devices (often written to their firmware) are in need of extremely _small_ implementations, possibly with only a part of the features implemented. But developers do not want to write their own `printf()`, and risk introducing their own bugs; they would rather rely on a popular - if not quite standard - implementation which has had any bugs and kinks worked out.

Hence:

### [printf](https://github.com/eyalroz/prinf/) - A standalone printf/sprintf formatted printing function library for embedded systems

I was going to "rely on a popular implementation" of `sprintf()` for use in my GPU code. I was first disappointed - though not surprised - that a decent one was not available which supports use in CUDA. I then turned to C-standard-libary-independent `printf()`-family libraries targetting embedded devices - and chose the most popular: `libprintf`, or just `printf`, by Macro Paland.

To my chagrin, Mr. Paland had effectively abandoned his popular library after 5 years of work, and it had languished between 2019 and 2021, with quite a few bug reports piling up. And as with other repositories in the past, here too I saw the familiar scene: A dozen forks, each fixing its pet bug, none merged back into the original repository.

So, I created my own forked, and proceeded with merging. While doing so, and trying to streamline the code and expand the test suite, I found... well, I found dozens of additional bugs and other issues myself. And when it was apparent I was an effective and responsive maintainer, other developers started making requests of their own - for features, compatibility and configurability. Within a few months I was approaching 200 (!) different commits on a library for nothing but the "trivial" task of
`printf()`-ing - after 5 years of work by other developers. I am still amazed :-)

The code is now somewhat longer, somewhat featureful, more widely compatible, compiles without warnings, much more robust, more accurate, and last but not least - significantly more readable too.



