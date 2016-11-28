# Command Line, Shell
`r format(Sys.time(), '%Y %B %d')`  




# Process lots of files

#### Fairly common problem {.bs-callout .bs-callout-red}

1. Data collection generates 1000s of data files and each one must be
   processed separately.

2. Project generates 1000s of pdf files and we are required to look
   through a large random sample, one-by-one.

3. Vacation photos are saved in super high resolution and we need to
   convert each one to something smaller for Instagram.

#### The shell offers a convenient "for" loop that can handle this. {.bs-callout .bs-callout-orange}

```
for index ...items list here...
   do
      ...commands involving $index
done
```

*Syntax*:  

1. *for*: Lets the shell know something is coming.
2. An "index" variable is created, which is used to refer to each one
   of the things, one at a time
3. Keywords *do* and *done* are bookmarks for a sequence of shell statements.

#### My Vacation Photo example. {.bs-callout .bs-callout-blue}

When I went on vacation, I saved photos that were way too huge. There
is a handy free program named "convert" that can rescale images
however you like, but it wants one file at a time. The syntax for
that is

```
$ convert file.jpg -resize 1400x1050 -quality 85 file.new.jpg
```

To process a lot of files, it is necessary to take each file, create a
new name, and then run convert on each one. 

I want output that takes the old name *file.jpg* and creates
the new name *file-1400x1050.jpg*. This file name part of the
assignment creates a little detour on splitting the file name in two
pieces. There is a handy program called *basename* that I use
often. 

We can write this out in 2 ways

1. The "jam it all into 1 line method" uses semi-colon (;) for
   puncutation.

   ```
   $ for fn in *.jpg; do base=`basename $fn .jpg`; convert $fn -resize 1400x1050 -quality 85 $base-1400x1050.jpg; done
   ```

2. The patient shell approach. BASH knows you are not
done typing when you hit return, it waits (signalling ">" to you)

```
$ for fn in *.jpg
> do 
>   base=`basename $fn .jpg` 
>   convert $fn -resize 1400x1050 -quality 85 $base-1400x1050.jpg
> done
```

If you type that in, the shell will wait until you hit enter after
done to begin.

Tricky bits. 

1. The first "fn" has no dollar sign, but when it is accessed, "$fn" it
   does! Among programming languages, that is unusual. The variable is
   created with no dollar sign, but to access it we require the dollar
   sign.

2. The "do" statement applies to all of the lines that follow, until
   done. The one line method makes it appear as though it only applies
   to the first.


## North Pacific gyre data example

Recall in the north-pacific-gyre folder, there are several data files
to be processed.







```
cd Users/nelle/north-pacific-gyre/2012-07-03
```



```bash
$ ls N*.txt
```

```
output: NENE01729A.txt
output: NENE01729B.txt
output: NENE01736A.txt
output: NENE01751A.txt
output: NENE01751B.txt
output: NENE01812A.txt
output: NENE01843A.txt
output: NENE01843B.txt
output: NENE01971Z.txt
output: NENE01978A.txt
output: NENE01978B.txt
output: NENE02018B.txt
output: NENE02040A.txt
output: NENE02040B.txt
output: NENE02040Z.txt
output: NENE02043A.txt
output: NENE02043B.txt
```

# Our Assignment: Run each txt file through a data processing script.

Recall the problems unearthed in data inspection

   1. One file too small
   2. The Z-ending files are not useful
 
    We are going to ignore problem 1 and deal with 2 by selectively
	processing files.

## The shell script "goostats" is used to process each file and create a new data file.


#### My opinion on where the output should go {.bs-callout .bs-callout-red}

- I strongly prefer to keep the output in a separate output directory.
- And I would almost certainly put the output directory outside the
  current working directory.





```bash
$ mkdir ../output
```

Why do I like that? No danger of disrupting original data.

In fact, I'd make the original data "read only", taking
away write permissions like so

```
chmod -w N*.txt
```

Projects I organize will have many separate folders.


## goostats is a script included with the project. 

Our assignment is to run goostats for each data file. 

#### run goostats once {.bs-callout .bs-callout-orange}

   * The correct way to process just one file, including 2 parameters
     that professor said we needed: 


```bash
$ bash goostats  -J 100 -r NENE01729A.txt ../output/NENE01729A-stats.txt
```

   * Did it work?


```bash
$ ls ../output
```

```
output: NENE01729A-stats.txt
```

   * Lets remove that output folder before we try again


```bash
$ rm -rf  "../output"
```


#### Run goostats in a for loop: *over and over* {.bs-callout .bs-callout-gray}

```
$ mkdir ../output
$ for fn in *[AB].txt
>    do
>        bash goostats -J 100 -r "$fn" "../output/stats-$fn"
> done
```

## That was "in" the command line

I did not make a script file. I relied on the patience of the shell
to let me type all of that in.

If I have to run this more than once, I'd rather save the commands
into a file that I can use over and over.  That's the topic of the
next section.

# Scripts and command line arguments

#### The Big Picture {.bs-callout .bs-callout-red}

1. Test commands that work in the command line
2. Put those lines into a file
3. Work out the command line arguments problem
4. Consider adding "hash-bang" in line 1



## Write a script

#### Create the script file--a text file--named "dostats.sh".{.bs-callout .bs-callout-green}

It looks nicer to write it like this:

```
for fn in *[AB].txt
do
    echo $fn
    bash goostats -J 100 -r "$fn" "output/stats-$fn" 
done
```

But it is allowed to use semi-colon to jamb it into one line

```
for fn in *[AB].txt; do  echo $fn;  bash goostats -J 100 -r "$fn" "../output/stats-$fn"; done
```

At the command line, if we type

```
$ bash dostats.sh
```

the script will run in a BASH shell


## Use command line arguments

Now we have the file names hard coded in the script as *[AB].txt. 
We'd rather be flexible.

Here we use the symbol "$@" to grab all command line arguments


```bash
$ rm -rf ../output
$ mkdir ../output
$ for fn in "$@"
$ do
$     echo $fn
$     bash goostats -J 100 -r "$fn" "../output/stats-$fn" 
$ done
```

## More about command line arguments

The shell command line arguments can be handled in many ways. The
simple way simply we describe next is not the best way, since there is
no error checking on the inputs. However, it is commonly used in small
projects.

#### Key Terms: $1 and $@. {.bs-callout .bs-callout-orange}

Inside a shell script, these are the simple ways to access command
line arguments.

1. The dollar sign picks individual arguments

   - $n means the n'th argument.

   - $1 means "the first command line argument"
   - $2 means "the second command line argument"

2. $@ collects up all of the command line arguments.

More rigorous ways exist to name and check command line
arguments. Don't get too committed to the simple $1 $2 notation.

#### Lets make a little test case. .{.bs-callout .bs-callout-gray}

Write the following into a file named *mytest.sh*

```
echo "$1"
echo "$2"
echo "OMG here is $1 again"
echo "I'll splat them together $1$2"
```

The double quotes on the first 2 echo statements
are defensive programming. If user supplied $1 with a 
space or other illegal character, script would break.

Test that in the command line

1. Two arguments with no spaces

```
sh mytest.sh hellopaul hellobill
```

2. Watch what goes wrong if you have a space in a argument name "hello paul"

```
sh mytest.sh hello paul hellobill
```

The shell can't tell you want the first argument to be "hello paul"

3. Quotation marks can keep that argument together, so $1 will work.

```
sh mytest.sh "hello paul" hellobill
```

## Detour on executable files and "bash" as a program.

Using goostats on a single file, novice might be tempted to run

```
goostats infile.txt outfile.txt
```

   However, we hit problem(s). 
   1. goostats.sh is not executable, and
   1. goostats.sh is not in the path

#### Working around problem that goostats is not executable{.bs-callout .bs-callout-orange}

So we can't run it

   * My natural inclination would be to make goostats executable

```
chmod +x goostats.sh
```

   * and then run with the "./" trick

```
./goostats.sh infile.txt outfile.txt
```

   * Suppose, for security reasons, the system administrators
     have forbidden us from creating new executable files.

   * Workaround: even though "goostats"
     is not executable, we are allowed to run the program "bash" and
     it can open goostats and run it for us.


   * `bash` or `sh` or other shells

In the simple cases we are using here, it is virtually certain the 
program would run in a simpler shell than BASH, such as the much more
generic `sh` or the "lightweight" derivatives like `zsh`

```
sh goostats.sh
```

I mention this because on some large multi user systems, the `bash` 
luxury might not be available, while `sh` almost certainly will be.


## Detour about the hash-bang

* If we could make this executable, then running it would not
  guarantee the correct shell is used to run it. We want to make
  sure that `bash` is used, for example.

  We showed above it is possible to launch a program by passing it to
  "bash". That's not unheard of, but it would be somewhat unusual to 
  do this when the work is finished.

#### The hash-bang specifies a shell in line 1 {.bs-callout .bs-callout-orange}

* #! is pronounced "hash bang". 

   Often people would insert a line 1 message like this. It makes sure
   that our script is run with `bash` if we type "./dostats.sh"

```
#!/bin/bash
```

* Make the script executable, run

```
chmod +x dostats.sh
```

* If we could make that executable, then we could launch the script

```
./dostats.sh
```

* But if we are not allowed to do that the usual Unix say, we run like this

```
bash dostats.sh
```

* The "-x" flag activates a debug mode in bash


```
bash -x dostats.sh
```
