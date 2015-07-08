---
layout: page
title: Illustration of Git Concepts
subtitle: At Their Simplest
minutes: 10 max
---
> ## Learning Objectives {.objectives}
>
> *  Draw on the board

#Person 1#
So, here is a representation of a file in our coding project.

**draws square in top center**

And here are some of the contents of the file.

**draws circles inside square**

Don't stress too much about what these are. These are just representations of things in a file (or a project?).
This version of the file is our original.
In our terrible version control nightmare from before, we kept saving new versions of the file. 

**draws another square filled with circles on the next level, to the left**

So, if I made a small change, like *this* one...

**substitutes one circle with another shape**

I would have a new version, or I would save over the old one, which, I might, ultimately regret.

But with git, we save the **change** that we made.

**draws arrow from first square to second with label of circle ---> square**

#Person Two#

(Please use your own name and email address instead of Dracula's.)

He also has to set his favorite text editor, following this table:

| Editor             | Configuration command                            |
|:-------------------|:-------------------------------------------------|
| nano               | `$ git config --global core.editor "nano -w"`    |
| Text Wrangler      | `$ git config --global core.editor "edit -w"`    |
| Sublime Text (Mac) | `$ git config --global core.editor "subl -n -w"` |
| Sublime Text (Win) | `$ git config --global core.editor "'c:/program files/sublime text 2/sublime_text.exe' -w"` |
| Notepad++ (Win)    | `$ git config --global core.editor "'c:/program files (x86)/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"`|
| Kate (Linux)       | `$ git config --global core.editor "kate"`       |
| Gedit (Linux)      | `$ git config --global core.editor "gedit -s"`   |


Git commands are written `git verb`,
where `verb` is what we actually want it to do.
In this case,
we're telling Git:

*   our name and email address,
*   to colorize output,
*   what our favorite text editor is, and
*   that we want to use these settings globally (i.e., for every project),

The four commands above only need to be run once: the flag `--global` tells Git
to use the settings for every project on this computer.

You can check your settings at any time:

~~~ {.bash}
$ git config --list
~~~

You can change your configuration as many times as you want: just use the
same commands to choose another editor or update your email address.

> ## Proxy {.callout}
>
> In some networks you need to use a
> [proxy](https://en.wikipedia.org/wiki/Proxy_server). If this is the case, you
> may also need to tell Git about the proxy:
>
> ~~~ {.bash}
> $ git config --global http.proxy proxy-url
> $ git config --global https.proxy proxy-url
> ~~~
>
> To disable the proxy, use
>
> ~~~ {.bash}
> $ git config --global --unset http.proxy
> $ git config --global --unset https.proxy
> ~~~
