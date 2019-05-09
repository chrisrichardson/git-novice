---
title: Local Setup
teaching: 5
exercises: 0
questions:
- "How do I get started?"
objectives:
- "Access a Linux machine"
keypoints:
- "We are using Linux command line."
- "There are some Git tools for Windows/Mac too."
---

## [Welcome](../Welcome.pdf)

## Using the UIS MCS Linux machines

You should have a machine which is booted into Linux. In order to have a
uniform environment, we are all going to use the MCS Linux service.

It uses the same password as Raven. If you have been in the University
for a while and not used MCS, you may need to [reset your
password](https://password.csx.cam.ac.uk).
Once you've logged in, you can open a terminal (Activities/Terminal)
and start typing commands.

### Using your own laptop
You may also use your own laptop to log in remotely using an SSH client
(e.g. [MobaXterm for Windows](https://mobaxterm.mobatek.net/)).
MacOS has a native ssh client, so you can just open a terminal and type:
~~~
ssh crsid@linux.ds.cam.ac.uk
~~~
{: .bash}
You still need a valid password, of course.

> If you have a problem with accounts or password, please ask.
{:callout}

## Command Line

Everything today will be done from the command line. You don't really
need an in-depth knowledge of Unix to do this, but familiarity with
the basics (`cd`, `ls`, `mkdir` etc.) is important. Additionally you need to be
able to use an editor - I recommend using `gedit` on the MCS service
(you can also use `vi` or `emacs` if you are using a remote login).
There are some graphical tools for Git available for
Windows and Mac, but we won't cover those today. Once you understand
the principles of operation, you will find it easier to switch to a
graphical tool later.

## Source Material

As you can see, the material today has been adapted from a course
given by the "software carpentry" team. The general approach will be
to work along with the instructor, typing commands in as we go.

### Web browser

You can follow the source material with a web browser by going to:

* [http://chrisrichardson.github.io](http://chrisrichardson.github.io)

* (the notes are derived from the software carpentry site [http://swcarpentry.github.io/git-novice/](http://swcarpentry.github.io/git-novice/))