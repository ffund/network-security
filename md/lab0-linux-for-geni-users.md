

## Note: pay attention to _where_ you are

When using remote systems (such as GENI VMs), a common
point of confusion is misunderstanding _where_ things are or happen.
For example: where a particular file is, what system a command
is run on, and what network link a packet will travel over.


Throughout this tutorial, try and pay attention to _where_ "things" are.

* What host (computer) am I on (your laptop? or a VM on GENI?)?
* What filesystem and directory am I in?
* What network am I on (the public Internet? or a private link on GENI?)?


# "Hello World" of the Bash shell


## Accessing a remote shell

Reserve a single VM using the GENI Portal.
Then, gain access to this VM by
opening a terminal on your laptop and using SSH to log in to it.

First, open a terminal:

* On OS X, open Applications > Utilities > Terminal.
* If you are using Windows, you should have previously installed Git Bash. To
open it, click the Windows or Start icon. In the Programs list, click on
Git > Git Bash.
* If you are running Ubuntu Linux, you can open the Dash (Super Key) or
Applications and type terminal. For other Linux flavors, you may have to modify these instructions
slightly.

This is your local shell. Make a note of what the prompt looks like.
For example, mine looks like this:

```
ffund@ffund-laptop:~$
```

It shows my username (`ffund`), hostname (`ffund-laptop`), my current
working directory (`~`), and then a `$` to signify that I'm working as a
normal (unprivileged) user. (If I was working as the privileged "root" user,
the prompt would end with a `#` instead.)

## Log in to your remote VM

Next get your login information for your newly reserved VM from the GENI Portal, and use SSH to log in to the remote shell.
You should run the rest of this tutorial **on the remote VM**, not on your local shell.


Now, if you look at your prompt, you should notice that the username and
hostname are different from your local shell. When working on remote servers,
the prompt is useful for determining *where* you are running a command -
on what host, and from what directory or filesystem. Unless otherwise specified, the commands in the rest of this tutorial should be run on the _remote_ shell.

## "Hello world"

For the standard "hello world" exercise, we use the `echo` command to
print a quoted string to the terminal output. At the terminal prompt, type:

```
echo "Hello world"
```

and then hit Enter to run the command you've just entered.


## Shell tricks

### Tab autocompletion

Many terminals have a feature called "tab autocompletion" where, when
you type a partial command and then press the Tab key, it will
finish the command for you.
Let's try this with the `whoami` command. First write out the entire command:

```
whoami
```

When you hit Enter, you should see that this command returns your
username. Now try typing just

```
whoa
```

and then hit Tab. At the prompt, the rest of the command `whoami` should
be filled out, and you can then hit Enter to run it.

Tab will only fill out the entire command if only one command on the
system matches what you've entered so far. If there are multiple matching
commands, Tab will show you all of them. You'll have to continue
typing in the one you want until there is only one match, and then Tab
will autocomplete it for you. Try typing

```
who
```

and then hit Tab to see how this works.

Tab autocompletion also works for file and directory names, for arguments to
many commands, and for variables.
For example, suppose you save the string "hello world" in a new variable called
"mymessage" like this:

```
mymessage="hello world"
```
(note that there is no space on either side of the `=`).
You can then run

```
echo $mym
```

and hit Tab, and it will be autocompleted to `echo $mymessage` (which
will print "hello world" to the terminal output).

### History

It's often useful to be able to see and re-run commands you've previously run.

You can use the up and down arrow keys to scroll
through your previous commands. Or, to see your command history all at once, run

```
history
```

You'll note that each line in the output of the `history` command has a number
next to it, with which you can re-run that command. To run a command that
appears as number `1` in your history, run

```
!1
```

or, to quickly run your last command again (without having to specify the
number), you can run

```
!!
```


# Navigating the filesystem

## Basics

First, check where you are currently located in the filesystem with the `pwd`
("**p**rint **w**orking **d**irectory") command:

```
pwd
```
Next, **l**i**s**t the contents of the directory you are in:

```
ls
```

To create a new directory inside our current directory, run `mkdir` and
specify a name for the new directory, like

```
mkdir new
```

You can **c**hange **d**irectory by running `cd` and specifying the directory
you want to change to. For example, to change to the directory you've just
created, run

```
cd new
```

and then use

```
pwd
```

again to verify your current working directory.

## Relative and absolute paths

You may have noticed that when you run the `pwd` command, it gives you
a full path with several directory names separated by a `/` character.
This is a _full path_. For example, after running the commands above, I would see
the following output for `pwd`:

```
/users/ff524/new
```

When you run commands that involve a file or directory, you can always
give a full path, which starts with a `/` and contains the entire directory
tree up until the file or directory you are interested in. For example, I
can run

```
cd /users/ff524
```

to return to my home directory. Alternatively, you can give a path that is
_relative_ to the directory you are in. For example, when I am inside my home
directory (`/users/ff524` - yours will be different), which has a directory
called `new` inside it, I can navigate into the `new` directory with
a relative path:

```
cd new
```

or the absolute path:


```
cd /users/ff524/new
```


## Shortcuts

* Running `cd` with no argument takes you to your home directory.
* The shorthand `..` refers to "the directory that is one level higher" (can be
used with `cd` and with other commands).
* The shorthand `~` refers to the current user's home directory (can be used
with `cd` and with other commands).
* After navigating to a new directory with `cd`, you can then use `cd -` to
return to the directory you were in previously.

Try these commands. Before and after each `cd` command, run `pwd` to see
where you have started and where you ended up after running the command.

```bash
cd       # takes you to your home directory
cd ..    # takes you one directory "higher" from where you were before
cd ~     # takes you to your home directory
cd ../.. # takes you two directories "higher" from where you were before
cd -     # takes you to the directory you were in before the last time you ran "cd"
```



# Working with files and directories

## Moving files around the local filesystem

The easiest way to create a file is to just open it for editing. We will
use the `nano` text editor to open file called `newfile.txt`:

```
nano newfile.txt
```

You can type some text into this file, then use Ctrl + O to write it
**o**ut to file, and hit Enter to confirm the file name to which to save.
Near the bottom of the screen, it should say e.g. "[ Wrote 1 line ]".
Then use Ctrl + X to exit.

To see the contents of a file, we can print the contents of the file
to the terminal output with `cat`:

```
cat newfile.txt
```

To copy a file, we use `cp`, and give the source and destination file names
as arguments:

```
cp newfile.txt copy.txt
```

To move (or rename) a file, we use the `mv` command:

```
mv copy.txt mycopy.txt
```

and we use `rm` to delete a file:

```
rm mycopy.txt
```

With `rm`, there is no "Recycle Bin" and no getting back files you've
deleted accidentally - so be very, very careful.

## Moving files over the Internet

We will often have to move files over the Internet - for example, get a file
from the Internet onto our local filesystem, or copy a file from a remote
system that we access with SSH to our local filesystem.

Use `wget` to download from the Internet.
For example, to download a file I've put at
https://witestlab.poly.edu/bikes/README.txt
we can run

```
wget https://witestlab.poly.edu/bikes/README.txt
```

Use

```
cat README.txt
```

to verify that you've retrieved the file and see its contents.
Similarly, you can download _anything_ from the web by URL.


## Useful flags

Bash utilities typically have some flags you can use to modify the way
they behave, or what their output looks like.

For example, take the `ls` command. We can:

* See one file per output line: `ls -1`
* See "long" output that includes file permissions, ownership, modification dates: `ls -l`
* See "long" output and also sort files in order of time of last modification: `ls -lt`
* See "long" output and sort files so that the most recently modified file is last: `ls -ltr`

With most utilities, you can use the `--help` flag to find out how to use
the utility and what flags are available for it:

```
ls --help
```

## Using `scp`

To move files back and forth between your laptop and a remote system that
you access with `ssh`, we can use `scp`. The syntax is:

```
scp source destination
```

When using `scp`, you have to pay attention to _where_ you are running a
command. Assuming you have a file `README.txt` located in your home directory
on your VM, you can run

```
scp -P PORT USERNAME@HOSTNAME:~/README.txt .
```

(substituting your own PORT, USERNAME, and HOSTNAME using the details provided by the GENI Portal.)

from a shell on your _laptop_ (in the _local_ shell) to retrieve that file from the server and copy it to whatever
directory you are working in on your laptop. (The `.` shortcut indicates
"put the file _here_".) Note that the
part immediately following the `:` is the _full path_ to the file you
want to transfer.

You'll have to make sure you have the
necessary file permissions to write files to the directory you are working in!
If you get a message indicating a file permission error, you may have to specify a path to a directory in which you have write permission, instead
of the `.` argument.

Once you have transferred the file, you can make changes to the file
locally and copy it back to your home directory on the server, with


```
scp -P PORT README.txt USERNAME@HOSTNAME:~/README2.txt
```



## Online sharing from the command line

Sometimes we'll want to do the "reverse" of `wget` - upload a file to the Internet,
using the Linux shell. There are several online services that provide an
API for this.  To use them, you'll need to first install `curl`:

```
sudo apt-get update
sudo apt-get -y install curl
```

For example, to upload the "bikes" `README.txt` you
downloaded earlier, you can run

```
curl --upload-file ./README.txt https://transfer.sh/README.txt
```

This will return a URL, which you can open in a browser to
see and download the file you've just uploaded.

# Manipulating output of a command

## See more or less

We'll often want to see more or less of a command that has a lot of output.

To see how this works, let's download a large text file - a book from
Project Gutenberg. Download it with

```
wget http://witestlab.poly.edu/files/book.txt
```

If you run

```
cat book.txt
```

to see the contents of the file, you won't see much - there's just too much
output, and it goes by too quickly.

To see the beginning of the book, use

```
head book.txt
```

To see just the end, use

```
tail book.txt
```

You can also specify the number of lines to see with either command, with e.g.

```
head --lines=5 book.txt
tail --lines=10 book.txt
```

To page through one line of output at a time, use

```
less book.txt
```

You can use Enter to continue scrolling through the file, or q
to quit at any time.

It's often useful to count the number of lines of output in a file.
We can use `wc`:

```
wc -l book.txt
```

Finally, it's nice to be able to see only lines matching a particular pattern.
There's a very powerful utility called "grep" that allows us to filter
the output to see only those lines that contain a particular word.
For example, to see lines containing the word "information", you can run

```
grep "information" book.txt
```

## I/O redirection and pipes

The real value of the shell comes in our ability to "chain" together multiple
utilities.

For example, suppose we want to count the number of lines in our book
that contain the work "information". We can save those lines to a file using
the `>` operator to redirect the output of the `grep` command:

```
grep "information" book.txt > infolines.txt
```

Use `cat infolines.txt` to verify the contents of the new file we've just created.
Now, we can run

```
wc -l infolines.txt
```

to see the number of lines.

Alternatively, we can skip writing to a file and just send the output of the
`grep` command directly to the `wc` command that follows it with the _pipe_
operator, `|`:

```
grep "information" book.txt | wc -l
```

We may occasionally want to send the output of a command to a file,
but append to an existing file rather than create a new one (as `>` does). To
append to an existing file we will use `>>`.

For example, to create a file that contains all lines with the word "when",
followed by all lines with the word "where", you can run

```
grep "when" book.txt" > morelines.txt
grep "where" book.txt >> morelines.txt
```

The second line won't overwrite the text that is written to `morelines.txt`
in the first line; it will append to the file instead.

Finally, another useful tool is `tee`, which we can use to send output to both the terminal and to a file.  For example, try

```
grep "when" book.txt | tee morelines.txt
```

# Writing shell scripts


## Creating a shell script

What makes the shell really powerful is your ability to take a complicated
workflow, save it in a file, and then re-run those operations later just
by running one command.

A shell script is just a file that contains commands, just as we would run 
them at the terminal. For example, to run the "Hello world" of shell scripts,
create a new file called `hello.sh` that contains the following:
                                                                               
```
echo "Hello world"
```

## Running a shell script

To run the shell script `hello.sh` that we have just created, we would run

```
bash hello.sh
```

We may prefer to run our scripts as `hello.sh` directly, 
without having to specify each time that they should be run using the Bash terminal. To do this, we'll add a line called a "shebang" at the top of our script that tells the operating system what program to use to run the script. To write a "shebang", we put the character sequence `#!` followed by the path to the interpreter at the top of our script. 

Modify your `hello.sh` script to look like this:

```
#!/bin/bash

echo "Hello world"
```

There's one more step we need to take: we need to mark the script as an 
executable file with `chmod`. First, verify that the script is _not_ marked
as executable:

```
ls -l
```

Note the `-rw-r--r--` next to `hello.sh`: this indicates that the file may be **r**ead and
**w**ritten by the user that owns it, **r**ead by members of the group that owns it, 
and **r**ead by all users of the system. (The user and group that own the file
are also listed in the `ls -l` output.)

To make it executable, we will run

```
chmod a+x hello.sh
```

to give the e**x**excutable permission to **a**ll users of the system.
Now, the `ls -l` output should show `-rwxr-xr-x`.
At this point we can run the script by either running

```
./hello.sh
```

while in the same directory, or by supplying the full path to `hello.sh`
from anywhere else in the system.



## Leave a script running for later

When working on a remote system, it's useful to be able to run a script and 
come back to it later.

Try saving the following script:

```
#!/bin/bash

for i in $(seq 100); do
  echo "On iteration $i"
  sleep 30
done
```

This script will run for a long time. Suppose you want to start it and come 
back to it later?

`screen` is a useful tool for this. Install `screen` with

```
sudo apt-get update
sudo apt-get -y install screen
```

Then, start a new screen session with 

```
screen -S "mysession"
```

(passing any name you like to the session). Start your very long script
running.

Then, _detach_ from your current `screen` session with
Ctrl + A + D.

Your script is still running; but you can go on and do other things, or log 
off and log back on. To resume your session, run 

```
screen -ls
```

to list all your sessions. Then run 

```
screen -R mysession
```

to re-attach to your running session, by name.

# More resources

If you are interested in more exercises related to using the Unix shell, see Software Carpentry: 

[http://swcarpentry.github.io/shell-novice/](http://swcarpentry.github.io/shell-novice/)
