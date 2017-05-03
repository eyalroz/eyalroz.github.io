---
layout: page
title: Analytic query processing on discrete GPUs
---

The goal of effectively utilizing GPUs for (analytic) DB query processing is at the same time both tempting and elusive. It is *tempting* because databases have a lot of data in uniform tables, implying a lot of uniformly-parallel work to be performed on that data when processing a query; and GPUs' applicability has expanded over the past decade from mostly graphics and physical system simulation to many other domains --- so why not this one?

... but it is also very *elusive*, since DB analytics don't generally involve that much computation as much as shuffling data around: retrieving it sporadically, rearranging it, applying (cheap-to-compute) filters to it, sorting, joining... and those are quite the real forte of GPUs. Still, they do have an awful lot of computational resources to perform these tasks, so their utilization is a non-trivial *challenge* rather than an illusion. (Discrete) GPUs also suffer from being "farther away" from system memory than a CPU, in a typical system: Data has to traverse the PCIe bus to go from main memory to the GPU and back; and this already is a significant limiting factor on squeezing performance out of it.

It's thus not surprising that quite a large number of proof-of-concept or experimental systems, processing some benchmark queries using a GPU, have been presented - but none has so far developed into a proper usable complete system, which could mature into a product competitive with the top-performing analytic CPU-based databases.

I hope to build such a query processor: Map the challenges along the way to making that happen, devise efficient, elegant and future-anticipatory approaches to overcome the challenge; implement these solution, and publish them --- both as FOSS and as academic papers regarding their design, impact and relation to alternatives.

This will involve the exploration of issues such as:

* GPU device-side code generation (in SPIR and/or PTX most probably) for fusing operations
* Formalisms for representating execution plan, the state of their executions, and transformation rules for them
* Algorithms for query plan optimization in the face of a much richer plan space, doing away with the distinction between "logical" and "physical" plans
* GPU device-side code generation (in SPIR and in PTX, but perhaps even C++ code)
* The spectrum of Lighter- and heavier-weight apriori compression of columns and column groups
* Pushing down operations on compressed or otherwise differently-represented data
* Benefits vs overheads of executing plans using finer granularity (smaller number of elements at a time) --- on devices which like big chunks of data
* Cost models for individual on-GPU operations and entire query plans
* Useful statistics and meta-data for making individual computational operations easier, and for replacing different kinds of operations and plan fragments with each other
* Strategies for combining the use of managed and unamanged memory on the GPU, considering both latencies and bandwidths of communication during plan query execution
* Result size estimation using the GPU-oriented/GPU-specific variants of computational operations within plans that are better studied in a more general setting

and in addition to all these, a lot of elbow grease and keyboard taps are required to bring into existence quite a mass of code which currently still doesn't exist (just as an example: A library for managing memory allocations within a CUDA pre-allocated slab of device memory - even for the simplest case of known-workload online allocation; it just doesn't exist!)


A final point is that if one is careful in one's design and conceptual work, it could very well be that a focus on just the difference between two kinds of computational devices and their placement in the system (the CPU and the discrete GPU) will result in a query processor which is well-suited to put additional computational devices, of other kinds, to [good use](../dbms_architecture_in_heterogeneous_systems).
