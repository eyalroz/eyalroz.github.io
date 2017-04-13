---
layout: post
title: Feeling giddy for DaMoN 2017
subtitle: Where we'll be decompressin' with my new FOSS library
---

<a style="display: block; text-align:center;" href="https://github.com/eyalroz/libgiddy/">libGiddy on GitHub</a>

Today the [DaMoN 2017](http://daslab.seas.harvard.edu/damon2017/) notifications went out. My paper with Peter (Boncz) was partially accepted into DaMoN, with one of the reviewers complaining that the paper reads more like a library documentation; another complained about lack of take-home's; and two reviewers complained about the paucity of discussion. The result is that an even-shorter version of the paper has been accepted, as well as a poster to be presented at the conference. 

I feel this is a manifetation of my personal focus on making usable, workable, hopefully-high-quality Free Software code available --- at the expense of a discussion on the abstract level. For a six-page submission you have to make a painful trade-off between the two, and my choice (despite Peter's involvement, it was a choice I made) to focus on "Here is something you can download, build and use today" was not well enough received. Our reviewers were making valid points, however, and I hope to build on the work I've done so far with a near-future submission heavier on the more abstract description and discussion of the novelty, implications and intended use.

Still --- short paper, longer paper or poster --- it's all good publicity to get the word out about the lightweight GPU decompression library: [Giddy](https://github.com/eyalroz/libgiddy/). Try it out...

Finally: A shoutout to my research group members [Hannes Mühleisen](http://homepages.cwi.nl/~lsidir/) and [Lefteris Sidirourgos](http://homepages.cwi.nl/~lsidir/), whose [paper](http://hannes.muehleisen.org/damon2017-simd-imprints.pdf) on optimizing MonetDB column [imprints](http://homepages.cwi.nl/~lsidir/publications/sigmod2013-sidirourgos.pdf) using SIMD made DaMoN 2017 properly. (Lefteris has just left us for the [ETH systems group](https://www.systems.ethz.ch/)).

<!---
You can write regular [markdown](http://markdowntutorial.com/) here and Jekyll will automatically convert it to a nice webpage.  I strongly encourage you to [take 5 minutes to learn how to write in markdown](http://markdowntutorial.com/) - it'll teach you how to transform regular text into bold/italics/headings/tables/etc.

**Here is some bold text**

## Here is a secondary heading

Here's a useless table:
 
| Number | Next number | Previous number |
| :------ |:--- | :--- |
| Five | Six | Four |
| Ten | Eleven | Nine |
| Seven | Eight | Six |
| Two | Three | One |
 

How about a yummy crepe?

![Crepe](http://s3-media3.fl.yelpcdn.com/bphoto/cQ1Yoa75m2yUFFbY2xwuqw/348s.jpg)

Here's a code chunk:

~~~
var foo = function(x) {
  return(x + 5);
}
foo(3)
~~~

And here is the same code with syntax highlighting:

```javascript
var foo = function(x) {
  return(x + 5);
}
foo(3)
```

And here is the same code yet again but with line numbers:

{% highlight javascript linenos %}
var foo = function(x) {
  return(x + 5);
}
foo(3)
{% endhighlight %}


--->
