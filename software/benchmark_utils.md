---
layout: page
title: Software
---

I've written free software coming from two different 'angles': As my own personal spare-time project, and more recently as part of my research work.

The first kind is a bit like scratching an itch: You're missing functionality on a system or in an application you're using, you find yourself repeating some tedious manual procedure, and at some point you just say "Fuck it, I'll just do it right once and for all". And then you spend a much-to-large amount of time working out all the corner cases, improving performance, adding feature you _don't_ need at all and you think are totally useless, but other users insist on having... so it takes on a life of its own.

## Thunderbird extensions 

The two prominent examples of the 'spare-time project' kind are my Thunderbird extensions. I'm a heavy user of email - receiving dozens a day, carefully auto-filtering them, and making sure I don't leave any unread (at worst I mark them unread if it's bulk I don't care for). Now, [Thunderbird](https://www.mozilla.org/thunderbird/) is not remotely the best mail client out there in many respects, but I used to use Netscape (which had a browser and a mail client combined) in the old days and the habit stuck. It's also multi-platform, relatively popular, based on a layout engine which pretty good support for Right-to-Left languages (my native language is Hebrew and I can also read Arabic with some effort), and - most importantly - it's very extension-friendly.

### [BiDi Mail UI](https://addons.mozilla.org/en-US/thunderbird/addon/bidi-mail-ui/) - BiDirectional language UI and other ehhancement

One extension was an initiative that two different people started simultaneously: Myself and [Asaf Romano](https://github.com/asaf-romano) were both frustrated by how Thunderbird was not exposing GUI for setting the direction of email messages you were reading - so that we were reading Hebrew email laid out the wrong way. Actually, there was an earlier extension which started addressing this problem, but most of the functionality was missing. So, both of us started improving it, and at some point we noticed each other's work, joined forces and merged our code. After that we added complex direction auto-detection, per-paragraph direction setting, correction of Mozilla's charset detection when it misses on right-to-left languages, etc. It's also important to mention additional [contributors](http://bidiui.mozdev.org/mail/credits.html) who, while not writing code for the most part, were instrumental in disseminating this work.

#Interestingly, this extension probably has many more users in the Arab countries and in Iran than in the much smaller Hebrew-speaking user base in Israel/Palestine - and it's been localized for those languages, and for less well-known-to-be-RTL languages - Urdu


### [Remove Duplicate Messages (Alternate)](https://addons.mozilla.org/addon/remove-duplicate-messages-alte/) - the sad consequence of non-free software

Don't you get annoyed when, by mistake, you get a bunch of emails re-sent to you? Or copy a folder with messages back into a folder which already has some of them? Well, I do. Now, there was already an extension for removing them, but alas - its license didn't allow for publishing modifications. So I had to blind-rewrite the whole damn thing! Luckily, I also made it a lot faster in the process and expanded the feature set, so it wasn't a complete waste of time. This one become an addons.mozilla.org recommended item for the message reading category, and by now has had over 100,000 users or so... my most popular piece of software to date.

## GPU & DBMS research-related

I've only gotten started with releasing pieces of the code I'm working on; but what I do release - I aim to be more widely applicable than just something you can plug into the rest of my code. So far I have:

* An on-GPU decompression library named [Giddy](https://github.com/eyalroz/libgiddy) for lightweight compression schemes, for use in a query processing engine or any other application with large amounts of compressible apriori-available data.
* A modern-C++ wrapper [library](https://github.com/eyalroz/cuda-api-wrappers) for the [CUDA Runtime API](http://docs.nvidia.com/cuda/cuda-runtime-api/) --- making it (hopefully) more streamlined, elegant and dare I say simple to use.
* Tools for automagically setting up (MonetDB) databases for benchmarking:

   * [tpch-tools](https://github.com/eyalroz/tpch-tools) using the [TPC-H](http://www.tpc.org/tpch/) benchmark
   * [usdt-ontime-tools](https://github.com/eyalroz/tpch-tools) using the US Department of Transport's [on-time flight data](https://www.transtats.bts.gov/ONTIME/)
   * ... and I'm planning to do the same for the SSB (Star-Schema Benchmark) sometime after SIGMOD 2017. That should also include merging some of the [forks](https://github.com/electrum/ssb-dbgen/network) of the benchmark's data generation utility [ssb-dbgen](https://github.com/electrum/ssb-dbgen)

---

I've also had the chance to work on some non-free software:

* Contributed to an implementation of greedy string memoization scheme within Actian Vector
* Worked on the back-end of Taboola's related-content recommendation engine
* Co-wrote a proof-of-concept query processor using discrete (nVIDIA) GPUs as part of a heterogeneous computing group in Hua Wei Israel (a.k.a. Toga Networks). This underpinned our [paper](https://www.researchgate.net/publication/308887432_Overtaking_CPU_DBMSes_with_a_GPU_in_Whole-Query_Analytic_Processing_with_Parallelism-Friendly_Execution_Plan_Optimization) in ADMS 2016 on the subject. Unfortunately, the group has been disbanded and the execution engine's code is just lying in some drawer to rot. Another consequence of code being closed-source... which made me promise myself to avoid working on non-free software again as much as I could.

