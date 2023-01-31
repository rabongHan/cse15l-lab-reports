## Week 1 Lab Report
by Jaewon Han 

Throughout this 15L course, we'll use course-specific account. 

This post is a tutorial about how to log into a course-specific account on `ieng6`.

### Part 1 - CSE15L Account
First of all, you should check your course-specific account for CSE15L.

You can find your account using this link: [https://sdacs.ucsd.edu/~icc/index.php](https://sdacs.ucsd.edu/~icc/index.php)

After logging into the website above, you should change your account to the additional account starting with `cse15l`.
![](/images/cse15l-account-1.png)

Then, you have to reset the password. If you've reset the password, you have to wait a few minutes(usually 15 mins) for it to take effect. 

### Part 2 - VScode
Now It's time to install the Visual Studio Code. Go to the Website [https://code.visualstudio.com/](https://code.visualstudio.com/), and download
and install it on your personal computer/laptop. But, you don't have to install VScode in your personal computer/laptop, which means you can do all your work on the lab computers during this quarter. 

![](/images/Vscode-1.png)
If it is installed successfully, you could see a window that looks similar to the image above. (It might have different colors or menus.)

### Part 3 - Remotely Connecting
Now we'll see how to use Vscode and terminal to connect to a remote computer(server) to work there. 

#### 1st step: installing git and git bash for Windows.
[Git for Windows](https://gitforwindows.org/)

[How to use Bash in VScode](https://stackoverflow.com/questions/42606837/how-do-i-use-bash-on-windows-from-the-visual-studio-code-integrated-terminal/50527994#50527994)

#### 2nd step: open terminal in VScode (For Mac users, begin from here)
To open terminal in VScode, you can press Ctrl or Command + ~, or use the Terminal | New Terminal menu option.
```
$ ssh cs15lwi23????@ieng6.ucsd.edu
```
You should replace `????` with your course-specific account.

Type `yes` and press enter, then give your password. 

Then you'll see the image like below.
![](/images/RemotelyConnecting-1.png)

Now you're connected to the remote server. 

### Part 4 - Some Commands
It's time to use some commands. Try running the commands like `cd`,`ls`,`pwd`,`cp`, and etc.
#### Explanation of commands
* `cd` : "Change Directory" Used to switch the current working directory to the given path.
* `ls` : "List" Used to list the files and folders the given path.
* `pwd`: "Print Working Directory" Used to display the current working directory.
* `cp` : "Copy" Used to copy files or gorup of files or directory. 

The below images are how you can use commands. They are just for example. Feel free to use in your own way. 
![](/images/Commands-1-1.png)
```
$ cd
```
Since we don't specify where to change directory, it is still in same directory.
```
$ cd ~
```
`~` is a directory where a user's files are stores, which we call as "Home Directory". So nothing changed.
```
$ ls
```
There is one directory shown: `perl5`
```
$ cd perl5
```
change directory to perl5. We can now see we are in the `perl5` directory.
```
$ cd .. 
```
`..` is a "Parent Directory". So, we are going back to the original directory. 

![](/images/Commands-1-2.png)
```
$ ls -lat
```
`ls` is "List" as we know. Using `-` symbol, we can specifiy which files and directories to be listed. 
`l` is a list with long format. `a` is all files including hidden files. `t` is sort by time&date. 
Thus, `ls -lat` means listing all files including hidden files in long format, sorted by time and date. 
We can notice that there were actually 124 different files and directories (not just perl5!)
![](/images/Commands-1-3.png)
```
$ cp /home/linux/ieng6/cs15lwi23/public/hello.txt ~/
```
We are now in the working directory `/home/linux/ieng6/cs15lwi23/cs15lwi23abo` (You might have different 3 alphabets after `cs15lwi23`.
We just copied file called `hello.txt` from `../public/hello.txt`. Before typing this command, try to find `hello.txt` in your directory. 
Then, after typing this command, try to find the same file in your directory. 
```
$ cat /home/linux/ieng6/cs15lwi23/public/hello.txt
```
`cat` command reads data from the file and gives their content as output. We can see the content of `hello.txt`.
But you should know that we access this file through `../public/hello.txt` not our working directory. 
(We have same file in our working directory too!)

You can log out of the remote server by using the command `exit` or pressing Ctrl-D.
![](/images/Commands-2.png)
