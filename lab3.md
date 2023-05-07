# Lab Report 3: Researching Commands
## __Command-Line Options and Other Ways to Use 'find' Command__
*Evelyn Quan, CSE15L Section A05*

<br/>

For this report, I have chosen to further research the command-line options and other ways to use <mark>find</mark>. 

### 1) find -mtime *n*

#### Example 1

```
$ find -mtime -0.001
```

gave me the following result: 

```
./technical/911report/chapter-1.txt
```

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

I found out about this mode/test for <mark>find</mark> through the [Linux man find page](https://linux.die.net/man/1/find), and I also received further guidance with understanding its conceptual reasoning through this [StackExchange](https://unix.stackexchange.com/questions/92346/why-does-find-mtime-1-only-return-files-older-than-2-days) page.

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

I learned about this mode/test for <mark>find</mark> through the [Linux man find page](https://linux.die.net/man/1/find).

<br/>

*Note: The source I used to find the above information can be found [here](https://linux.die.net/man/1/find). This is the find Linux man page.*

*I also used [this source](https://opensource.com/article/21/9/linux-find-command) for further guidance on how to type out certain commands with their options, such as maxdepth.*

https://stackoverflow.com/questions/3165883/checking-file-size

https://unix.stackexchange.com/questions/92346/why-does-find-mtime-1-only-return-files-older-than-2-days
