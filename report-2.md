## Week 2 Lab Report
by Jaewon Han 

This post is a report about servers and bugs.

### Part 1 - Web Server called `StringServer`
![](/images/Part_1_1.png)
The image above is the code for my `StringServer`. There are two classes inside the file: Handler class and StringServer class. 
As we type `java StringServer.java 9500`, we can access to our Web Server using `https://localhost:9500`.

![](/images/Part_1_2_1.png)
After typing 
```
/add-message?s=Hello I'm Jaewon
```
the method `handleRequest`inside the `Handler_search` is called. `handlerRequest` method reads the `url` input and uses that input to work its task. This method decide which path the user is now using. If the path includes `/add-message`, then it determines if the path has correct queries. (In this case, `?s=<String>`). Then, put the strings inside the query section into the variable called `strs`, which refers to ArrayList in String type. Then, everytime we request the path which includes `/add-message`, the page shows the strings that has been added. In this case, it was first request of `/add-message`, so the page only shows `Hello I'm Jaewon`.

![](/images/Part_1_2_2.png)
After typing 
```
/add-message?s=Nice to meet you
```
the method `handleRequest` is called again. This time, variable `strs` has one more elements - `"Nice to meet you"`. Thus, the page shows two strings in each line.

### Part 2 - Bugs
Now It's time to install the Visual Studio Code. Go to the Website [https://code.visualstudio.com/](https://code.visualstudio.com/), and download
and install it on your personal computer/laptop. But, you don't have to install VScode in your personal computer/laptop, which means you can do all your work on the lab computers during this quarter. 

![](/images/Vscode-1.png)
If it is installed successfully, you could see a window that looks similar to the image above. (It might have different colors or menus.)

### Part 3 - What I've learned :)
