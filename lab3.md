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

For example, writing the full command `find -mtime +1` would find all the files whose data modification time was more than 1 + 1 = 2 days ago. `find -mtime -1` will find files with the data modification time less than 1 day ago, and `find -mtime 1` finds the files that were modified at least 1 day ago and at most 1 + 1 = 2 days. 

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

I found out about this mode/test for <mark>find</mark> through the [Linux man find page](https://linux.die.net/man/1/find).

<br/>

### 3) find -maxdepth *levels*

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

We see that the files under `./technical/government/*` that started with "a" were not included in the output, because this would have required a maxdepth of at least 4.

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

I found out about this option for <mark>find</mark> through the [Linux man find page](https://linux.die.net/man/1/find), and also used this [Opensource article](https://opensource.com/article/21/9/linux-find-command) to better understand how the option worked through looking at an example.

<br/>

### 4) find -path *pattern*

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

I learned about this mode/test for <mark>find</mark> through the [Linux man find page](https://linux.die.net/man/1/find).

<br/>

https://stackoverflow.com/questions/3165883/checking-file-size

https://unix.stackexchange.com/questions/92346/why-does-find-mtime-1-only-return-files-older-than-2-days
