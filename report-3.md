## Week 5 Lab Report 3
by Jaewon Han 

This post is a report about the different ways to use researching commands

### Researching Commands
There are different commands that we can use for researching: `less`,`find`,`grep`, and others.
In this post, we'll focus on a `find` command. 

### Command - `find` 
The `find` searches for files in a directory hierarchy.

[https://man7.org/linux/man-pages/man1/grep.1.html](https://man7.org/linux/man-pages/man1/grep.1.html)

According to the link above, there are different command-line options to use the command `find`.
We'll look two examples each for four different command-line options of the command `find`. In this report, we'll use `ieng6` server to demonstrate how the command-line options can be used. 

#### 1st Option: `-name` 
Command-line option called `-name` can be used when we know the name of a file, but we don't know the specific place(directory). 
For 1st example here, we refers to [https://man7.org/linux/man-pages/man1/grep.1.html](https://man7.org/linux/man-pages/man1/grep.1.html).
For 2nd example here, we refers to [https://www.geeksforgeeks.org/find-command-in-linux-with-examples](https://www.geeksforgeeks.org/find-command-in-linux-with-examples)

```
$ find ./written_2 -name "ch1.txt"
```
This command-line allows us to find to search files called "ch1.txt" from the `./written_2`. 
It is useful when we want to know the exact location of the files. 
The below is the output of the command above.
![](/images/1_name_1.png)

```
$ find ./written_2 -name *ch1*.txt
```
This command-line does the same task with the first example. However, the difference is we're now using the pattern.
The command above will give all files which includes `ch1` in the name and have `.txt` at the end. The below is the output.
![](/images/1_name_2.png)

#### 2nd Option: `-exec CMD` 
Command-line option called `-exec CMD` allows us to execute commands on the resulting paths. 
For 1st and 2nd example here, we refers to [https://www.baeldung.com/linux/find-exec-command](https://www.baeldung.com/linux/find-exec-command).

```
$ find ./written_2 -name "ch1.txt" -exec file {} \;
```
This command-line allows us to run the `file` command on the list of files which have `ch1` as the name of the file. 
It is useful as we can execute some commands directly on the files that we want to apply.
The below is the output of the command above.
![](/images/2_exec_1.png)

```
$ find ./written_2 -name "ch1.txt" -exec echo {} +
```
This command-line also finds the files which have name `ch1`. However, the difference is we used `echo {} +` execution as command-line option, which allows us to show all of the expressions' results concatenated and passed as a whole to the `-exec` command, which will run only once. The below is the output
![](/images/2_exec_2.png)

#### 3rd Option: `-type` 
Command-line option called `-type` allows us to find the files by type. 
For 1st and 2nd example here, we refers to [https://www.redhat.com/sysadmin/linux-find-command](https://www.redhat.com/sysadmin/linux-find-command) and [https://linuxize.com/post/how-to-find-files-in-linux-using-the-command-line/](https://linuxize.com/post/how-to-find-files-in-linux-using-the-command-line/).

```
$ find ./written_2 -type d 
```
This command-line allows us to find only the listing of directories in a path. Here, `d` refers to the directories. 
It is useful when we only want to list directories root in a path that we wrote. 
The below is the output of the command above.
![](/images/3_type_1.png)

```
$ find ./written_2 -type f
```
This command-line allows us to find only the regular files in a path. Here, 'f' refers to the regular file.
It is useful when we only want to list regular files except directories and other things in a path.
The below is the output of the command above. 
![](/images/3_type_2.png)

#### 4th Option: `-size` 
Command-line option called `-size` allows us to find the files by size.
For 1st and 2nd example here, we refers to [https://linuxconfig.org/how-to-use-find-command-to-search-for-files-based-on-file-size](https://linuxconfig.org/how-to-use-find-command-to-search-for-files-based-on-file-size).

```
$ find ./written_2 -size 6k
```
This command-line allows us to find the files which have 6 kilobytes of size. Here, `k` refers to the `kilobytes`.
It is useful when we want to categorize the files based on the size or if the system requires certain amount of size. 
The below is the output of the command above.
![](/images/4_size_1.png)

```
$ find ./written_2 -size +6k -size -8k
```
This command-line allows us to find the files which have greater than 6 kilobytes of size but smaller than 8 kilobytes of size. Here, `k` refers to the `kilobytes`.
It is useful when we only want to list regular files except directories and other things in a path.
The below is the output of the command above. 
![](/images/4_size_2.png)
