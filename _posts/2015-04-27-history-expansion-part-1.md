---
layout:     post
title:      History Expansion, Part 1
date:       2015-04-27 18:30:00
summary:    Use Bash History Expansion to recall prior commands
categories: shells
---

There are a lot of ways to work with history in Bash, but I'm going to show just a couple of simple ones in this post, and expand on this topic in later posts, where the methods become a little more involved.

One thing that I find myself doing often is either repeating a command in whole, or prefixing it with `sudo` because I've forgotten I'll need elevated privileges to execute the command. This is easily done with `!!`.

{% highlight bash %}
$ ntpd restart
27 Apr 13:00:23 ntpd[23283]: must be run as root, not uid 1000
$ sudo !!
sudo ntpd restart
{% endhighlight %}

(As usual on \*nix, no output means it worked.)

Notice Bash actually reports the expanded command it's executing, so you can see exactly what it looks like. That will be more important later when using more complex expansion methods.

The other history expansion method I want to demonstrate in this post is referencing an argument from the previous command, which is often useful when running a sequence of commands against a single file. For example here we want to extract the files for Twine after downloading it:

{% highlight bash %}
$ file twine_2.0.4.zip
twine_2.0.4.zip: Zip archive data, at least v1.0 to extract
$ unzip -q !$
unzip -q twine_2.0.4.zip
{% endhighlight %}

Again, you see the expanded command. While unzip would normally tell us all the files it's pulled out of the archive, we pass `-q` (quiet) to keep the example tidy.

You may wonder now what happens if we use `!$` again. Will it reference `-q` or the file name, `twine_2.0.4.zip`? Let's find out by trying to delete the zip file, since we don't need it anymore.

{% highlight bash %}
$ rm !$
rm twine_2.0.4.zip
{% endhighlight %}

So, yeah, options (`-q` in this case) are ignored. Makes sense because you're probably not running the same command and options are very specific to the command.

In the next post (or two) I'll cover some additional ways of working with history that are a little more powerful and flexible.

