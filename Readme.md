# The Shell

**Material by Paul Wilson, Milad Fatenejad, Sasha Wood, and Radhika Khetani**
* Modified by Tracy Teal and Jory Schossau*

# What is the shell? How do I access the shell?

The *shell* is a program that presents a command line interface
which allows you to control your computer using commands entered
with a keyboard instead of controlling graphical user interfaces
(GUIs) with a mouse/keyboard combination.

Use a browser to open the tutorial on github, located at:

    https://https://github.com/JorySchossau/shell

A *terminal* is a program you run that gives you access to the
shell. There are many different terminal programs that vary across
operating systems.

There are many reasons to learn about the shell. In our opinion, the
most important reasons are that:

1.  It is very common to encounter the shell and
    command-line-interfaces in scientific computing, so you will
    probably have to learn it eventually

2.  The shell is a really powerful way of interacting with your
    computer. GUIs and the shell are complementary - by knowing both
    you will greatly expand the range of tasks you can accomplish with
    your computer. You will also be able to perform many tasks more
    efficiently.

The shell is just a program and there are many different shell
programs that have been developed. The most common shell (and the one
we will use) is called the Bourne-Again SHell (bash). Even if bash is
not the default shell, it is usually installed on most systems and can be
started by typing `bash` in the terminal. Many commands, especially a
lot of the basic ones, work across the various shells but many things
are different. We recommend sticking with bash and learning it well.
([Here is a link for more information](http://en.wikipedia.org/wiki/Bash_(Unix_shell))

# The Example: Manipulating Experimental Data Files

We will spend most of our time learning about the basics of the shell
by manipulating some known filfes. To get
the data for this part just enter the
command:

    git clone -b https://github.com/JorySchossau/shell.git

This command will grab all of the data needed for this workshop from
the internet.  (Titus can talk about the `git` command later.)

# Let's get started

One very basic command is `echo`. This command just prints text to
the terminal. Try the command:

    echo Hello, World

Then press enter. You should see the text "Hello, World" printed back
to you. The echo command is useful for printing from a shell script,
for displaying variables, and for generating known values to pass
to other programs.

## Moving around the file system

Let's learn how to move around the file system using command line
programs. This is really easy to do using a GUI (just click on
things). Once you learn the basic commands, you'll see that it is
really easy to do in the shell too.

First we have to know where we are. The program `pwd` (print working
directory) tells you where you are sitting in the directory tree. The
command `ls` will list the files in files in the current
directory. Directories are often called "folders" because of how they
are represented in GUIs. Directories are just listings of files. They
can contain other files or directories.

Whenever you start up a terminal, you will start in a special
directory called the *home* directory. Every user has their own home
directory where they have full access to do whatever they want. In
this case since we're all logged in as the same user we created directories to use as home. Whenever we talk about *home* during this workshop we mean **/mnt/<yourlogin>**. In this case, the `pwd` command tells us that we are in the `/mnt/<yourlogin`
directory.

## File Types

When you enter the `ls` command lists the contents of the current
directory. There are several items in the home directory, notice that
they are all colored blue. This tells us that all of these items are
directories as opposed to files.

Lets create an empty file using the `touch` command. Enter the
command:

    touch testfile

Then list the contents of the directory again. You should see that a
new entry, called `testfile`, exists. It is colored white meaning that
it is a file, as opposed to a directory. The `touch` command just
creates an empty file.

Some terminals will not color the directory entries in this very
convenient way. In those terminals, use `ls -F` instead of `ls`. The
`-F` argument modifies the results so that a slash is placed at the
end of directories. If the file is *executable* meaning that it can be
run like a program, then a star will be placed at the end of of the
file name.

You can also use the command `ls -l` to see whether items in a
directory are files or directories. `ls -l` gives a lot more
information too, such as the size of the file and information about
the owner. If the entry is a directory, then the first letter will be
a "d". The fifth column shows you the size of the entries in
bytes. Notice that `testfile` has a size of zero.

Now, let's get rid of `testfile`. To remove a file, just enter the
command:

    rm testfile

The `rm` command can be used to remove files. If you enter `ls` again,
you will see that `testfile` is gone.


## Changing Directories

Now, let's move to a different directory. The command `cd` (change
directory) is used to move around. Let's move into the `shell`
directory. Enter the following command:

    cd shell

Use the `ls` command to see what is inside this directory.  This
directory contains all of the material for this boot camp. Now move to
the directory containing some data:

    cd data

Now use the `ls` command to see what is inside this directory. You
will see that there is an entry which is green. This means that this
is an executable. If you use `ls -F` you will see that this file ends
with a star.

## Arguments

Most programs take additional arguments that control their exact
behavior. For example, `-F` and `-l` are arguments to `ls`.  The `ls`
program, like many programs, take a lot of arguments. But how do we
know what the options are to particular commands?

Most commonly used shell programs have a manual. You can access the
manual using the `man` program. Try entering:

    man ls

This will open the manual page for `ls`. Use the space key to go
forward and b to go backwards. When you are done reading, just hit `q`
to quit.

Programs that are run from the shell can get extremely complicated. To
see an example, open up the manual page for the `find` program. 
No one can possibly learn all of
these arguments, of course. So you will probably find yourself
referring back to the manual page frequently.

* * * *
**Short Exercise**

1. Use the manual page for `ls` to guess what you would expect from
using the arguments `-l`, '-t', '-r' at the same time.
2. Try the following and see if you can figure out what they do, either by examining the results or consulting the manual page.
   * `ls -lS` (equivalent to `ls -l -S`)
   * `ls -lt` (equivalent to `ls -l -t`)
   * `ls -1`  (that's the number one, not a letter 'ell')

* * * *


## Examining the contents of other directories

By default, the `ls` commands lists the contents of the working
directory (i.e. the directory you are in). You can always find the
directory you are in using the `pwd` command. However, you can also
give `ls` the names of other directories to view. Navigate to the
home directory if you are not already there. 

Type:

    cd

Then enter the command:

    ls shell

This will list the contents of the `shell` directory without
you having to navigate there. Now enter:

    ls shell/data

This prints the contents of `data`. The `cd` command works in a
similar way. Try entering:

    cd shell/data

and you will jump directly to `data` without having to go through
the intermediate directory.

## Full vs. Relative Paths

The `cd` command takes an argument which is the directory
name. Directories can be specified using either a *relative* path a
full *path*. The directories on the computer are arranged into a
hierarchy. The full path tells you where a directory is in that
hierarchy. Navigate to your home directory. Now, enter the `pwd`
command and you should see:

    /mnt/<yourlogin>

This tells you that you
are in a directory with the same name as your loginid, 
which sits inside a directory called
`mnt` which sits inside the very top directory in the hierarchy. The
very top of the hierarchy is a directory called `/` which is usually
referred to as the *root directory*. So, to summarize: `<yourlogin>` is a
directory in `mnt` which is a directory in `/`.

Now enter the following command:

    cd /mnt/<yourlogin>/shell/data

This jumps to `shell`. Now go back to the home directory (cd). We saw
earlier that the command:

    cd shell/data

had the same effect - it took us to the `shell` directory. But,
instead of specifying the full path
(`/mnt/<yourlogin>/shell/data`), we specified a *relative path*. In
other words, we specified the path relative to our current
directory. A full path always starts with a `/`. A relative path does
not. You can usually use either a full path or a relative path
depending on what is most convenient. If we are in the home directory,
it is more convenient to just enter the relative path since it
involves less typing.

Over time, it will become easier for you to keep a mental note of the
structure of the directories that you are using and how to quickly
navigate amongst them.

* * * *
**Short Exercise**

Now, list the contents of the /bin directory. Do you see anything
familiar in there?

* * * *

## Saving time with shortcuts, wild cards, and tab completion

### Shortcuts

There are some shortcuts which you should know about. The shortcut `..` always refers to the directory
above your current directory. Thus:

    ls ..

prints the contents of the `/mnt/<yourlogin>/shell`. You can chain
these together, so:

    ls ../../

prints the contents of `/mnt/<yourlogin>` which is your home
directory. Finally, the special directory `.` always refers to your
current directory. So, `ls`, `ls .`, and `ls ././././.` all do the
same thing, they print the contents of the current directory. This may
seem like a useless shortcut right now, but we'll see when it is
needed in a little while.

To summarize, while you are in the `data` directory, the commands
`ls ../../`, and `ls /mnt/<yourlogin>` all do exactly the
same thing. These shortcuts are not necessary, they are provided for
your convenience.

## Scripting: Where the #! hits the bash

Scripting allows us to automate command-line commands.
Lets make a script using some of the commands we've already covered.

To open files and edit them we can use a text editor. There are many available for the command-line but let's just use a basic one called `nano`. Type `nano` to open the editor.

    nano

Nano is a very basic text editor, but allows you to move around using the arrow keys, home, end, use delete and backspace just like any other basic editor.

Let's have our script greet us with a `Good afternoon` greeting. We've already learned how to make text appear on the screen using `echo` so let's use that now to show our message. Keep in mind we're simply editing a text file, so these commands don't do anything at the moment.

    echo Good afternoon.

Now, to save the file and exit we can just press `Control-x` (That's holdingdown the control key near the spacebar, and tapping x). Nano asks if we want to save (answer `y`). Nano then asks us for a filename, so let's type in `greeting.sh`. The `.sh` on the end is just for our benefit, so we know we should run this file as a shell script, and not some other kind of script.

Let's make sure the file is there by using the `ls` command to list the contents.

    ls

Let's make sure the bash command to generate the greeting is indeed saved in the file, using either the `cat` or `less` command and typing our filename as the first argument to the command.

    cat greeting.sh

To run the script we just wrote, we pass it as an argument to the shell. Type `bash greeting.sh`

    bash greeting.sh

That made bash run the echo command saved in the file named `greeting.sh`. Let's add another command to the file. So open up the `greeting.sh` file in nano again. This time we can tell nano which file we want to edit when we run the editor.

    nano greeting.sh

Now we have our file open again and let's add a second command that prints the current working directory. Remember that command? After adding that line, close with saving again. Now run the script again.

    bash greeting.sh

We can include any of the command-line commands in script files, and run them any time we like. What we had bash do was interpret the commands saved in `greeting.sh`. In fact, any simple text file like this can contain commands for any interpreter. Like earlier, we had python interpret a file with python commands, and that script converted data to a .csv file.

### Exercise: DIY

Here's a [bash commands cheatsheet](https://github.com/JorySchossau/shell/blob/master/shell_cheatsheet.md) which shows you the commands we've covered, as well as some other common ones. Use this list to help you write a new script which creates what you think is an appropriately named backup of one of the data files we used during Titus' earlier lessons. The script should also print out the full path of the new backup file.

### Executable scripts

Add the line `#!/bin/bash` at the top of your script. This is a special command that tells the shell which program should interpret the commands in this script file. In this case we tell the shell that bash itself should interpret the following commands. A python script might look like `#!/bin/python`. 

Now flag the file as an executable file using a command you've used earlier today.

    chmod +x myscript.sh

If you use the `ls` command, it should now highlight the script differently, indicating it's an executable. Now we can run the script by typing one of two invocations.

If you're in the directory of the script itself

    ./myscript.sh

If you are in any other directory

    /full/path/to/myscript.sh

Notice there's no leading period on the second form.
