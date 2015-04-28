---
layout:     post
title:      Brace Expansion
date:       2015-04-23 23:01:00
summary:    Use brace expansion to collapse multiple commands that are mostly identical into a single command.
categories: shells
---

One feature of Bash that would have saved me a lot of keystrokes if I'd known about it sooner is [brace expansion](https://www.gnu.org/software/bash/manual/bash.html#Brace-Expansion).

Here's the most common way I use it. Instead of typing out both full filenames when renaming a file, as you would like this:

{% highlight bash %}
$ mv README.markdown README.md
{% endhighlight %}

You can instead use brace expansion to specify what to change:

{% highlight bash %}
$ mv README.{markdown,md}
{% endhighlight %}

It's not even necessary to include a value on both sides of the comma, so if you're appending text to a filename it would look like this:

{% highlight bash %}
$ mv README{,.md}
{% endhighlight %}

For `mv`, the values are *old* and *new* but you can also use brace expansion with commands like mkdir or touch. Say you want to set up a new workspace for programming Go, you can do this in a single command like this:

{% highlight bash %}
$ mkdir -p ~/go/{bin,pkg,src}
{% endhighlight %}

One last thing. Brace expansion also supports iterating, and while I can't imagine a good use for it, here's how it's done:

{% highlight bash %}
$ touch emptyfile-{00..20}
$ ls
emptyfile-00    emptyfile-03    emptyfile-06    emptyfile-09    emptyfile-12    emptyfile-15    emptyfile-18
emptyfile-01    emptyfile-04    emptyfile-07    emptyfile-10    emptyfile-13    emptyfile-16    emptyfile-19
emptyfile-02    emptyfile-05    emptyfile-08    emptyfile-11    emptyfile-14    emptyfile-17    emptyfile-20
{% endhighlight %}

By prefixing the first value with an extra zero, Bash knows to pad all of the numbers with zeros to match the width of the end value.

The iteration can also accept a value to describe the increment used, like so:

{% highlight bash %}
$ touch evenfile-{2..20..2}
$ ls
evenfile-10     evenfile-14     evenfile-18     evenfile-20     evenfile-6
evenfile-12     evenfile-16     evenfile-2      evenfile-4      evenfile-8
{% endhighlight %}

But really, the only place I find myself using brace expansion frequently is for `mv` operations, and it's fantastic just for that.

