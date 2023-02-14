## Week 3 Lab Report
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
For 2nd example here, we refers to [https://www.geeksforgeeks.org/find-command-in-linux-with-examples/]([https://man7.org/linux/man-pages/man1/grep.1.html](https://www.geeksforgeeks.org/find-command-in-linux-with-examples/))
```
$ find ./written_2 -name "ch1.txt"
```
This command-line option allows us to find to search files called "ch1.txt" from the `./written_2`. 
It is useful when we want to know the exact location of the files. 
The below is the output of the command above.
![](/images/1_name_1.png)

```
$ find ./written_2 -name *ch1*.txt
```
This command-line option does the same task with the first example. However, the difference is we're now using the pattern.
The command above will give all files which includes `ch1` in the name and have `.txt` at the end. The below is the output.
![](/images/1_name_2.png)

#### 2nd Option: `-exec CMD` 

#### 3rd Option: `-type` 

#### 4th Option: `-ls` 
