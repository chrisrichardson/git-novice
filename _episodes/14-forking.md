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
the first way you will really get to use revision control.

~~~
git clone https://bitbucket.org/chris_richardson/wallis_pi
~~~

Remember, this will clone into a folder called "wallis_pi" and will automatically set the "origin" to point to https://bitbucket.org/chris_richardson/wallis_pi

~~~
git remote -v
~~~

~~~
origin	https://github.com/chris_richardson/wallis_pi.git (fetch)
origin	https://github.com/chris_richardson/wallis_pi.git (push)
~~~

Once you have made a copy of the repository, you can edit the files as usual.

This is a Python project, which calculates the value of pi, using a
rather inefficient formula. You can test out the project on
`linux.ds.cam.ac.uk` by running `python3 pi.py`. The other file is
`bitbucket-pipelines.yml` which runs a test every time a change is
made to the repository. Try changing the code, and see what effect
it has on the test.

Unless we have contacted the author we can't push changes back to
their repository. We could continue editing, and making any changes we
want, doing `git add` and `git commit` as we go, but we can't push any
changes back to "origin".

Let's create another new private repo called "wallis_pi" on bitbucket, and
push to that instead. We need to give it a local name for the
push/pull location, e.g. "myfork".

~~~
git remote add myfork https://your_name@bitbucket.org/your_name/wallis_pi
~~~

Replace "your_name" with your username.

~~~
git remote -v
~~~

Now we will see two possible locations, one the "origin" (which we can
pull from but not push to), and the other is "myfork" which we have
full access to:

~~~
myfork	https://your_name@bitbucket.org/your_name/wallis_pi (fetch)
myfork	https://your_name@bitbucket.org/your_name/wallis_pi (push)
origin	https://bitbucket.org/chris_richardson/wallis_pi.git (fetch)
origin	https://bitbucket.org/chris_richardson/wallis_pi.git (push)
~~~

Let's push back to "myfork"

~~~
git push myfork master
~~~

You can continue changing the files, doing `git add`, `git commit` and
`git push myfork master` as much as you like. Try pushing to `origin
master` and see what happens. Take a look at the commits on the
bitbucket website.
