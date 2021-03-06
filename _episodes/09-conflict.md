---
title: Conflicts
teaching: 15
exercises: 0
questions:
- "What do I do when my changes conflict with someone else's?"
objectives:
- "Explain what conflicts are and when they can occur."
- "Resolve conflicts resulting from a merge."
keypoints:
- "Conflicts occur when two or more people change the same file(s) at the same time."
- "The version control system does not allow people to overwrite each other's changes blindly, but highlights conflicts so that they can be resolved."
---

As soon as people can work in parallel, it's likely someone's going to
step on someone else's toes.  This will even happen with a single
person: if we are working on a piece of software on both our laptop
and a server in the lab, we could make different changes to each copy.
Version control helps us manage these
[conflicts]({{ page.root }}/reference/#conflicts)
by giving us tools to [resolve]({{ page.root }}/reference/#resolve)
overlapping changes.

To see how we can resolve conflicts, we must first create one.  The file
`pi.py` currently looks like this in both partners' copies of our `picalc`
repository:

~~~
$ cat pi.py
~~~
{: .bash}

~~~
# Add a comment line by collaborator
a = 2.0
nmax = 100000
for n in range(1, nmax):
    a = a * (n*n)/(n*n - 0.25)
print(a)
~~~
{: .output}

Let's add a line to one partner's copy only:

~~~
$ gedit pi.py
$ cat pi.py
~~~
{: .bash}

~~~
# Add a comment line by collaborator
a = 2.0
nmax = 100000
for n in range(1, nmax):
    a = a * (n*n)/(n*n - 0.25)
print(a)
print(" - which should be close to pi")
~~~
{: .output}

and then push the change to GitHub:

~~~
$ git add pi.py
$ git commit -m "Adding a line in our home copy"
~~~
{: .bash}

~~~
[master 5ae9631] Adding a line in our home copy
 1 file changed, 1 insertion(+)
~~~
{: .output}

~~~
$ git push
~~~
{: .bash}

~~~
Counting objects: 5, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 352 bytes, done.
Total 3 (delta 1), reused 0 (delta 0)
To https://github.com/vlad/picalc
   29aba7c..dabb4c8  master -> master
~~~
{: .output}

Now let's have the other partner
make a different change to their copy
*without* updating from GitHub:

~~~
$ gedit pi.py
$ cat pi.py
~~~
{: .bash}

~~~
# Add a comment line by collaborator
a = 2.0
nmax = 100000
for n in range(1, nmax):
    a = a * (n*n)/(n*n - 0.25)
print(a)
print("QED")
~~~
{: .output}

We can commit the change locally:

~~~
$ git add pi.py
$ git commit -m "Adding a line in my copy"
~~~
{: .bash}

~~~
[master 07ebc69] Adding a line in my copy
 1 file changed, 1 insertion(+)
~~~
{: .output}

but git won't let us push it to GitHub:

~~~
$ git push
~~~
{: .bash}

~~~
To https://github.com/vlad/picalc.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/vlad/picalc.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Merge the remote changes (e.g. 'git pull')
hint: before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
~~~
{: .output}

![The Conflicting Changes](../fig/conflict.svg)

Git detects that the changes made in one copy overlap with those made in the other
and stops us from trampling on our previous work.
What we have to do is pull the changes from GitHub,
[merge]({{ page.root }}/reference/#merge) them into the copy we're currently working in,
and then push that.
Let's start by pulling:

~~~
$ git pull
~~~
{: .bash}

~~~
remote: Counting objects: 5, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 3 (delta 1)
Unpacking objects: 100% (3/3), done.
From https://github.com/vlad/picalc
 * branch            master     -> FETCH_HEAD
Auto-merging pi.py
CONFLICT (content): Merge conflict in pi.py
Automatic merge failed; fix conflicts and then commit the result.
~~~
{: .output}

`git pull` tells us there's a conflict,
and marks that conflict in the affected file:

~~~
$ cat pi.py
~~~
{: .bash}

~~~
a = 2.0
nmax = 100000
for n in range(1, nmax):
    a = a * (n*n)/(n*n - 0.25)
    print(a)
<<<<<<< HEAD
print("QED")
=======
print(" - which should be close to pi")
>>>>>>> dabb4c8c450e8475aee9b14b4383acc99f42af1d
~~~
{: .output}

Our change—the one in `HEAD`—is preceded by `<<<<<<<`.
Git has then inserted `=======` as a separator between the conflicting changes
and marked the end of the content downloaded from GitHub with `>>>>>>>`.
(The string of letters and digits after that marker
identifies the commit we've just downloaded.)

It is now up to us to edit this file to remove these markers
and reconcile the changes.
We can do anything we want: keep the change made in the local repository, keep
the change made in the remote repository, write something new to replace both,
or get rid of the change entirely.
Let's replace both so that the file looks like this:

~~~
$ cat pi.py
~~~
{: .bash}

~~~
a = 2.0
nmax = 100000
for n in range(1, nmax):
    a = a * (n*n)/(n*n - 0.25)
print(a)
print("QED - which should be close to pi")
~~~
{: .output}

To finish merging,
we add `pi.py` to the changes being made by the merge
and then commit:

~~~
$ git add pi.py
$ git status
~~~
{: .bash}

~~~
On branch master
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:

	modified:   pi.py

~~~
{: .output}

~~~
$ git commit -m "Merging changes from GitHub"
~~~
{: .bash}

~~~
[master 2abf2b1] Merging changes from GitHub
~~~
{: .output}

Now we can push our changes to GitHub:

~~~
$ git push
~~~
{: .bash}

~~~
Counting objects: 10, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 697 bytes, done.
Total 6 (delta 2), reused 0 (delta 0)
To https://github.com/vlad/picalc.git
   dabb4c8..2abf2b1  master -> master
~~~
{: .output}

Git keeps track of what we've merged with what,
so we don't have to fix things by hand again
when the collaborator who made the first change pulls again:

~~~
$ git pull
~~~
{: .bash}

~~~
remote: Counting objects: 10, done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 6 (delta 2), reused 6 (delta 2)
Unpacking objects: 100% (6/6), done.
From https://github.com/vlad/picalc
 * branch            master     -> FETCH_HEAD
Updating dabb4c8..2abf2b1
Fast-forward
 pi.py | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
~~~
{: .output}

We get the merged file:

~~~
$ cat pi.py
~~~
{: .bash}

~~~
a = 2.0
nmax = 100000
for n in range(1, nmax):
    a = a * (n*n)/(n*n - 0.25)
print(a)
print("QED - which should be close to pi")
~~~
{: .output}

We don't need to merge again because Git knows someone has already done that.

Version control's ability to merge conflicting changes
is another reason users tend to divide their programs and papers into multiple files
instead of storing everything in one large file.
There's another benefit too:
whenever there are repeated conflicts in a particular file,
the version control system is essentially trying to tell its users
that they ought to clarify who's responsible for what,
or find a way to divide the work up differently.

> ## Solving Conflicts that You Create
>
> Clone the repository created by your instructor.
> Add a new file to it,
> and modify an existing file (your instructor will tell you which one).
> When asked by your instructor,
> pull the changes from the repository to create a conflict,
> then resolve it.
{: .challenge}

> ## Conflicts on Non-textual files
>
> What does Git do
> when there is a conflict in an image or some other non-textual file
> that is stored in version control?
{: .challenge}

> ## A Typical Work Session
>
> You sit down at your computer to work on a shared project that is tracked in a
> remote Git repository. During your work session, you take the following
> actions, but not in this order:
>
> - *Make changes* by appending the number `100` to a text file `numbers.txt`
> - *Update remote* repository to match the local repository
> - *Celebrate* your success with beer(s)
> - *Update local* repository to match the remote repository
> - *Stage changes* to be committed
> - *Commit changes* to the local repository
>
> In what order should you perform these actions to minimize the chances of
> conflicts? Put the commands above in order in the *action* column of the table
> below. When you have the order right, see if you can write the corresponding
> commands in the *command* column. A few steps are populated to get you
> started.
>
> |order|action . . . . . . . . . . |command . . . . . . . . . . |
> |-----|---------------------------|----------------------------|
> |1    |                           |                            |
> |2    |                           | `echo 100 >> numbers.txt`  |
> |3    |                           |                            |
> |4    |                           |                            |
> |5    |                           |                            |
> |6    | Celebrate!                | `AFK`                      |
{: .challenge}
