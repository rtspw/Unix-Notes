# 0 - Basic Unix Commands

## Format

A basic command comes in the following structure:

`Command` `Options` `Arguments`

<br>

## Option Styles

Most options take the form `-a` or any other letter.
However, recently, we have more verboose options that take two dashes.

This is more explicit, although it is longer to type.
Many times, the help screen will give options for both:
```
  -r, --reverse              reverse order while sorting
  -R, --recursive            list subdirectories recursively
  -s, --size                 print the allocated size of each file, in blocks
  -S                         sort by file size, largest first

```

<br>

## Man(ual) Pages

Sometimes, the help screen won't help with arcane letters and vague meanings. 
The **Man pages** are a tool to explain many of the important flags.
```bash
man ls
```

<br>

## Common Commands

### $ ls

The most basic command is `ls`, which is used to list directory contents of files and directories.

If you use `ls -l`, you will get the long format with permissions.

```bash
drwxr-xr-x 1 Super Panama World 197121   0 Feb 12 17:58  Notable/
drwxr-xr-x 1 Super Panama World 197121   0 Jan 15 15:33  Projects/
drwxr-xr-x 1 Super Panama World 197121   0 Jan  4 14:03  R/
drwxr-xr-x 1 Super Panama World 197121   0 Feb 19 18:47  Textbooks/
drwxr-xr-x 1 Super Panama World 197121   0 Dec 19 15:11  Textfiles/
-rw-r--r-- 1 Super Panama World 197121 402 Dec 18 23:49  desktop.ini
```
Permissions go by the form:
| Directory? | Owner | Group | Everyone |
|---|---|---|---|
|  d|rwx|rwx|rwx|

Letter meanings:
|r|w|x|
|---|---|---|
|Readable|Writable|Executable|

<br>

### $ ps 

Shows the running processes on the system for the current user.

```bash
    PID  TTY        STIME COMMAND
  24632 ?        18:47:43 /usr/bin/mintty
   8332 pty0     21:25:15 /usr/bin/ps
  16308 cons0    13:05:07 /c/Program Files/nodejs/node
  11960 cons0    13:05:06 /usr/bin/sh
  19152 pty0     18:47:44 /usr/bin/bash
  21636 cons1    13:54:30 /usr/bin/bash
  14332 cons0    13:00:18 /usr/bin/bash
```

Some meanings:
| Acronym | Meaning |
|---|---|
|PID|Unique Process ID|
|TTY|Terminal process is from|
|STIME|Time the process started|
|PRI|Priority|
|NI|Nice Value (Relative Priority)|
|ADDR|Memory address|
|VSZ|Size of process in memory (in kb)|

<br>

- You can use the flag `-a` to see all users.
- You can use `--format=colname1,colname2,...` to select columns
  For example: `--format=pid,pri`

<br>

### $ grep

Grep is a command which is used to find lines in a file that match a text pattern. 

A simple format would be:
```
$ grep [options] "string" [filename]
```

For example:
```bash
$ grep "can" ./Notable/Notes/Basic\ Unix\ Commands.md
Sometimes, the help screen won't help with arcane letters and vague meanings.
- You can use the flag `-a` to see all users.
- You can use `--format=colname1,colname2,...` to select columns
You can take the output of one command and feed it into the next command using **piping**.
```

<br>

### $ cat

Cat is another useful command to print the contents of a text file to the console window.
```bash
$ cat [options] [filename] [filename]
```

For example:
```bash
$ cat -n ./Notable/Notes/Basic\ Unix\ Commands.md
     1  ---
     2  title: Basic Unix Commands
     3  tags: [Notebooks/CS 14]
     4  created: '2019-02-20T04:06:53.933Z'
     5  modified: '2019-02-20T05:48:34.416Z'
     6  ---
     7
     8  # Basic Unix Commands
     9
    10  ## Commands
    11
    12  A basic command comes in the following structure:
    13
    14  `Command` `Options` `Arguments`
    15
    ...
```
where `-n` is the flag to show line numbers.

Cat stands for **concatenate**, and as such can also be used to join two text files.

```bash
$ cat ./textfile1.txt ./textfile2.txt
```

<br>

## Piping

You can take the output of one command and feed it into the next command using **piping**.

To pipe, we use the `|` operator.

For example, we can take the output of `ls -l` and search for the term "Notable":
```bash
$ ls -l | grep "Notable"
drwxr-xr-x 1 Super Panama World 197121   0 Feb 12 17:58 Notable/
```