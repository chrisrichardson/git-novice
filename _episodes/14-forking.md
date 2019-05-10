---
title: Forking
teaching: 25
exercises: 0
questions:
- "How can I make changes to a repo I don't have write access to?"
objectives:
- "Clone a remote repository read-only."
- "Add a remote to push to"
keypoints:
- "We can `git clone` any remote repository we have access to, and make our own online copy."
---

Previously when we looked at collaborating together, we cloned a repository and
the Owner gave access to the Collaborator. There are many projects we
might want to copy and work on, but don't have write access to the
repository.

## Cloning a public repository

First, let's choose a public repository to clone. There are lots of
public repositories on github and bitbucket, and this is quite likely
the first way you will really get to use revision control. For this
example, you can just clone the public version of my "picalc"
repository.

~~~
git clone https://github.com/chrisrichardson/picalc picalc_chris
~~~

Remember, this will clone into a folder called "picalc_chris" and will automatically set the "origin" to point to https://github.com/chrisrichardson/picalc

~~~
git remote -v
~~~

~~~
origin	https://github.com/chris_richardson/picalc.git (fetch)
origin	https://github.com/chris_richardson/picalc.git (push)
~~~

Once you have made a copy of the repository, you can edit the files as usual.

Unless we have contacted the author we can't push changes back to
their repository. We could continue editing, and making any changes we
want, doing `git add` and `git commit` as we go, but we can't push any
changes back to "origin".

Let's create another new private repo called "picalc_chris" on GitHub, and
push to that instead. We need to give it a local name for the
push/pull location, e.g. "myfork".

~~~
git remote add myfork https://your_name@github.com/your_name/picalc_chris
~~~

Replace "your_name" with your username on GitHub.

~~~
git remote -v
~~~

Now we will see two possible locations, one the "origin" (which you can
pull from but not push to), and the other is "myfork" which you have
full access to:

~~~
myfork	https://your_name@github.com/your_name/picalc_chris (fetch)
myfork	https://your_name@github.com/your_name/picalc_chris (push)
origin	https://github.com/chris_richardson/picalc.git (fetch)
origin	https://github.com/chris_richardson/picalc.git (push)
~~~

Let's push back to "myfork"

~~~
git push myfork master
~~~

You can continue changing the files, doing `git add`, `git commit` and
`git push myfork master` as much as you like. Try pushing to `origin
master` and see what happens. Take a look at the commits on the GitHub website.
