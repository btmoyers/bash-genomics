---
title: Introducing the Shell
teaching: 20
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Describe key reasons for learning shell.
- Navigate your file system using the command line.
- Access and read help files for `bash` programs and use help files to identify useful command options.
- Demonstrate the use of tab completion, and explain its advantages.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- What is a command shell and why would I use one?
- How can I move around on my computer?
- How can I see what files and directories I have?
- How can I specify the location of a file or directory on my computer?

::::::::::::::::::::::::::::::::::::::::::::::::::

## What is a shell and why should I care?

A *shell* is a computer program that presents a command line interface
which allows you to control your computer using commands entered
with a keyboard instead of controlling graphical user interfaces
(GUIs) with a mouse/keyboard/touchscreen combination.

There are many reasons to learn about the shell:

- Many bioinformatics tools can only be used through a command line interface. Many more
  have features and parameter options which are not available in the GUI.
  BLAST is an example. Many of the advanced functions are only accessible
  to users who know how to use a shell.
- The shell makes your work less boring. In bioinformatics you often need to repeat tasks with a large number of files. With the shell, you can automate those repetitive tasks and leave you free to do more exciting things.
- The shell makes your work less error-prone. When humans do the same thing a hundred different times
  (or even ten times), they're likely to make a mistake. Your computer can do the same thing a thousand times
  with no mistakes.
- The shell makes your work more reproducible. When you carry out your work in the command-line
  (rather than a GUI), your computer keeps a record of every step that you've carried out, which you can use
  to re-do your work when you need to. It also gives you a way to communicate unambiguously what you've done,
  so that others can inspect or apply your process to new data.
- Many bioinformatic tasks require large amounts of computing power and can't realistically be run on your
  own machine. These tasks are best performed using remote computers or cloud computing, which can only be accessed
  through a shell.

In this lesson you will learn how to use the command line interface to move around in your file system.

## How to access the shell

On a Mac or Linux machine, you can access a shell through a program called "Terminal", which is already available
on your computer. The Terminal is a window into which we will type commands. If you're using Windows,
you'll need to download a separate program to access the shell.

To save time, we are going to be working on a remote server where all the necessary data and software available.
When we say a 'remote server', we are talking about a computer that is not the one you are working on right now.
You will access the UMass Boston remote server named "chimera" where everything is prepared for the lesson.
We will learn the basics of the shell by manipulating some data files. Some of these files are very large
, and would take time to download to your computer.
We will also be using several bioinformatic packages in later lessons and installing all of the software
would take up time even more time. A 'ready-to-go' server lets us focus on learning.

## How to access the remote server

Because we have already created an account for you, you can log in to the remote server "chimera" with your UMass Boston email credentials (same username and password) by opening your terminal and typing: 

```bash
$ ssh your.umb.username@chimera.umb.edu
```

The press the `Enter` key. If it asks you to confirm the server identity or ssh key certificate (which should happen the first time you log in), type yes and press the `Enter` key. When prompted, type in your UMass Boston email password and the `Enter` key.

After logging in, you will see a screen showing something like this:

```output
Activate the web console with: systemctl enable --now cockpit.socket

Last login: Wed Aug  7 00:40:39 2024 from 10.23.0.78
```

This provides some information about the remote server that you're logging into. We're not going to use most of this information for
our workshop, so you can clear your screen using the `clear` command.

Type the word `clear` into the terminal and press the `Enter` key.

```bash
$ clear
```

This will scroll your screen down to give you a fresh screen and will make it easier to read.
You haven't lost any of the information on your screen. If you scroll up, you can see everything that has been output to your screen
up until this point.

:::::::::::::::::::::::::::::::::::::::::  callout

## Tip

Hot-key combinations are shortcuts for performing common commands.
The hot-key combination for clearing the console is `Ctrl+L`. Feel free to try it and see for yourself.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Navigating your file system

The part of the operating system that manages files and directories
is called the **file system**.
It organizes our data into files,
which hold information,
and directories (also called "folders"),
which hold files or other directories.

Several commands are frequently used to create, inspect, rename, and delete files and directories.

:::::::::::::::::::::::::::::::::::::::::  callout

## Preparation Magic

You may have a prompt (the characters to the left of the cursor) that looks different from the `$` sign character used here.
If you would like to change your prompt to match the example prompt, first type the command:
`echo $PS1`
into your shell, followed by pressing the <kbd>Enter</kbd> key.

This will print the bash special characters that are currently defining your prompt.
To change the prompt to a `$` (followed by a space), enter the command:
`PS1='$ '`
Your window should look like our example in this lesson.

To change back to your original prompt, type in the output of the previous command `echo $PS1` (this will be different depending on the
original configuration) between the quotes in the following command:
`PS1=""`

For example, if the output of `echo $PS1` was `\u@\h:\w $ `,
then type those characters between the quotes in the above command: `PS1="\u@\h:\w $ "`.
Alternatively, you can reset your original prompt by exiting the shell and opening a new session.

This isn't necessary to follow along (in fact, your prompt may have other helpful information you want to know about).  This is up to you!

::::::::::::::::::::::::::::::::::::::::::::::::::

```bash
$
```

The dollar sign is a **prompt**, which shows us that the shell is waiting for input;
your shell may use a different character as a prompt and may add information before
the prompt. When typing commands, either from these lessons or from other sources,
do not type the prompt, only the commands that follow it.

Let's find out where we are by running a command called `pwd`
(which stands for "print working directory").
At any moment, our **current working directory**
is our current default directory,
i.e.,
the directory that the computer assumes we want to run commands in,
unless we explicitly specify something else.
Here,
the computer's response is `/home/your.UMB.username`,
which is your personal home folder on the chimera server:

```bash
$ pwd
```

```output
/home/your.UMB.username
```

Let's look at how our file system is organized. We can see what files and subdirectories are in this directory by running `ls`,
which stands for "listing":

```bash
$ ls
```

```output
bin  itcga_workshop
```

`ls` prints the names of the files and directories in the current directory in
alphabetical order,
arranged neatly into columns.
We'll be working within the `itcga_workshop` subdirectory, and creating new subdirectories, throughout this workshop.

The command to change locations in our file system is `cd`, followed by a
directory name to change our working directory.
`cd` stands for "change directory".

Let's say we want to navigate to the `itcga_workshop` directory we saw above.  We can
use the following command to get there:

```bash
$ cd itcga_workshop
```

Let's look at what is in this directory:

```bash
$ ls
```

```output
metadata  untrimmed_fastq
```

We can make the `ls` output more comprehensible by using the **flag** `-F`,
which tells `ls` to add a trailing `/` to the names of directories:

```bash
$ ls -F
```

```output
metadata/  untrimmed_fastq/
```

Anything with a "/" after it is a directory. Things with a "\*" after them are programs. If
there are no decorations, it's a file.

`ls` has lots of other options. To find out what they are, we can type:

```bash
$ man ls
```

`man` (short for manual) displays detailed documentation (also referred as man page or man file)
for `bash` commands. It is a powerful resource to explore `bash` commands, understand
their usage and flags. Some manual files are very long. You can scroll through the
file using your keyboard's down arrow or use the <kbd>Space</kbd> key to go forward one page
and the <kbd>b</kbd> key to go backwards one page. When you are done reading, hit <kbd>q</kbd>
to quit.

:::::::::::::::::::::::::::::::::::::::  challenge

## Challenge

Use the `-l` option for the `ls` command to display more information for each item
in the directory. What is one piece of additional information this long format
gives you that you don't see with the bare `ls` command?

:::::::::::::::  solution

## Solution

```bash
$ ls -l
```

```output
total 1
drwxrwxr-x 2 brook.moyers brook.moyers 2 Aug  7 00:50 metadata
drwxrwxr-x 2 brook.moyers brook.moyers 2 Aug  7 00:50 untrimmed_fastq
```

The additional information given includes the name of the owner of the file,
when the file was last modified, and whether the current user has permission
to read and write to the file.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

No one can possibly learn all of these arguments, that's what the manual page
is for. You can (and should) refer to the manual page or other help files
as needed.

Let's go into the `untrimmed_fastq` directory and see what is in there.

```bash
$ cd untrimmed_fastq
$ ls -F
```

```output
C1_S4_L001_R1_001_downsampled.fastq  T1_S7_L001_R2_001_downsampled.fastq
C1_S4_L001_R2_001_downsampled.fastq  V1_S1_L001_R1_001_downsampled.fastq
T1_S7_L001_R1_001_downsampled.fastq  V1_S1_L001_R2_001_downsampled.fastq
```

This directory contains six files with `.fastq` extensions. FASTQ is a format
for storing information about sequencing reads and their quality.
We will be learning more about FASTQ files in a later lesson.

### Shortcut: Tab Completion

Typing out file or directory names can waste a
lot of time and it's easy to make typing mistakes. Instead we can use tab complete
as a shortcut. When you start typing out the name of a directory or file, then
hit the <kbd>Tab</kbd> key, the shell will try to fill in the rest of the
directory or file name.

Return to your home directory:

```bash
$ cd
```

then enter:

```bash
$ cd it<tab>
```

The shell will fill in the rest of the directory name for
`itcga_workshop`.

Now change directories to `untrimmed_fastq` in `itcga_workshop`

```bash
$ cd itcga_workshop
$ cd untrimmed_fastq
```

Using tab complete can be very helpful. However, it will only autocomplete
a file or directory name if you've typed enough characters to provide
a unique identifier for the file or directory you are trying to access.

For example, if we now try to list the files which names start with `C1`
by using tab complete:

```bash
$ ls C1<tab>
```

The shell auto-completes your command to `C1_S4_L001_R`, because all file names in
the directory begin with this prefix. When you hit
<kbd>Tab</kbd> again, the shell will list the possible choices.

```bash
$ ls C1_S4_L001_R<tab><tab>
```

```output
C1_S4_L001_R1_001_downsampled.fastq  C1_S4_L001_R2_001_downsampled.fastq
```

Tab completion can also fill in the names of programs, which can be useful if you
remember the beginning of a program name.

```bash
$ pw<tab><tab>
```

```output
pwck              pwd               pwhistory_helper  pwscore           
pwconv            pwdx              pwmake            pwunconv
```

Displays the name of every program that starts with `pw`.

## Summary

We now know how to move around our file system using the command line.
This gives us an advantage over interacting with the file system through
a GUI as it allows us to work on a remote server, carry out the same set of operations
on a large number of files quickly, and opens up many opportunities for using
bioinformatic software that is only available in command line versions.

In the next few episodes, we'll be expanding on these skills and seeing how
using the command line shell enables us to make our workflow more efficient and reproducible.

:::::::::::::::::::::::::::::::::::::::: keypoints

- The shell gives you the ability to work more efficiently by using keyboard commands rather than a GUI.
- Useful commands for navigating your file system include: `ls`, `pwd`, and `cd`.
- Most commands take options (flags) which begin with a `-`.
- Tab completion can reduce errors from mistyping and make work more efficient in the shell.

::::::::::::::::::::::::::::::::::::::::::::::::::


