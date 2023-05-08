# Lab Report 3: Researching Commands
## __Command-Line Options and Other Ways to Use 'find' Command__
*Evelyn Quan, CSE15L Section A05*

<br/>

For this report, I have chosen to further research the command-line options and other ways to use <mark>find</mark>. 

### 1) find -mtime *n*

*-mtime* gives you the files that were last modified based on the *n* value given. *n* is a numeric argument which is specified as such:

- *+n* is for all numeric values greater than *n*
- *-n* is for all values less than *n*
- *n* is for simply the value *n*.

However, something important to note is that the file modification time is truncated. For instance, if a file was last modified 23 hours, 59 minutes, amd 59 seconds ago, using -mtime would still count the file as being 0 days old. Therefore, somewhat not as intuitively, these rules can help better to determine what time span you want to search for files in, with *a* standing for the time the file was last modified:

- `find -mtime n` would give *n ≤ a < n + 1* as the time span for the modification of the file. 
- `find -mtime -n` gives *a < n*. 
- `find -mtime +n` gives *n + 1 ≤ a*. 

For example, writing the full command `find . -mtime +1` would find all the files whose data modification time was more than 1 + 1 = 2 days ago. `find . -mtime -1` will find files with the data modification time less than 1 day ago, and `find . -mtime 1` finds the files that were modified at least 1 day ago and at most 1 + 1 = 2 days. 

<br/> 

#### Example 1

```
$ find -mtime -0.001
```

Gave me the following result: 

```
./technical/911report/chapter-1.txt
```

<br/>

I had modified only <mark>chapter-1.txt</mark> right before running this command, and I find that the output gives me back only the path to this file. The *n* of -0.001 means that all the files that were last modified less than 0.001 * 24 = 0.024 hours, or 0.024 * 60 = 1.44 minutes ago. Because I did not modify any of the files less than 1.44 minutes ago besides <mark>chapter-1.txt</mark> in <mark>./technical</mark>, it is expected that this file is the only one that was given in the output.

This is useful, because it allows us to track which files we have edited recently, so we can make sure we are tracking and working in the right file if we want to check where our work was done later on.

<br/>

#### Example 2

```
$ find ./technical/911report -mtime 0.005
```

Result:

```
./technical/911report
./technical/911report/chapter-1.txt
./technical/911report/chapter-10.txt
./technical/911report/chapter-11.txt
./technical/911report/chapter-12.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-5.txt
./technical/911report/chapter-6.txt
./technical/911report/chapter-7.txt
./technical/911report/chapter-8.txt
./technical/911report/chapter-9.txt
./technical/911report/preface.txt
```

<br/>

The *n* of 0.005 in this command checks for all the files in <mark>./technical/911report</mark> that were modified at least 0.005 * 24 * 60 = 7.2 minutes ago, but less than 1.005 * 24.12 hours ago. Since I cloned the respository for this lab on the day that I ran this command, I would expect to see all the files in <mark>./technical/911report</mark> show up in the output of this command. This is useful, because this allows us to check certain time frames that we may have modified files in a particular directory, so we can keep track of which file our work was done in.

I found out about this mode/test for <mark>find</mark> through the [Linux man find page](https://linux.die.net/man/1/find), and I also received further guidance with understanding its conceptual reasoning through this [StackExchange](https://unix.stackexchange.com/questions/92346/why-does-find-mtime-1-only-return-files-older-than-2-days) page.

(Here are the links written out since you can't see them when I save this report as a PDF:
https://linux.die.net/man/1/find,
https://unix.stackexchange.com/questions/92346/why-does-find-mtime-1-only-return-files-older-than-2-days)

<br/>

### 2) find -size *n*\[cwbkMG]

*-size* gives all the files that fall under the numerical value of *n*(which similarly follows the same rules as it does for *-mtime* with + and - signs), and the unit of one of the following:

- c (bytes)
- w (two-byte words)
- b (512-byte blocks)
- k (Kilobytes, which are units of 1024 bytes)
- M (Megabytes, which are units of 1038576 bytes)
- G (Gigabytes, which are units of 1073741824 bytes)

For instance, `find . -size 1000M` would find all the files in the directory that have a size less than 1000 Megabytes.

<br/> 

#### Example 1

```
$ find ./technical/plos/* -size -2k
```

Result:

```
./technical/plos/pmed.0020191.txt
./technical/plos/pmed.0020226.txt
```

<br/>

In this example, I found all the files in the <mark>plos</mark> folder inside <mark>./technical</mark> that had a size less than 2 Kilobytes, which were only 2 files, pmed.0020191.txt and pmed.0020226.txt. This mode/test for <mark>find</mark> is useful, because it allows us to find files that may fit a certain threshold of being uploaded to a site. For example, if a site has a maximum of 2 Kilobyte files that it will allow you to upload, then you know which files in your directory are small enough to fit the criterion.

<br/>

#### Example 2

```
$ find ./technical/plos/* -size +2k -size -4k
```

Result:

```
./technical/plos/pmed.0010025.txt
./technical/plos/pmed.0010029.txt
./technical/plos/pmed.0010067.txt
./technical/plos/pmed.0010068.txt
./technical/plos/pmed.0020021.txt
./technical/plos/pmed.0020022.txt
./technical/plos/pmed.0020024.txt
./technical/plos/pmed.0020027.txt
./technical/plos/pmed.0020085.txt
./technical/plos/pmed.0020086.txt
./technical/plos/pmed.0020145.txt
./technical/plos/pmed.0020278.txt
./technical/plos/pmed.0020281.txt
```

<br/>

For Example 2 of this mode/test, I found all the files under the directory with path <mark>./technical/plos/*</mark> which had a size greater than 2 Kilobytes but less than 4 Kilobytes, which subsequently printed out the files that matched these criteria. This example illustrates that this mode/test of <mark>find</mark> is useful for finding files within a certain size range, so that for instance, you can try to maximize the amount of data you can upload with greater file sizes but also fits within the size range that an application or size allows you to upload in.

I found out about this mode/test for <mark>find</mark> through the [Linux man find page](https://linux.die.net/man/1/find). (Link: https://linux.die.net/man/1/find)

<br/>

### 3) find -maxdepth *levels*

*-maxdepth* will search for all files that are at most *levels* below the directory command line argument given, or the current directory if no argument is given. *levels* should be a non-negative integer. For instance, `find . -maxdepth 7 -name "*.txt"` would search for all files at most 7 levels of directories below the home directory that have the extension .txt.

<br/> 

#### Example 1

```
$ find -maxdepth 3 -name "a*.txt"
```

Result:

```
./technical/biomed/ar104.txt
./technical/biomed/ar118.txt
./technical/biomed/ar120.txt
./technical/biomed/ar130.txt
./technical/biomed/ar140.txt
./technical/biomed/ar149.txt
./technical/biomed/ar297.txt
./technical/biomed/ar309.txt
./technical/biomed/ar319.txt
./technical/biomed/ar321.txt
./technical/biomed/ar328.txt
./technical/biomed/ar331.txt
./technical/biomed/ar383.txt
./technical/biomed/ar387.txt
./technical/biomed/ar407.txt
./technical/biomed/ar408.txt
./technical/biomed/ar409.txt
./technical/biomed/ar422.txt
./technical/biomed/ar429.txt
./technical/biomed/ar430.txt
./technical/biomed/ar601.txt
./technical/biomed/ar612.txt
./technical/biomed/ar615.txt
./technical/biomed/ar619.txt
./technical/biomed/ar624.txt
./technical/biomed/ar68.txt
./technical/biomed/ar745.txt
./technical/biomed/ar750.txt
./technical/biomed/ar774.txt
./technical/biomed/ar778.txt
./technical/biomed/ar79.txt
./technical/biomed/ar792.txt
./technical/biomed/ar795.txt
./technical/biomed/ar799.txt
./technical/biomed/ar93.txt
```

<br/>

In this example, I tried to find all files that were at most 3 levels of directories below my current directory that had a name starting with "a" and also had the extension .txt. This found many of the files in the <mark>biomed</mark> folder in <mark>./technical</mark> which fit these criteria. We see that the files under <mark>./technical/government/*</mark> that started with "a" were not included in the output, because this would have required a maxdepth of at least 4, since there are more folders that are inside the <mark>government</mark> folder.

This is useful to note, because we are able to specify which files we want to find and how deep within our directory we want to go to find these files.

<br/>

#### Example 2

```
$ find -maxdepth 4 -name "r*.txt"
```

Result:

```
./technical/biomed/rr166.txt
./technical/biomed/rr167.txt
./technical/biomed/rr171.txt
./technical/biomed/rr172.txt
./technical/biomed/rr191.txt
./technical/biomed/rr196.txt
./technical/biomed/rr37.txt
./technical/biomed/rr73.txt
./technical/biomed/rr74.txt
./technical/government/About_LSC/reporting_system.txt
./technical/government/Env_Prot_Agen/ro_clear_skies_book.txt
./technical/government/Media/residents_sue_city.txt
```

<br/>

For Example 2, I found all files at most 4 levels of directories below my current directory which were of the .txt extension and started with "r". Because we went 4 levels this time instead of 3 below the current directory, we were able to access files within the folders inside <mark>government</mark> as well this time, as seen in our output. Therefore, this example shows that this option for <mark>find</mark> is very useful for getting specific with what levels of directories below the one we give we want to look for files in, which can better help us navigate through our directories to find the data we may want.

I found out about this option for <mark>find</mark> through the [Linux man find page](https://linux.die.net/man/1/find), and also used this [Opensource article](https://opensource.com/article/21/9/linux-find-command) to better understand how the option worked through looking at an example.

(Links:
https://linux.die.net/man/1/find,
https://opensource.com/article/21/9/linux-find-command)

<br/>

### 4) find -path *pattern*

*-path* finds all the files/directories that match the *pattern* given, in the current directory by default or by the directory given as a command line argument. For instance, `find -path "./sr*sc"` may give an output for a directory called "./src/misc".

Note: One useful action to add onto using *-path* is *-prune*, which is if the path given is a directory, to not descend into it.

<br/> 

#### Example 1

```
$ find . -path "./technical/911report/chapter-*.txt"
```

Result:

```
./technical/911report/chapter-1.txt
./technical/911report/chapter-10.txt
./technical/911report/chapter-11.txt
./technical/911report/chapter-12.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-2.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-5.txt
./technical/911report/chapter-6.txt
./technical/911report/chapter-7.txt
./technical/911report/chapter-8.txt
./technical/911report/chapter-9.txt
```

<br/>

I tried to find in my current directory all the files that matched the path I provided of being in the directory <mark>./technical/911report/</mark> with the extension .txt and starting with "chapter-". All the files in the output match this path. *-path* is useful to use, because as seen in this example, you can find all the files or directories that match a particular path which can help you more easily locate files and navigate through your data.

<br/>

#### Example 2

```
$ find . -path "./technical/*" -prune
```

Result:

```
./technical/911report
./technical/biomed
./technical/government
./technical/plos
```

<br/>

In this example, not only did I use *-path* but I also added *-prune* as previously mentioned. I tried to find all the directories in my current directory which matched the path of <mark>./technical/*</mark>, and by using *-prune*, I made sure to not descend into the directory of the path. Therefore, in my output, I find only the paths of the directories 1 level down from <mark>./technical</mark> instead of having an output of all the .txt files in each of these directories as well.

This is useful, because it allows us to simplify our output to be as specific as we can, so we are able to find paths to particular directories more easily.

I learned about this mode/test for <mark>find</mark> through the [Linux man find page](https://linux.die.net/man/1/find).

(Link: https://linux.die.net/man/1/find)

<br/>

https://stackoverflow.com/questions/3165883/checking-file-size

https://unix.stackexchange.com/questions/92346/why-does-find-mtime-1-only-return-files-older-than-2-days
