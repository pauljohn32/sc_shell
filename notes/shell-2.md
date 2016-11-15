<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#org1d62c40">1. Get the SWC files</a>
<ul>
<li><a href="#org493b145">1.1. We use git as a file retriever.</a></li>
<li><a href="#org081470e">1.2. <b>ls</b>: Inspect those files</a></li>
<li><a href="#org79e28b7">1.3. Use du check disk space used</a>
<ul>
<li><a href="#orgdc0fdef">1.3.1. Want less detail? add "&#x2013;max-depth" flag</a></li>
</ul>
</li>
</ul>
</li>
<li><a href="#org87308df">2. Inspect Contents (cat, head, tail)</a>
<ul>
<li><a href="#org5aaf74e">2.1. The North Pacific Gyre data</a>
<ul>
<li><a href="#org98550af">2.1.1. cd into directory that has some of Nelle's data</a></li>
</ul>
</li>
<li><a href="#org8b8ca67">2.2. cat: "concatenate" files and write on standard output</a></li>
<li><a href="#org4fc374f">2.3. head and tail: checking contents of big files</a>
<ul>
<li><a href="#orgee0bc80">2.3.1. head</a></li>
<li><a href="#org5a3917d">2.3.2. tail: check the last (default: 10) lines</a></li>
</ul>
</li>
<li><a href="#orgcb3089e">2.4. more and less</a>
<ul>
<li><a href="#org78a80bf">2.4.1. Run the more program to see "one screen at a time".</a></li>
</ul>
</li>
</ul>
</li>
<li><a href="#orgf886297">3. Executable Path</a>
<ul>
<li><a href="#org34bf484">3.1. Launch a program by name, including all directory structure</a></li>
<li><a href="#orgbfb83ae">3.2. Enter the <b>PATH</b></a>
<ul>
<li><a href="#org2f50edc">3.2.1. Note what Git Bash does</a></li>
</ul>
</li>
<li><a href="#org57b7b18">3.3. Text versus GUI programs</a>
<ul>
<li><a href="#orgdcbc290">3.3.1. On a Linux/Unix system, simply typing a GUI program's name will</a></li>
<li><a href="#org791170b">3.3.2. On Macintosh:</a></li>
<li><a href="#orgea32f2a">3.3.3. Windows</a></li>
</ul>
</li>
<li><a href="#org59183ee">3.4. What about programs that are not on the PATH?</a>
<ul>
<li><a href="#org1cb4f5a">3.4.1. We are swimming upstream, unfortunately</a></li>
</ul>
</li>
<li><a href="#orgfa41add">3.5. Need to add some directories to the PATH, probably&#x2026;</a></li>
</ul>
</li>
<li><a href="#org0319813">4. Programs talk to each other</a>
<ul>
<li><a href="#org5e6aa6e">4.1. The Pipe "|"</a></li>
<li><a href="#orga0ba94a">4.2. Programs I associate with back end of the pipe</a></li>
<li><a href="#org68ac502">4.3. Lets look at User nelle's files on molecules</a></li>
<li><a href="#orgfce906f">4.4. The wc program</a></li>
<li><a href="#orgfdb1c0d">4.5. "&gt;" and "&gt;&gt;" for redirecting output</a></li>
<li><a href="#org1cc6ee5">4.6. Pipe to more or less, for example</a></li>
</ul>
</li>
<li><a href="#org0e23201">5. grep is for Filtering</a>
<ul>
<li>
<ul>
<li><a href="#org6f7e87b">5.0.1. What is "regular expression"</a></li>
<li><a href="#org4289b06">5.0.2. Get out of jail free card for grep users</a></li>
</ul>
</li>
<li><a href="#orgc54f5e7">5.1. Use these skills to check the North Pacific Gyre data</a></li>
</ul>
</li>
</ul>
</div>
</div>


<a id="org1d62c40"></a>

# Get the SWC files


<a id="org493b145"></a>

## We use git as a file retriever.

git is the name of a "command line" program. 
Git's project management concepts will be discussed elsewhere.

    cd
    cd GIT/github
    git clone https://github.com/oulib-swc/ou_swc_files.git
    cd ou_swc_files


<a id="org081470e"></a>

## **ls**: Inspect those files

1.  list the items in the top level directory (ls)

2.  lists items

    ls

    gapminder
    inflammation
    Users

-   I need "-F" because color coding is lost in this output

    ls -F

    gapminder/
    inflammation/
    Users/

-   show hidden items

    ls -Fa

    ./
    ../
    gapminder/
    .git/
    inflammation/
    Users/

-   show detailed information

    ls -Fla

    total 24
    drwxrwxr-x 6 pauljohn pauljohn 4096 Nov 13 10:49 ./
    drwxrwxr-x 9 pauljohn pauljohn 4096 Nov 14 12:45 ../
    drwxrwxr-x 3 pauljohn pauljohn 4096 Nov 13 10:49 gapminder/
    drwxrwxr-x 8 pauljohn pauljohn 4096 Nov 14 14:00 .git/
    drwxrwxr-x 4 pauljohn pauljohn 4096 Nov 13 10:49 inflammation/
    drwxrwxr-x 5 pauljohn pauljohn 4096 Nov 13 10:49 Users/

-   List contents, including one level below

    ls -F *

    gapminder:
    data/
    
    inflammation:
    data/
    python/
    
    Users:
    imhotep/
    larry/
    nelle/

-   List files recursively with -R

    ls -FR

    .:
    gapminder/
    inflammation/
    Users/
    
    ./gapminder:
    data/
    
    ./gapminder/data:
    gapminder_all.csv
    gapminder_gdp_africa.csv
    gapminder_gdp_americas.csv
    gapminder_gdp_asia.csv
    gapminder_gdp_europe.csv
    gapminder_gdp_oceania.csv
    
    ./inflammation:
    data/
    python/
    
    ./inflammation/data:
    inflammation-01.csv
    inflammation-02.csv
    inflammation-03.csv
    inflammation-04.csv
    inflammation-05.csv
    inflammation-06.csv
    inflammation-07.csv
    inflammation-08.csv
    inflammation-09.csv
    inflammation-10.csv
    inflammation-11.csv
    inflammation-12.csv
    small-01.csv
    small-02.csv
    small-03.csv
    
    ./inflammation/python:
    argv-list.py
    arith.py
    check.py
    count-stdin.py
    errors_01.py
    errors_02.py
    gen-inflammation.py
    line-count.py
    my_ls.py
    readings-01.py
    readings-02.py
    readings-03.py
    readings-04.py
    readings-05.py
    readings-06.py
    readings-07.py
    readings-08.py
    readings-09.py
    rectangle.py
    sys-version.py
    
    ./Users:
    imhotep/
    larry/
    nelle/
    
    ./Users/imhotep:
    
    ./Users/larry:
    
    ./Users/nelle:
    creatures/
    data/
    Desktop/
    molecules/
    north-pacific-gyre/
    notes.txt
    pizza.cfg
    solar.pdf
    writing/
    
    ./Users/nelle/creatures:
    basilisk.dat
    unicorn.dat
    
    ./Users/nelle/data:
    amino-acids.txt
    animals.txt
    elements/
    morse.txt
    pdb/
    planets.txt
    salmon.txt
    sunspot.txt
    
    ./Users/nelle/data/elements:
    Ac.xml
    Ag.xml
    Al.xml
    Am.xml
    Ar.xml
    As.xml
    At.xml
    Au.xml
    Ba.xml
    Be.xml
    Bi.xml
    Bk.xml
    Br.xml
    B.xml
    Ca.xml
    Cd.xml
    Ce.xml
    Cf.xml
    Cl.xml
    Cm.xml
    Co.xml
    Cr.xml
    Cs.xml
    Cu.xml
    C.xml
    Dy.xml
    Er.xml
    Es.xml
    Eu.xml
    Fe.xml
    Fm.xml
    Fr.xml
    F.xml
    Ga.xml
    Gd.xml
    Ge.xml
    He.xml
    Hf.xml
    Hg.xml
    Ho.xml
    H.xml
    In.xml
    Ir.xml
    I.xml
    Kr.xml
    K.xml
    La.xml
    Li.xml
    Lr.xml
    Lu.xml
    Md.xml
    Mg.xml
    Mn.xml
    Mo.xml
    Na.xml
    Nb.xml
    Nd.xml
    Ne.xml
    Ni.xml
    No.xml
    Np.xml
    N.xml
    Os.xml
    O.xml
    Pa.xml
    Pb.xml
    Pd.xml
    Pm.xml
    Po.xml
    Pr.xml
    Pt.xml
    Pu.xml
    P.xml
    Ra.xml
    Rb.xml
    Re.xml
    Rh.xml
    Rn.xml
    Ru.xml
    Sb.xml
    Sc.xml
    Se.xml
    Si.xml
    Sm.xml
    Sn.xml
    Sr.xml
    S.xml
    Ta.xml
    Tb.xml
    Tc.xml
    Te.xml
    Th.xml
    Ti.xml
    Tl.xml
    Tm.xml
    U.xml
    V.xml
    W.xml
    Xe.xml
    Yb.xml
    Y.xml
    Zn.xml
    Zr.xml
    
    ./Users/nelle/data/pdb:
    aldrin.pdb
    ammonia.pdb
    ascorbic-acid.pdb
    benzaldehyde.pdb
    camphene.pdb
    cholesterol.pdb
    cinnamaldehyde.pdb
    citronellal.pdb
    codeine.pdb
    cubane.pdb
    cyclobutane.pdb
    cyclohexanol.pdb
    cyclopropane.pdb
    ethane.pdb
    ethanol.pdb
    ethylcyclohexane.pdb
    glycol.pdb
    heme.pdb
    lactic-acid.pdb
    lactose.pdb
    lanoxin.pdb
    lsd.pdb
    maltose.pdb
    menthol.pdb
    methane.pdb
    methanol.pdb
    mint.pdb
    morphine.pdb
    mustard.pdb
    nerol.pdb
    norethindrone.pdb
    octane.pdb
    pentane.pdb
    piperine.pdb
    propane.pdb
    pyridoxal.pdb
    quinine.pdb
    strychnine.pdb
    styrene.pdb
    sucrose.pdb
    testosterone.pdb
    thiamine.pdb
    tnt.pdb
    tuberin.pdb
    tyrian-purple.pdb
    vanillin.pdb
    vinyl-chloride.pdb
    vitamin-a.pdb
    
    ./Users/nelle/Desktop:
    
    ./Users/nelle/molecules:
    cubane.pdb
    ethane.pdb
    methane.pdb
    octane.pdb
    pentane.pdb
    propane.pdb
    records.txt
    
    ./Users/nelle/north-pacific-gyre:
    2012-07-03/
    output/
    
    ./Users/nelle/north-pacific-gyre/2012-07-03:
    goodiff
    goostats
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
    
    ./Users/nelle/north-pacific-gyre/output:
    NENE01729A-stats.txt
    
    ./Users/nelle/writing:
    data/
    haiku.txt
    old/
    thesis/
    tools/
    
    ./Users/nelle/writing/data:
    one.txt
    two.txt
    
    ./Users/nelle/writing/old:
    
    ./Users/nelle/writing/thesis:
    empty-draft.md
    
    ./Users/nelle/writing/tools:
    format
    old/
    stats
    
    ./Users/nelle/writing/tools/old:
    oldtool


<a id="org79e28b7"></a>

## Use du check disk space used

Default unit of measurement will be value not useful to humans, so add
"-h" flag to du command

    du -h

    84K	./inflammation/python
    112K	./inflammation/data
    200K	./inflammation
    88K	./gapminder/data
    92K	./gapminder
    4.0K	./.git/refs/tags
    8.0K	./.git/refs/remotes/origin
    12K	./.git/refs/remotes
    8.0K	./.git/refs/heads
    28K	./.git/refs
    8.0K	./.git/info
    4.0K	./.git/branches
    44K	./.git/hooks
    8.0K	./.git/logs/refs/remotes/origin
    12K	./.git/logs/refs/remotes
    8.0K	./.git/logs/refs/heads
    24K	./.git/logs/refs
    32K	./.git/logs
    4.0K	./.git/objects/info
    192K	./.git/objects/pack
    200K	./.git/objects
    364K	./.git
    4.0K	./Users/larry
    4.0K	./Users/nelle/Desktop
    212K	./Users/nelle/data/pdb
    416K	./Users/nelle/data/elements
    736K	./Users/nelle/data
    12K	./Users/nelle/creatures
    32K	./Users/nelle/molecules
    140K	./Users/nelle/north-pacific-gyre/2012-07-03
    8.0K	./Users/nelle/north-pacific-gyre/output
    152K	./Users/nelle/north-pacific-gyre
    4.0K	./Users/nelle/writing/thesis
    4.0K	./Users/nelle/writing/old
    28K	./Users/nelle/writing/data
    4.0K	./Users/nelle/writing/tools/old
    16K	./Users/nelle/writing/tools
    60K	./Users/nelle/writing
    1.1M	./Users/nelle
    4.0K	./Users/imhotep
    1.1M	./Users
    1.7M	.


<a id="orgdc0fdef"></a>

### Want less detail? add "&#x2013;max-depth" flag

    du -h --max-depth=1

    200K	./inflammation
    92K	./gapminder
    364K	./.git
    1.1M	./Users
    1.7M	.


<a id="org87308df"></a>

# Inspect Contents (cat, head, tail)


<a id="org5aaf74e"></a>

## The North Pacific Gyre data


<a id="org98550af"></a>

### cd into directory that has some of Nelle's data

    cd Users/nelle/north-pacific-gyre/2012-07-03

    ls -la

    total 144
    drwxrwxr-x 2 pauljohn pauljohn 4096 Nov 13 15:44 .
    drwxrwxr-x 4 pauljohn pauljohn 4096 Nov 13 15:44 ..
    -rw-rw-r-- 1 pauljohn pauljohn  184 Nov 13 10:49 goodiff
    -rw-rw-r-- 1 pauljohn pauljohn  198 Nov 13 10:49 goostats
    -r--r--r-- 1 pauljohn pauljohn 4406 Nov 13 10:49 NENE01729A.txt
    -r--r--r-- 1 pauljohn pauljohn   43 Nov 13 14:50 NENE01729B.txt
    -r--r--r-- 1 pauljohn pauljohn 4371 Nov 13 10:49 NENE01736A.txt
    -r--r--r-- 1 pauljohn pauljohn 4411 Nov 13 10:49 NENE01751A.txt
    -r--r--r-- 1 pauljohn pauljohn 4409 Nov 13 10:49 NENE01751B.txt
    -r--r--r-- 1 pauljohn pauljohn 4401 Nov 13 10:49 NENE01812A.txt
    -r--r--r-- 1 pauljohn pauljohn 4395 Nov 13 10:49 NENE01843A.txt
    -r--r--r-- 1 pauljohn pauljohn 4375 Nov 13 10:49 NENE01843B.txt
    -r--r--r-- 1 pauljohn pauljohn 4372 Nov 13 10:49 NENE01971Z.txt
    -r--r--r-- 1 pauljohn pauljohn 4381 Nov 13 10:49 NENE01978A.txt
    -r--r--r-- 1 pauljohn pauljohn 4389 Nov 13 10:49 NENE01978B.txt
    -r--r--r-- 1 pauljohn pauljohn 3517 Nov 13 10:49 NENE02018B.txt
    -r--r--r-- 1 pauljohn pauljohn 4391 Nov 13 10:49 NENE02040A.txt
    -r--r--r-- 1 pauljohn pauljohn 4367 Nov 13 10:49 NENE02040B.txt
    -r--r--r-- 1 pauljohn pauljohn 4381 Nov 13 10:49 NENE02040Z.txt
    -r--r--r-- 1 pauljohn pauljohn 4386 Nov 13 10:49 NENE02043A.txt
    -r--r--r-- 1 pauljohn pauljohn 4393 Nov 13 10:49 NENE02043B.txt


<a id="org8b8ca67"></a>

## cat: "concatenate" files and write on standard output

"cat goodiff" is manageable output

    cat goodiff

    # difference of two input files
    # demo version, just return a random number or "files are identical"
    if [ "$1" == "$2" ]
    then
        echo "files are identical"
    else
        echo 0.$RANDOM
    fi

This is a "shell script", a series of commands cobbled together.


<a id="org4fc374f"></a>

## head and tail: checking contents of big files


<a id="orgee0bc80"></a>

### head

If we simply run "cat NENE02040B.txt" to see what's in there,
everything will run by on  the screen very quickly. One way to deal
with that is to only look at the top part of the file

    head NENE02040B.txt

    0.616254506154
    0.283755587068
    0.156990583983
    0.404143324251
    1.40467049524
    0.563505688711
    4.04569329033
    1.58230309459
    0.438038008849
    1.24649230763

Head defaults to display 10 lines, but perhaps I only need to see the
first 5.

    head -n5 NENE02040B.txt

    0.616254506154
    0.283755587068
    0.156990583983
    0.404143324251
    1.40467049524

Here is an example of the long and short style of command line
argument. The short argument is "-n" with no equal sign, but the long
version is

    head --lines=5 NENE02040B.txt

    0.616254506154
    0.283755587068
    0.156990583983
    0.404143324251
    1.40467049524


<a id="org5a3917d"></a>

### tail: check the last (default: 10) lines

    tail NENE02040B.txt

    1.1069459452
    0.073897931368
    0.0755146936238
    0.609976382121
    0.106432564
    0.485084647673
    2.98671436729
    1.13033139062
    0.518031268789
    0.788386986395

    tail -n3 NENE02040B.txt

    1.13033139062
    0.518031268789
    0.788386986395


<a id="orgcb3089e"></a>

## more and less

So far as I can tell, more and less are equivalent!  *more* is an
older program over which one company asserted ownership, while *less*
is the free version created in response. Some systems have one, 
some systems have both. 
Need to scan entire file?

Running "cat" will spew out the results too fast.  Some terminals
are able to scroll back in history, but these are not always
available.


<a id="org78a80bf"></a>

### Run the more program to see "one screen at a time".

    more NENE02040B.txt

**Space bar** to see next screen

**q** to quit


<a id="orgf886297"></a>

# Executable Path

**Question**: Why didn't we have to type "/usr/bin/git"?


<a id="org34bf484"></a>

## Launch a program by name, including all directory structure

    $ /usr/bin/git

or 

    $ /usr/bin/du

We don't usually have to do that for the most frequently used
programs in the shell.  


<a id="orgbfb83ae"></a>

## Enter the **PATH**

**PATH** Special directories where the shell can look
for executable programs.

Here's my path

    echo $PATH

    /home/pauljohn/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/home/pauljohn/bin

On many computers, there will be 100s or 1000s of programs
available. Many are in the executable path. Perhaps not some
you might expect to be.

My path has the "bin" directory in my user account, plus lots
of others that come with the OS.


<a id="org2f50edc"></a>

### Note what Git Bash does

On Git Bash in Windows: the style of the path is different from what
you might see in Windows description of itself (to see what I mean,
run the program "cmd" and type "echo %PATH%".)


<a id="org57b7b18"></a>

## Text versus GUI programs

-   Text based terminal programs "stay in the terminal".

-   GUI programs can be "launched" onto desktop


<a id="orgdcbc290"></a>

### On a Linux/Unix system, simply typing a GUI program's name will

launch it on the screen.


<a id="org791170b"></a>

### On Macintosh:

The open function

    $ open file-name-or-URL

    $ open -a program-name file-name-or-URL

If you don't include "-a program-name" then Mac uses the
default program to open the file-name-or-URL

See: <http://brettterpstra.com/2014/08/06/shell-tricks-the-os-x-open-command/>


<a id="orgea32f2a"></a>

### Windows

Git Bash will launch Windows programs that are in the Windows System Path!

2 examples, with and without the special "start" program.

    $ notepad whatever1.txt

    $ start notepad whatever2.txt

Usually I'd just do this. I believe it is preferable to interact with
projects in this way.

    $ explorer .


<a id="org59183ee"></a>

## What about programs that are not on the PATH?

1.  We can type out their names in full, beginning with "/"

2.  We can use relative file paths (the "./" trick).

3.  We add them to the path (either temporarily IN the shell or

permanently in the OS setup).


<a id="org1cb4f5a"></a>

### We are swimming upstream, unfortunately

The trend in Windows and Macintosh has been to NOT put programs
in the PATH. Both of them have created an alternative model
where programs are installed and they notify the operating system
about themselves. These systems have a "desktop" metaphor
where users can 

1.  Launch from Menu

2.  Launch from "open with" feature in file manager


<a id="orgfa41add"></a>

## Need to add some directories to the PATH, probably&#x2026;

Terminal users find it inconvenient when important programs are not in
the path. For convenience, it is necessary to add program folders to
the system PATH.

In Windows, when we install **Git**, **Notepad++**, **Emacs**, **R**, and so
forth, we always say YES if the installer offers to put the programs
in the path, and if we are not asked, then we do it manually.


<a id="org0319813"></a>

# Programs talk to each other


<a id="org5e6aa6e"></a>

## The Pipe "|"

Many of the traditional Unix functions are build so that the output of
one function can "go into" another one. Sending "standard output" from
the first as "standard input" to the follower. Many, not all programs,
are designed this way.


<a id="orga0ba94a"></a>

## Programs I associate with back end of the pipe

-   **wc** counts lines or words
-   **sort** sorts output alphabetically
-   **uniq** keeps unique items (sort first)
-   **grep** filters (looks for text strings)

These is still quite frequently used by text analysts.


<a id="org68ac502"></a>

## Lets look at User nelle's files on molecules


    cd Users/nelle/molecules

    ls -la

    total 36
    drwxrwxr-x 2 pauljohn pauljohn 4096 Nov 14 13:17 .
    drwxrwxr-x 8 pauljohn pauljohn 4096 Nov 13 10:49 ..
    -rw-rw-r-- 1 pauljohn pauljohn 1158 Nov 13 10:49 cubane.pdb
    -rw-rw-r-- 1 pauljohn pauljohn  622 Nov 13 10:49 ethane.pdb
    -rw-rw-r-- 1 pauljohn pauljohn  422 Nov 13 10:49 methane.pdb
    -rw-rw-r-- 1 pauljohn pauljohn 1828 Nov 13 10:49 octane.pdb
    -rw-rw-r-- 1 pauljohn pauljohn 1226 Nov 13 10:49 pentane.pdb
    -rw-rw-r-- 1 pauljohn pauljohn  825 Nov 13 10:49 propane.pdb
    -rw-rw-r-- 1 pauljohn pauljohn  110 Nov 14 13:17 records.txt

These are small files, we might as well look at one:

    more cubane.pdb

    ::::::::::::::
    cubane.pdb
    ::::::::::::::
    COMPND      CUBANE
    AUTHOR      DAVE WOODCOCK  95 12 06
    ATOM      1  C           1       0.789  -0.852   0.504  1.00  0.00
    ATOM      2  C           1      -0.161  -1.104  -0.624  1.00  0.00
    ATOM      3  C           1      -1.262  -0.440   0.160  1.00  0.00
    ATOM      4  C           1      -0.289  -0.202   1.284  1.00  0.00
    ATOM      5  C           1       1.203   0.513  -0.094  1.00  0.00
    ATOM      6  C           1       0.099   1.184   0.694  1.00  0.00
    ATOM      7  C           1      -0.885   0.959  -0.460  1.00  0.00
    ATOM      8  C           1       0.236   0.283  -1.269  1.00  0.00
    ATOM      9  H           1       1.410  -1.631   0.942  1.00  0.00
    ATOM     10  H           1      -0.262  -2.112  -1.024  1.00  0.00
    ATOM     11  H           1      -2.224  -0.925   0.328  1.00  0.00
    ATOM     12  H           1      -0.468  -0.501   2.315  1.00  0.00
    ATOM     13  H           1       2.224   0.892  -0.134  1.00  0.00
    ATOM     14  H           1       0.240   2.112   1.251  1.00  0.00
    ATOM     15  H           1      -1.565   1.730  -0.831  1.00  0.00
    ATOM     16  H           1       0.472   0.494  -2.315  1.00  0.00
    TER      17              1
    END

How many lines are there in the file cubane.pdb?

    wc -l cubane.pdb

    20 cubane.pdb

If the file were bigger, we might just scan the top or the bottom 5
lines (using head and tail)

    head -5 cubane.pdb

    COMPND      CUBANE
    AUTHOR      DAVE WOODCOCK  95 12 06
    ATOM      1  C           1       0.789  -0.852   0.504  1.00  0.00
    ATOM      2  C           1      -0.161  -1.104  -0.624  1.00  0.00
    ATOM      3  C           1      -1.262  -0.440   0.160  1.00  0.00

    tail -5 cubane.pdb

    ATOM     14  H           1       0.240   2.112   1.251  1.00  0.00
    ATOM     15  H           1      -1.565   1.730  -0.831  1.00  0.00
    ATOM     16  H           1       0.472   0.494  -2.315  1.00  0.00
    TER      17              1
    END


<a id="orgfce906f"></a>

## The wc program

How many lines are there in the pdb files?

    wc *.pdb

     20  156 1158 cubane.pdb
     12   84  622 ethane.pdb
      9   57  422 methane.pdb
     30  246 1828 octane.pdb
     21  165 1226 pentane.pdb
     15  111  825 propane.pdb
    107  819 6081 total

3 results: 

-new lines

-words

-bytecount

Usually I just want the number of rows, can add "-l" flag.

    wc -l *.pdb

     20 cubane.pdb
     12 ethane.pdb
      9 methane.pdb
     30 octane.pdb
     21 pentane.pdb
     15 propane.pdb
    107 total

The results are out of order, pipe them to the sort function:

    wc -l *.pdb | sort

    107 total
     12 ethane.pdb
     15 propane.pdb
     20 cubane.pdb
     21 pentane.pdb
     30 octane.pdb
      9 methane.pdb

The results are still out of order, need to think harder (read help
page). sort defaults to an alphabetical search, need to do numerical
sort:

    wc -l *.pdb | sort -n

      9 methane.pdb
     12 ethane.pdb
     15 propane.pdb
     20 cubane.pdb
     21 pentane.pdb
     30 octane.pdb
    107 total


<a id="orgfdb1c0d"></a>

## ">" and ">>" for redirecting output

The results (so far) have been printed into the screen. We
may need a record, so we write them in a file.

**>**  will ERASE a pre-existing file's content

**>>** will add output to a pre-existing files, or create a new file.

Try that with the sorted line list:

    wc -l *.pdb | sort -n > records.txt

    cat records.txt

      9 methane.pdb
     12 ethane.pdb
     15 propane.pdb
     20 cubane.pdb
     21 pentane.pdb
     30 octane.pdb
    107 total


<a id="org1cc6ee5"></a>

## Pipe to more or less, for example

Any time output goes by too fast, put "| more" on the end.

I do that so often I never run more or less as the primary command

I often find myself tacking on the end of the command line with either

-   "cat file1 file2 | more"

-   "cat file1 file2 | less"


<a id="org0e23201"></a>

# grep is for Filtering

**grep** = **GNU regular expression parser**

It can be used in 2 ways

1.  A command you run in the command line

List all lines that match a target string

I use that to find out "in which file is there a certain word?"

Check the AUTHOR line in each pdb file:

    grep AUTHOR *.pdb

    cubane.pdb:AUTHOR      DAVE WOODCOCK  95 12 06
    ethane.pdb:AUTHOR      DAVE WOODCOCK  95 12 18
    methane.pdb:AUTHOR      DAVE WOODCOCK  95 12 18
    octane.pdb:AUTHOR      DAVE WOODCOCK  96 01 05
    pentane.pdb:AUTHOR      DAVE WOODCOCK  95 12 18
    propane.pdb:AUTHOR      DAVE WOODCOCK  95  12 18

1.  Suppose we run some command that causes 100s and 100s of lines to
    spill out into the terminal.  I want to keep only the one that have
    the part I want.

A contrived example, running "cat \*.pdb" will spill all of the files.

Pipe that to grep to just keep the ones that have "COMPND"

    cat *.pdb | grep COMPND

    COMPND      CUBANE
    COMPND      ETHANE
    COMPND      METHANE
    COMPND      OCTANE
    COMPND      PENTANE
    COMPND      PROPANE


<a id="org6f7e87b"></a>

### What is "regular expression"

It is a fancy language text sub-string matching. Regular expression
syntax is used a great deal in more advanced shell and programming
exercises.  Regular expressions give a comprehensive scheme to isolate
parts of a string, to pick and choose among sub-pieces.

I don't want to teach that now, but can give the big picture.

**regular expression cheat sheet**

-   ^ beginning of a string
-   $ end of a string
-   . any character
-   \* quantifier meaning "any number of times", so ".\*" matches whole string

Suppose we want to keep only the words out of the molecule files if
they begin with "ATOM".  Here is the reqular expression recipe I would
use with grep:

    grep "^ATOM" *.pdb

If I run that, it will fill up my terminal with output, so I'll
pipe the result to tail so we see just the last 10 lines:

    grep "^ATOM.*" *.pdb | tail

    propane.pdb:ATOM      2  C           1      -0.011  -0.441   0.333  1.00  0.00
    propane.pdb:ATOM      3  C           1      -1.176   0.296  -0.332  1.00  0.00
    propane.pdb:ATOM      4  H           1       1.516   0.699  -0.675  1.00  0.00
    propane.pdb:ATOM      5  H           1       2.058  -0.099   0.827  1.00  0.00
    propane.pdb:ATOM      6  H           1       1.035   1.354   0.913  1.00  0.00
    propane.pdb:ATOM      7  H           1      -0.283  -0.691   1.359  1.00  0.00
    propane.pdb:ATOM      8  H           1       0.204  -1.354  -0.225  1.00  0.00
    propane.pdb:ATOM      9  H           1      -0.914   0.551  -1.359  1.00  0.00
    propane.pdb:ATOM     10  H           1      -1.396   1.211   0.219  1.00  0.00
    propane.pdb:ATOM     11  H           1      -2.058  -0.345  -0.332  1.00  0.00

grep has many arguments, we might not want the file name with each
one, for example

    grep -h  "^ATOM.*" *.pdb | tail

    ATOM      2  C           1      -0.011  -0.441   0.333  1.00  0.00
    ATOM      3  C           1      -1.176   0.296  -0.332  1.00  0.00
    ATOM      4  H           1       1.516   0.699  -0.675  1.00  0.00
    ATOM      5  H           1       2.058  -0.099   0.827  1.00  0.00
    ATOM      6  H           1       1.035   1.354   0.913  1.00  0.00
    ATOM      7  H           1      -0.283  -0.691   1.359  1.00  0.00
    ATOM      8  H           1       0.204  -1.354  -0.225  1.00  0.00
    ATOM      9  H           1      -0.914   0.551  -1.359  1.00  0.00
    ATOM     10  H           1      -1.396   1.211   0.219  1.00  0.00
    ATOM     11  H           1      -2.058  -0.345  -0.332  1.00  0.00

In the Unix system, there are many programs designed for the further
manipulation of these outputs. In case you ever wander into a help
page that suggest you use programs like "tr", "sed", "perl" or such,
you will know (vaguely) what they are talking about.


<a id="org4289b06"></a>

### Get out of jail free card for grep users

In some chores, the power to designate "at the beginning of a string"
is not needed.  

The flag "-F" allows us to use grep as a text scanner, without worring
about regular expressions.

The word ATOM is used, no matter where it is in the line.

    grep "^ATOM.*" *.pdb

    cubane.pdb:ATOM      1  C           1       0.789  -0.852   0.504  1.00  0.00
    cubane.pdb:ATOM      2  C           1      -0.161  -1.104  -0.624  1.00  0.00
    cubane.pdb:ATOM      3  C           1      -1.262  -0.440   0.160  1.00  0.00
    cubane.pdb:ATOM      4  C           1      -0.289  -0.202   1.284  1.00  0.00
    cubane.pdb:ATOM      5  C           1       1.203   0.513  -0.094  1.00  0.00
    cubane.pdb:ATOM      6  C           1       0.099   1.184   0.694  1.00  0.00
    cubane.pdb:ATOM      7  C           1      -0.885   0.959  -0.460  1.00  0.00
    cubane.pdb:ATOM      8  C           1       0.236   0.283  -1.269  1.00  0.00
    cubane.pdb:ATOM      9  H           1       1.410  -1.631   0.942  1.00  0.00
    cubane.pdb:ATOM     10  H           1      -0.262  -2.112  -1.024  1.00  0.00
    cubane.pdb:ATOM     11  H           1      -2.224  -0.925   0.328  1.00  0.00
    cubane.pdb:ATOM     12  H           1      -0.468  -0.501   2.315  1.00  0.00
    cubane.pdb:ATOM     13  H           1       2.224   0.892  -0.134  1.00  0.00
    cubane.pdb:ATOM     14  H           1       0.240   2.112   1.251  1.00  0.00
    cubane.pdb:ATOM     15  H           1      -1.565   1.730  -0.831  1.00  0.00
    cubane.pdb:ATOM     16  H           1       0.472   0.494  -2.315  1.00  0.00
    ethane.pdb:ATOM      1  C           1      -0.752   0.001  -0.141  1.00  0.00
    ethane.pdb:ATOM      2  C           1       0.752  -0.001   0.141  1.00  0.00
    ethane.pdb:ATOM      3  H           1      -1.158   0.991   0.070  1.00  0.00
    ethane.pdb:ATOM      4  H           1      -1.240  -0.737   0.496  1.00  0.00
    ethane.pdb:ATOM      5  H           1      -0.924  -0.249  -1.188  1.00  0.00
    ethane.pdb:ATOM      6  H           1       1.158  -0.991  -0.070  1.00  0.00
    ethane.pdb:ATOM      7  H           1       0.924   0.249   1.188  1.00  0.00
    ethane.pdb:ATOM      8  H           1       1.240   0.737  -0.496  1.00  0.00
    methane.pdb:ATOM      1  C           1       0.257  -0.363   0.000  1.00  0.00
    methane.pdb:ATOM      2  H           1       0.257   0.727   0.000  1.00  0.00
    methane.pdb:ATOM      3  H           1       0.771  -0.727   0.890  1.00  0.00
    methane.pdb:ATOM      4  H           1       0.771  -0.727  -0.890  1.00  0.00
    methane.pdb:ATOM      5  H           1      -0.771  -0.727   0.000  1.00  0.00
    octane.pdb:ATOM      1  C           1      -4.397   0.370  -0.255  1.00  0.00
    octane.pdb:ATOM      2  C           1      -3.113  -0.447  -0.421  1.00  0.00
    octane.pdb:ATOM      3  C           1      -1.896   0.386  -0.007  1.00  0.00
    octane.pdb:ATOM      4  C           1      -0.611  -0.426  -0.198  1.00  0.00
    octane.pdb:ATOM      5  C           1       0.608   0.405   0.216  1.00  0.00
    octane.pdb:ATOM      6  C           1       1.892  -0.400   0.001  1.00  0.00
    octane.pdb:ATOM      7  C           1       3.113   0.429   0.414  1.00  0.00
    octane.pdb:ATOM      8  C           1       4.397  -0.374   0.199  1.00  0.00
    octane.pdb:ATOM      9  H           1      -4.502   0.681   0.785  1.00  0.00
    octane.pdb:ATOM     10  H           1      -5.254  -0.243  -0.537  1.00  0.00
    octane.pdb:ATOM     11  H           1      -4.357   1.252  -0.895  1.00  0.00
    octane.pdb:ATOM     12  H           1      -3.009  -0.741  -1.467  1.00  0.00
    octane.pdb:ATOM     13  H           1      -3.172  -1.337   0.206  1.00  0.00
    octane.pdb:ATOM     14  H           1      -1.992   0.668   1.044  1.00  0.00
    octane.pdb:ATOM     15  H           1      -1.849   1.286  -0.621  1.00  0.00
    octane.pdb:ATOM     16  H           1      -0.515  -0.707  -1.248  1.00  0.00
    octane.pdb:ATOM     17  H           1      -0.659  -1.326   0.417  1.00  0.00
    octane.pdb:ATOM     18  H           1       0.520   0.671   1.270  1.00  0.00
    octane.pdb:ATOM     19  H           1       0.645   1.314  -0.386  1.00  0.00
    octane.pdb:ATOM     20  H           1       1.979  -0.666  -1.054  1.00  0.00
    octane.pdb:ATOM     21  H           1       1.855  -1.309   0.604  1.00  0.00
    octane.pdb:ATOM     22  H           1       3.030   0.696   1.467  1.00  0.00
    octane.pdb:ATOM     23  H           1       3.155   1.337  -0.188  1.00  0.00
    octane.pdb:ATOM     24  H           1       4.493  -0.641  -0.854  1.00  0.00
    octane.pdb:ATOM     25  H           1       4.368  -1.282   0.801  1.00  0.00
    octane.pdb:ATOM     26  H           1       5.254   0.230   0.498  1.00  0.00
    pentane.pdb:ATOM      1  C           1       2.484  -0.389   0.322  1.00  0.00
    pentane.pdb:ATOM      2  C           1       1.261   0.350  -0.243  1.00  0.00
    pentane.pdb:ATOM      3  C           1      -0.027  -0.348   0.199  1.00  0.00
    pentane.pdb:ATOM      4  C           1      -1.249   0.421  -0.326  1.00  0.00
    pentane.pdb:ATOM      5  C           1      -2.536  -0.311   0.047  1.00  0.00
    pentane.pdb:ATOM      6  H           1       2.471  -1.420  -0.033  1.00  0.00
    pentane.pdb:ATOM      7  H           1       2.443  -0.371   1.412  1.00  0.00
    pentane.pdb:ATOM      8  H           1       3.393   0.112  -0.016  1.00  0.00
    pentane.pdb:ATOM      9  H           1       1.324   0.350  -1.332  1.00  0.00
    pentane.pdb:ATOM     10  H           1       1.271   1.378   0.122  1.00  0.00
    pentane.pdb:ATOM     11  H           1      -0.074  -0.384   1.288  1.00  0.00
    pentane.pdb:ATOM     12  H           1      -0.048  -1.362  -0.205  1.00  0.00
    pentane.pdb:ATOM     13  H           1      -1.183   0.500  -1.412  1.00  0.00
    pentane.pdb:ATOM     14  H           1      -1.259   1.420   0.112  1.00  0.00
    pentane.pdb:ATOM     15  H           1      -2.608  -0.407   1.130  1.00  0.00
    pentane.pdb:ATOM     16  H           1      -2.540  -1.303  -0.404  1.00  0.00
    pentane.pdb:ATOM     17  H           1      -3.393   0.254  -0.321  1.00  0.00
    propane.pdb:ATOM      1  C           1       1.241   0.444   0.349  1.00  0.00
    propane.pdb:ATOM      2  C           1      -0.011  -0.441   0.333  1.00  0.00
    propane.pdb:ATOM      3  C           1      -1.176   0.296  -0.332  1.00  0.00
    propane.pdb:ATOM      4  H           1       1.516   0.699  -0.675  1.00  0.00
    propane.pdb:ATOM      5  H           1       2.058  -0.099   0.827  1.00  0.00
    propane.pdb:ATOM      6  H           1       1.035   1.354   0.913  1.00  0.00
    propane.pdb:ATOM      7  H           1      -0.283  -0.691   1.359  1.00  0.00
    propane.pdb:ATOM      8  H           1       0.204  -1.354  -0.225  1.00  0.00
    propane.pdb:ATOM      9  H           1      -0.914   0.551  -1.359  1.00  0.00
    propane.pdb:ATOM     10  H           1      -1.396   1.211   0.219  1.00  0.00
    propane.pdb:ATOM     11  H           1      -2.058  -0.345  -0.332  1.00  0.00

1.  Pipe to grep

A command that causes profuse output&#x2013;say a huge list of
files&#x2013;can be filtered by piping the output to grep.

Suppose we start back at the top level of the ou<sub>swc</sub><sub>files</sub> directory

    ls */*/*

    gapminder/data/gapminder_all.csv
    gapminder/data/gapminder_gdp_africa.csv
    gapminder/data/gapminder_gdp_americas.csv
    gapminder/data/gapminder_gdp_asia.csv
    gapminder/data/gapminder_gdp_europe.csv
    gapminder/data/gapminder_gdp_oceania.csv
    inflammation/data/inflammation-01.csv
    inflammation/data/inflammation-02.csv
    inflammation/data/inflammation-03.csv
    inflammation/data/inflammation-04.csv
    inflammation/data/inflammation-05.csv
    inflammation/data/inflammation-06.csv
    inflammation/data/inflammation-07.csv
    inflammation/data/inflammation-08.csv
    inflammation/data/inflammation-09.csv
    inflammation/data/inflammation-10.csv
    inflammation/data/inflammation-11.csv
    inflammation/data/inflammation-12.csv
    inflammation/data/small-01.csv
    inflammation/data/small-02.csv
    inflammation/data/small-03.csv
    inflammation/python/argv-list.py
    inflammation/python/arith.py
    inflammation/python/check.py
    inflammation/python/count-stdin.py
    inflammation/python/errors_01.py
    inflammation/python/errors_02.py
    inflammation/python/gen-inflammation.py
    inflammation/python/line-count.py
    inflammation/python/my_ls.py
    inflammation/python/readings-01.py
    inflammation/python/readings-02.py
    inflammation/python/readings-03.py
    inflammation/python/readings-04.py
    inflammation/python/readings-05.py
    inflammation/python/readings-06.py
    inflammation/python/readings-07.py
    inflammation/python/readings-08.py
    inflammation/python/readings-09.py
    inflammation/python/rectangle.py
    inflammation/python/sys-version.py
    Users/nelle/notes.txt
    Users/nelle/pizza.cfg
    Users/nelle/solar.pdf
    
    Users/nelle/creatures:
    basilisk.dat
    unicorn.dat
    
    Users/nelle/data:
    amino-acids.txt
    animals.txt
    elements
    morse.txt
    pdb
    planets.txt
    salmon.txt
    sunspot.txt
    
    Users/nelle/Desktop:
    
    Users/nelle/molecules:
    cubane.pdb
    ethane.pdb
    methane.pdb
    octane.pdb
    pentane.pdb
    propane.pdb
    records.txt
    
    Users/nelle/north-pacific-gyre:
    2012-07-03
    output
    
    Users/nelle/writing:
    data
    haiku.txt
    old
    thesis
    tools

We don't want to see all of those files

Perhaps I only want to see the ones that have "txt" in their names:

    ls */*/* | grep txt

    Users/nelle/notes.txt
    amino-acids.txt
    animals.txt
    morse.txt
    planets.txt
    salmon.txt
    sunspot.txt
    records.txt
    haiku.txt

    ls */*/* | grep txt

    Users/nelle/notes.txt
    amino-acids.txt
    animals.txt
    morse.txt
    planets.txt
    salmon.txt
    sunspot.txt
    records.txt
    haiku.txt


<a id="orgc54f5e7"></a>

## Use these skills to check the North Pacific Gyre data

If you are still in the molecules data, this should work to
change the working directory to north-pacific-gyre/2012-07-03

    cd ../north-pacific-gyre/2012-07-03
    ## File check
    ls

    goodiff
    goostats
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

If you are at the top level of the Git clone, do this instead:

    cd Users/nelle/north-pacific-gyre/2012-07-03

1.  Use wc to check number of lines within each file:

    wc -l NENE*.txt

     300 NENE01729A.txt
       3 NENE01729B.txt
     300 NENE01736A.txt
     300 NENE01751A.txt
     300 NENE01751B.txt
     300 NENE01812A.txt
     300 NENE01843A.txt
     300 NENE01843B.txt
     300 NENE01971Z.txt
     300 NENE01978A.txt
     300 NENE01978B.txt
     240 NENE02018B.txt
     300 NENE02040A.txt
     300 NENE02040B.txt
     300 NENE02040Z.txt
     300 NENE02043A.txt
     300 NENE02043B.txt
    4743 total

Notes about problem files

-   NENE01729B.txt has only 3 lines. We better double-check the data
    source
-   Somebody in the project told me the ones that end in "Z" are
    probably wrong.  NENE02040Z.txt

It is easy to select all the ones that end with A or B. The shell
Wildcard globbing allows hard brackets like this [AB] to mean either
"A" or "B"

    ls *[AB].txt

    NENE01729A.txt
    NENE01729B.txt
    NENE01736A.txt
    NENE01751A.txt
    NENE01751B.txt
    NENE01812A.txt
    NENE01843A.txt
    NENE01843B.txt
    NENE01978A.txt
    NENE01978B.txt
    NENE02018B.txt
    NENE02040A.txt
    NENE02040B.txt
    NENE02043A.txt
    NENE02043B.txt

