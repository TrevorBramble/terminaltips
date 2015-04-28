---
layout:     post
title:      Changing Shells
date:       2014-12-31 00:10:00
summary:    Changing your default shell, trying other shells temporarily.
categories: shells
---

When using a terminal to interact with your system, the command-line interface is provided by a shell program. The two most commonly chosen shells are [Bash](https://www.gnu.org/software/bash/) (the Bourne Again SHell) and [Z Shell](http://www.zsh.org/) (zsh).

First see if you even need to switch, or if you're already using the shell you want by printing the name of the current shell.

{% highlight bash %}
$ echo $0
bash
{% endhighlight %}

You may have come across the `$SHELL` environment variable, but it won't always do what you expect it to do as you can see below when I switch to `zsh` and `bash` is still the value of `$SHELL`, so you're better off just relying on `$0`.

{% highlight bash %}
$ echo $SHELL
bash
$ zsh
$ echo $SHELL
bash
{% endhighlight %}

So if I've confirmed I'm using `bash` and I actually want to tinker with `zsh`, I can either invoke `zsh` as above to use it temporarily, or I can make it my default shell, so it will be the shell used automatically in new terminal sessions.

Changing your default (or login) shell is done using the `chsh` utility. First we'll list the available shells to make sure it's been correctly installed.

{% highlight bash %}
$ chsh -l
/bin/sh
/bin/bash
/bin/zsh
/usr/bin/zsh
{% endhighlight %}

Which is simply the contents of `/etc/shells`.

{% highlight bash %}
$ cat /etc/shells
/bin/sh
/bin/bash
/bin/zsh
/usr/bin/zsh
{% endhighlight %}

Now I invoke `chsh` and specify the shell I want to use.

{% highlight bash %}
$ chsh -s /usr/bin/zsh
Changing shell for trevor.
Password:
Shell changed.
{% endhighlight %}

And after logging out and logging back in (just opening a new terminal won't work) I can confirm that `zsh` is now my shell.

{% highlight bash %}
$ echo $0
zsh
{% endhighlight %}


