---
layout: page
title: Analytic query processing on discrete GPUs
---

The goal of effectively utilizing GPUs for (analytic) DB query processing is at the same time both tempting and elusive. It is *tempting* because databases have a lot of data in uniform tables, implying a lot of uniformly-parallel work to be performed on that data when processing a query; and GPUs' applicability has expanded over the past decade from mostly graphics and physical system simulation to many other domains --- so why not this one?

... but it is very *elusive*, since DB analytics usually doesn't involve so much computation as shuffling data around --- accessing it, rearranging it, applying filters (which are usually cheap to compute), sorting, joining etc --- and that is not actually GPUs' forte. They do have an awful lot of computational resources to perform these, however, so their utilization is a non-trivial *challenge* rather than an illusion. (Discrete) GPUs also suffer from being "farther away" from system memory than a CPU, in a typical system: Data has to traverse the PCIe bus to go from main memory to the GPU and back; and this already is a significant limiting factor on squeezing performance out of it.

It's thus not surprising that proof-of-concept or experimental systems, processing some benchmark queries, have been presented - but none has so far developed into a proper usable system, which are competitive with the top-performing analytic CPU-based databases.

I hope to build such a query processor --- or more specifically, map the challenges along the way to making that happen, devise efficient, elegant and future-anticipatory approaches to overcome the challenge; implement these solution, and publish them --- both as FOSS and as academic papers.

This will involve the exploration of issues such as:

* GPU device-side code generation (in SPIR and/or PTX most probably) for fusing operations
* Formalisms for representating execution plan, the state of their executions, and transformation rules for them
* Algorithms for query plan optimization in the face of a much richer plan space, doing away with the distinction between "logical" and "physical" plans
* GPU device-side code generation (in SPIR and PTX, but perhaps even C++ code)
* The spectrum of Lighter- and heavier-weight apriori compression
* Pushing down operations on compressed or otherwise differently-represented data
* Benefits vs overheads of finer granularity --- on device which like big chunks of data
* Useful statistics and meta-data for making the GPU's job easier
* Allocation of managed and unamanged memory on the GPU, considering both latencies and bandwidths of communication during plan query execution
* Time and space cost models for on-GPU work


A final point is that if one is careful in your design and conceptual work, it could very well be that a focus on just the difference between two kinds of computational devices and their placement in the system (the CPU and the discrete GPU) will result in a query processor which is relatively well-suited to put other computational devices to [good use](../dbms_architecture_in_heterogeneous_systems).
