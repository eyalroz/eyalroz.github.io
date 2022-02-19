---
layout: page
title: Software
---

## CUDA & GPU Programming

Unfortunately, most of my work writing software utilizing GPUs has been closed-source. But from other periods in my career-of-sorts, and my own unfunded efforts in parallel with paid work, I've been able to come up with two pieces of software which are quite generic, and of very wide applicability, for people using NVIDIA's CUDA ecosystem for programming GPUs.

Before presenting them, I have to offer an apology for the fact that this software is essentially vendor-specific. For various reasons - not the least of which being NVIDIA's own fault - I could not stick to the vendor-neutral standard which is OpenCL. I do, however, have some OpenCL-related ideas, so if you're an undergraduate student looking for an interesting coding project, or just an enthusiast in search of how to contribute, do [write me](../contact)

### [cuda-api-wrappers](https://github.com/eyalroz/cuda-api-wrappers/) - The CUDA Modern-C++ API Wrappers library

... as [presented](https://www.youtube.com/watch?v=aY3iD0dzsiw) (YouTube) to the Moscow CUDA Community meetup.

NVIDIA has invested significant effort in supporting modern C++ when writing the code which actually runs on the GPU: "Kernels" and (GPU-)device-side functions. However, the host-side API for setting up and orchestrating GPU execution is both fractured ("runtime" vs "driver" APIs, partially overlapping and not easy to combine), messy (think 20 kinds of `copySomethingToSomething()` functions), and hopelessly C-ish: Out-parameter pointer-to-pointer, error value returned from every function, no composability, no automatic resource cleanup, nothing.

I was not planning on addressing this problem generally, but as I was working on my analytic-DBMS-related kernels, I wrote a convience wrapper for some API call here, and there, and before you know it I had a large chunk of the whole runtime API (of that time) covered. So, I decided to go the whole way and complete it into a full set of wrappers.

This has been a 7-year journey in API design, adaptation and re-design, with NVIDIA adding new functionality and changing or deprecating existing API calls. Other than being quite useful for itself, writing something like this really makes you dig deep into the nooks and crannies of what CUDA offers.

Recently I've expanded the library's scope to include the CUDA Driver and JIT-compilation capabilities, bridging the fracture I'd mentioned above with a unified offering.

### [cuda-kat](https://github.com/eyalroz/cuda-kat/) - A CUDA Kernel Author's Toolkit 

... as [presented](https://www.youtube.com/watch?v=9WWCylrMNWo) (YouTube) to the Moscow CUDA Community meetup.

This library is mostly a collection of idioms I found myself repeating when writing GPU code. Unlike `cuda-api-wrappers`, here the focus is on _device-side_ code: Actual code running on the GPU, written in CUDA C++. Each set of "tools" in the "kit" covers another aspect of kernel authoring: Effectively using compiler builtins, Accessing PTX capabilities not made available by default, convenient functions for expressing information regarding the launch grid and the position with in it; and so on. Each of these can also be used more-or-less independently of the others, i.e. you don't have to "buy" into an entire framework, like you might have to when using, say, NVIDIA's [Thrust](https://nvidia.github.io/thrust/). On the other hand, when they are all combined, they make it _much_ easier to write _templated_ kernels, which plain vanilla CUDA does not really cater to.

