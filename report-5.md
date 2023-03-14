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
The above script is the full line of grading script that I wrote. 
In this section, I'll explain how each line works and why it is useful. 

``` CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar' ``` 
>>  This first line is for the JUnit library path. This grading script is using JUnit to test student code, so this line is necessary for using JUnit. 

``` 
rm -rf student-submission 
rm -rf tests 
``` 
>>  This first line is for the JUnit library path. This grading script is using JUnit to test student code, so this line is necessary for using JUnit. 

>   ``` CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar' ``` 
>>  This first line is for the JUnit library path. This grading script is using JUnit to test student code, so this line is necessary for using JUnit. 

>   ``` CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar' ``` 
>>  This first line is for the JUnit library path. This grading script is using JUnit to test student code, so this line is necessary for using JUnit. 

>   ``` CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar' ``` 
>>  This first line is for the JUnit library path. This grading script is using JUnit to test student code, so this line is necessary for using JUnit. 

>   ``` CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar' ``` 
>>  This first line is for the JUnit library path. This grading script is using JUnit to test student code, so this line is necessary for using JUnit. 
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
