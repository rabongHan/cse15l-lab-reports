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
⋅⋅* `cd` : "Change Directory" Used to switch the current working directory to the given path.
⋅⋅* `ls` : "List" Used to list the files and folders the given path.
⋅⋅* `pwd` : "Print Working Directory" Used to display the current working directory.
⋅⋅* `cp` : "Copy" Used to copy files or gorup of files or directory. 

The below images are how you can use commands. They are just for example. Feel free to use in your own way. 
![](/images/Commands-1.png)

You can log out of the remote server by using the command `exit` or pressing Ctrl-D.
![](/images/Commands-2.png)
