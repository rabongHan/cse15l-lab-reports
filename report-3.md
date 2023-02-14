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
We'll look two examples each for four different command-line options of the command `find`.

#### 1st Option: `-name` 
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

```
static int[] reversed(int[] arr) {
  int[] newArray = new int[arr.length];
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = newArray[arr.length - i - 1];
  }
  return arr;
} 
```

#### 2nd Option: `-exec CMD` 

#### 3rd Option: `-type` 

#### 4th Option: `-ls` 
