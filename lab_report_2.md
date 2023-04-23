# Lab Report 2

## **Objectives:**

1. Write a web server.

2. Analyze a bug from Lab 3.

3. Reflect on what I learned.

## **1: Write a web server**

> ### Step 1 -  Installing VScode:


  * Go to [VScode](https://code.visualstudio.com).
  * Select your operating system from the dropdown list.
  
      <img src="vscod.png" width="200" height="180">
  
  * Follow the instructions to download and install VScode.
   
*(If you are not using Windows operating system, skip to Step 2.)*
  * Download and install [Git for Windows](https://gitforwindows.org).
  * Follow the steps on this [link](https://stackoverflow.com/questions/42606837/how-do-i-use-bash-on-windows-from-the-visual-studio-code-integrated-terminal/50527994#50527994) to learn how to use Bash on VScode.

> ### Step 2 - Remotely Connecting


  * Open the Terminal window on VScode, using ctrl or command + ` or by clicking on Terminal -> New Terminal menu option.
  
      <img src="terminal.png" width="400" height="200">
      
  * Copy and paste (or type) the following command on your Terminal window: `ssh cs15lsp23zz@ieng6.ucsd.edu`
 
      <img src="ssh.png" width="500" height="120">
      
  * Replace "zz" in the command with the letters in your course-specific account and press Enter.
  * You will be prompted to enter your account password, type in your password and press Enter.
  
      <img src="password.png" width="500" height="140">
      
  * Congratulations! Now, you're remotely connected to your account.
     
      <img src="connected.png" width="600" height="220">
      
> ### Step 3 - Trying some commands


*(Note: Prior to performing the following steps, if your terminal is open, kill the Terminal to avoid the 'Permission Denied' error.)*
      
## **2: Analyze a bug from Lab 3**

> ### Step 1 -  Choose a bug from Lab 3:

I am choosing an **'infinite loop' bug** I found in the "merge" method of the file named "ListExamples.java", the original code for which is as follows:
<br />

<code>// Takes two sorted list of strings (so "a" appears before "b" and so on),<br /><br />
 // and return a new list that has all the strings in both list in sorted order.<br /><br />
  static List<String> merge(List<String> list1, List<String> list2) {<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;List<String> result = new ArrayList<>();<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;int index1 = 0, index2 = 0;<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;while(index1 < list1.size() && index2 < list2.size()) {<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if(list1.get(index1).compareTo(list2.get(index2)) < 0) {<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;result.add(list1.get(index1));<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;index1 += 1;<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;else {<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;result.add(list2.get(index2));<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;index2 += 1;<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;}<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;while(index1 < list1.size()) {<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;result.add(list1.get(index1));<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;index1 += 1;<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;}<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;while(index2 < list2.size()) {<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;result.add(list2.get(index2));<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;index1 += 1;<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;}<br /><br />
  &nbsp;&nbsp;&nbsp;&nbsp;return result;<br /><br />
  }</code>
 <br />
 <br />
> ### Step 2 -  Failure inducing input:
  An example of a **failure inducing input** (as a JUnit test) where we try to merge two sorted ArrayLists is as follows:
  <br />
  
  <code>@Test<br />
  public void testMerge(){<br />
  &nbsp;&nbsp;&nbsp;&nbsp;// inputs<br />
  &nbsp;&nbsp;&nbsp;&nbsp;List<String> input1 = Arrays.asList("a", "c", "e");<br />
  &nbsp;&nbsp;&nbsp;&nbsp;List<String> input2 = Arrays.asList("b", "d", "f");<br />
  &nbsp;&nbsp;&nbsp;&nbsp;List<String> expected1 = Arrays.asList("a", "b", "c", "d", "e", "f");<br />
  &nbsp;&nbsp;&nbsp;&nbsp;assertEquals(null, expected1, ListExamples.merge(input1, input2));<br />    
  }</code>
  <br />
 <br />
> ### Step 3 -  Passing input:
  An example of an **input that doesn't cause failure** (as a JUnit test) where we try to merge two sorted ArrayLists is as follows:
  <br />
  
  <code>@Test<br />
  public void testMerge1(){<br />
  &nbsp;&nbsp;&nbsp;&nbsp;// inputs<br />
  &nbsp;&nbsp;&nbsp;&nbsp;List<String> input1 = Arrays.asList("a", "c", "e");<br />
  &nbsp;&nbsp;&nbsp;&nbsp;List<String> input2 = Arrays.asList();<br />
  &nbsp;&nbsp;&nbsp;&nbsp;List<String> expected1 = Arrays.asList("a", "c", "e");<br />
  &nbsp;&nbsp;&nbsp;&nbsp;assertEquals(null, expected1, ListExamples.merge(input1, input2));<br />     
  }</code>   
 <br />
 <br />
> ### Step 4 -  Output of running both tests:
  When we run the aforementioned tests, we get the following output:
 
      <img src="Output-for-tests.png" width="300" height="110">
  

## **3: Reflect on what I learned**

  * To see your current working directory, type the command: `pwd`
  
       <img src="pwd.png" width="500" height="280">
  
  * To list the contents in this directory, type the command: `ls`

       <img src="ls.png" width="500" height="300">

  * To print out the contents of a text file, type the command: `cat helloworld.txt` (Note: file name might be different for you)
 
       <img src="cat.png" width="500" height="320">

 
> ## Congratulations! you have successfully completed all of the objectives.
