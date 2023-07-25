# Expanding on Previous Tasks

One of my favorite tasks from the labs was working on the script for `grade.sh`. It was quite interesting to see how we could create a bash script to carry out the entire process of:
1) Trying to clone a repository from github
2) Checking if the file to be graded actually exists within the repository cloned
3) Checking if the file to be graded even compiles correctly
4) Running the JUnit Tests on the submission
5) Giving the user some sort of feedback on how their code performed on the JUnit tests

For this lab report, I will be showcasing my grading scirpt by showing it's contents asa well as the output it produces when it is run on various sample submissions. 

---

## Bash Script for Grading

The following segment displays my bash script, I have tried to add some comments in the bash script as well so that you can easily keep a track of what each of the components of the script does. Subsequently, I will be showing how to run it and give various examples of doing so.

```
# Defining the class path
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

# Removing the previous student submission directory so that we can clone another repository
rm -rf student-submission

# Cloning the repository
git clone $1 student-submission
echo 'Finished cloning'

# Changing the directory to move into the folder with cloned contents
cd student-submission

# Checking if the correct file has been submitted
if [[ -e ListExamples.java ]]
then 
    echo "File with the correct name was submitted (ListExamples.java)"
else 
    echo "File with incorrect name was submitted. Rename to ListExamples.java"
    exit
fi

cd ../

# Somehow get the student code and your test .java file into the same directory
cp ./student-submission/ListExamples.java ./

# Compiling the files
javac -cp $CPATH *.java > error-trace.txt


# Checking for compilation errors
if [[ $? -ne 0 ]]
then 
    echo "There was an error compiling the file submitted"
    cat error-trace.txt
    exit
else 
    echo "The java code was compiled successfully"
fi


# Running the JUnit tests
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples > test-output.txt

# Fetcing the last line of the JUnit output and displaying it to the user
echo "================================"
last_line=$(tail -n 2 test-output.txt)
echo $last_line
echo "================================"

echo "Execution ended"
```

---

## Trying the Script on Various Sample Submissions

To run the grading script, execute the following command:

```bash grade.sh <link to github repo with submission>```

### Test 1
Starter code from Lab 3

**Output:**
```
[cs15lwi23aaq@ieng6-203]:list-examples-grader:501$ bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-lab3
Cloning into 'student-submission'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
Finished cloning
File with the correct name was submitted (ListExamples.java)
The java code was compiled successfully
================================
Tests run: 1, Failures: 1
================================
Execution ended
```
**Interpretation** - everything worked but the student's submission failed one of the JUnit tests

### Test 2
The perfect submission, in which every method works as intended

**Output:**
```
[cs15lwi23aaq@ieng6-203]:list-examples-grader:503$ bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-corrected
Cloning into 'student-submission'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
Finished cloning
File with the correct name was submitted (ListExamples.java)
The java code was compiled successfully
================================
OK (1 test)
================================
Execution ended
```
**Interpretation** - all the JUnit tests passed

### Test 3
The submission has a missing semi-colon at the end of one of the lines. As a result, we should obtain a compilation error in this case.

**Output:**
```
[cs15lwi23aaq@ieng6-203]:list-examples-grader:509$ bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-compile-error
Cloning into 'student-submission'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
Finished cloning
File with the correct name was submitted (ListExamples.java)
ListExamples.java:15: error: ';' expected
        result.add(0, s)
                        ^
1 error
There was an error compiling the file submitted
```
**Interpretation** - the bash script not only tells us that there was an error during compilation, but also gives us the error trace to help us debug the code. The idea of output re-direction while compilation was used to achieve this result.

### Test 4
The submission has has the types for the arguments of filter in the wrong order, so it doesn’t match the expected behavior.

**Output:**
```
[cs15lwi23aaq@ieng6-203]:list-examples-grader:510$ bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-signature    
Cloning into 'student-submission'...
remote: Enumerating objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 3
Receiving objects: 100% (3/3), done.
Finished cloning
File with the correct name was submitted (ListExamples.java)
The java code was compiled successfully
================================
OK (1 test)
================================
Execution ended
```
**Interpretation** - the bash script is running the JUnit tests from `TestListExamples.java`, which has one test method that checks the working of `merge`. Since we are not even testing the `filter` method, the one test that was run passes successfully.

### Test 5
This submission has a great implementation saved in a file with the wrong name.

**Output:**
```
[cs15lwi23aaq@ieng6-203]:list-examples-grader:513$ bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-filename 
Cloning into 'student-submission'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
Finished cloning
File with incorrect name was submitted. Rename to ListExamples.java
```
**Interpretation** - the bash script tells the user that the file name was incorrect and prompts them to change it to `ListExamples.java` so that the JUnit tests can we executed on them.

---

## In Conclusion

I believe that this grading script does a great job of evaluating submissions, handing some of the edge cases, and catching errors that occcur in the process. However, there is still a lot of room for improvement. Adding the following features would make this script even more robust:
* Instead of searching for the file `ListExamples.java` right inside the folder cloned, we could probably try to do a recurive search for it in that folder as well as all of its sub-directories.
* The output could be formatted in a sligtly better manner.
* A message of encouragement can be added when all the JUnit tests pass successfully!

