Download Link: https://assignmentchef.com/product/solved-csci-1933-lab-10-stacks-and-exceptions
<br>
<h1>1           Exceptions</h1>

In this lab you will be experimenting with try, catch, and finally statements. Exceptions are used in a program to signal that some error or exceptional situation has occurred, and that it doesn’t make sense to continue the program flow until the exception has been handled.

In Java, exceptions are all objects. An exception can be created like any other object, for example

RuntimeException e = new RuntimeException(“Stack is empty!”). This exception can then be thrown by using the throw e command.

When an exception is thrown, functions on the call stack will fail one at a time until a catch ( RuntimeException e) statement is encountered or the main method is reached and the program crashes. While crashing programs is generally bad, smart use of exceptions can force programmers to handle them and thus avoid errors.

catch (ExceptionType e) statements have the property that they will catch any exceptions that are of the type ExceptionType or <em>a subclasses of that type</em>. Thus catch (Exception e) catches everything since Exception is the base class of all exceptions. Specifying the specific type of exception can be useful, however, in cases where different exceptions should lead to different catch blocks.

finally statements have the property that they will always execute, even after an exception is caught.

Create a class, StackException extends Exception, with the following methods:

<ul>

 <li>StackException(int size) – This is the constructor that will set the variable that keeps track of the size of the stack.</li>

</ul>

<ol start="2">

 <li>A GENERIC STACK CLASS</li>

</ol>

<ul>

 <li>int getSize() – This is the method that will return the size of the stack. This will be helpful in handling exceptions by helping to determine the size of the stack at the time the exception was thrown.</li>

</ul>

<h1>2           A Generic Stack Class</h1>

A stack is an abstract data type which has a “last-in, first-out” structure for data or objects. Your goal is to implement a <em>generic </em>stack data structure that can be flexible in the type of objects stored on the stack.

To start, create your own class, public class Stack&lt;T extends Comparable&lt;T&gt;&gt;, that will allow you to make arrays of generic objects with the following methods:

<ul>

 <li>Stack() – This is the default constructor, it should set the initial size of the stack to 5.</li>

 <li>Stack(int size) – This will initialize the size of the stack to size.</li>

 <li>T pop() – This will remove and return the object at the top of the stack.</li>

 <li>void push(T item)throws StackException – This will add an item to the top of the stack and throw an exception if the stack size is exceeded.</li>

</ul>

Note: The generic type/object “T extends Comparable&lt;T&gt;” means that whatever kind of object T is, it should either implement or inherit from Comparable. Some examples are the Integer, Double, and String classes.

<h1>3           Applying Stacks – Postfix Evaluation</h1>

In this section you will be implementing a postfix evaluation algorithm using your Stack class. Create another class, public class Postfix, that will contain the static double evaluate( String[] expression) method for evaluating a postfix expression.

Here are some examples of normal expressions followed by their array postfix equivalents:

<ol start="4">

 <li>INTEGRATING EXCEPTIONS</li>

</ol>

<table width="0">

 <tbody>

  <tr>

   <td width="138">5 + 2</td>

   <td width="27">=</td>

   <td width="267">{“5”, “2”, “+”}</td>

  </tr>

  <tr>

   <td width="138">1 – 2</td>

   <td width="27">=</td>

   <td width="267">{“1”, “2”, “-“}</td>

  </tr>

  <tr>

   <td width="138">3 + (4 * 5)</td>

   <td width="27">=</td>

   <td width="267">{“4”, “5”, “*”, “3”, “+”}</td>

  </tr>

  <tr>

   <td width="138">(1 + 2)/ (3 + 4)</td>

   <td width="27">=</td>

   <td width="267">{“1”, “2”, “+”, “3”, “4”, “+”, “/”}</td>

  </tr>

 </tbody>

</table>

The pseudocode for the algorithm using a stack is outlined below:

1: <strong>function </strong>Evaluate(<em>expression</em>)

2:              <em>S </em>:= empty stack

3:          <strong>for each </strong><em>token </em>in <em>expression </em><strong>do </strong>4:         <strong>if </strong><em>token </em>is a number <strong>then</strong>

<table width="0">

 <tbody>

  <tr>

   <td width="39">5:</td>

   <td width="307">Push(<em>S,token</em>)</td>

   <td width="270"><em>. </em>push <em>token </em>onto <em>S</em></td>

  </tr>

  <tr>

   <td width="39">6:</td>

   <td width="307"><strong>else</strong></td>

   <td width="270"><em>. token </em>is an operator</td>

  </tr>

  <tr>

   <td width="39">7:</td>

   <td width="307"><em>num</em>1 := Pop(<em>S</em>)</td>

   <td width="270"> </td>

  </tr>

  <tr>

   <td width="39">8:</td>

   <td width="307"><em>num</em>2 := Pop(<em>S</em>)</td>

   <td width="270"> </td>

  </tr>

  <tr>

   <td width="39">9:</td>

   <td width="307">Push(<em>S,num</em>2 (<em>token</em>) <em>num</em>1)</td>

   <td width="270"><em>. </em>here, <em>token </em>is an operator, i.e., +<em>,</em>−<em>,</em>∗<em>,/</em></td>

  </tr>

 </tbody>

</table>

10:                  <strong>end if</strong>

11:          <strong>end for</strong>

12:           <strong>return </strong>top of <em>S</em>

13: <strong>end function</strong>

Some simplifying assumptions

<ul>

 <li>You do not have to worry about parentheses. This is a benefit of postfix notation since it makes it clear about the ordering of operations, compared to the standard infix notation.</li>

 <li>You do not have to worry about dividing by zero. However, think about an appropriate course of action to take should there be one.</li>

 <li>You only have to worry about the four arithmetic operators: <strong>+</strong><em>,−,∗,/</em></li>

 <li>Your method must account for negatives and decimal numbers (e.g. <em>−</em><strong>3</strong><em>.</em><strong>14</strong>)</li>

</ul>

Hint: Your function takes in an array of String. Don’t program something to translate expressions (yet). All you need to do is translate the Strings into their double values, or the appropriate operator, and then evaluate. It may be easiest to hard code the translation of the tokens to the operators.

Milestone 3:

Write a main method to show that your evaluate() method works. Note that in order to get this class to compile, you will have to remove the throws StackException from the method push in the Stack class because the compiler may not let you compile with an unhandled exception. You will add this clause back for step four.

<ol start="4">

 <li>INTEGRATING EXCEPTIONS</li>

</ol>

<h1>4           Integrating Exceptions</h1>

In this section you will be integrating try catch finally statements into the previous step. As you probably noticed, the size of the stack is always fixed. Thus it will not be able to evaluate postfix expressions with too many leading numbers. Do the following:

<ul>

 <li>Restore the “throws StackException” if you had removed it earlier.</li>

 <li>Create a postfix expression that will cause the stack to throw a StackException.</li>

 <li>Catch the exception thrown and print out the size of the stack when the exception occurred.</li>

 <li>Add a finally block that prints ”Evaluation Complete” and be able to explain when this block is executed.</li>

</ul>

Milestone 4:

Modify your main method so that it tries to evaluate an expression that causes a

StackException to be thrown and caught according to the above instructions. Show a TA your code and the resulting output.

<h1>5           Honors Extension: Tower of Hanoi</h1>

<em>This section and milestone are only required for students in the honors section. However, students in other sections are still encouraged to work on this if they are interested and time permits.</em>

5.1       Background

Methods that generate recursive processes make extensive use of a stack, specifically, the system stack. In fact, anytime a method is called, a new stack frame is pushed onto the stack to keep track of that method. For example, if methodA() calls methodB() which then calls methodC(), all three calls will cause an “<strong>activation record</strong>”, or a stack frame, to be pushed onto the system stack. The last method called, in this case, methodC(), will appear on top of the stack, since this is a property of stack data structures. The next is methodB(), then methodA(), in that order on the stack.

On the system stack, an activation record exists for <em>each </em>instance of a method that is active or <em>waiting </em>for another method to complete. In recursion, there will be many activation records/stack frames pushed onto the stack for the same method, since that method is recursively calling itself. In most situations, the main() method will be the first method pushed onto the stack, and calls to other methods will push new activation records on top of main()’s activation record.

Other than the text/instructions of a method’s code, activation records contain all the pertinent information about a specific instance of a method call. When the method is finished, its activation method is popped off the system stack and returns control of the program to its caller, which is

<ol start="5">

 <li>HONORS EXTENSION: TOWER OF HANOI</li>

</ol>

now at the top of the stack.

Typical information contained within an activation record are:

<ul>

 <li><strong>values of all formal parameters</strong></li>

 <li><strong>values of all local (method) variables</strong></li>

 <li><strong>return location – where to resume when returning to the calling method</strong></li>

 <li><strong>some type of reference to the method’s code/instructions</strong></li>

</ul>

Note that the return value from a method call should be kept in a global place where it is available to this activation record, or the the previous activation record, or for processing the final value. Before operating systems used a system stack, it was difficult for programming languages to allow methods to call themselves (i.e., recursion). While recursive calls to methods (whether for an iterative or recursive process) are naturally implemented today using the system stack, they call also be implemented by constructing your own stack. That is what we will do in this week’s lab.

5.2       Files Provided

For this lab, you may use Java’s built-in Stack class, which we already import for you in the resource files. There are a few files provided for this step of lab:

<ul>

 <li>java</li>

 <li>java</li>

 <li>java</li>

 <li>java</li>

</ul>

The first file, ActivationRecord.java, is a simple class which outlines the functionality of classes which can implement recursive functions in an iterative way, by using a stack. The next two files are a completed solution for implementing the factorial function in this way. You can use this as an example and guideline for solving the Tower of Hanoi problem. The provided Hanoi.java is the recursive solution to the classic Tower of Hanoi problem. <strong>Your task is to create the iterative solution by using a stack</strong>, similar to the given factorial implementation.

5.3       First Steps

Create a HanoiR.java file which will contain a class called HanoiR and a main method within, similar to how FactR has been implemented. Include a local stack for activation records using one of the generic stacks from lecture. Not that while you can include a returnValue variable in your class similar to that included in FactR, you will <strong>not </strong>need to use it because the method for solving Tower of Hanoi does not return anything. Rather, it simply prints instructions with System.out .println() directly from the method. The while loop that iterates until the stack is empty will be the same except you will be pushing and running HanoidRecords instead of FactRecords.

<ol start="5">

 <li>HONORS EXTENSION: TOWER OF HANOI</li>

</ol>

5.4         The Long and Short of It

Write an implementation of the ActivationRecord interface that is specific to the Tower of Hanoi problem. Call it HanoiRecord.java. In it, you will create local variables to implement the parameters:

<ul>

 <li>from to represent the source tower</li>

 <li>to to represent the destination tower</li>

 <li>tmp to represent the temporary/spare tower</li>

 <li>count to represent the disk number</li>

</ul>

These local variables are analogous to the input parameters to each call of Hanoi(int n, char source, char dest, char temp), where n is the disk number, source is a source tower, labelled by a letter, dest is the destination tower, and temp is a temporary/spare tower, also labelled with a letter. Write a constructor that accepts the four parameters and have it initialize your local variables accordingly.

After you have implemented the local variables and constructor, implement the run() method. It will be similar to FactRecord’s run() method, but obviously it will be specific to solving the Tower of Hanoid problem. Be careful about where you push() and pop()HanoiRecords as well as how you update the return locations.