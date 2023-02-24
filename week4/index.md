# Learning How to Use the Terminal Efficiently

---
## Overview

In this week's lab, we were told to perform the following tasks in the shortest amount of time possible, by minimizing the amount we type and avoiding tying mistakes. The following were the steps to be performed

1. Setup Delete any existing forks of the repository you have on your account
2. Setup Fork the repository
3. The real deal Start the timer!
4. Log into ieng6
5. Clone your fork of the repository from your Github account
6. Run the tests, demonstrating that they fail
7. Edit the code file to fix the failing test
8. Run the tests, demonstrating that they now succeed
9. Commit and push the resulting change to your Github account

---
## The Process

### Step 1: Setup Delete any existing forks of the repository you have on your account

In order to delete any existing forks of the current repository,
* Open the fork on github and click on the settings tab

![image](https://user-images.githubusercontent.com/63532613/221065310-33a06e72-f980-4c43-8b5f-207c4916674f.png)

* Scroll all the way to the bottom and click `Delete this repository`, confirm this action when asked to do so.

![image](https://user-images.githubusercontent.com/63532613/221065360-0099ee6c-5fd0-4324-9478-23cafa30b4a7.png)

### Step 2: Setup Fork the repository

To create a fork, open [Lab 7](https://github.com/ucsd-cse15l-w23/lab7) and click on the fork button that appears on the top right corner of the screen.

![image](https://user-images.githubusercontent.com/63532613/221065725-0a8be2eb-c171-41dc-a685-76f8f9c4850e.png)

### Step 3: The real deal Start the timer!

The aim of this lab was to perform a certain set of tasks quickly. You can use your phone to time your initial speed. Subsequently, you can try to evaluate the extent to which you were able to improve on this baseline time.

### Step 4: Log into ieng6

Type `ssh cs15lwi23<...>@ieng6.ucsd.edu` to log in to the remote server. The `<...>` should be replaced by your own unique id for the ieng6 remote server. 

![image](https://user-images.githubusercontent.com/63532613/221066272-fd7666e4-e03c-49c9-9a47-b0c0b2b0eecb.png)

### Step 5: Clone your fork of the repository from your Github account

Copy the ssh key to clone the fork of the repository from github.

![image](https://user-images.githubusercontent.com/63532613/221070426-76b32ef7-89e6-4d9f-924d-6c7ffde21e72.png)

On the terminal, type `git clone <Ctrl - V>`. Here, `Ctrl - V` would paste the link of the repository onto the terminal. Then you can simply press enter to run the command.

![image](https://user-images.githubusercontent.com/63532613/221066647-b1c5a7b7-a668-45ac-96fa-e8e4312d8501.png)

### Step 6: Run the tests, demonstrating that they fail

To move into the folder that was cloned, run `cd la<tab>`. Pressing tab would auto-complete to the folder's name `lab7`. This assumes that you don't already have a folder in your current directory that starts with the prefix `la`.

![image](https://user-images.githubusercontent.com/63532613/221067015-68f301b0-4584-4c40-bd54-7144f497b5cb.png)

To compile the java files and run the JUnit tests, we will just copy and paste the commands from week 3 of the course website instead of typing them out.

![image](https://user-images.githubusercontent.com/63532613/221067272-214aafd2-3531-468c-994b-b3da97789baf.png)

Copy the first command as is, and in the terminal type `<Ctrl - V>`

```
[cs15lwi23aaq@ieng6-203]:lab7:496$ javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
```

To run the tests, copy the second command from the course website but remember to NOT copy the file name since it is different here. On the terminal, do `<Ctrl -V> L<tab>T<tab><backspace>`. Whenever bash is not sure about how to autocomplete due to a common prefix, we can either type out the remaining part or complete it to a point after which no ambiguity remains.

Here, the tabs are used for auto-complete while the backspace would be used to remove the period that comes in the end. When we are running a compiled file, we just need to write the filename, without the `.java` or `.class` extension. 

![image](https://user-images.githubusercontent.com/63532613/221067746-563e3b86-d03a-4a01-ae7a-14d6e612f61a.png)

### Step 7: Edit the code file to fix the failing test

To open the text editor, `nano L<tab>.j<tab>`. Then go to the 43rd line and change the index that is being updated. It should be `index2` instead of `index 1`. 

![image](https://user-images.githubusercontent.com/63532613/221068277-72af7ab0-8292-4785-9ef2-1250e8402c62.png)

To save changes, `<Ctrl - O><Enter>`
To exit nano, `<Ctrl - X>`

### Step 8: Run the tests, demonstrating that they now succeed

We had already run the commands to compile and run the tests, so we can just re-use that by using the up arrow keys, which allow us to move through the previously executed commands.

To compile the files, `<up-arrow><up-arrow><up-arrow><up-arrow>` and then press enter. 

```
[cs15lwi23aaq@ieng6-203]:lab7:496$ javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
```

To run the tests, `<up-arrow><up-arrow><up-arrow>` and then press enter.

![image](https://user-images.githubusercontent.com/63532613/221068954-9d5829ae-3b0e-4c5e-8422-6dd75c431826.png)


### Step 9: Commit and push the resulting change to your Github account

To see changes, `git status`

![image](https://user-images.githubusercontent.com/63532613/221069565-29ef5df1-3c4a-455d-b4dc-35dfb47608d6.png)

To stage changes, `git add L<tab>.j<tab>`. Whenever bash is not sure about how to autocomplete due to a common prefix, we can either type out the remaining part or complete it to a point after which no ambiguity remains.

```
[cs15lwi23aaq@ieng6-203]:lab7:499$ git add ListExamples.java
```

To commit changes, `git commit -m "Update"`. It is important to provide a message while we are committing changes.

![image](https://user-images.githubusercontent.com/63532613/221070069-61df5213-eb95-47af-b257-f1d62e916499.png)

To push changes to the github repository, `git push origin main`.

![image](https://user-images.githubusercontent.com/63532613/221070942-af432084-b8ce-4b05-9f4f-bc2d697f2d02.png)

The changes pushed can clearly be seen on github as well.

![image](https://user-images.githubusercontent.com/63532613/221071028-b2f56cd8-a6da-451c-b652-6d5d867f2189.png)
