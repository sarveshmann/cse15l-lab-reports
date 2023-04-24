# Lab Report 2

## **Objectives:**

1. Write a web server.

2. Analyze a bug from Lab 3.

3. Reflect on what I learned.

<br />

## **1: Write a web server**

> ### Step 1 -  Code for the StringServer:

```
import java.io.IOException;
import java.net.URI;

class StringHandler implements URLHandler {
    // Greeting
    private static String GREETING = "Welcome to your String Server!"
        + "\n\nTo add a message, use the add-message query." 
        + "\n\nHere are all of your messages:\n\n%s";
    
    // String to store all the messages
    String str = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format(GREETING, str); 
        } else {
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    str += parameters[1] + "\n";
                    return String.format(GREETING, str);
                }
            }
            return "404 Not Found!";
        }
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new StringHandler());
    }
}
```

<br />

> ### Step 2 - Two screenshots of using add-message:

* **Output 1:**

<img src="https://github.com/sarveshmann/cse15l-lab-reports/blob/c66b34f12af2760aafc09fa5f843d1b98d7ff031/server-output-1.png" width=50% height=50%>


* **Output 2:**

<img src="https://github.com/sarveshmann/cse15l-lab-reports/blob/c66b34f12af2760aafc09fa5f843d1b98d7ff031/server-output-2.png" width=50% height=50%>


<br />

> ### Step 3 - Description of each output:

### **For Output 1:**
    
**Important variables at start:**
* Private static String variable `GREETING` which does not change and gets printed out at the top everytime.

```
// Greeting
    private static String GREETING = "Welcome to your String Server!"
        + "\n\nTo add a message, use the add-message query." 
        + "\n\nHere are all of your messages:\n\n%s";
```

* String variable `str` used to store messsages.

```
// String to store all the messages
    String str = "";
```
<br />

**Operations:**

* `handleRequest` method takes in the url `http://localhost:2028/add-message?s=Hello`.
* Inside this method, first `if` statement checks if the path is equal to `/`, which is not, so the `else` branch gets executed.
* Inside the `else` branch, another `if` statment checks if the path contains `/add-message`, which it does, so the `if` branch gets executed.
* Inside the `if` branch, the query string gets split using `=` as the splitter, and gets stored in the String array called `parameters`.
* Then, another `if` statement checks if the first element inside the `parameters` array is equal to `"s"`, which is true, so the `if` branch gets executed.
* Inside the `if` branch, the second element of `parameters` array, which is `Hello`, and a new line `"\n"` get concatenated to `str`.
* Finally, a formatted String gets returned which includes the `GREETING` and `str`, which is the added message.

<br />

### **For Output 2:**</u>

**Important variables at start:**

<br />

* Private static String variable `GREETING` which does not change and gets printed out at the top everytime.

```
// Greeting
    private static String GREETING = "Welcome to your String Server!"
        + "\n\nTo add a message, use the add-message query." 
        + "\n\nHere are all of your messages:\n\n%s";
```

* String variable `str` used to store messsages.

```
// String to store all the messages
    String str = "Hello\n";
```
<br />

**Operations:**

* `handleRequest` method takes in the url `http://localhost:2028/add-message?s=How%20are%20you`. (*Note: spaces automatically get replaced with `%20`.*)
* Inside this method, first `if` statement checks if the path is equal to `/`, which is not, so the `else` branch gets executed.
* Inside the `else` branch, another `if` statment checks if the path contains `/add-message`, which it does, so the `if` branch gets executed.
* Inside the `if` branch, the query string gets split using `=` as the splitter, and gets stored in the String array called `parameters`.
* Then, another `if` statement checks if the first element inside the `parameters` array is equal to `"s"`, which is true, so the `if` branch gets executed.
* Inside the `if` branch, the second element of `parameters` array, which is `How are you`, and a new line `"\n"` get concatenated to `str`.
* Finally, a formatted String gets returned which includes the `GREETING` and `str` (the added message).

<br />
<br />

## **2: Analyze a bug from Lab 3**

> ### Step 1 -  Choose a bug from Lab 3:

I am choosing an **'infinite loop' bug** I found in the "merge" method of the file named "ListExamples.java", the original code for which is as follows:
<br />

``` 
// Takes two sorted list of strings (so "a" appears before "b" and so on),
// and return a new list that has all the strings in both list in sorted order.
static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;<br />
    while(index1 < list1.size() && index2 < list2.size()) {
        if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
            result.add(list1.get(index1));
            index1 += 1;
        }
        else {
            result.add(list2.get(index2));
            index2 += 1;
        }
    }
    while(index1 < list1.size()) {
        result.add(list1.get(index1));
        index1 += 1;
    }
    while(index2 < list2.size()) {
        result.add(list2.get(index2));
        index1 += 1;
    }
    return result;
}
 ```
  
 <br />
 
> ### Step 2 -  Failure inducing input:

  An example of a **failure inducing input** (as a JUnit test) where we try to merge two sorted ArrayLists is as follows:
  <br />
  
``` 
@Test
public void testMerge(){
      // inputs
      List<String> input1 = Arrays.asList("a", "c", "e");
      List<String> input2 = Arrays.asList("b", "d", "f");
      List<String> expected1 = Arrays.asList("a", "b", "c", "d", "e", "f");
      assertEquals(null, expected1, ListExamples.merge(input1, input2));   
} 
```
  
 <br />
 
> ### Step 3 -  Passing input:

  An example of an **input that doesn't cause failure** (as a JUnit test) where we try to merge two sorted ArrayLists is as follows:
  <br />
  
``` 
@Test
public void testMerge1(){
      // inputs
      List<String> input1 = Arrays.asList("a", "c", "e");
      List<String> input2 = Arrays.asList();
      List<String> expected1 = Arrays.asList("a", "c", "e");
      assertEquals(null, expected1, ListExamples.merge(input1, input2));    
} 
```   
  
 <br />
 
> ### Step 4 -  Output of running both tests before fixing the bug:


  When we run the aforementioned tests, we get the following output:
  
![Output](Output-for-tests.png)

<br />

> ### Step 5 -  Analyze the output to find the bug:
  
  We can find the bug by analyzing the output of the test results above:
  * Two tests were ran but one of them failed.
  * The **passing input** test passed, however, the **failure inducing input** test caused the Java heap space to run out.
  * The line number that caused this symptom can be found at the very end of the test result, which is line number 33.
  * Line number 33 in my code is the last line of the **failure inducing input** test, however this does not inform us much about the bug.
  * If we look at the second to last line of the test result, we can see that the **line number 42** of the **merge method** caused the heap space to run out.
  * Line number 42 is inside the last **while loop** of the **merge** method, which is as follows:
  
```
while(index2 < list2.size()) {
      result.add(list2.get(index2)); //line 42
      index1 += 1;
} 
```

  * Looking at the code above, we can quickly find the **bug** that since we are updating **index1** instead of **index2**, the while loop never ends.
  * Therefore, **changing the index1 to index2 in line number 43 should fix the bug**.
  
<br />

> ### Step 5 -  Fix the bug:

  * **Code Before:**

``` 
// Takes two sorted list of strings (so "a" appears before "b" and so on),
// and return a new list that has all the strings in both list in sorted order.
static List<String> merge(List<String> list1, List<String> list2) {
      List<String> result = new ArrayList<>();
      int index1 = 0, index2 = 0;<br />
      while(index1 < list1.size() && index2 < list2.size()) {
            if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
            result.add(list1.get(index1));
            index1 += 1;
            }
            else {
                  result.add(list2.get(index2));
                  index2 += 1;
            }
      }
      while(index1 < list1.size()) {
            result.add(list1.get(index1));
            index1 += 1;
      }
      while(index2 < list2.size()) {
            result.add(list2.get(index2));
            index1 += 1; // line 43
      }
      return result;
} 
 ```
 
 <br />
 
  * **Code After:**

``` 
// Takes two sorted list of strings (so "a" appears before "b" and so on),
// and return a new list that has all the strings in both list in sorted order.
static List<String> merge(List<String> list1, List<String> list2) {
      List<String> result = new ArrayList<>();
      int index1 = 0, index2 = 0;<br />
      while(index1 < list1.size() && index2 < list2.size()) {
            if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
                  result.add(list1.get(index1));
                  index1 += 1;
            }
            else {
                  result.add(list2.get(index2));
                  index2 += 1;
      }
      }
      while(index1 < list1.size()) {
            result.add(list1.get(index1));
            index1 += 1;
      }
      while(index2 < list2.size()) {
            result.add(list2.get(index2)); 
            index2 += 1; // line 43
      }
      return result;
} 
```
  
 <br />
  
> ### Step 6 -  Output of both tests after fixing the bug:

![Output](Output-for-fix.png)

<br />
<br />

## **3: Reflect on what I learned**

<br />

In the week 2 and 3's labs, I have learned a lot of new things that I never knew how to do before. During the week 2 lab, I learned how the servers work, how they they take querries, and provide outputs. I also learned how to make my own server and run it remotely, which can let my peers access the server as well. During the week 3 lab, I gained some debugging skills and knowledge about JUnit tests. I learned the importance of taking a systematic approach to fix bugs where you first, test the code with **failure inducing inputs** through JUnit tests, check the **symptoms**, which is described as the unexpected behavior of a code, by looking at the output of these tests, and, finally, finding the bug to fix. Overall, I am glad to learn a lot of new things that will help me a lot in my future both as a computer science student and a software developer.

<br />

# *Thank you for your time!*
