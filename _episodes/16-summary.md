---
title: Summary
teaching: 10
exercises: 0
questions:
- "How can I remember all this stuff?"
objectives:
- "Reiterate the key points and look at a typical workflow"
- "How can you fix things when they go wrong"
keypoints:
- "It is hard to remember. Practice makes perfect."
- "Fill out the [feedback form](http://feedback.training.cam.ac.uk/ucs/form.php)"
---

This page is really just a revision reminder and cheat-sheet. There is
already a really good [cheat-sheet](../reference) available in the
reference page.

## How to start things off

~~~
git init
git remote add origin https://git.repository.org/user/project
~~~
You don't have to use a "remote", but it makes your repository much
"safer" as you can `git push` it to the remote server. Even if you are
not collaborating with others, this is a useful backup. Remember to
create the empty repository on the server first!

or, if you want to copy an existing repository on a remote server:

~~~
git clone https://git.repository.org/user/project
~~~

## Adding and editing files

Now, you can add files, and do:
~~~
git add filename.txt
git commit -m "Added a file called filename.txt"
~~~

A common mistake is to create a new file, and forget to add it to the
repository. You can always check how things are going with:

~~~
git status
~~~

If you edit files, you can check the changes with
~~~
git diff
~~~

and then add and commit the changes too:
~~~
git add filename.txt
git commit -m "Edited a file called filename.txt"
~~~

## Checking what you have done

You might want to look at the history:
~~~
git log
~~~
Note that there are lots of useful options to git log which you can
explore.

## Working with a remote

Once up and running with a remote server, you might collaborate with
others. In which case, you should probably do this:

~~~
git pull origin master
~~~
before doing anything else
and
~~~
git push origin master
~~~
when you have finished. A typical session would look like this:
~~~
git pull origin master
# Edit files
git add filename.txt
git commit -m "Edited a file"
git push origin master
~~~

## Renaming, deleting, resetting

If you need to rename or delete files, try to use `git mv` and `git
rm` instead of `mv` and `rm`. It makes it easier for git to follow.

Sometimes, things do get messed up. One useful command is:
~~~
git clean -fdx
~~~

which essentially cleans out any untracked files in your repository,
and resets everything to the origin state. It is somewhat similar to:
~~~
rm -rf *
git clone https://git.repository.org/user/repo
~~~

i.e. delete everything locally, and copy again from the server
(assuming you are using one). With the web interface, it is always
possible to check the state of the server files before you do this.

Finally, use the `git help` command to get help, and you will also
find tons of advice on git online with google and stackexchange.

