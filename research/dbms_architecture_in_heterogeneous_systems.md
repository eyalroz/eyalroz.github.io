---
layout: page
title: Analytic DBMSes in the face of heterogenous systems
subtitle: Architectural considerations facing non-uniform, intra-distributed, non-CPU-like processing
---

So, what's the best computational device to use for processing (analytic) DB queries, or doing other kinds of data-intensive analytic process? Should we bet on...

* [GPUs](../gpu_query_processing)?
* MICs (like Intel's Xeon Phi)?
* FGPAs?
* CPUs with speciality DBMS-oriented silicon (like Sparc M7)?
* ASICs?
* Perhaps the good old CPUs, close to the system memory and now with more cores and AVX register width?

The answer: None, that's the wrong question! Even if we ignore clusters of multiple machines, already in a single box you have multiple processors:

* Multiple sockets on the board, often with different processors in different sockets (e.g. Intel Harp)
* Coprocessors across buses such as PCIe, NVLink etc.
* Processing capability on NICs, on disk controllers, and soon perhaps next to memory

Sadly, it can be said with certainty that the DBMS world has barely begun coping with this heterogeneous reality. I mean, even single-device-focused query processing is still lacking *loads* of research, to establish how-we-can-do-what-fast on any of the devices available to us. So --- adding a second device to the mix? We're essentially clueless. Existing research on such cases follows almost exclusively the pattern of "Let's offload operations from the CPU to the Magical Device". Not that this is without merit --- it can well be useful --- but clearly we need to re-engineer our query processing engine to account for multiple devices, in different locations (i.e. different access possibilities to memory and other resources), with different constraints, strengths and weaknesses.

This is not entirely surprising, as even the leading DBMSes for analytics --- HyperDB, Vectorwise, or the not-as-fast but prominent FOSS solution, MonetDB --- are at their heart still hearkening back to the age of the single thread on the single core executing instructions one by one. Everything else is mostly an extension, a patch, on the basic design (Caveat: That observation is based on my own limited knowledge and experience.) Thus it is conceptually pretty difficult to throw in another, independent and different, computational unit into the mix.

During the latter part of my work at Huawei Research, we were just scratching surface of figuring out how CPU and GPU performance compared according to certain parameters, and were puzzling at even the simple dilemmata of which task to schedule were. But one should actually consider larger chunks of query execution plans: Sometimes an entirely different approach is better on some device than on others; sometimes it may be better to send some things back-and-forth; sometimes you should just have both devices working on the same thing, each one with its customized plan-fragment, divvying up the data between them so that it balances their perforamcne differently.


