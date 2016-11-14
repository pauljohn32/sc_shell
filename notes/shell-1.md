# Command Line, Shell
`r format(Sys.time(), '%Y %B %d')`  







## Getting Started in the Shell

### Start a Terminal Emulator
   * Mac (Utilities/Terminal, iTerm, many others)
   * Windows (Git for Windows provides a BASH shell). Others available (Cygwin, Ubuntu BASH for Windows)
   * Linux (many terminal programs, some more exciting than others)

### High points
   * Type commands, see textual output
   * Not much pointing and clicking (copy/paste possible on some)
   
### What is a Shell?
   * Computer has many settings that programs can access. A "shell" is a "behind the scenes" program that keeps those settings and passes them out to programs when needed
   * BASH: Bourne Again Shell, a widely-used shell
   * Almost all Unix/Mac systems will have many shell programs available, such as "sh", "bash", "dash", and so forth. We are mostly interested in BASH because it has the most user comfort
   * A terminal program relies on the shell to translate between user and operating system
   
#### **Prompt**. Where you type {.bs-callout .bs-callout-info}
   * Prompt might be verbose 
```
pauljohn:Documents/Projects $
```
   * On some it is very lean, just the dollar sign
```
$
```
   * Dollar sign is customary prompt for non-root user (non-administrators)
   * Prompt is configurable, it is a good exercise for somebody who has used the Terminal for a week or two on a daily basis.
   
## Basic things to type

#### What is my user name? Run "whoami" {.bs-callout .bs-callout-warning}

```bash
$ whoami
```

```
output: pauljohn
```
   * What's that doing? *It asks **the environment** for the value of* "$USER". 
   * We should get the same if we run

```bash
$ echo $USER
```

```
output: pauljohn
```
**echo**: prints out a value to the screen
   
   * I have usually done that, rather than `whoami`.
   * To be perfectly honest, I did not know `whoami` existed until I watched an SC video. 


#### Why did USER have a dollar sign on it?

    * In the standard shell, variables in *the environment* are named with capitals, like "USER"
    * but to access (retrieve) we need to add dollar sign

#### Where Am I? Run "pwd"


```bash
$ pwd
```
**pwd**: print working directory

   * Start a "fresh" terminal, the output for the working directory is *almost always* the user HOME folder.

#### Fastest way to HOME folder

   * If you find your working directory is not the HOME folder, the fastest way home is

```bash
$ cd
```
    * Will see later that cd is a multipurpose command.

#### Where is pauljohn as he works on this document? 

```bash
$ pwd
```

```
output: /home/pauljohn/GIT/github/sc_shell/notes
```

#### Where's HOME? Operating Systems Differ {.bs-callout .bs-callout-warning}

```bash
$ echo $HOME
```

```
output: /home/pauljohn
```

   * Linux  "/home/pauljohn"
   * Macintosh  "/Users/pauljohn"
   * Windoze  "/c/Users/pauljohn"
       * Even though Windows refers to its directory as "C:\\Users\\pauljohn", BASH won't!
   * FORWARD SLASHES separate directory and file names
   * Shell "homogenizes" appearance of directories and files across operating systems, making them look Unix-like.

#### What is especially important about HOME? {.bs-callout .bs-callout-danger}
   * HOME is the only folder where a user is sure to be able to read and write
   * HOME is where the configuration files are stored. 
   * Customary: config files and directories begin with the letter "."
   * Many file-listing programs will NOT print the items that begin with "."
   * In my HOME, I have folders like ".mozilla", ".thunderbird", ".config", etc
   * $HOME is often referred to by a shortcut symbol, "~" (tilde)
   
#### Setting HOME {.bs-callout .bs-callout-info} 
   * Usually, when you start a terminal program, the working directory will be HOME.
   * Unix, Linux, Mac systems all use environment variable HOME as a key organizing concept.
   * Windows does not, by default, have an environment variable named HOME!
       * Some Terminals or Shells will try to guess what HOME ought to be
   * If the Terminal program guesses incorrectly, we should fix ASAP
      * Must fix ASAP, or else nothing we do in the shell will make sense!
   * Know what HOME ought to be? Can set manually within the current shell's session. 
```
export HOME="/c/Users/pauljohn"
```
    * But there should be some better, less error-prone way. This is slightly better:

```
export HOME="/c/Users/$USER"
```
	
**export**: A BASH shell command that takes the following value and places it into the environment for the duration of the session.

    * A more permanent and direct approach is to create an environment variable within the Windows system, which Git BASH can then inherit.  This can be done in Control Panel -> System menu, but it can also be done in a DOS Command box:


```bash
$ setx HOME "%USERPROFILE%" 
```
			
### Portable concepts: All Terminals Today will have

   * History. 
      * Usually accessed by up arrow key
	     * up arrow restores previous command, can edit and re-run
      * or the command `history`
   * **Tab completion**: start typing a command or directory or file name and hit the TAB key
   * Optional color coded output of file and directory listings
   * Many Terminals have magic short-cut keys (that I did not know about until recently)
      * Ctl-R reverse search in history
	  * Ctl-k erase command line from cursor to the end

### Better check what shell I'm running

```bash
$ echo $SHELL
```

```
output: /bin/bash
```
	  
### Quick Summary:
   * Terminals have command lines
   * Shells watch what you type and try to gather information and put it to use
   * HOME: a special user-controlled file folder where user documents and configurations are stored
   * Environment: a place where the Shell stores its information
   * pwd: displays the working directory name. Important because programs often assume the WD is the place where files are found or to be created.
   * cd: takes user to the HOME folder, from any WD
   * echo: prints out information to the terminal

#### In case you are **curious for adventure**?  {.bs-callout .bs-callout-danger}
   * Run this to see all of the variables in your shell's environment. But be ready for a *big, unintelligible splat*.

```bash
$ env
```
   * Now you should see why we checked individual itty-bitty-pieces from the environment with `whoami` or `echo $USER` or `echo $HOME`.


   
# Listings

#### The "ls" function is a workhorse {.bs-callout .bs-callout-warning} 

   * ls is a short name because it is used very often

```bash
$ ls
```
   * I'm unable to show you my color-coded command line in this document because the colors are lost in the document compilation process. But can show you in person :)
	
   * Make sure your terminal has color-coded output
      * files should be visibly different from directories or other items

```bash
$ ls --color=always
```

   * "--color=always" is a *long form* command line **argument**. 
   * Short form arguments with `ls` are `-l`, `-a`, `-S`, `-1`, `-F`
   
   * See why color-coded output in the Terminal was a major breakthrough?

```bash
$ ls --color=never
```

```
output: kutils.css
output: ou_swc_files
output: rmd2html.sh
output: shell-1.html
output: shell-1.Rmd
output: shell-2.aux
output: shell-2.html
output: shell-2.html~
output: shell-2.log
output: shell-2.org
output: shell-2.org~
output: shell-2.out
output: shell-2.Rmd
output: shell-2.tex
output: shell-2.tex~
output: shell-2.toc
output: shell-3.html
output: shell-3.html~
output: shell-3.org
output: shell-3.org~
output: shell.html
output: shell.Rmd
output: test_dummy.html
output: #test_dummy.Rmd#
output: test_dummy.Rmd
output: test_dummy.Rmd~
output: tmpout
```
   * In the olden days, before color-coded output, they would add the argument -F to put a slash on the end of directory names so that they were visibly different

```bash
$ ls --color=never -F 
```

```
output: kutils.css
output: ou_swc_files/
output: rmd2html.sh*
output: shell-1.html
output: shell-1.Rmd
output: shell-2.aux
output: shell-2.html
output: shell-2.html~
output: shell-2.log
output: shell-2.org
output: shell-2.org~
output: shell-2.out
output: shell-2.Rmd
output: shell-2.tex
output: shell-2.tex~
output: shell-2.toc
output: shell-3.html
output: shell-3.html~
output: shell-3.org
output: shell-3.org~
output: shell.html
output: shell.Rmd
output: test_dummy.html
output: #test_dummy.Rmd#
output: test_dummy.Rmd
output: test_dummy.Rmd~
output: tmpout/
```
   * On Mac and Linux, one can read the built-in manual page for ls to see all possibilities  


```bash
$ man ls
```

   * In Git BASH, those documents were omitted, so one can Google search "man ls".
   
### Wildcards: Shell globs (*)

`ls` lists everything by default. But it might be used to list

   * only files that begin with "r"

```
ls a*
```

   * only files that end with ".Rmd"

```
ls *.Rmd
```

The symbol * matches anything, any number of times.

Shell globs are easy and quick, but not very powerful.
If you move further into the command line interface
(or programming in general), the "regular expressions"
will come into play.

	
### The ls arguments I use most often are `-l` and `-a`

    * Default will not list "hidden" items, things that begin with period

```bash
$ ls -a
```

```
output: .
output: ..
output: kutils.css
output: ou_swc_files
output: .Rhistory
output: rmd2html.sh
output: shell-1.html
output: shell-1.Rmd
output: shell-2.aux
output: shell-2.html
output: shell-2.html~
output: shell-2.log
output: shell-2.org
output: shell-2.org~
output: shell-2.out
output: shell-2.Rmd
output: shell-2.tex
output: shell-2.tex~
output: shell-2.toc
output: shell-3.html
output: shell-3.html~
output: shell-3.org
output: shell-3.org~
output: shell.html
output: shell.Rmd
output: test_dummy.html
output: .#test_dummy.Rmd
output: #test_dummy.Rmd#
output: test_dummy.Rmd
output: test_dummy.Rmd~
output: tmpout
```

   * The -l argument asks for more comprehensive information

```bash
$ ls -l
```

```
output: total 2440
output: -rw-rw-r-- 1 pauljohn pauljohn   7480 Nov 14 17:46 kutils.css
output: drwxrwxr-x 6 pauljohn pauljohn   4096 Nov 11 19:20 ou_swc_files
output: -rwxrwxr-x 1 pauljohn pauljohn   1182 Nov 11 08:38 rmd2html.sh
output: -rw-rw-r-- 1 pauljohn pauljohn 733511 Nov 14 17:47 shell-1.html
output: -rw-rw-r-- 1 pauljohn pauljohn  22198 Nov 14 17:48 shell-1.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn   6903 Nov 13 15:22 shell-2.aux
output: -rw-rw-r-- 1 pauljohn pauljohn  44626 Nov 13 15:21 shell-2.html
output: -rw-rw-r-- 1 pauljohn pauljohn  44623 Nov 13 15:16 shell-2.html~
output: -rw-rw-r-- 1 pauljohn pauljohn  41563 Nov 13 15:22 shell-2.log
output: -rw-rw-r-- 1 pauljohn pauljohn  29842 Nov 14 17:18 shell-2.org
output: -rw-rw-r-- 1 pauljohn pauljohn  13993 Nov 13 13:04 shell-2.org~
output: -rw-rw-r-- 1 pauljohn pauljohn   2488 Nov 13 15:22 shell-2.out
output: -rw-rw-r-- 1 pauljohn pauljohn   1431 Nov 11 19:31 shell-2.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn  26446 Nov 13 15:22 shell-2.tex
output: -rw-rw-r-- 1 pauljohn pauljohn  16246 Nov 13 14:05 shell-2.tex~
output: -rw-rw-r-- 1 pauljohn pauljohn      0 Nov 13 15:22 shell-2.toc
output: -rw-rw-r-- 1 pauljohn pauljohn  16300 Nov 13 16:21 shell-3.html
output: -rw-rw-r-- 1 pauljohn pauljohn  12035 Nov 13 15:44 shell-3.html~
output: -rw-rw-r-- 1 pauljohn pauljohn   5629 Nov 13 16:25 shell-3.org
output: -rw-rw-r-- 1 pauljohn pauljohn   1416 Nov 13 15:33 shell-3.org~
output: -rw-rw-r-- 1 pauljohn pauljohn 719850 Nov 11 17:34 shell.html
output: -rw-rw-r-- 1 pauljohn pauljohn    286 Nov 11 08:38 shell.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn 669702 Nov 14 09:02 test_dummy.html
output: -rw-rw-r-- 1 pauljohn pauljohn   3063 Nov 14 09:10 #test_dummy.Rmd#
output: -rw-rw-r-- 1 pauljohn pauljohn   2535 Nov 14 09:03 test_dummy.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn  21726 Nov 14 08:36 test_dummy.Rmd~
output: drwxrwxr-x 2 pauljohn pauljohn   4096 Nov 11 08:38 tmpout
```

   * Often I put the two together

```bash
$ ls -la
```

```
output: total 2452
output: drwxrwxr-x 4 pauljohn pauljohn   4096 Nov 14 17:48 .
output: drwxrwxr-x 4 pauljohn pauljohn   4096 Nov 13 10:44 ..
output: -rw-rw-r-- 1 pauljohn pauljohn   7480 Nov 14 17:46 kutils.css
output: drwxrwxr-x 6 pauljohn pauljohn   4096 Nov 11 19:20 ou_swc_files
output: -rw-rw-r-- 1 pauljohn pauljohn    822 Nov 14 09:03 .Rhistory
output: -rwxrwxr-x 1 pauljohn pauljohn   1182 Nov 11 08:38 rmd2html.sh
output: -rw-rw-r-- 1 pauljohn pauljohn 733511 Nov 14 17:47 shell-1.html
output: -rw-rw-r-- 1 pauljohn pauljohn  22198 Nov 14 17:48 shell-1.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn   6903 Nov 13 15:22 shell-2.aux
output: -rw-rw-r-- 1 pauljohn pauljohn  44626 Nov 13 15:21 shell-2.html
output: -rw-rw-r-- 1 pauljohn pauljohn  44623 Nov 13 15:16 shell-2.html~
output: -rw-rw-r-- 1 pauljohn pauljohn  41563 Nov 13 15:22 shell-2.log
output: -rw-rw-r-- 1 pauljohn pauljohn  29842 Nov 14 17:18 shell-2.org
output: -rw-rw-r-- 1 pauljohn pauljohn  13993 Nov 13 13:04 shell-2.org~
output: -rw-rw-r-- 1 pauljohn pauljohn   2488 Nov 13 15:22 shell-2.out
output: -rw-rw-r-- 1 pauljohn pauljohn   1431 Nov 11 19:31 shell-2.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn  26446 Nov 13 15:22 shell-2.tex
output: -rw-rw-r-- 1 pauljohn pauljohn  16246 Nov 13 14:05 shell-2.tex~
output: -rw-rw-r-- 1 pauljohn pauljohn      0 Nov 13 15:22 shell-2.toc
output: -rw-rw-r-- 1 pauljohn pauljohn  16300 Nov 13 16:21 shell-3.html
output: -rw-rw-r-- 1 pauljohn pauljohn  12035 Nov 13 15:44 shell-3.html~
output: -rw-rw-r-- 1 pauljohn pauljohn   5629 Nov 13 16:25 shell-3.org
output: -rw-rw-r-- 1 pauljohn pauljohn   1416 Nov 13 15:33 shell-3.org~
output: -rw-rw-r-- 1 pauljohn pauljohn 719850 Nov 11 17:34 shell.html
output: -rw-rw-r-- 1 pauljohn pauljohn    286 Nov 11 08:38 shell.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn 669702 Nov 14 09:02 test_dummy.html
output: lrwxrwxrwx 1 pauljohn pauljohn     35 Nov 14 09:03 .#test_dummy.Rmd -> pauljohn@delllap-16.3060:1478924101
output: -rw-rw-r-- 1 pauljohn pauljohn   3063 Nov 14 09:10 #test_dummy.Rmd#
output: -rw-rw-r-- 1 pauljohn pauljohn   2535 Nov 14 09:03 test_dummy.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn  21726 Nov 14 08:36 test_dummy.Rmd~
output: drwxrwxr-x 2 pauljohn pauljohn   4096 Nov 11 08:38 tmpout
```

   * The far left part is read, write, and execute permissions.
   * Windows handles permissions differently than Unix/Linux, so
   	  * The BASH shell's view of them is not entirely accurate all the time
      * Well, its accurate, but not "fine-grained".

#### And Now, some PATH magic {.bs-callout .bs-callout-warning} 

   * We can repeatedly display contents of subdirectories
      * Run `ls`, hopefully you see at least one directory. Suppose that's called "Documents"
      * Try this

```bash
$ ls Documents
```

      * If we are lucky, Documents has another directory, say "Papers" inside it


```bash
$ ls Documents/Papers
```

   * That is a "**relative path**", the directories are viewed within context of current directory.

	


```bash
$ ls ..
```
   * What is ".."?

```bash
$ ls ../..
```
	

```bash
$ ls /
```
   * Mac & Linux differ from MS DOS/Windows on the definition of the "top level" folder.
      * Mac & Linux: the highest level accessible is always "/", the root directory
	     * external devices are "mounted" somewhere under "/"
      * Windows "top level" is "My Computer", in which different drives are lettered
	     * C:\  (Typical "Main drive")
		 * D:\
      * The Shell represents that Windows tendency by engulfing the lettered devices within a higher level "/", so within the Git BASH shell on Windows, these appear as


```bash
$ /c/
```

   * Suppose $HOME is /c/Users/pauljohn

If we set the working directory as $HOME with

```bash
$ cd
```
   
Then inspecting a sub-folder with   

```bash
$ ls Documents/Papers
```
is equivalent to using a full, absolute path

```bash
$ ls /c/Users/pauljohn/Documents/Papers
```
	
   * The "**absolute path**" always begin with "/" and it explicitly shows each directory name.

   * Many ways to show HOME (if working directory is somewhere else)

```bash
$ ls $HOME
```
Is the same as


```bash
$ ls ~
```
And relative PATH will work in an understandable way

```bash
$ ls ~/Documents
```
	

## Quick Summary
 
   * ls: a program for listing contents of folders	
   * PATH: directory names separated by "/"
   * ~ is a synonym for $HOME



# Change the working directory

#### cd: change directory
  * We already saw that `cd` (without arguments) returns user to $HOME
  * More generally `cd` can change the specified working directory

### `cd` examples everybody should try.

   * First, run `ls -F` to find a directory name (thing with slash on end), e.g. `Desktop`, then


```bash
$ cd Desktop
$ pwd
$ ls -F
```
**cd**: change the working directory	

   * If `ls` shows there is another directory, then `cd` into it. Run `ls` again

   * Run `cd` to go back to HOME.

   * Now please verify the following.
      1. TAB completion works. If you type `cd Des` and stop typing, and then hit TAB, does it auto-complete the word Desktop?
	  2. Continue with autocompletion. When "Desktop" is filled in, hit TAB a couple of times. It will show nothing if there are no directories within Desktop, but if there are, it will show them on the screen.
	  3. Type the first few letters of a directory name, hit TAB again.
   * After all of that TABing, you shoud have a prompt that looks like this

```bash
$ cd Desktop/whatever_subdir
```
      * hit enter, then run `pwd` to make sure you are in there
	  * perhaps the prompt changed to let you know, without running pwd

   * Oops, you went one too far! Go back

```bash
$ cd ..
```
   * Benefits of TAB completion. *Too numerous to write out in their entirety* :)




   

# Make a directory

#### This will change something in your computer, so pay attention {.bs-callout .bs-callout-danger}

   * Change to a directory where you would put your work for today.
   * Most people choose (e.g., Desktop or Documents)


```bash
$ cd Desktop
```
   * Make a new directory
   	

```bash
$ mkdir sc-20161115
```
**mkdir**: make a new directory

   * Make sure it is there with `ls`
   * Change into that directory, (don't forget TAB completion)!

   * recursive (nested) directories

      * By default, `mkdir` is willing to create only one new "layer".

	  * `mkdir Desktop/sc-20161115/topdir/middir/lowerdir` will be rejected.
	  * To create a hierarchy of directories in one command, add the `-p` flag

```bash
$ mkdir -p Desktop/sc-20161115/topdir/middir/lowerdir
```

## Quick Summary
 
   * mkdir: creates a directory. Only adds "one level deeper"


   * mkdir -p: create recursively  


	
# Worlds Collide
  
   * Lets figure out how to see your new directory Desktop/sc-20161115
     in your "Modern Graphical Operating System".
   
   * Launch a file manager in the usual way (Windows Explorer, Mac Finder, Linux
     Nautilus, etc)

	    * Navigate to Desktop/sc-20161115

   * Terminal programs can launch those file managers		
   
   * Git BASH for Windows includes a shortcut command. Type
   

```bash
$ explorer .
```
   * Terminal on Macintosh can launch a File Finder:
   

```bash
$ open .
```

	* In both of these, "." means "Current Working Directory"
	
##  Please do some practices
	
   * Make a disposable directory.

```bash
$ cd
$ mkdir -p Desktop/mistake
```
	
   * Check to see if the directory mistake is visible
   
      * inside the Terminal
	  
      * in the graphical file manager program

   * Use the graphical file manager to create a directory inside `mistake`.

   * Make sure you can see that from inside the terminal

   * Then create an empty file this way


```bash
$ cd Desktop/mistake
$ touch great_file.txt
```

**touch**: sets current time on a file. If no file exists, create
  emtpty file with that date.

   * Run `ls -la` to make sure the file is there

   * Use the graphical file manager program to see if "great_file.txt"
     exists.

   * Does right-click "edit with" give you any candidate editors? We
     need a text editor. Not a Word Processor (Word, Libre Office),
     but rather a "flat text" editor. Save the file.

   * Back in the terminal, lets inspect what happened.
   

```bash
$ ls -la
$ cat great_file.txt
```
**cat**: opens file and displays it from top to bottom	
	
   * There are editors that work well "in the terminal", but using
     them is a lost art, except among programmers and truly
	 devoted terminal-loving data scientists. My
     Mom could do this in 1985, you could too.
   
      * nano is available on most Mac and Linux systems, and it
        *might* be available in a Windows BASH shell program.

	  * vi is an old old fast fast flat text editor I can demonstrate.

		 * It will be launched often by programs like Git, so one must
           get some tolerance for it.
		 
         * The get out of jail keystrokes: `Esc : wq` (Yes, Escape,
           followed by a colon. If you watch the very bottom of the terminal,
		   you get a hint it is accepting commands. Then type `w` and `q` (to
		   "write" and "quit")
		   
      * I'm an Emacs enthusiast, but NOT in the terminal. That's too
        severe without menus.

	     * The get-out-of-jail key sequence is `Ctl-x Ctl-c` to close it down.

## Quick Summary
 
   * A part of the hard disk file storage can be thought of as
     'shared' content between 2 separate systems.

   * Shell commands like "mkdir" and "cd" have obvious equivalents in
     the GUI File Manager

   * A benefit of the Terminal/Shell is that problems too big, which
     would overwhelm the GUI, can still be done.


		 
# Delete directories and files

#### Terminal Defaults: no "safety net"{.bs-callout .bs-callout-danger}

   * There's no "Trash Can" built into the shell

   * Default setup will not ask "do you really mean to delete that?"
     It will just do it.

   * There is a "safe delete" flag, `-i`

      * If that is included in usage of all file mover/destroyer functions,
      system will not follow your orders right away.

      * When I go to a new computer account, the first thing I do is
        insert a shell configuration that inserts `-i` with all usages of `rm`,
        `cp` and `mv`.  (keywords: `alias` and `profile`).

### `rm` deletes things	 
	 
   * `cd` into directory that has the trash file we were fiddling with "great_file.txt"

   * Delete that file


```bash
$ rm great_file.txt
```
   * If there is no message, that means it worked!
      * Check in the terminal with `ls`
	  * Check in the GUI file manager

### Delete a directory that is not empty

	* rm will refuse a request to delete a non-empty directory

      * Error message will be something like
```      
	rm: cannot remove 'mistake': Is a directory
```

	* Flags "-r" and "-f" override that resistance

	   * "**-r**": recursive
	   * "**-f**": force (don't bother me with warnings)

 	* If the mistake directory is still there, get rid of it


```bash
$ cd
$ cd Desktop
$ ls mistake
$ rm -rf mistake
```

### A Safer Workflow might Use move commands, which we will see
	next.
	 
	   
## Quick Summary
 
   * rm: can remove a file, or several files.
   * rm -rf: remove a folder and everything in it  
   * The default setup has no warning or "do you really want to do this?"



# Move and Rename: same thing!

####  mv is multi-talented {.bs-callout .bs-callout-info}
 
   * General syntax `mv x y`

      * x is the source

      * y is the target

   * If x is a directory, and

      * y does not exist, then x is renamed as y

   * If y is a directory name that already exists, x is moved inside y.


   * Re-create the mistake directory.
      * Use cd to reposition yourself
   

```bash
$ mkdir mistake
```
	   * Spawn a few empty files in there

```bash
$ touch mistake/myfile1.txt
$ touch mistake/myfile2.txt
$ ls -la mistake
```

```
output: total 8
output: drwxrwxr-x 2 pauljohn pauljohn 4096 Nov 14 17:48 .
output: drwxrwxr-x 5 pauljohn pauljohn 4096 Nov 14 17:48 ..
output: -rw-rw-r-- 1 pauljohn pauljohn    0 Nov 14 17:48 myfile1.txt
output: -rw-rw-r-- 1 pauljohn pauljohn    0 Nov 14 17:48 myfile2.txt
```


```bash
$ ls -laF
```

```
output: total 2456
output: drwxrwxr-x 5 pauljohn pauljohn   4096 Nov 14 17:48 ./
output: drwxrwxr-x 4 pauljohn pauljohn   4096 Nov 13 10:44 ../
output: -rw-rw-r-- 1 pauljohn pauljohn   7480 Nov 14 17:46 kutils.css
output: drwxrwxr-x 2 pauljohn pauljohn   4096 Nov 14 17:48 mistake/
output: drwxrwxr-x 6 pauljohn pauljohn   4096 Nov 11 19:20 ou_swc_files/
output: -rw-rw-r-- 1 pauljohn pauljohn    822 Nov 14 09:03 .Rhistory
output: -rwxrwxr-x 1 pauljohn pauljohn   1182 Nov 11 08:38 rmd2html.sh*
output: -rw-rw-r-- 1 pauljohn pauljohn 733511 Nov 14 17:47 shell-1.html
output: -rw-rw-r-- 1 pauljohn pauljohn  22198 Nov 14 17:48 shell-1.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn   6903 Nov 13 15:22 shell-2.aux
output: -rw-rw-r-- 1 pauljohn pauljohn  44626 Nov 13 15:21 shell-2.html
output: -rw-rw-r-- 1 pauljohn pauljohn  44623 Nov 13 15:16 shell-2.html~
output: -rw-rw-r-- 1 pauljohn pauljohn  41563 Nov 13 15:22 shell-2.log
output: -rw-rw-r-- 1 pauljohn pauljohn  29842 Nov 14 17:18 shell-2.org
output: -rw-rw-r-- 1 pauljohn pauljohn  13993 Nov 13 13:04 shell-2.org~
output: -rw-rw-r-- 1 pauljohn pauljohn   2488 Nov 13 15:22 shell-2.out
output: -rw-rw-r-- 1 pauljohn pauljohn   1431 Nov 11 19:31 shell-2.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn  26446 Nov 13 15:22 shell-2.tex
output: -rw-rw-r-- 1 pauljohn pauljohn  16246 Nov 13 14:05 shell-2.tex~
output: -rw-rw-r-- 1 pauljohn pauljohn      0 Nov 13 15:22 shell-2.toc
output: -rw-rw-r-- 1 pauljohn pauljohn  16300 Nov 13 16:21 shell-3.html
output: -rw-rw-r-- 1 pauljohn pauljohn  12035 Nov 13 15:44 shell-3.html~
output: -rw-rw-r-- 1 pauljohn pauljohn   5629 Nov 13 16:25 shell-3.org
output: -rw-rw-r-- 1 pauljohn pauljohn   1416 Nov 13 15:33 shell-3.org~
output: -rw-rw-r-- 1 pauljohn pauljohn 719850 Nov 11 17:34 shell.html
output: -rw-rw-r-- 1 pauljohn pauljohn    286 Nov 11 08:38 shell.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn 669702 Nov 14 09:02 test_dummy.html
output: lrwxrwxrwx 1 pauljohn pauljohn     35 Nov 14 09:03 .#test_dummy.Rmd -> pauljohn@delllap-16.3060:1478924101
output: -rw-rw-r-- 1 pauljohn pauljohn   3063 Nov 14 09:10 #test_dummy.Rmd#
output: -rw-rw-r-- 1 pauljohn pauljohn   2535 Nov 14 09:03 test_dummy.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn  21726 Nov 14 08:36 test_dummy.Rmd~
output: drwxrwxr-x 2 pauljohn pauljohn   4096 Nov 11 08:38 tmpout/
```
### Move a directory = rename that directory


```bash
$ ls -laF
```

```
output: total 2456
output: drwxrwxr-x 5 pauljohn pauljohn   4096 Nov 14 17:48 ./
output: drwxrwxr-x 4 pauljohn pauljohn   4096 Nov 13 10:44 ../
output: -rw-rw-r-- 1 pauljohn pauljohn   7480 Nov 14 17:46 kutils.css
output: drwxrwxr-x 2 pauljohn pauljohn   4096 Nov 14 17:48 mistake/
output: drwxrwxr-x 6 pauljohn pauljohn   4096 Nov 11 19:20 ou_swc_files/
output: -rw-rw-r-- 1 pauljohn pauljohn    822 Nov 14 09:03 .Rhistory
output: -rwxrwxr-x 1 pauljohn pauljohn   1182 Nov 11 08:38 rmd2html.sh*
output: -rw-rw-r-- 1 pauljohn pauljohn 733511 Nov 14 17:47 shell-1.html
output: -rw-rw-r-- 1 pauljohn pauljohn  22198 Nov 14 17:48 shell-1.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn   6903 Nov 13 15:22 shell-2.aux
output: -rw-rw-r-- 1 pauljohn pauljohn  44626 Nov 13 15:21 shell-2.html
output: -rw-rw-r-- 1 pauljohn pauljohn  44623 Nov 13 15:16 shell-2.html~
output: -rw-rw-r-- 1 pauljohn pauljohn  41563 Nov 13 15:22 shell-2.log
output: -rw-rw-r-- 1 pauljohn pauljohn  29842 Nov 14 17:18 shell-2.org
output: -rw-rw-r-- 1 pauljohn pauljohn  13993 Nov 13 13:04 shell-2.org~
output: -rw-rw-r-- 1 pauljohn pauljohn   2488 Nov 13 15:22 shell-2.out
output: -rw-rw-r-- 1 pauljohn pauljohn   1431 Nov 11 19:31 shell-2.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn  26446 Nov 13 15:22 shell-2.tex
output: -rw-rw-r-- 1 pauljohn pauljohn  16246 Nov 13 14:05 shell-2.tex~
output: -rw-rw-r-- 1 pauljohn pauljohn      0 Nov 13 15:22 shell-2.toc
output: -rw-rw-r-- 1 pauljohn pauljohn  16300 Nov 13 16:21 shell-3.html
output: -rw-rw-r-- 1 pauljohn pauljohn  12035 Nov 13 15:44 shell-3.html~
output: -rw-rw-r-- 1 pauljohn pauljohn   5629 Nov 13 16:25 shell-3.org
output: -rw-rw-r-- 1 pauljohn pauljohn   1416 Nov 13 15:33 shell-3.org~
output: -rw-rw-r-- 1 pauljohn pauljohn 719850 Nov 11 17:34 shell.html
output: -rw-rw-r-- 1 pauljohn pauljohn    286 Nov 11 08:38 shell.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn 669702 Nov 14 09:02 test_dummy.html
output: lrwxrwxrwx 1 pauljohn pauljohn     35 Nov 14 09:03 .#test_dummy.Rmd -> pauljohn@delllap-16.3060:1478924101
output: -rw-rw-r-- 1 pauljohn pauljohn   3063 Nov 14 09:10 #test_dummy.Rmd#
output: -rw-rw-r-- 1 pauljohn pauljohn   2535 Nov 14 09:03 test_dummy.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn  21726 Nov 14 08:36 test_dummy.Rmd~
output: drwxrwxr-x 2 pauljohn pauljohn   4096 Nov 11 08:38 tmpout/
```



```bash
$ mv mistake success
```


```bash
$ ls -laF
```

```
output: total 2456
output: drwxrwxr-x 5 pauljohn pauljohn   4096 Nov 14 17:48 ./
output: drwxrwxr-x 4 pauljohn pauljohn   4096 Nov 13 10:44 ../
output: -rw-rw-r-- 1 pauljohn pauljohn   7480 Nov 14 17:46 kutils.css
output: drwxrwxr-x 6 pauljohn pauljohn   4096 Nov 11 19:20 ou_swc_files/
output: -rw-rw-r-- 1 pauljohn pauljohn    822 Nov 14 09:03 .Rhistory
output: -rwxrwxr-x 1 pauljohn pauljohn   1182 Nov 11 08:38 rmd2html.sh*
output: -rw-rw-r-- 1 pauljohn pauljohn 733511 Nov 14 17:47 shell-1.html
output: -rw-rw-r-- 1 pauljohn pauljohn  22198 Nov 14 17:48 shell-1.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn   6903 Nov 13 15:22 shell-2.aux
output: -rw-rw-r-- 1 pauljohn pauljohn  44626 Nov 13 15:21 shell-2.html
output: -rw-rw-r-- 1 pauljohn pauljohn  44623 Nov 13 15:16 shell-2.html~
output: -rw-rw-r-- 1 pauljohn pauljohn  41563 Nov 13 15:22 shell-2.log
output: -rw-rw-r-- 1 pauljohn pauljohn  29842 Nov 14 17:18 shell-2.org
output: -rw-rw-r-- 1 pauljohn pauljohn  13993 Nov 13 13:04 shell-2.org~
output: -rw-rw-r-- 1 pauljohn pauljohn   2488 Nov 13 15:22 shell-2.out
output: -rw-rw-r-- 1 pauljohn pauljohn   1431 Nov 11 19:31 shell-2.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn  26446 Nov 13 15:22 shell-2.tex
output: -rw-rw-r-- 1 pauljohn pauljohn  16246 Nov 13 14:05 shell-2.tex~
output: -rw-rw-r-- 1 pauljohn pauljohn      0 Nov 13 15:22 shell-2.toc
output: -rw-rw-r-- 1 pauljohn pauljohn  16300 Nov 13 16:21 shell-3.html
output: -rw-rw-r-- 1 pauljohn pauljohn  12035 Nov 13 15:44 shell-3.html~
output: -rw-rw-r-- 1 pauljohn pauljohn   5629 Nov 13 16:25 shell-3.org
output: -rw-rw-r-- 1 pauljohn pauljohn   1416 Nov 13 15:33 shell-3.org~
output: -rw-rw-r-- 1 pauljohn pauljohn 719850 Nov 11 17:34 shell.html
output: -rw-rw-r-- 1 pauljohn pauljohn    286 Nov 11 08:38 shell.Rmd
output: drwxrwxr-x 2 pauljohn pauljohn   4096 Nov 14 17:48 success/
output: -rw-rw-r-- 1 pauljohn pauljohn 669702 Nov 14 09:02 test_dummy.html
output: lrwxrwxrwx 1 pauljohn pauljohn     35 Nov 14 09:03 .#test_dummy.Rmd -> pauljohn@delllap-16.3060:1478924101
output: -rw-rw-r-- 1 pauljohn pauljohn   3063 Nov 14 09:10 #test_dummy.Rmd#
output: -rw-rw-r-- 1 pauljohn pauljohn   2535 Nov 14 09:03 test_dummy.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn  21726 Nov 14 08:36 test_dummy.Rmd~
output: drwxrwxr-x 2 pauljohn pauljohn   4096 Nov 11 08:38 tmpout/
```

Check that the files are still in there


```bash
$ ls -laF success
```

```
output: total 8
output: drwxrwxr-x 2 pauljohn pauljohn 4096 Nov 14 17:48 ./
output: drwxrwxr-x 5 pauljohn pauljohn 4096 Nov 14 17:48 ../
output: -rw-rw-r-- 1 pauljohn pauljohn    0 Nov 14 17:48 myfile1.txt
output: -rw-rw-r-- 1 pauljohn pauljohn    0 Nov 14 17:48 myfile2.txt
```

### Move a directory = relocate whole directory (and all contents within)

   * In previous example, the target directory "success" did not exist, so
     Shell understood what we needed.

   * If target directory did exist, then whole "mistake" directory would
     be moved into it.


```bash
$ mkdir wonderful
$ ls -F
$ # Move success into wonderful:
$ mv success wonderful
```

```
output: kutils.css
output: ou_swc_files/
output: rmd2html.sh*
output: shell-1.html
output: shell-1.Rmd
output: shell-2.aux
output: shell-2.html
output: shell-2.html~
output: shell-2.log
output: shell-2.org
output: shell-2.org~
output: shell-2.out
output: shell-2.Rmd
output: shell-2.tex
output: shell-2.tex~
output: shell-2.toc
output: shell-3.html
output: shell-3.html~
output: shell-3.org
output: shell-3.org~
output: shell.html
output: shell.Rmd
output: success/
output: test_dummy.html
output: #test_dummy.Rmd#
output: test_dummy.Rmd
output: test_dummy.Rmd~
output: tmpout/
output: wonderful/
```


```bash
$ ls -laF
```

```
output: total 2456
output: drwxrwxr-x 5 pauljohn pauljohn   4096 Nov 14 17:48 ./
output: drwxrwxr-x 4 pauljohn pauljohn   4096 Nov 13 10:44 ../
output: -rw-rw-r-- 1 pauljohn pauljohn   7480 Nov 14 17:46 kutils.css
output: drwxrwxr-x 6 pauljohn pauljohn   4096 Nov 11 19:20 ou_swc_files/
output: -rw-rw-r-- 1 pauljohn pauljohn    822 Nov 14 09:03 .Rhistory
output: -rwxrwxr-x 1 pauljohn pauljohn   1182 Nov 11 08:38 rmd2html.sh*
output: -rw-rw-r-- 1 pauljohn pauljohn 733511 Nov 14 17:47 shell-1.html
output: -rw-rw-r-- 1 pauljohn pauljohn  22198 Nov 14 17:48 shell-1.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn   6903 Nov 13 15:22 shell-2.aux
output: -rw-rw-r-- 1 pauljohn pauljohn  44626 Nov 13 15:21 shell-2.html
output: -rw-rw-r-- 1 pauljohn pauljohn  44623 Nov 13 15:16 shell-2.html~
output: -rw-rw-r-- 1 pauljohn pauljohn  41563 Nov 13 15:22 shell-2.log
output: -rw-rw-r-- 1 pauljohn pauljohn  29842 Nov 14 17:18 shell-2.org
output: -rw-rw-r-- 1 pauljohn pauljohn  13993 Nov 13 13:04 shell-2.org~
output: -rw-rw-r-- 1 pauljohn pauljohn   2488 Nov 13 15:22 shell-2.out
output: -rw-rw-r-- 1 pauljohn pauljohn   1431 Nov 11 19:31 shell-2.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn  26446 Nov 13 15:22 shell-2.tex
output: -rw-rw-r-- 1 pauljohn pauljohn  16246 Nov 13 14:05 shell-2.tex~
output: -rw-rw-r-- 1 pauljohn pauljohn      0 Nov 13 15:22 shell-2.toc
output: -rw-rw-r-- 1 pauljohn pauljohn  16300 Nov 13 16:21 shell-3.html
output: -rw-rw-r-- 1 pauljohn pauljohn  12035 Nov 13 15:44 shell-3.html~
output: -rw-rw-r-- 1 pauljohn pauljohn   5629 Nov 13 16:25 shell-3.org
output: -rw-rw-r-- 1 pauljohn pauljohn   1416 Nov 13 15:33 shell-3.org~
output: -rw-rw-r-- 1 pauljohn pauljohn 719850 Nov 11 17:34 shell.html
output: -rw-rw-r-- 1 pauljohn pauljohn    286 Nov 11 08:38 shell.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn 669702 Nov 14 09:02 test_dummy.html
output: lrwxrwxrwx 1 pauljohn pauljohn     35 Nov 14 09:03 .#test_dummy.Rmd -> pauljohn@delllap-16.3060:1478924101
output: -rw-rw-r-- 1 pauljohn pauljohn   3063 Nov 14 09:10 #test_dummy.Rmd#
output: -rw-rw-r-- 1 pauljohn pauljohn   2535 Nov 14 09:03 test_dummy.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn  21726 Nov 14 08:36 test_dummy.Rmd~
output: drwxrwxr-x 2 pauljohn pauljohn   4096 Nov 11 08:38 tmpout/
output: drwxrwxr-x 3 pauljohn pauljohn   4096 Nov 14 17:48 wonderful/
```


```bash
$ ls -laF wonderful
```

```
output: total 12
output: drwxrwxr-x 3 pauljohn pauljohn 4096 Nov 14 17:48 ./
output: drwxrwxr-x 5 pauljohn pauljohn 4096 Nov 14 17:48 ../
output: drwxrwxr-x 2 pauljohn pauljohn 4096 Nov 14 17:48 success/
```

### Move a directory "Up" to $HOME directory


```bash
$ cd wonderful
$ mv success ~/
$ cd ..
```

Recall, "**~**": Tilde is shorthand for $HOME

### Go back one level and retrieve that directory. It should end up back
where we started.


```bash
$ mv ~/success  .
$ ls -laF
```

```
output: total 2460
output: drwxrwxr-x 6 pauljohn pauljohn   4096 Nov 14 17:48 ./
output: drwxrwxr-x 4 pauljohn pauljohn   4096 Nov 13 10:44 ../
output: -rw-rw-r-- 1 pauljohn pauljohn   7480 Nov 14 17:46 kutils.css
output: drwxrwxr-x 6 pauljohn pauljohn   4096 Nov 11 19:20 ou_swc_files/
output: -rw-rw-r-- 1 pauljohn pauljohn    822 Nov 14 09:03 .Rhistory
output: -rwxrwxr-x 1 pauljohn pauljohn   1182 Nov 11 08:38 rmd2html.sh*
output: -rw-rw-r-- 1 pauljohn pauljohn 733511 Nov 14 17:47 shell-1.html
output: -rw-rw-r-- 1 pauljohn pauljohn  22198 Nov 14 17:48 shell-1.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn   6903 Nov 13 15:22 shell-2.aux
output: -rw-rw-r-- 1 pauljohn pauljohn  44626 Nov 13 15:21 shell-2.html
output: -rw-rw-r-- 1 pauljohn pauljohn  44623 Nov 13 15:16 shell-2.html~
output: -rw-rw-r-- 1 pauljohn pauljohn  41563 Nov 13 15:22 shell-2.log
output: -rw-rw-r-- 1 pauljohn pauljohn  29842 Nov 14 17:18 shell-2.org
output: -rw-rw-r-- 1 pauljohn pauljohn  13993 Nov 13 13:04 shell-2.org~
output: -rw-rw-r-- 1 pauljohn pauljohn   2488 Nov 13 15:22 shell-2.out
output: -rw-rw-r-- 1 pauljohn pauljohn   1431 Nov 11 19:31 shell-2.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn  26446 Nov 13 15:22 shell-2.tex
output: -rw-rw-r-- 1 pauljohn pauljohn  16246 Nov 13 14:05 shell-2.tex~
output: -rw-rw-r-- 1 pauljohn pauljohn      0 Nov 13 15:22 shell-2.toc
output: -rw-rw-r-- 1 pauljohn pauljohn  16300 Nov 13 16:21 shell-3.html
output: -rw-rw-r-- 1 pauljohn pauljohn  12035 Nov 13 15:44 shell-3.html~
output: -rw-rw-r-- 1 pauljohn pauljohn   5629 Nov 13 16:25 shell-3.org
output: -rw-rw-r-- 1 pauljohn pauljohn   1416 Nov 13 15:33 shell-3.org~
output: -rw-rw-r-- 1 pauljohn pauljohn 719850 Nov 11 17:34 shell.html
output: -rw-rw-r-- 1 pauljohn pauljohn    286 Nov 11 08:38 shell.Rmd
output: drwxrwxr-x 2 pauljohn pauljohn   4096 Nov 14 17:48 success/
output: -rw-rw-r-- 1 pauljohn pauljohn 669702 Nov 14 09:02 test_dummy.html
output: lrwxrwxrwx 1 pauljohn pauljohn     35 Nov 14 09:03 .#test_dummy.Rmd -> pauljohn@delllap-16.3060:1478924101
output: -rw-rw-r-- 1 pauljohn pauljohn   3063 Nov 14 09:10 #test_dummy.Rmd#
output: -rw-rw-r-- 1 pauljohn pauljohn   2535 Nov 14 09:03 test_dummy.Rmd
output: -rw-rw-r-- 1 pauljohn pauljohn  21726 Nov 14 08:36 test_dummy.Rmd~
output: drwxrwxr-x 2 pauljohn pauljohn   4096 Nov 11 08:38 tmpout/
output: drwxrwxr-x 2 pauljohn pauljohn   4096 Nov 14 17:48 wonderful/
```

"**.**": Period is shorthand for here!, the current working directory

## Poor Person's Trash Folder

   * My aim is to create a Trash directory in my home account.


```bash
$ if [ ! -d ~/Trash ] 
$ then 
$    mkdir ~/Trash
$ fi
```
   
   * apologize for the if/then magic, will explain in shell-2.


Instead of running `rm` on unwanted things, consider


```bash
$ mv wonderful ~/Trash 
```


```bash
$ ls -laF ~/Trash
```

```
output: total 16
output: drwxrwxr-x  4 pauljohn pauljohn 4096 Nov 14 17:48 ./
output: drwxr-xr-x 82 pauljohn pauljohn 4096 Nov 14 17:48 ../
output: drwxr-xr-x  5 pauljohn pauljohn 4096 Jul  9 22:17 VBox/
output: drwxrwxr-x  2 pauljohn pauljohn 4096 Nov 14 17:48 wonderful/
```

## Quick Summary
  
   * `mv x y` will rename a file x as y if y does not exist
 
   * `mv x y` will move x into y if y is a directory

   * `mv x y` will obliterate y if y is a file

   * `y` can be a relative or absolute path 



# `cp` is for Copy: enough different from `mv` to be frustrating

### Syntax looks similar where files are concerned

   * `cp x y` # copies file `x` to file name `y`
   * `cp -R x y` # copies *recursively* directory x to y
   * recall I always have `-i` on uses of rm, cp, and mv


   * Like mv, if y is a directory that exists, then x is moved within it.

   * Biggest difference from `mv` is that `cp` will do nothing to copy a directory
   if you forget the -R. 
      * Error is like this
 ```
$  cp success ~/Trash
cp: omitting directory 'success'
 ```     

 # Big summary. We have reviewed

### The important creature comforts of a terminal

   * TAB completion
   * History (up arrow or "history" command)
   * Syntax highlighting

### Key concepts
   * HOME folder, known as ~
   * Absolute path begins with /, the root directory
   * Relative path begins with
      * directory name in current directory if "going downwards"
      * "../" if "going up" before possibly going downward again    

### We have reviewed the most essential commands needed to navigate in a Terminal/Shell

   * `pwd` print working directory
   * `ls` list files
   * `cd` change directory
   * `mkdir` create a directory

### And to remove and relocate files and directories   
   * `rm`  remove (delete)
   * `mv`  move / rename
   * `cp`: copy directories and files

### And some less vital, but useful commands

   * `echo $XYZ` prints out the contents of an environment variable `XYZ`
   * `cat xyz` prints out the contents of a file named `xyz`
   * `env` prints out the entire contents of the environment

