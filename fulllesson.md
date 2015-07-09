#Open Up Your Terminal#


> ## Learning Objectives {.objectives}
>
> *   Understand the benefits of an automated version control system.
> *   Understand the basics of how Git works.

We'll start by exploring how version control can be used
to keep track of what one person did and when.
Even if you aren't collaborating with other people,
automated version control is much better than this situation:

[![Piled Higher and Deeper by Jorge Cham, http://www.phdcomics.com](fig/phd101212s.gif)](http://www.phdcomics.com)

"Piled Higher and Deeper" by Jorge Cham, http://www.phdcomics.com

We've all been in this situation before: it seems ridiculous to have multiple nearly-identical versions of the same document. Some word processors let us deal with this a little better, such as Microsoft Word's "Track Changes" or Google Docs' version history.

The key to understanding git is to remember that instead of storing multiple versions of the whole file, git, instead keeps track of the **differences** between each version.
_______

## Demonstrate on Board with Pete ##

1. Original file
2. A copy at the top of my branch
3. I share with Pete, copy at top of his branch.
4. I make a change.
5. Meanwhile Pete makes multiple changes with multiple commits.
6. We merge the two improved versions by applying Pete's commits to my file.

[![Demonstration](fig/IMG_0281.jpg)]

_______________

Version control systems start with a base version of the document and then save just the changes you made at each step of the way. You can think of it as a tape: if you rewind the tape and start at the base document, then you can play back each change and end up with your latest version.



Once you think of changes as separate from the document itself, you can then think about "playing back" different sets of changes onto the base document and getting different versions of the document. For example, two users can make independent sets of changes based on the same document.



If there aren't conflicts, you can even try to play two sets of changes onto the same base document. This is what we did during that last step.



A version control system is a tool that keeps track of these changes for us and
helps us version and merge our files. It allows you to
decide which changes make up the next version, called a
[commit](reference.html#commit), and keeps useful metadata about them. The
complete history of commits for a particular project and their metadada make up
a [repository](reference.html#repository). Repositories can be kept in sync
across different computers facilitating collaboration among different people.


#Setting Up Git#

> ## Learning Objectives {.objectives}
>
> *  Configure `git` the first time is used on a computer.
> *  Understand the meaning of the `--global` configuration flag.

When we use Git on a new computer for the first time,
we need to configure a few things. Rememberthe email address you used to register with github? Go ahead and use that during this part of the setup.


~~~ {.bash}
$ git config --global user.name "Vlad Dracula"
$ git config --global user.email "vlad@tran.sylvan.ia"
$ git config --global color.ui "auto"
~~~

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

Also, instruct everyone to navigate to **home directory**:

~~~ {.bash}
$ cd
~~~


#COMPREHENSION CHECK VIA STICKIES#



> ## Learning Objectives {.objectives}
> 
> *   Create a local Git repository.

Once Git is configured,
we can start using it.
**REMINDER** : Check to makes sure you are in the right directory -- the home directory.

~~~ {.bash}
$ pwd
~~~



Let's create a directory for our work and then move into that directory:

~~~ {.bash}
$ mkdir planets
$ cd planets
~~~

The directory "planets" should be empty since we just made it. I'm going to use the `-a` flag so that `ls` will show me everything in the directory, including any hidden files:

~~~ {.bash}
$ ls -a
~~~


Now we tell Git to make `planets` a [repository](reference.html#repository)&mdash; a place where
Git can store versions of our files:

~~~ {.bash}
$ git init
~~~

If we use `ls` to show the directory's contents,
it appears that nothing has changed:

~~~ {.bash}
$ ls
~~~

But if we use that `-a` flag to show everything,
we can see that Git has created a hidden directory within `planets` called `.git`:

~~~ {.bash}
$ ls -a
~~~
~~~ {.output}
.	..	.git
~~~

Git stores information about the project in this special sub-directory.
If we ever delete it,
we will lose the project's history.

We can check that everything is set up correctly
by asking Git to tell us the status of our project:

~~~ {.bash}
$ git status
~~~
~~~ {.output}
# On branch master
#
# Initial commit
#
nothing to commit (create/copy files and use "git add" to track)
~~~


#STICKY CHECK#

> ## Learning Objectives {.objectives}
> 
> *   Go through the modify-add-commit cycle for single and multiple files.
> *   Explain where information is stored at each stage of Git commit workflow.

Let's create a file called `venus.txt` that contains some awesome facts about the planet, Venus. In this case, I'm going to use `nano` to create and edit the file, like so:

~~~ {.bash}
$ nano venus.txt
~~~

Type the text below into the `venus.txt` file:

~~~ {.output}
A day on Venus is longer than a year on Venus.
~~~
Now, we use the command `CTRL + O` to write to the file; press enter to confirm the name of the file to which we want to save the contents; and now `CTRL + X` to exit the editor.
(Windows users, you may notice that your command history has -- seemingly -- disappeared from your terminal, but if you use the up arrow, you should still be able to recall previous commands.)


`venus.txt` now contains a single line, which we can see by running:

~~~ {.bash}
$ ls
~~~
~~~ {.output}
venus.txt
~~~
~~~ {.bash}
$ cat venus.txt
~~~
~~~ {.output}
A day on Venus is longer than a year on Venus.
~~~

If we check the status of our project again,
Git tells us that it's noticed the new file:

~~~ {.bash}
$ git status
~~~
~~~ {.output}
# On branch master
#
# Initial commit
#
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#	venus.txt
nothing added to commit but untracked files present (use "git add" to track)
~~~

The "untracked files" message means that there's a file in the directory
that Git isn't keeping track of.
We can tell Git to track a file using `git add`:

~~~ {.bash}
$ git add venus.txt
~~~

and then check that the right thing happened:

~~~ {.bash}
$ git status
~~~
~~~ {.output}
# On branch master
#
# Initial commit
#
# Changes to be committed:
#   (use "git rm --cached <file>..." to unstage)
#
#	new file:   venus.txt
#
~~~

Git now knows that it's supposed to keep track of `venus.txt`,
but it hasn't recorded these changes as a commit yet.
To get it to do that,
we need to run one more command:

~~~ {.bash}
$ git commit -m "Start listing facts about Venus"
~~~
~~~ {.output}
[master (root-commit) f22b25e] Start listing facts about Venus
 1 file changed, 1 insertion(+)
 create mode 100644 venus.txt
~~~

When we run `git commit`,
Git takes everything we have told it to save by using `git add`
and stores a copy permanently inside the special `.git` directory.
This permanent copy is called a [commit](reference.html#commit)
(or [revision](reference.html#revision)) and its short identifier is `f22b25e`
(Your commit may have another identifier.)

We use the `-m` flag (for "message")
to record a short, descriptive, and specific comment that will help us remember later on what we did and why.
If we just run `git commit` without the `-m` option,
Git will launch `nano` (or whatever other editor we configured as `core.editor`)
so that we can write a longer message.

[Good commit messages][commit-messages] start with a brief (<50 characters) summary of
changes made in the commit. 


If we run `git status` now:

~~~ {.bash}
$ git status
~~~
~~~ {.output}
# On branch master
nothing to commit, working directory clean
~~~

it tells us everything is up to date. This means that the current state of the repository matches the most recent snapshop that git has stored.
If we want to know what we've done recently,
we can ask Git to show us the project's history using `git log`:

~~~ {.bash}
$ git log
~~~
~~~ {.output}
commit f22b25e3233b4645dabd0d81e651fe074bd8e73b
Author: Vlad Dracula <vlad@tran.sylvan.ia>
Date:   Thu Aug 22 09:51:46 2013 -0400

    Start listing facts about Venus
~~~

`git log` lists all commits  made to a repository in reverse chronological order.
The listing for each commit includes
the commit's full identifier
(which starts with the same characters as
the short identifier printed by the `git commit` command earlier),
the commit's author,
when it was created,
and the log message Git was given when the commit was created.

> ## Where Are My Changes? {.callout}
>
> If we run `ls` at this point, we will still see just one file called `mars.txt`.
> That's because Git saves information about files' history
> in the special `.git` directory mentioned earlier
> so that our filesystem doesn't become cluttered
> (and so that we can't accidentally edit or delete an old version).

Now suppose we add more information to the file. I know plenty of interesting things about venus.
(Again, we'll edit with `nano` and then `cat` the file to show its contents;
you may use a different editor, and don't need to `cat`.)

~~~ {.bash}
$ nano venus.txt
$ cat venus.txt
~~~
~~~ {.output}
A day on Venus is longer than a year on Venus.
Venus moves around the Sun in the opposite direction as Earth.
~~~

When we run `git status` now,
it tells us that a file it already knows about has been modified:

~~~ {.bash}
$ git status
~~~
~~~ {.output}
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#	modified:   venus.txt
#
no changes added to commit (use "git add" and/or "git commit -a")
~~~

The last line is the key phrase:
"no changes added to commit".
We have changed this file,
but we haven't told Git we will want to save those changes
(which we do with `git add`)
nor have we saved them (which we do with `git commit`).
So let's do that now. It is good practice to always review
our changes before saving them. We do this using `git diff`.
This shows us the differences between the current state
of the file and the most recently saved version:

~~~ {.bash}
$ git diff
~~~
~~~ {.output}
diff --git a/venus.txt b/venus.txt
index df0654a..315bf3a 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1 +1,2 @@
 A day on Venus is longer than a year on Venus.
+Venus moves around the Sun in the opposite direction as Earth.
~~~

The output is cryptic because
it is actually a series of commands for tools like editors and `patch`
telling them how to reconstruct one file given the other.
If we break it down into pieces:

1.  The first line tells us that Git is producing output similar to the Unix `diff` command
    comparing the old and new versions of the file.
2.  The second line tells exactly which versions of the file
    Git is comparing;
    `df0654a` and `315bf3a` are unique computer-generated labels for those versions.
3.  The third and fourth lines once again show the name of the file being changed.
4.  The remaining lines are the most interesting, they show us the actual differences
    and the lines on which they occur.
    In particular,
    the `+` markers in the first column show where we have added lines.

After reviewing our change, it's time to commit it:

~~~ {.bash}
$ git commit -m "Add another fascinating fact about the second planet"
$ git status
~~~
~~~ {.output}
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#	modified:   venus.txt
#
no changes added to commit (use "git add" and/or "git commit -a")
~~~

Whoops:
Git won't commit because we didn't use `git add` first.
Let's fix that:

~~~ {.bash}
$ git add venus.txt
$ git commit -m "Add another fascinating fact about the second planet"
~~~
~~~ {.output}
[master 34961b1] Add another fascinating fact about the second planet
 1 file changed, 1 insertion(+)
~~~


##Exercise 1##

Add another fact about the planet Venus to venus.txt. Stage the change (with `add`) and then commit it.

(If you don’t know any other facts, you can google it or make one up -- dealer’s choice!)





##not planning on saying this
Git insists that we add files to the set we want to commit
before actually committing anything
because we may not want to commit everything at once.
For example,
suppose we're adding a few citations to our supervisor's work
to our thesis.
We might want to commit those additions,
and the corresponding addition to the bibliography,
but *not* commit the work we're doing on the conclusion
(which we haven't finished yet).

To allow for this,
Git has a special *staging area*
where it keeps track of things that have been added to
the current [change set](reference.html#change-set)
but not yet committed.

> ## Staging area {.callout}
> If you think of Git as taking snapshots of changes over the life of a
> project,
> `git add` specifies *what* will go in a snapshot
> (putting things in the staging area),
> and `git commit` then *actually takes* the snapshot, and
> makes a permanent record of it (as a commit).
> If you don't have anything staged when you type `git commit`,
> Git will prompt you to use `git commit -a` or `git commit --all`,
> which is kind of like gathering *everyone* for the picture!
> However, it's almost always better to
> explicitly add things to the staging area, because you might
> commit changes you forgot you made. (Going back to snapshots,
> you might get the extra with incomplete makeup walking on
> the stage for the snapshot because you used `-a`!)
> Try to stage things manually,
> or you might find yourself searching for "git undo commit" more
> than you would like!

![The Git Staging Area](fig/git-staging-area.svg)

Let's watch as our changes to a file move from our editor
to the staging area
and into long-term storage.
First,
we'll add another line to the file:

~~~ {.bash}
$ nano mars.txt
$ cat mars.txt
~~~
~~~ {.output}
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
~~~
~~~ {.bash}
$ git diff
~~~
~~~ {.output}
diff --git a/mars.txt b/mars.txt
index 315bf3a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1,2 +1,3 @@
 Cold and dry, but everything is my favorite color
 The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
~~~

So far, so good:
we've added one line to the end of the file
(shown with a `+` in the first column).
Now let's put that change in the staging area
and see what `git diff` reports:

~~~ {.bash}
$ git add mars.txt
$ git diff
~~~

There is no output:
as far as Git can tell,
there's no difference between what it's been asked to save permanently
and what's currently in the directory.
However,
if we do this:

~~~ {.bash}
$ git diff --staged
~~~
~~~ {.output}
diff --git a/mars.txt b/mars.txt
index 315bf3a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1,2 +1,3 @@
 Cold and dry, but everything is my favorite color
 The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
~~~

it shows us the difference between
the last committed change
and what's in the staging area.
Let's save our changes:

~~~ {.bash}
$ git commit -m "Discuss concerns about Mars' climate for Mummy"
~~~
~~~ {.output}
[master 005937f] Discuss concerns about Mars' climate for Mummy
 1 file changed, 1 insertion(+)
~~~

check our status:

~~~ {.bash}
$ git status
~~~
~~~ {.output}
# On branch master
nothing to commit, working directory clean
~~~

and look at the history of what we've done so far:

~~~ {.bash}
$ git log
~~~
~~~ {.output}
commit 005937fbe2a98fb83f0ade869025dc2636b4dad5
Author: Vlad Dracula <vlad@tran.sylvan.ia>
Date:   Thu Aug 22 10:14:07 2013 -0400

    Discuss concerns about Mars' climate for Mummy

commit 34961b159c27df3b475cfe4415d94a6d1fcd064d
Author: Vlad Dracula <vlad@tran.sylvan.ia>
Date:   Thu Aug 22 10:07:21 2013 -0400

    Add concerns about effects of Mars' moons on Wolfman

commit f22b25e3233b4645dabd0d81e651fe074bd8e73b
Author: Vlad Dracula <vlad@tran.sylvan.ia>
Date:   Thu Aug 22 09:51:46 2013 -0400

    Start notes on Mars as a base
~~~

To recap, when we want to add changes to our repository,
we first need to add the changed files to the staging area
(`git add`) and then commit the staged changes to the
repository (`git commit`):

![The Git Commit Workflow](fig/git-committing.svg)

#AND WE'RE BACK#

##Log Into Github##
Explain that, unless you pay, all github repositories are public. This can be a little daunting. Gihub has a special developer pack that they are willing to give you for free, since you are students. This will allow you to have a few private repositories, which might be good, since public repositories can make some people feel a little self conscious. You don't have to do it this instant, but I encourage you to apply for the free pack here:

**EDUPACK** link: 
https://education.github.com/pack


> ## Learning Objectives {.objectives}
>
> *   Explain what remote repositories are and why they are useful.
> *   Clone a remote repository. 
> *   Push to or pull from a remote repository.

Version control really comes into its own
when we begin to collaborate with other people.
We already have most of the machinery we need to do this;
the only thing missing is to copy changes from one repository to another.

Systems like Git allow us to move work between any two repositories.
In practice,
though,
it's easiest to use one copy as a central hub,
and to keep it on the web rather than on someone's laptop.
Most programmers use hosting services like
[GitHub](http://github.com),
[BitBucket](http://bitbucket.org) or
[GitLab](http://gitlab.com/)
to hold those master copies.

Let's start by sharing the changes we've made to our current project with the world.
Log in to GitHub,
then click on the `+` icon in the top right corner to create a new repository called `planets`:



Name your repository "planets" and then click "Create Repository":


GitHub displays a page with a URL and some information on how to configure your local repository:


This effectively does the following on GitHub's servers:

~~~ {.bash}
$ mkdir planets
$ cd planets
$ git init
~~~

But, you'll notice, when you look at the list of files in our github repository, that our `venus.txt` isn't listed. This is because we haven't connected to the two repositories yet.


The next step is to connect the two repositories.
We do this by making the GitHub repository a [remote](reference.html#remote)
for the local repository.
The home page of the repository on GitHub includes
the string we need to identify it:

![Where to Find Repository URL on GitHub](fig/github-find-repo-string.png)

Click on the 'HTTPS' link to change the [protocol](reference.html#protocol) from SSH to HTTPS.

Copy that URL from the browser,
go into the local `planets` repository,
and run this command, but make sure to substitute your username for mine:

~~~ {.bash}
$ git remote add origin https://github.com/realviacauchy/planets
~~~

Unfortunately, if you are working on a windows machine, the copy/paste/clipboard functions will not work, so you will have to type the repository URL in by hand. Take your time, and if you have any trouble, make sure to put up a sticky so that someone can come assist you.

Make sure to use the URL for your repository rather than mine:
the only difference should be your username instead of `realviacauchy`.

We can check that the command has worked by running `git remote -v`:

~~~ {.bash}
$ git remote -v
~~~
~~~ {.output}
origin   https://github.com/realviacauchy/planets.git (push)
origin   https://github.com/realviacauchy/planets.git (fetch)
~~~

The name `origin` is a local nickname for your remote repository:
we could use something else if we wanted to,
but `origin` is by far the most common choice.

Once the nickname `origin` is set up,
this command will push the changes from our local repository
to the repository on GitHub:

~~~ {.bash}
$ git push origin master
~~~
~~~ {.output}
Counting objects: 9, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (9/9), 821 bytes, done.
Total 9 (delta 2), reused 0 (delta 0)
To https://github.com/realviacauchy/planets
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
~~~


Our local and remote repositories are now in the same state. If you reload your github repository page, you will now see the `venus.txt` file in the remote repo.

##Moving On##

In a browser, navigate to this webpage:

https://try.github.io

There is an app at this link, that will walk you through all the material we just covered, along with a bit more that we didn't have time to touch on. Please take some time now to work through it, and let us know if you have any questions.

Additionally, there is a really helpful, more advanced Git app here:

http://bioconnector.org/learngit/

I recommend checking it out in the future. It will help you better visualize the workflow of using git as part of a collaboration.






#NOT PLANNING TO COVER THIS#
![GitHub Repository After First Push](fig/github-repo-after-first-push.svg)

> ## The '-u' Flag {.callout}
>
> You may see a `-u` option used with `git push` in some documentation.
> It is related to concepts we cover in our intermediate lesson,
> and can safely be ignored for now.

We can pull changes from the remote repository to the local one as well:

~~~ {.bash}
$ git pull origin master
~~~
~~~ {.output}
From https://github.com/vlad/planets
 * branch            master     -> FETCH_HEAD
Already up-to-date.
~~~

Pulling has no effect in this case
because the two repositories are already synchronized.
If someone else had pushed some changes to the repository on GitHub,
though,
this command would download them to our local repository.

> ## GitHub Timestamp {.challenge}
>
> Create a repository on GitHub,
> clone it,
> add a file,
> push those changes to GitHub,
> and then look at the [timestamp](reference.html#timestamp) of the change on GitHub.
> How does GitHub record times, and why?
