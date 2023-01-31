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
For Part 2, we will use this buggy code in file called `ArrayExamples`(class name: `ArrayExamples`) given below.
```
static int[] reversed(int[] arr) {
  int[] newArray = new int[arr.length];
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = newArray[arr.length - i - 1];
  }
  return arr;
} 
```

Firstly, let's see which input is failure-inducing input and which input is not.
We'll use two JUnit tests shown below.
```
public void testReversed1() {
  int[] input1 = { };
  assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
}
```
The first test includes the non-failure-inducing input, which is just empty array. The reason why this is an input that doesn't induce a failure is because, even though we put the empty array as input into `reversed` method, it doesn't give errors. We can check it through running the tests. The screenshot below is the output of running the first test.
![](/images/Part_2_1.png)

```
public void testReversed2() {
  int[] input1 = {3, 2, 1};
  assertArrayEquals(new int[]{1, 2, 3}, ArrayExamples.reversed(input1));
}
```
The second test includes the failure-inducing input, which is just `{3, 2, 1}` int array. The reason why this is an input that doesn't induce a failure is because, whenh we put the input into `reversed` method, it doesn't give what we expected, raising error during test. We can check it through running the tests. The screenshot below is the output of running the second test.
![](/images/Part_2_2.png)
While the expected value was `{1, 2, 3}`, the actual value was `{0, 0, 0}`. Here, the symptom is that all return values are the array in the same size of `arr` but filled with `0`s.

Looking at the old code, we can find the bug which causes the sypmptom that we found above. We have to change the order of `newArray` and `arr` inside the for-loop. Then, we also have to change the method to return `newArray` instead of `arr`. The reason why all return values were array filled with `0`s was because the method changed all elements inside the `arr` with 0 and returned `arr`. 
Below is the code after fixing the bug.
```
static int[] reversed(int[] arr) {
  int[] newArray = new int[arr.length];
  for(int i = 0; i < arr.length; i += 1) {
    newArray[i] = arr[arr.length - i - 1];
  }
  return newArray;
} 
```

### Part 3 - What I've learned :)
