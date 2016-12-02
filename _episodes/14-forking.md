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

First, let's choose a public repository to clone. We could use anything, but
for example, how about a [Javascript Fruit Machine](https://github.com/odhyan/slot).

~~~
git clone https://github.com/odhyan/slot
~~~

Remember, this will clone into a folder called "slot" and will automatically set the "origin" to point to https://github.com/odhyan/slot

~~~
git remote -v
~~~

~~~
origin	https://github.com/odhyan/slot.git (fetch)
origin	https://github.com/odhyan/slot.git (push)
~~~

You can try out the slot machine my navigating your browser to:
`file:///home/crsid/Desktop/slot/index.html`. Now let's edit the file
`slot.js` and make some trivial change.

~~~
git diff
~~~

~~~
diff --git a/slot.js b/slot.js
index b2234e7..fd1b07c 100644
--- a/slot.js
+++ b/slot.js
@@ -175,7 +175,7 @@ $(document).ready(function() {
         if(win[a.pos] === win[b.pos] && win[a.pos] === win[c.pos]) {
             res = "You Win!";
         } else {
-            res = "You Lose";
+            res = "Ha ha! You Lose";
         }
         $('#result').html(res);
     }
~~~

Unless we have contacted the author we can't push changes back to
their repository. Anyway, you probably don't even have a password for
github yet!

Let's add another repo on bitbucket, and push to that instead.
We need to give it a local name for the push/pull location, e.g. "myfork".

~~~
git remote add myfork https://vlad@bitbucket.org/vlad/slot
~~~

~~~
git remote -v
~~~

Now we will see two possible locations, one the "origin" (which we can
pull from but not push to), and the other is "myfork" which we have
full access to.