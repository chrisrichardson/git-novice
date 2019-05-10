---
title: Creating a Repository
teaching: 10
exercises: 0
questions:
- "Where does Git store information?"
objectives:
- "Create a local Git repository."
keypoints:
- "`git init` initializes a repository."
---

Once Git is configured, we can start using it.
Let's create a directory for our work and then move into that directory.
For today, we'll be working on a simple Python program.
Let's call the project "myproject".

~~~
$ mkdir myproject
$ cd myproject
~~~
{: .bash}

Then we tell Git to make `myproject` a [repository]({{ page.root }}/reference/#repository)
— a place where Git can store versions of our files:

~~~
$ git init
~~~
{: .bash}

If we use `ls` to show the directory's contents,
it appears that nothing has changed:

~~~
$ ls
~~~
{: .bash}

But if we add the `-a` flag to show everything,
we can see that Git has created a hidden directory within `myproject` called `.git`:

~~~
$ ls -a
~~~
{: .bash}

~~~
.	..	.git
~~~
{: .output}

Git stores information about the project in this special sub-directory.
If we ever delete it, we will lose the project's history.

We can check that everything is set up correctly
by asking Git to tell us the status of our project:

~~~
$ git status
~~~
{: .bash}

~~~
# On branch master
#
# Initial commit
#
nothing to commit (create/copy files and use "git add" to track)
~~~
{: .output}

> ## Places to Create Git Repositories
>
> Dracula starts a new project, `sphere_calc`, related to his `myproject` project.
> Despite his colleague's concerns, he enters the following sequence of commands to
> create one Git repository inside another:
>
> ~~~
> $ cd               # return to home directory
> $ mkdir myproject  # make a new directory myproject
> $ cd myproject     # go into myproject
> $ git init         # make the myproject directory a Git repository
> $ mkdir sphere_calc    # make a sub-directory myproject/sphere_calc
> $ cd sphere_calc       # go into myproject/sphere_calc
> $ git init         # make the sphere_calc sub-directory a Git repository
> ~~~
> {: .bash}
>
> Why is it a bad idea to do this? (Notice here that the `myproject` project is now also tracking the entire `sphere_calc` repository.)
> How can Dracula undo his last `git init`?
>
> > ## Solution
> >
> > Git repositories can interfere with each other if they are "nested" in the
> > directory of another: the outer repository will try to version-control
> > the inner repository. Therefore, it's best to create each new Git
> > repository in a separate directory. To be sure that there is no conflicting
> > repository in the directory, check the output of `git status`. If it looks
> > like the following, you are good to go to create a new repository.
> >
> > repository as shown:
> >
> > ~~~
> > $ git status
> > ~~~
> > {: .bash}
> > ~~~
> > fatal: Not a git repository (or any of the parent directories): .git
> > ~~~
> > {: .output}
> >
> > Note that we can track files in directories within a Git:
> >
> > ~~~
> > $ touch ball.py ovoid.py       # create some sphere_calc files
> > $ cd ..                        # return to myproject directory
> > $ ls sphere_calc               # list contents of the sphere_calc directory
> > $ git add sphere_calc/*        # add all contents of myproject/sphere_calc
> > $ git status                   # show sphere_calc files in staging area
> > $ git commit -m "add sphere_calc files"    # commit myproject/sphere_calc to myproject Git repository
> > ~~~
> > {: .bash}
> >
> > Similarly, we can ignore (as discussed later) entire directories, such as the `sphere_calc` directory:
> >
> > ~~~
> > $ nano .gitignore # open the .gitignore file in the texteditor to add the sphere_calc directory
> > $ cat .gitignore # if you run cat afterwards, it should look like this:
> > ~~~
> > {: .bash}
> >
> > ~~~
> > sphere_calc
> > ~~~
> > {: .output}
> >
> > To recover from this little mistake, Dracula can just remove the `.git`
> > folder in the sphere_calc subdirectory. To do so he can run the following command from inside the 'sphere_calc' directory:
> >
> > ~~~
> > $ rm -rf .git
> > ~~~
> > {: .bash}
> >
> > But be careful! Running this command in the wrong directory, will remove
> > the entire git-history of a project you might wanted to keep. Therefore, always check your current directory using the
> > command `pwd`.
> {: .solution}
{: .challenge}
