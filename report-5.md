## Week 9 Lab Report 5
by Jaewon Han 

This post is a report that introduces grading script and demonstrates grading script working from lab 6. 

### The Grading Script
```
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf tests

git clone $1 student-submission
echo "--------------------------------"
echo "Finished cloning"
echo "--------------------------------"

FILE_PATH=$(find student-submission/ -name "ListExamples.java" -type f)

if [[ -z "$FILE_PATH" ]]; then
    echo "Error: the file submitted has incorrect name or is missing" 
    exit 1
else 
    if [[ -e student-submission/ListExamples.java ]]; then
        if [[ -f student-submission/ListExamples.java ]]; then
            echo "Success: Found correct file"
            echo "--------------------------------"
        else
            echo "Error: the file submitted is not regular file"
            exit 1
        fi
    else
        echo "Error: the file submitted has correct name but in nested directory"
        exit 1
    fi
fi

mkdir tests
cp student-submission/ListExamples.java tests/
cp TestListExamples.java tests/
cp -R ./lib tests/

cd tests

javac -cp $CPATH *.java > compile-output.txt


if [[ $? -ne 0 ]]; then
    echo "Error: Compilation failed"
    echo "--------------------------------"
    exit 1
fi

java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > test-output.txt

if grep -q "FAILURES!!!" test-output.txt; then
    FAILURES=$(grep "Failures:" test-output.txt | awk '{print $NF}' | cut -d':' -f2)
    echo "$FAILURES Test(s) Failed among 3 Tests"
    echo "--------------------------------"
    PERCENTAGE=$(printf "%.2f" $(echo "(3-$FAILURES)/3*100" | bc -l))
    echo "Total Grade: $PERCENTAGE%"
else
    echo "Test Succeed"
    echo "--------------------------------"
    echo "Total Grade: 100%"
fi
```
The above script(`grade.sh`) is the full line of grading script that I wrote. 
In this section, I'll explain how each line works and why it is useful. 

``` 
1   CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar' 
``` 
>>  The line 1 is for the `JUnit` library path. This grading script is using `JUnit` to test student code, so this line is necessary for using `JUnit`. 

``` 
3   rm -rf student-submission 
4   rm -rf tests 
``` 
>>  The line 3 and 4 removes the student-submission and tests directory. These lines are necessary to prevent the case where previous student code is overlapped with current student code. Here, the `rm` command is used to remove the files and directories, and `-rf` command-line option makes `rm` command to delete the directory and all of its contents without prompting confirmation. 

``` 
6   git clone $1 student-submission
7   echo "--------------------------------"
8   echo "Finished cloning"
9   echo "--------------------------------"
``` 
>>  The line 6 allows us to clone the student code repository into the directory called `student-submission`. The line 7 is for printing the `clone` sucess, and line 8 and 9 are for visual effect to divide the texts with each other when print multiple lines. Here `$1` indicates the first argument to a script after we call `bash grade.sh`. 

``` 
11  FILE_PATH=$(find student-submission/ -name "ListExamples.java" -type f)
``` 
>>  The line 11 is for the student code file path. This path is necessary to be used later to determine if file has correct name or file is not in nested directory. The `find` command finds files or directories. Here, `find` command finds only files because of `-type f` option and finds the files named `ListExamples.java` which is the correct name for student code.  

``` 
13  if [[ -z "$FILE_PATH" ]]; then
14      echo "Error: the file submitted has incorrect name or is missing" 
15      exit 1
16  else 
17      if [[ -e student-submission/ListExamples.java ]]; then
18          if [[ -f student-submission/ListExamples.java ]]; then
19              echo "Success: Found correct file"
20              echo "--------------------------------"
21          else
22              echo "Error: the file submitted is not regular file"
23              exit 1
24          fi
25      else
26          echo "Error: the file submitted has correct name but in nested directory"
27          exit 1
28      fi
29  fi
``` 
>>  The lines from 13 to 29 is for determining if student code submission was correct, depending on (1) its name, (2) its directory (3) file type. The line 13 checks if `FILE_PATH` we got from line 11 is empty. If `FILE_PATH` is empty, it means file has incorrect name or is missing. The line 17 checks if `student-submission/ListExamples.java` exists. If it is true, it means that file has correct name and is direct child of `student-submission` directory. The line 18 checks if `student-submission/ListExamples.java` exists and also is regular file. The line 25 indicates that file name is correct, but in nested directory. Only in case where if statement in line 17 and line 18 is satisfied, the bash is keep continued. Otherwise, the bash is exited. These lines are necessary to check if submission was correct.

``` 
31  mkdir tests
32  cp student-submission/ListExamples.java tests/
33  cp TestListExamples.java tests/
34  cp -R ./lib tests/
``` 
>>  The line 31 makes new directory called `tests`. This directory will store `JUnit` library, `TestListExamples.java` which is tester code for student code, and `ListExamples.java` which is student code. The line from 32 to 34 all copies the files mentioned right before into the directory `tests`. The command-line option `-R` in line 34 stands for recursive and allows user to copy directories and their contents. 

``` 
36  cd tests
``` 
>>  The line 36 makes current workig directory to be moved to `tests` directory. 

``` 
38  javac -cp $CPATH *.java > compile-output.txt
``` 
>>  The line 38 compiles all the `java` files in `tests` directory and puts the results into `compile-output.txt`. Here, `$CPATH` is the path for `JUnit` library that we set at the first line. 

``` 
41  if [[ $? -ne 0 ]]; then
42      echo "Error: Compilation failed"
43      echo "--------------------------------"
44      exit 1
45  fi
``` 
>>  The lines from 41 to 45 is to determine whether compilation was succeed or not. The line 41 `[[ $? -ne 0]]` is used to check if the previous command executed successfully or not. Here, `-ne` is a comparison operator that stands for not equal. `$?` is a special variable that holds the exit status of the last executed command. 

``` 
47  java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > test-output.txt
``` 
>>  The line 47 runs the tester file called `TestListExamples.java` and puts the results into `test-output.txt`. Here, `$CPATH` is the path for `JUnit` library that we set at the first line. 

``` 
49  if grep -q "FAILURES!!!" test-output.txt; then
50      FAILURES=$(grep "Failures:" test-output.txt | awk '{print $NF}' | cut -d':' -f2)
51      echo "$FAILURES Test(s) Failed among 3 Tests"
52      echo "--------------------------------"
53      PERCENTAGE=$(printf "%.2f" $(echo "(3-$FAILURES)/3*100" | bc -l))
54      echo "Total Grade: $PERCENTAGE%"
55  else
56      echo "Test Succeed"
57      echo "--------------------------------"
58      echo "Total Grade: 100%"
59  fi
``` 
>>  The lines from 49 to 59 checks whether the `JUnit` test was successful or not. The line 49 checks if `test-output.txt` has `FAILURES!!!` strings inside. It this is true, then it means test was failed. Otherwise, the test was succeed. If the test was failed, the lines from 50 to 54 is executed. The line 50 assigns the number of failures into `FAILURES` variable. The `grep` command first searches for the line contatining `Failures:` in the `test-output.txt` file. Then, `awk` command extracts the certain part. Here, `awk` command exxtracts the last part of the line using the command-line option called `$NF` which represents the last field of the current record. Then, `cut` command extracts only the number part. Here, `cut` command uses `-d` option which specifies the delimiter to split theline at the `":"` character and then uses `-f2` options to extract the second field which indicates strings after `":"` (number of failures). Then, calculate the grade percentage by `(3-number of failures)/3*100`, using math library called by `bc`. Here, we restricts the result into 2 floating decimal points using `printf "%.2f"`.

### Testing 
![](/images/step5_1.png)
>   *Keys pressed*: ``` git<space>clone<space><command + v><enter> ```
>>  I copied the **SSH** of forked repository called `lab7`. Then paste that after typing `git clone`. This allows me to clone my fork of the repository. 

![](/images/step5_2.png)
* [1] `ls`
>   *Keys pressed*: ``` ls<enter> ```
>>  I typed `ls` to check if cloning worked well. `ls` command shows me the direcotry and file list, and I checked the folder called `lab7`.  

* [2] `cd lab7`
>   *Keys pressed*: ``` cd<space>lab7<enter> ```
>>  Then I moved my working directory to `lab7` folder by typing `cd lab7`.

* [3] `ls`
>   *Keys pressed*: ``` ls<enter> ```
>>  I typed `ls` to check which files and direcotries are inside the `lab7` folder. This was to see certain file's name later on step 6. 

### Conclusion
It took 1 minute and 25 seconds for me to finish all the steps. 
