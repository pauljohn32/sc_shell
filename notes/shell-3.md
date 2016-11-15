<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#org46c8c0a">1. Process lots of files</a>
<ul>
<li><a href="#org7e350ae">1.1. Fairly common problem</a></li>
</ul>
</li>
<li><a href="#orgd420349">2. The shell offers a convenient "for" loop that can handle this.</a>
<ul>
<li><a href="#org4ee09df">2.1. My Vacation Photo example.</a></li>
<li><a href="#orgffa40e0">2.2. North Pacific gyre data example</a></li>
<li><a href="#org54deaf2">2.3. My opinion on where the output should go</a></li>
<li><a href="#orgbc20d42">2.4. goostats is a script included with the project.</a>
<ul>
<li><a href="#org7a5b221">2.4.1. run goostats once</a></li>
<li><a href="#orgc482bc2">2.4.2. For loop: run <b>over and over</b></a></li>
</ul>
</li>
</ul>
</li>
<li><a href="#orgd42f6f4">3. Scripts and command line arguments</a>
<ul>
<li><a href="#org7d9efb9">3.1. The Big Picture</a>
<ul>
<li><a href="#org9be4028">3.1.1. Create the text file "dostats.sh".</a></li>
<li><a href="#orgc47d667">3.1.2. Deal with the command line arguments</a></li>
</ul>
</li>
<li><a href="#orgdb431b3">3.2. Command line arguments</a>
<ul>
<li><a href="#orgeeec3e1">3.2.1. Key Terms</a></li>
<li><a href="#orgd411091">3.2.2. Lets make a little test case.</a></li>
</ul>
</li>
<li><a href="#orgc779cf4">3.3. Detour on executable files and "bash" as a program.</a></li>
<li><a href="#org37b51bf">3.4. Detour about the hash-bang</a></li>
</ul>
</li>
</ul>
</div>
</div>


<a id="org46c8c0a"></a>

# Process lots of files


<a id="org7e350ae"></a>

## Fairly common problem

1.  Data collection generates 1000s of data files and each one must be
    processed separately.

2.  Project generates 1000s of pdf files and we are required to look
    through a large random sample, one-by-one.

3.  Vacation photos are saved in super high resolution and we need to
    convert each one to something smaller for Instagram.


<a id="orgd420349"></a>

# The shell offers a convenient "for" loop that can handle this.

    for index ...items list here...
       do
          ...commands involving $index
    done

**Syntax**:  

1.  **for**: Lets the shell know something is coming.
2.  An "index" variable is created, which is used to refer to each one
    of the things, one at a time
3.  Keywords **do** and **done** are bookmarks for a sequence of shell statements.


<a id="org4ee09df"></a>

## My Vacation Photo example.

When I went on vacation, I saved photos that were way too huge. There
is a handy free program named "convert" that can rescale images
however you like, but it wants one file at a time. The syntax for
that is

    $ convert file.jpg -resize 1400x1050 -quality 85 file.new.jpg

To process a lot of files, it is necessary to take each file, create a
new name, and then run convert on each one. 

I want output that takes the old name **file.jpg** and creates
the new name **file-1400x1050.jpg**. This file name part of the
assignment creates a little detour on splitting the file name in two
pieces. There is a handy program called **basename** that I use
often. 

We can write this out in 2 ways

1.  The "jam it all into 1 line method" uses semi-colon (;) for
    puncutation.
    
        $ for fn in *.jpg; do base=`basename $fn .jpg`; convert $fn -resize 1400x1050 -quality 85 $base-1400x1050.jpg; done

2.  The patient shell approach. BASH knows you are not

done typing when you hit return, it waits (signalling ">" to you)

    $ for fn in *.jpg
    > do 
    >   base=`basename $fn .jpg` 
    >   convert $fn -resize 1400x1050 -quality 85 $base-1400x1050.jpg
    > done

If you type that in, the shell will wait until you hit enter after
done to begin.

Tricky bits. 

1.  The first "fn" has no dollar sign, but when it is accessed, "$fn" it
    does! Among programming languages, that is unusual. The variable is
    created with no dollar sign, but to access it we require the dollar
    sign.

2.  The "do" statement applies to all of the lines that follow, until
    done. The one line method makes it appear as though it only applies
    to the first.


<a id="orgffa40e0"></a>

## North Pacific gyre data example

Recall in the north-pacific-gyre folder, there are several data files
to be processed.

    ls N*.txt

    NENE01729A.txt
    NENE01729B.txt
    NENE01736A.txt
    NENE01751A.txt
    NENE01751B.txt
    NENE01812A.txt
    NENE01843A.txt
    NENE01843B.txt
    NENE01971Z.txt
    NENE01978A.txt
    NENE01978B.txt
    NENE02018B.txt
    NENE02040A.txt
    NENE02040B.txt
    NENE02040Z.txt
    NENE02043A.txt
    NENE02043B.txt

**Our Assignment**: Run each txt files through a data processing script.

Recall the problems unearthed in data inspection

1.  One file too small
2.  The Z-ending files are not useful

The shell script "goostats" is used to process each file and
create a new data output file.


<a id="org54deaf2"></a>

## My opinion on where the output should go

-   I strongly prefer to keep the output in a separate output directory.
-   And I would almost certainly put the output directory outside the
    current working directory.

    mkdir ../output

Why do I like that? No danger of disrupting original data.

In fact, I'd make the original data read only like so

    chmod -w N*.txt


<a id="orgbc20d42"></a>

## goostats is a script included with the project.

Our assignment is to run each file through goostats. 


<a id="org7a5b221"></a>

### run goostats once

-   The correct way to process just one file, including 2 parameters
    that professor said we needed.:

    bash goostats  -J 100 -r NENE01729A.txt ../output/NENE01729A-stats.txt

-   Did it work?

    ls ../output

    NENE01729A-stats.txt

-   Lets remove that output folder before we try again

    rm -rf  "../output"


<a id="orgc482bc2"></a>

### For loop: run **over and over**

    $ mkdir ../output
    $ for fn in *[AB].txt
    >    do
    >        bash goostats -J 100 -r "$fn" "../output/stats-$fn"
    > done


<a id="orgd42f6f4"></a>

# Scripts and command line arguments


<a id="org7d9efb9"></a>

## The Big Picture

1.  Test commands that work in the command line
2.  Put those lines into a file
3.  Work out the command line arguments problem
4.  Consider adding "hash-bang" in line 1


<a id="org9be4028"></a>

### Create the text file "dostats.sh".

It looks nicer to write it like this:

    for fn in *[AB].txt
    do
        echo $fn
        bash goostats -J 100 -r "$fn" "output/stats-$fn" 
    done

But it is allowed to use semi-colon to jamb it into one line

    for fn in *[AB].txt; do  echo $fn;  bash goostats -J 100 -r "$fn" "../output/stats-$fn"; done


<a id="orgc47d667"></a>

### Deal with the command line arguments

Now we have the file names hard coded in the script.

Here we use the shortcut "$@" to grab all command line arguments

    ### rm -rf ../output
    mkdir ../output
    for fn in "$@"
    do
    	echo $fn
    	bash goostats -J 100 -r "$fn" "../output/stats-$fn" 
    done


<a id="orgdb431b3"></a>

## Command line arguments

The shell command line arguments can be handled in many ways. The
simple way simply used arguments by their position in the command
line. This is not the best way, since there is no error checking
on the inputs. However, it is commonly used in small projects.


<a id="orgeeec3e1"></a>

### Key Terms

Inside a shell script, these are the simple ways to access command
line arguments.

1.  The dollar sign picks individual arguments
    -   $n means the n'th argument.
    
    -   $1 means "the first command line argument"
    -   $2 means "the second command line argument"

2.  $@ collects up all of the command line arguments.

More rigorous ways exist to name and check command
line arguments. Don't get too committed to the simple
$1 $2 notation.


<a id="orgd411091"></a>

### Lets make a little test case.

**mytest.sh**

    echo "$1"
    echo "$2"
    echo "OMG here is $1 again"
    echo "I'll splat them together $1$2"

I often forget the double-quotes on the arguments.

Test that in the command line

1.  No quotes

    sh mytest.sh hellopaul hellobill

1.  Watch what goes wrong if you have a space in a argument name "hello paul"

    sh mytest.sh hello paul hellobill

1.  Need to quote the argument to keep the pieces together

    sh mytest.sh "hello paul" hellobill


<a id="orgc779cf4"></a>

## Detour on executable files and "bash" as a program.

Using goostats on a single file, novice might be tempted to run

    goostats infile.txt outfile.txt

However, we hit problem(s). 

1.  goostats.sh is not executable, and
2.  goostats.sh is not in the path

So we can't run it

-   My natural inclination would be to make goostats executable

    chmod +x goostats.sh

-   and then run with the "./" trick

    ./goostats.sh infile.txt outfile.txt

-   however, for security reasons, the system administrators have
    forbidden us from creating new executable files.

-   there is a work-around, however, because even though "goostats"
    is not executable, we are allowed to run the program "bash" and
    it can open goostats and run it for us.

-   \`bash\` or \`sh\` or other shells

In the simple cases we are using here, it is virtually certain the 
program would run in a simpler shell than BASH, such as the much more
generic \`sh\` or the "lightweight" derivatives like \`zsh\`

    sh goostats.sh

I mention this because on some large multi user systems, the \`bash\` 
luxury might not be available, while \`sh\` almost certainly will be.


<a id="org37b51bf"></a>

## Detour about the hash-bang

-   If we could make this executable, then running it would not
    guarantee the correct shell is used to run it. We want to make
    sure that \`bash\` is used, for example.
    
    We showed above it is possible to launch a program by passing it to
    "bash". That's not unheard of, but it would be somewhat unusual to 
    do this when the work is finished.

-   \#! is pronounced "hash bang". 
    
    Often people would insert a line 1 message like this

    #!/bin/bash

-   Make the script executable, run

    chmod +x dostats.sh

-   If we could make that executable, then we could launch the script

    ./handlegoo.sh

-   But if we are not allowed to do that the usual Unix say, we run like this

    bash handlegoo.sh

-   The "-x" flag activates a debug mode in bash

    bash -x handlegoo.sh

