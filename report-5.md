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
>>  The line 1 is for the JUnit library path. This grading script is using JUnit to test student code, so this line is necessary for using JUnit. 

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
>>  The line 31 makes new directory called `tests`. This 

``` 
3   rm -rf student-submission 
4   rm -rf tests 
``` 
>>  The line 3 and 4 removes the student-submission and tests directory. These lines are necessary to prevent the case where previous student code is overlapped with current student code. Here, the `rm` command is used to remove the files and directories, and `-rf` command-line option makes `rm` command to delete the directory and all of its contents without prompting confirmation. 

``` 
3   rm -rf student-submission 
4   rm -rf tests 
``` 
>>  The line 3 and 4 removes the student-submission and tests directory. These lines are necessary to prevent the case where previous student code is overlapped with current student code. Here, the `rm` command is used to remove the files and directories, and `-rf` command-line option makes `rm` command to delete the directory and all of its contents without prompting confirmation. 

``` 
3   rm -rf student-submission 
4   rm -rf tests 
``` 
>>  The line 3 and 4 removes the student-submission and tests directory. These lines are necessary to prevent the case where previous student code is overlapped with current student code. Here, the `rm` command is used to remove the files and directories, and `-rf` command-line option makes `rm` command to delete the directory and all of its contents without prompting confirmation. 


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
