---
layout: page
title: Benchmark utilities
---

When you're studying or designing analytic query processing/DBMS engines, you're obviously interested in performance. This is a vague term, and especially so in this field, where there is so much variety of systems, settings and workloads. A natural --- and somewhat problematic --- tendency is to focus on concrete benchmarks: Combinations of query sets (or query distributions); data sets (or generators for them); and testing procedures. These allow some sort of quantitative comparison of different systems, and perhaps more importantly, are useful when working on improvements of the same system.

My own limited work on analytic query processing involved two proper benchmarks, and and one data set which isn't a full-fledged benchmark, but has been rather popular in evaluating and showcasing systems. For each of these I ended up contributing some utility code, which either nobody had stepped up to write, or on the contrary --- many people had stepped up to write parts of, but no-one had integrated.

### [TPC-H dbgen](https://github.com/eyalroz/tpch-dbgen/) - Unified data set generator for the TPC-H benchmark

[TPC-H](http://www.tpc.org/tpch/) is by far the most well-known and widely-used benchmark for analytical DBMSes. In fact, it is massively overused and misused, with some systems developed with only TPC-H performance in mind. It is not a large benchmark suite of benchmarks, and its queries are not too complex, helping its popularity. However, it is absolutely non-representative of any real-world usage scenario, for a plethora of reasons (for example, see the discussion here: [this](https://ir.cwi.nl/pub/27429/27429.pdf). Despite this fact, and its gaining in age, it remains popular.

TPC-H is published by the [Transaction Processing Council](http://www.tpc.org), a sort of industry consortium, also responsible for other important benchmarks; and its speficiation document is accompanied by a liberally-licensed utility for generating the data: `dbgen`.

Unfortunately, TPC is a sluggish bureacuracy of rivals, not a software development outfit, and thus - their `dbgen` utility is not high-quality portable software, and is riddled by many bugs and some functional deficiencies. Over the years, dozens - if not hundreds - of people have had to fix the specific issues manifesting on their own systems, creating custom versions of the utility. Even if we limit our focus to the brave souls who posted their code on GitHub, we have [(at least) 79 such repositores](https://github.com/eyalroz/tpch-dbgen/network/members).

I took it upon myself to merge all of those forks, which had changes which were somehow applicable and useful to the general public. This was not a trivial feat, since different authors made conflicting changes, and would sometime break compatibility with one platform or configuration while making the utility suit their needs. At some point, I also realized it was time to have a proper build system generator, rather than manually edit a Makefile --- so I switched the repository to using CMake.

### [TPC-H tools](https://github.com/eyalroz/tpch-tools/) - Tools for using the TPC-H benchmark with MonetDB

To use a benchmark with a DBMS, it's not sufficient to just generate the test data. You need to work with the DBMS to set up a new DB, schemata, constraints, and then to load the data you created. Such work is not generic, but rather DBMS-specific; and this repository covers it for [MonetDB](https://www.monetdb.org/).

MonetDB is a columnar, analytics-focused DBMS which serves as a baseline for a lot of research work has been, originated at [Database Architectures research group at CWI Amsterdam](https://www.cwi.nl/research/groups/database-architectures) (though now maintained and developed by a commercial spin-off which coexists with the research group). I had worked with MonetDB when I was at Toga Networks/Huawei, and then I joined the research group at Amsterdam, so I have a soft spot for it besides its technical virtues.


### [SSB dbgen](https://github.com/eyalroz/ssb-dbgen/) - Unified data set generator for the SSB benchmark

The "Star-Schema Benchmark", or SSB, is a somewhat-popular benchmark derived from TPC-H by researchers at the University of Massachsats Boston, rearranging the data tables into a [star schema](https://en.wikipedia.org/wiki/Star_schema) and authoring a different query set. Unlike the TPC-H, there is no organization backing this benchmark, and no official distribution of its data generation utility.

Since SSB's data generation utility is a fork of TPC-H, it was relatively straightforward to give it the same treatment: Collect bug fixes, transition to CMake, identify additional sources of bugs, avoid warnings etc.

### [SSB  tools](https://github.com/eyalroz/ssb-tools/) - Tools for using the SSB benchmark with MonetDB

The SSB equivalent of #TPC-H-tools .


### [USDT-Ontime tools](https://github.com/eyalroz/usdt-ontime-tools/) - Tools for using the USDT On-Time performance dataset with MonetDB

Unlike TCP-H and SSB, there is no benchmark called "USDT Ontime". There is, however, a popular data set published by the United States Bureau of Transport Statistics: Data about domestic US flights, their schedules and actual arrivals, departures, delays and cancellations. This raw data is available as compressed monthly CSV file, for download over the Internet.

Since data isn't generated here, this utility involves downloading, decompressing, parsing and loading in parts - with carefully-chosen schema field sizes.




