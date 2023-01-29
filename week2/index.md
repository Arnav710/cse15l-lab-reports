# Lab Report 2 - Servers and Bugs
---

The following are the various components from this lab report:
1. __Part 1__ : Writing a web server
2. __Part 2__ : Failure Inducing Input, Symptoms, Bugs
3. __Part 3__ : New Learnings

---

## Part 1: Writing a web server

A file called `StringServer.java` was implemented that listened to the incoming requests and kept a track of the various strings entered by the users in the form of search queries. Following that alld of those queries were displayed on a page, separated by a newline break.

The following was the format for specifying the path and the query in the URL:`/add-message?s=<string>`

Here, `/add-message` is the path name and `s=<string>` represents the query where <string> is a placeholder for the string that would be entered by the user.

The file `StringServer.java` can be implemented in the follwing way:
  
  ```
  import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {

    ArrayList<String> inputList = new ArrayList<String>();

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            String syntax = "/add-message?s=<string>";
            return "Perform a add-message query as follows" + "\n\n" + syntax;
        } else if (url.getPath().contains("/add-message")) {
            String[] params = url.getQuery().split("=");
            if (params[0].equals("s")) {
                String inputString = params[1];
                inputList.add(inputString);
                return String.join("\n", inputList);
            }
            return "404 not found";
        } else {
            return "404 not found";
        }
    }
}

public class StringServer {
    public static void main(String[] args) throws IOException {
        if (args.length == 0) {
            System.out.println(
                    "You forgot to pass the PORT number as a coomand line argument! Try any number between 1024 and 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}

  ```
  
  Now, let's try to run a few queries to see what the output would look like,
  <p align="center">
  <img width="750" alt="image" src="https://user-images.githubusercontent.com/63532613/215251543-a4c79098-fcdc-4fcd-8b71-10a2e96f82b5.png">
  </p>
  While executing this query, the `main` and the `handleRequest` methods are called. The `main` method takes an `args` parameter which specifies the PORT on which the localhost is running, while the `handleRequest` method takes in an parameter of type URI called the `url`.

  The values of the relevant fields change in the following manner:
  * `params = {"s", "--------"}`
  * `inputList = {"--------"}`
  
   <p align="center">
  <img width="750" alt="image" src="https://user-images.githubusercontent.com/63532613/215251576-cc22ca41-408b-4384-9c21-ac9e1c5a7d08.png">
  </p>
  While executing this query, the `main` and the `handleRequest` methods are called. The `main` method takes an `args` parameter which specifies the PORT on which the localhost is running, while the `handleRequest` method takes in an parameter of type URI called the `url`.

  The values of the relevant fields change in the following manner:
  * `params = {"s", "This is a line"}`
  * `inputList = {"--------", "This is a line"}`
  
  When the `inputList` is being displayed, it is converted to a string with all the elements being separated by new line characters.
  
---

## Part 2: Failure Inducing Inputs, Symptoms, Bugs
  
  We will be taking the example of a function called that is supposed to reverse the elements of an array in place. This means that when an array is passed into that function as a parameter, its values should be modified such the array appears to be flipped around. The given code for the same in `ArrayExamples.java` has a bug and we'll be trying to resolve the same.
  
  __Error Induing Input__
 ```
  @Test
  public void testReverseInPlaceFails1() {
    int[] input = { 1, 2, 3, 4 };
    ArrayExamples.reverseInPlace(input);
    assertArrayEquals(new int[] { 4, 3, 2, 1 }, input);
  }
 ```
  __Input Resulting in Correct Output__
  ```
  @Test
  public void testReverseInPlacePasses1() {
    int[] input = { 1, 2, 1 };
    ArrayExamples.reverseInPlace(input);
    assertArrayEquals(new int[] { 1, 2, 1 }, input);
  }
  ```
  
  Here are a few running examples of JUnit test cases that pass, followed by tests that fail.
  
  <p align="center">
  <img width="500" alt="image" src="https://user-images.githubusercontent.com/63532613/215252917-a84bb630-ec40-4179-acc1-98fa43d7cd52.png">
  </p>
  <p align="center">
<img width="500" alt="image" src="https://user-images.githubusercontent.com/63532613/215252952-316c4a42-f710-4f2d-ae87-7eec867a51bc.png">  </p>
  <p align="center">
<img width="500" alt="image" src="https://user-images.githubusercontent.com/63532613/215252981-6aa4cd06-ac52-478c-9408-119397f928c7.png">  </p>
  <p align="center">
  <img width="500" alt="image" src="https://user-images.githubusercontent.com/63532613/215253051-ed80e97a-40e5-43a8-bc0e-343fff8789c8.png">
  </p>
  
  __Given Code and The Bug__<br>
  The problem with this code is that when we reach the second half of the array, the values in the first half of the array have already been re-assigned. So, we are not able to construct the second half of the array in the correct manner. 
  
  For instance, if `arr = {1, 2, 3, 4}`, when we reach index 2, `arr = {4, 3, 3, 4}`. Consequently, when we reach index = 2 we assign arr[2] = arr[1]. So, arr[2] is now assigned a value of 3 while it should actually be assigned a value of 2.
  
  ```
  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for (int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
  ```
  __Resolving the Bug__<br>
  In order to fix this bug, we will start our traversal from the beginning of the array and end at the mid-point. For each index `i`, we would swap the values at the indices `i` and `arr.length - i - 1` using a temporary variable.

 ``` 
  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for (int i = 0; i < arr.length / 2; i += 1) {
      int tmp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = tmp;
    }
  }
 ```
 
  <p align="center">
  <img width="500" alt="image" src="https://user-images.githubusercontent.com/63532613/215254001-355f2fd5-ac2e-4d21-a811-d905c23e13cc.png">
  </p>
  
---
  
## Part 3: New Learnings

  * Over the past few months I had been trying to pick up web development by self learning HTML, CSS, JavaScript, and React. So, I found it pretty interesting to learn more about the URLHandler interface in Java and the kinds of programs you can create with it.
  * Experimenting with the `NumberSever.java` file are running it on the remote server truly made me understand the importance of connecting to a remote server for classes like CSE 15L. Unlike the localhost, the website could be accessed from any system over the internet since it was being run and hosted by a centralized server.
  * Degugging is a critical component of software development and it was great to learn about how debugging should be approached in a structural and logical manner. The multiple exercises from the Week 3 lab made me learn about importance of coming up with a series of error inducing inputs and then trying to isolate the potential causes for those. 
  * It was also very intersting to think about how multiple bugs in the program may be leading to the same symptom, making it even harrder to debug!
  
 ---
