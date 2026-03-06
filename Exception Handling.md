## Exception Handling
- [Exception Handling](#exception-handling)
  - [Introduction](#introduction)
  - [Runtime stack mechanism](#runtime-stack-mechanism)
  - [Default exception handling in java](#default-exception-handling-in-java)
  - [Exception Hierarchy](#exception-hierarchy)
    - [Exception](#exception)
    - [Error](#error)
  - [Checked Vs Unchecked Exception](#checked-vs-unchecked-exception)
    - [Fully Checked Vs Partially Checked](#fully-checked-vs-partially-checked)
  - [Customized exception handling by using try catch](#customized-exception-handling-by-using-try-catch)
  - [Control flow in try catch](#control-flow-in-try-catch)
  - [Methods to print Exception information](#methods-to-print-exception-information)
  - [Try With Multiple catch Block](#try-with-multiple-catch-block)
  - [Difference between final,finally,finalize](#difference-between-finalfinallyfinalize)
    - [### Final](#-final)
    - [Finally](#finally)
    - [Finalize()](#finalize)
  - [control flow in try-catch-finally](#control-flow-in-try-catch-finally)
  - [various possible combinations of try catch finally](#various-possible-combinations-of-try-catch-finally)
  - [Throw Keyword](#throw-keyword)
    - [Case](#case)
  - [Throws keyword](#throws-keyword)
    - [Case](#case-1)
  - [Exception handling keywords summary](#exception-handling-keywords-summary)
  - [Various Possible Compile Time Error in Exception Handling](#various-possible-compile-time-error-in-exception-handling)
  - [Customized or User Defined Exception](#customized-or-user-defined-exception)
  - [Top 10 Exception](#top-10-exception)
    - [JVM Exceptions](#jvm-exceptions)
    - [Programmatic Exceptions](#programmatic-exceptions)
    - [List of Top 10 Java Exceptions](#list-of-top-10-java-exceptions)
      - [ArrayIndexOutOfBoundException](#arrayindexoutofboundexception)
      - [NullPointerException](#nullpointerexception)
      - [ClassCasedException](#classcasedexception)
      - [StackOverFlowError](#stackoverflowerror)
      - [NoClassDefFoundError](#noclassdeffounderror)
      - [ExceptionInInitializerError](#exceptionininitializererror)
      - [IllegalArgumentException](#illegalargumentexception)
      - [NumberFormateExceptiion](#numberformateexceptiion)
      - [IllegalStateException](#illegalstateexception)
      - [AssertionError](#assertionerror)
  - [1.7 version enhancements](#17-version-enhancements)
    - [Try-with-Resources](#try-with-resources)
      - [Problems with this Approach](#problems-with-this-approach)
      - [Try-with-Resources (Introduced in Java 1.7)](#try-with-resources-introduced-in-java-17)
      - [Advantages of Try-with-Resources](#advantages-of-try-with-resources)
      - [Conclusion](#conclusion)
    - [Multi-catch Block](#multi-catch-block)
    - [Exception Propagation](#exception-propagation)
    - [Re-throwing Exception](#re-throwing-exception)

### Introduction

An unexpected and unwanted event that disturbs the normal flow of a program is called an `exception`.

Example :- FileNotFoundException, ArrayIndexOutOfBoundsException, etc.

- It is highly recommended to handle exceptions. The main objective of exception handling is the graceful termination of the program.

- Exception handling does not mean repairing an exception. It means providing an alternative way to allow the rest of the program to continue normally. This is the concept of exception handling.

- For example, suppose our programming requirement is to read data from a remote file located in London. At runtime, if the London file is not available, our program should not terminate abnormally. Instead, we should provide a local file so that the rest of the program can continue normally. This way of defining an alternative flow is called `exception handling`.

Example:-
```text
try{
    Read data from remote file locating in london
}
catch(FilenotFoundException e){
    use local file & continue rest of the program normally
}
```

### Runtime stack mechanism

- For every thread, the JVM creates a runtime stack.
- Each method call performed by that thread is stored in the corresponding stack.
- Each entry in the stack is called a stack frame or activation record.
- After completing a method call, the corresponding entry is removed from the stack.
- After completing all method calls, the stack becomes empty, and the JVM destroys that empty stack just before terminating the thread.

Example :- [Image](https://tinyurl.com/55t5fcfd)
```java
class Test{
    public static void main(String[] args){
        doStuff();
    }
    public static void doStuff(){
        doMoreStuff();
    }
    public static void doMoreStuff(){
        System.out.println("Hello");
    }
}
```

### Default exception handling in java

- Inside a method if any exception occurs the method in which it is raised is respoansible to create Exception object by including the following information 
    1. Name of the exception
    1. Description of the exception
    1. Location where the exception occurred (stack trace)

- After creating the exception object, the method hands over the object to the JVM.

- The JVM checks whether the method contains any exception-handling code or not. If the method does not contain exception-handling code, the JVM terminates that method abnormally and removes the corresponding entry from the stack.
- Then, the JVM identifies the caller method and checks whether it contains any exception-handling code.

-  If the caller method does not contain handling code, the JVM terminates that caller method abnormally and removes the corresponding entry from the stack.

- This process continues until the `main` method. If the main method also does not contain exception-handling code, the JVM terminates the main method abnormally and removes its stack entry.

- Then, the JVM hands over the responsibility of exception handling to the `default exception handler`, which is part of the JVM
- The default exception handler prints the exception information in the following format and then terminates the program abnormally:
`This format -> Exception in thread "xyz" <ExceptionName>: <description>
    <stack trace>`

Example 1 :- [Image](https://tinyurl.com/yretbhas)
```java
class Test{
    public static void main(String[] args){
        doStuff();
    }
    public static void doStuff(){
        doMoreStuff();
    }
    public static void doMoreStuff(){
        System.out.println(10/0);
    }
}
```
Output :-
```output
exception in thread "main" java.lang.ArithmeticException : / by zero
at Test.doMoreStuff
at Test.doStuff
at Test.main
```
Example 2 :- 
```java
class Test{
    public static void main(String[] args){
        doStuff();
    }
    public static void doStuff(){
        doMoreStuff();
        System.out.println(10/0);
    }
    public static void doMoreStuff(){
        System.out.println("Hello");
    }
}
```
Output :-
```output
Hello
exception in thread "main" java.lang.ArithmeticException : / by zero
at Test.doStuff
at Test.main
```
Example 3 :-
```java
class Test{
    public static void main(String[] args){
        doStuff();
        System.out.println(10/0);
    }
    public static void doStuff(){
        doMoreStuff();
        System.out.println("Hii");
    }
    public static void doMoreStuff(){
        System.out.println("Hello");
    }
}
```
Output :-
```output
Hello
Hii
exception in thread "main" java.lang.ArithmeticException : / by zero
at Test.main
```

> **NOTE :- 
> - In a program, if at least one method terminates abnormally, then the program termination is considered abnormal termination. 
> - If all methods terminate normally, then the program termination is normal termination.

### Exception Hierarchy 

- The `Throwable` class acts as the root of the Java exception hierarchy.
- The Throwable class defines two child classes.
    1. Exception
        1. RuntimeException
            1. ArithmeticException (AE)
            1. NullPointerException (NPE)
            1. ClassCastException (CCE)
            1. IndexOutOfBoundsException (IOOBE)
                1. ArrayIndexOutOfBoundsException (ArrayIOOBE)
                1. StringIndexOutOfBoundsException (StringIOOBE)
            1. IllegalArgumentException
                1. NumberFormateException
        1. IOException
            1. EOFException
            1. FileNotFoundException
            1. InterruptedIOException
            1. UnsupportedEncodingException
            1. SocketException
            1. MalformedURLException
            1. StreamCorruptedException
            1. SyncFailedException
            1. UTFDataFormatException
            1. WriteAbortedException
        1. ServletException
        1. RemoteException
        1. InterruptedException

    1. Error
        1. VirtualMachineError
            1. StackOverFlowError
            1. OutOfMemeoyError
        1. AssertionError
        1. ExceptionInInitializerError

[Image](https://tinyurl.com/327d6su5)

#### Exception

- Most of the time, exceptions are caused by our program, and these exceptions are recoverable.

- For example, suppose our programming requirement is to read data from a remote file located in London. At runtime, if the remote file is not available, we will get a runtime exception such as `FileNotFoundException`. When this exception occurs, we can provide a local file and continue the rest of the program normally.
```java
try {
    // Read data from a remote file located in London
}
catch (FileNotFoundException e) {
    // Use a local file and continue the rest of the program normally
}
```
This approach allows the program to recover from the exception and proceed gracefully.

#### Error

- Most of the time, errors are not caused by our program. They usually occur due to a lack of system resources, and such errors are non-recoverable.

- For example, if an `OutOfMemoryError` occurs, as programmers we cannot do anything, and the program will terminate abnormally.

- A system administrator or server administrator is responsible for increasing the heap memory.

### Checked Vs Unchecked Exception

|Checked | Unchecked |
|--------| ----------|
| Checked exceptions are exceptions that are checked by the compiler to ensure the smooth execution of a program. | Unchecked exceptions are exceptions that are not checked by the compiler, whether the programmer handles them or not. |
| Examples: `HallTicketMissingException`, `PenNotWorkingException`, `FileNotFoundException`, etc. | Examples: `ArithmeticException`, `NullPointerException`, etc. |
| In our program, if there is a possibility of a checked exception being raised, we must compulsorily handle it—either by using a `try-catch` block or by declaring it with the `throws` keyword. Otherwise, we will get a compile-time | |


> **NOTE :-**
> - Whether an exception is checked or unchecked, every exception occurs only at runtime. There is no chance of an exception occurring at compile time.
> - `RuntimeException` and its child classes, and `Error` and its child classes, are unchecked exceptions. All remaining exceptions are checked exceptions.

#### Fully Checked Vs Partially Checked

| Fully Checked | Partially Checked |
|-------------| ----------------------|
| A checked exception is said to be fully checked if and only if all of its child classes are also checked exceptions. | A checked exception is said to be partially checked if and only if some of its child classes are unchecked exceptions. |
| Examples: `IOException`, `InterruptedException` | Examples: `Exception`, `Throwable` |

> **NOTE :-** The only partially checked exceptions in Java are `Exception` and `Throwable`.

### Customized exception handling by using try catch

- It is highly recommended to handle exceptions.

Code that may raise an exception is called risky code, and we should define that code inside a `try` block. The corresponding handling code should be defined inside a `catch` block.
[Image](https://tinyurl.com/yz2x5x9k )

```java
try{
    // Risky code
}
catch(exception e){
    // Handling Code
}
```

🔴 Example :- Without try-catch
```java
class Test{
    public static void main(String[]args){
        System.out.println("Statement-1");
        System.out.println(10/0);
        System.out.println("Statement-3");
    }
}
```
Output:- Abnormal Termination
```output
Statement-1
Runtime Error: ArithmeticException: 1by zero
```
🟢 Example :- With try-catch
```java
class Test{
    public static void main(String[]args){
        System.out.println("Statement-1");
        try{
            System.out.println(10/0);
        }
        catch(ArithmeticException e){
            System.out.println(10/2);
        }
        System.out.println("Statement-3");
    }
}
```
Output:- Normal Termination
```output
Statement-1
5
Statemnt-3
```
### Control flow in try catch

```java
try{
    statement-1;
    statement-2;
    statement-3;
}
catch(Exception e){
    statement-4;
}
    statement-5;
```

<details>
<summary>
Case 1 :- If there is no exception in the above code, then the output will be
</summary> 

Output:- Normal termination
```output
statement-1
statement-2
statement-3
statement-5
```
</details>

<details>
<summary>
Case 2 :- If an exception is raised at statement-2 and the corresponding catch block matches
</summary>

Output:- Normal termination
```output
statement-1
statement-4
statement-5
```
</details>

<details>
<summary>
Case 3 :- If an exception is raised at statement-2 and the corresponding catch block does not match
</summary>

Output:- Abnormal termination
```output
statement-1
```
</details>

<details>
<summary>
Case 4 :- If an exception is raised at statement-4 or statement-5
</summary>

If an exception is raised at statement-4 or statement-5, then it always results in abnormal termination.
</details>

> **NOTE :-** 
> - Within a try block, if an exception is raised at any point, the remaining statements in the try block will not be executed, even if the exception is handled. Hence, only risky code should be placed inside the try block, and the length of the try block should be as small as possible.
> - In addition to the try block, there is also a possibility of an exception being raised inside the catch and finally blocks.
> - If any statement that is not part of a try block raises an exception, it will always result in abnormal termination.


### Methods to print Exception information

The Throwable class defines the following methods to print exception information.

| Method | Printable Format |
|--------|-------------- |
| `printStackTrace()` | Name of the exception, description, and stack trace |
| `toString()`        | Name of the exception and description               |
| `getMessage()`      | Description only                                    |

Example :- 
```java
class Test{
    public static void main(String[] args){
        try{
            System.out.println(10/0);
        }
        catch(ArthmeticException e){
            System.out.println("--Print Stack Trace--");
            e.printStackTrace();
            System.out.println("--toString--");
            System.out.println(e.toString());
            System.out.println("--getMessage--")
            System.out.println(e.getMessage());
        }
    }
}
```
Output :-
```output
--Print Stack Trace--
java.lang.ArthmeticException: /by zero
at.Test main()

--toString--
java.lang.ArthmeticException: /by zero

--getMessage--
/ by zero
```
> **NOTE :-** Internally, the [default exception handler](#default-exception-handling-in-java) uses the `printStackTrace()` method to print exception information to the console.

### Try With Multiple catch Block

- The way of handling an exception varies from one exception to another. Hence, for each exception type, it is highly recommended to use a separate catch block. That is, using a try block with multiple catch blocks is always possible and recommended.

Example :- Worst Programming Practice
```java
try {
    // Risky code
}
catch (Exception e) {
    // Handle all exceptions in a generic way
}
```

Example :- Best Programming Practice

```java
try {
    // Risky code
}
catch (ArithmeticException e) {
    // Perform an alternative arithmetic operation
}
catch (SQLException e) {
    // Use MySQL DB instead of Oracle DB
}
catch (FileNotFoundException e) {
    // Use a local file instead of a remote file
}
catch (Exception e) {
    // Default exception handling
}
```
This approach improves readability, maintainability, and precise exception handling.

- If a `try` block has multiple `catch` blocks, then the order of the `catch` blocks is very important. We must place the child exception first and then the parent exception later, Otherwise, we will get a compile-time error saying `Exception XYZ has already been caught`.

Example (Wrong Order):

```java
try {
    // risky code
}
catch (Exception e) {
    // generic handling
}
catch (ArithmeticException e) {   // compile-time error
    // specific handling
}
```
Output :- Compile-time Error
```output
Exception java.lang.ArithmeticException has already been caught
```
Example (Correct Order):
```java
try {
    // risky code
}
catch (ArithmeticException e) {
    // specific handling
}
catch (Exception e) {
    // generic handling
}
```
This is because the parent exception can handle all its child exceptions, making the child `catch` block unreachable if placed after the parent.

- We can’t declare two catch blocks for the same exception; otherwise, we will get a compile-time error.

Example :-

```java
try {
    // risky code
}
catch (ArithmeticException e) {
    // specific handling
}
catch (ArithmeticException e) {
    // specific handling
}
```
Output :- Compile-time Error
```output
Exception java.lang.ArithmeticException has already been caught
```


### Difference between final,finally,finalize

#### ### Final

- `final` is a modifier applicable to classes, methods, and variables.

- If a class is declared as `final`, we cannot extend that class.That means we cannot create a child class, so inheritance is not possible for final classes.

- If a method is declared as `final`, we cannot override that method in a child class.

- If a variable is declared as `final`, we cannot reassign a new value to that variable.


#### Finally

- `finally` is a block that is always associated with `try–catch` to maintain cleanup code.

Syntax :-
```java
try{
    // Risky code
}
catch(Exception e){
    // Handling code
}
finally{
    // cleanup code
}
```

- The speciality of the finally block is that it always executes, irrespective of:
    - whether an exception is raised or not, and
    - whether the raised exception is handled or not.


#### Finalize()

- `finalize()` is a method that is invoked by the Garbage Collector just before destroying an object, to perform cleanup activities. 
- Once the `finalize()` method completes, the Garbage Collector immediately destroys that object.

> **NOTE :-**
>- The `finally` block is responsible for performing cleanup activities related to the `try` block. That is, any resources opened inside the `try` block should be closed inside the `finally` block.
>- Whereas the `finalize()` method is responsible for performing cleanup activities related to an object. That is, any resources associated with the object will be deallocated before the object is destroyed by the Garbage Collector using the `finalize()` method.


### control flow in try-catch-finally

- In `try–catch–finally`, the order is important.

- Whenever we write a `try` block, it is mandatory to write either a `catch` block or a `finally` block. Otherwise, we will get a compile-time error. That is, `try` without `catch` or `finally` is invalid.

- Whenever we write a `catch` block, a `try` block is compulsory. That is, `catch` without `try` is invalid.

- Whenever we write a `finally` block, a `try` block is compulsory. That is, `finally` without `try` is invalid. 

- Inside `try`, `catch`, and `finally` blocks, we can declare other `try–catch–finally` blocks. That is, nesting of `try–catch–finally` is allowed.

- For `try`, `catch`, and `finally` blocks, curly braces `{ }` are mandatory.

### various possible combinations of try catch finally

[Image-1](https://tinyurl.com/4jxx4k97)  [Image-2](https://tinyurl.com/k96tfuvm)

🟢 Example 1 :- Correct
```java
try{}
catch(Exception e){}
```

🟢 Example 2 :- ✅ Correct
```java
try{}
catch(NullPointerException e){}
catch(Exception e){}
```
 
🔴 Example 3 :- wrong
```java
try{}
catch(Exception e){}
catch(Exception e){}
```
Output:-
```output
Compiletime error: Exception XYZ has already been caught
```

🟢 Example 4 :- ✅ Correct
```java
try{}
catch(Exception e){}
finally{}
```

🟢 Example 5 :- ✅ Correct
```java
try{}
finally{}
```

🟢 Example 6 :- ✅ Correct
```java
try{}
catch(Exception e){}
try{}
catch(NullPointerException e){}
```

🟢 Example 7 :- ✅ Correct
```java
try{}
catch(Exception e){}
try{}
finally{}
```
🔴 Example 8 :- ❌ Wrong
```java
try{}
```
Output :-
```output
Compiletime error: try without catch or finally
```
🔴 Example 9 :- ❌ Wrong
```java
catch(Exception e){}
```
Output :-
```output
Compiletime error: catch without try
```

🔴 Example 10 :- ❌ Wrong
```java
finally{}
```
Output :-
```output
Compiletime error: finally without try
```
🔴 Example 11 :- ❌ Wrong
```java
try{}
finally{}
catch(Exception e){}
```
Output :-
```output
Compiletime error: finally without try
```
🔴 Example 12 :- ❌ Wrong
```java
try{}
System.out.println("Hello");
catch(Exception e){}
```
Output :-
```output
Compiletime error 1: try without catch or finally
Compiletime error 2: catch without try
```
🔴 Example 13 :- ❌ Wrong
```java
try{}
catch(Exception e){}
System.out.println("Hello");
catch(Exception e){}
```
Output :-
```output
Compiletime error: catch without try
```
🔴 Example 14 :- ❌ Wrong
```java
try{}
catch(Exception e){}
System.out.println("Hello");
finally{}
```
Output :-
```output
Compiletime error: finally without try
```
🔴 
🟢 Example 15 ❌ Wrong ✅ Correct (Nested try–catch)
```java
try{
    try{}
    catch(Exception e){}
}
catch(Exception e){}
```
🔴 Example 16 :- ❌ Wrong
```java
try{
    try{}
}
catch(Exception e){}
```
Output:-
```output
Compiletime error: try without catch or finally
```

🟢 Example 17 :- ✅ Correct
```java
try{
    try{}
    finally{}
}
catch(Exception e){}
```

🟢 Example 18 :- ✅ Correct
```java
try{}
catch(Exception e){
    try{}
    finally{}
}
```
🔴 Example 19 :- ❌ Wrong
```java
try{}
catch(Exception e){
    finally{}
}
```
Output:-
```output
Compiletime error: finally without try
```

🟢 Example 20 :- ✅ Correct
```java
try{}
catch(Exception e){}
finally{
    try{}
    catch(Exception e){}
}
```
🔴 Example 21 :- ❌ Wrong
```java
try{}
catch(Exception e){}
finally{
    finally{}
}
```
Output:-
```output
Compiletime error: finally without try
```
🔴 Example 22 :- ❌ Wrong
```java
try{}
catch(Exception e){}
finally{}
finally{}
```
Output:-
```output
Compiletime error: finally without try
```
🔴 Example 23 :- ❌ Wrong
```java
try
System.out.println("Hello");
catch(Exception e){
    System.out.println("catch");
}
finally{}
```
🔴 Example 24 :- ❌ Wrong
```java
try{}
catch(Exception e)
    System.out.println("Hello");
finally{}
```
🔴 Example 25 :- ❌ Wrong
```java
try{}
catch(Exception e){}
finally
    System.out.println("finally");
```

### Throw Keyword

[Image](https://tinyurl.com/27tfunen)

- Sometimes we can create an exception object explicitly and hand it over to the JVM manually. For this purpose, we have to use the `throw` keyword. [Image](https://tinyurl.com/u4ym99e8)

Syntax :- `throw new ArithmeticException("/ by Zero");`

- Hence, the main objective of the `throw` keyword is to manually hand over a programmer-created exception object to the JVM.

- Hence, the result of the following two programs is exactly the same.
    - In this case, the main method is responsible for creating the exception object and handing it over to the JVM.
   
   🔴 Example 1:-
    ```java
    class Test{
        public static void main(String[]args){
            System.out.println(10/0);
        }
    }
    ```
    Output:-
    ```output
    Exception in thread main java.lang.ArithmeticException: / by zero
    ar Test main()
    ```

    - In this case, the programmer explicitly creates the exception object and hands it over to the JVM manually.
    Example 2:-
    ```java
    class Test{
        public static void main(String[]args){
            throw new ArithmeticException("/ by zero");
        }
    }
    ```
    Output:-
    ```output
    Exception in thread main java.lang.ArithmeticException: / by zero
    ar Test main()
    ```

> **NOTE :-*** The best use of the throw keyword is for user-defined (customized) exceptions.

#### Case

<details>
<summary>
Case 1 throw e
</summary>

If the reference variable `e` points to `null` and we try to use it, a `NullPointerException` will be thrown.

Example 1:-
```java
class Test{
    static ArithmeticException e = new ArithmeticException();
    public static void main(String[]args){
        throw e;
    }
}
```
Output :-
```output
Runtime Error: ArithmeticException
```

Example 2:-
```java
class Test{
    static ArithmeticException e;
    public static void main(String[]args){
        throw e;
    }
}
```
Output :-
```output
Runtime Error: NullPointerException
```
</details>

<details>
<summary>
Case 2
</summary>

After a throw statement, we are not allowed to write any statements directly; otherwise, we will get a `compile-time error saying unreachable statement`.

Example 1:-
```java
class Test{
    public static void main(String[]args){
        System.out.println(10/0);
        System.out.println("Hello");
    }
}
```
Output :-
```output
Runtime error ArithmeticException: / by zero
```
Example 2:-
```java
class Test{
    public static void main(String[]args){
        throw new ArithmeticException("/ by zero");
        System.out.println("Hello");
    }
}
```
Output :-
```output
Compiletime error unreachable statement
```
</details>

<details>
<summary>
Case 3
</summary>

We can use the `throw` keyword only with objects of type `Throwable` (or its subclasses). If we try to use `throw` with a normal Java object, we will get a `compile-time error saying incompatible types`.

Example 1:-
```java
class Test{
    public static void main(String[]args){
        throw new Test();
    }
}
```
Output :-
```output
Compiletime error: incompatible types found: Test required: java.lang.Throwable
```
Example 2:-
```java
class Test extends RuntimeException{
    public static void main(String[]args){
        throw new Test();
    }
}
```
Output :-
```output
Runtime exception in thread main Test
at Test.main()
```
</details>

### Throws keyword

In a program, if there is a possibility of raising a checked exception, it must be handled; otherwise, we will get a compile-time error stating: `unreported exception XXX; must be caught or declared to be thrown`

🔴 Example 1:- Without try-catch
```java
class Test{
    public static void main(String[]args){
        PrintWriter pw = new PrintWriter("abc.txt");
        pw.println("hello");
    }
}
```
Output :-
```output
compiletime error: unreputted exception java.io.FileNotFoundException, must be caught or declared to be thrown
```
🔴 Example 2:- Without try-catch
```java
class Test{
    public static void main(String[]args){
        Thread.sleep(10000);
    }
}
```
Output :-
```output
compiletime error: unreputted exception java.lang.InterruptedException, must be caught or declared to be thrown
```
🟢 Example 3:- With try-catch
```java
class Test{
    public static void main(String[]args){
        try{
            Thread.sleep(10000);
        }
        catch(InterruptedException e){
            System.out.println(e);
        }
    }
}
```
- We can use the `throws` keyword to delegate the responsibility of exception handling to the caller (which may be another method or the JVM). In this case, the caller method becomes responsible for handling the exceptio.

🟢 Example 4:- By using throws Kewywords
```java
class Test{
    public static void main(String[]args)throws InterruptedException {
            Thread.sleep(10000);
    }
}
```
- The `throws` keyword is required only for checked exceptions. Using the `throws` keyword for unchecked exceptions has no use or impact.
- The `throws` keyword is used only to satisfy the compiler. Its usage does not prevent abnormal termination of the program.

🟢 Example 4:- By using throws Kewywords
```java
class Test{
    public static void main(String[]args)throws InterruptedException {
        doStuff();
    }
    public static void doStuff()throws InterruptedException {
            doMoreStuff();
    }
    public static void doMoreStuff()throws InterruptedException {
            Thread.sleep(10000);
    }
}
```
- In the above program, if we remove at least one throws statement, the code will not compile.

[Image](https://tinyurl.com/yvr8jnsm)

> **NOTE :-** it is recommended to use try catch over throws keyword

#### Case

<details>
<summary>
Case 1
</summary>

We can use the `throws` keyword with methods and constructors, but not with classes.

🔴 Example :-
```java
class Test throws Exception{
    Test() throws Exception{}
    public void m1() throws Exception{}
}
```
</details>

<details>
<summary>
Case 2
</summary>

We can use the `throws` keyword only with `Throwable` types. If we try to use it with normal Java classes, we will get a compile-time error stating incompatible types.

🔴 Example :-
```java
class Test {
    public void m1() throws Test{}
}
```
Output :-
```output
comipletime error: incomppotible types found Test required: Java.lang.Throwable
```

🟢 Example :-
```java
class Test extends RuntimeException{
    public void m1() throws Test{}
}
```
</details>

<details>
<summary>
Case 3
</summary>

🔴 Example :- Checked
```java
class Test{
    public static void main(String[]args){
        throw new Exception();
    }
}
```
Output :-
```output
Compiletime Error:- unreputted exception java.lang.Exception must be caught or declared to be thrown
```
🔴 Example :- Unchecked
```java
class Test{
    public static void main(String[]args){
        throw new Error();
    }
}
```
Output :-
```output
Runtime Error:- Exception in thread main java.lang.Error
at Test.main()
```
</details>

<details>
<summary>
Case 4
</summary>

- Within a try block, if there is no possibility of an exception being raised, we cannot write a catch block for that exception. Otherwise, we will get a compile-time error stating:

`Exception XXX is never thrown in the body of the corresponding try statement.`

However, this rule is applicable only to fully checked exceptions.

🟢 Example :-
```java
class Test{
    public static void main(String[]args){
        try{
            System.out.println("Hello");
        }
        catch(ArithmeticException e){}
    }
}
```
Output :-
```output
Hello
```
🟢 Example :-
```java
class Test{
    public static void main(String[]args){
        try{
            System.out.println("Hello");
        }
        catch(Exception e){}
    }
}
```
Output :-
```output
Hello
```
🔴 Example :-
```java
import java.io.*;
class Test{
    public static void main(String[]args){
        try{
            System.out.println("Hello");
        }
        catch(IOException e){}
    }
}
```
Output :-
```output
Compiletime error: exception java.io.IOException is never throw in body of corresponding try statement
```
🔴 Example :-
```java
class Test{
    public static void main(String[]args){
        try{
            System.out.println("Hello");
        }
        catch(InterruptedException e){}
    }
}
```
Output :-
```output
Compiletime error: exception java.io.InterruptedException is never throw in body of corresponding try statement
```
🟢 Example :-
```java
class Test{
    public static void main(String[]args){
        try{
            System.out.println("Hello");
        }
        catch(Error e){}
    }
}
```
Output :-
```output
Hello
```
</details>

### Exception handling keywords summary

- `try` → Used to maintain risky code
- `catch` → Used to maintain exception-handling code
- `finally` → Used to maintain cleanup code
- `throw` → Used to manually hand over a created exception object to the JVM
- `throws` → Used to delegate the responsibility of exception handling to the caller

### Various Possible Compile Time Error in Exception Handling

- unreported exception XXX; must be caught or declared to be thrown
- exception XXX has already been caught
- exception XXX is never thrown in the body of the corresponding try statement
- unreachable statement
- incompatible types: found: Test, required: java.lang.Throwable
- try without catch or finally
- catch without try
- finally without try

### Customized or User Defined Exception

- Sometimes, to meet programming requirements, we can define our own exceptions. Such exceptions are called **Customized Exceptions or User-Defined Exceptions**.

Example :- TooYoungException, TooOldException, InsufficientFundsException

```java
class TooYoungException extends RuntimeException {
    TooYoungException(String message) {
        super(message);
    }
}

class TooOldException extends RuntimeException {
    TooOldException(String message) {
        super(message); // to make description available to default exception handler
    }
}

class CustomExceptionDemo {
    public static void main(String[] args) {
        int age = Integer.parseInt(args[0]);

        if (age < 18) {
            throw new TooYoungException(
                "You are too young. Please wait for some more time."
            );
        } 
        else if (age > 60) {
            throw new TooOldException(
                "Your age has crossed the marriage limit."
            );
        } 
        else {
            System.out.println(
                "You will receive match details soon via email!"
            );
        }
    }
}
```
> - The `throw` keyword is best suited for user-defined (customized) exceptions, but not recommended for predefined exceptions.
> - It is highly recommended to define customized exceptions as unchecked exceptions; therefore, we should extend `RuntimeException`, not `Exception`.

### Top 10 Exception

Based on the person who raises an exception, all exceptions are divided into two categories:
1. [JVM Exceptions](#jvm-exceptions)
2. [Programmatic Exceptions](#programmatic-exceptions)

#### JVM Exceptions
Exceptions that are raised automatically by the JVM whenever a particular runtime event occurs are called **JVM exceptions**.

Examples:
ArithmeticException, NullPointerException, etc.

#### Programmatic Exceptions
Exceptions that are raised explicitly either by the **programmer** or by the **API developer** to indicate that something has gone wrong are called **programmatic exceptions**.

Examples:
TooOldException, IllegalArgumentException, etc.

#### List of Top 10 Java Exceptions
1. ArrayIndexOutOfBoundException
2. NullPointerException
3. ClassCasedException
4. StackOverFlowError
5. NoClassDefFoundError
6. ExceptionInInitializerError
7. IllegalArgumentException
8. NumberFormateExceptiion
9. IllegalStateException
10. AssertionError

##### ArrayIndexOutOfBoundException

- It is a child class of `RuntimeException`; hence, it is an unchecked exception.
- It is raised automatically by the JVM whenever we try to access an array element using an index that is out of range.
  
Example :-
```java
int[] arr = new int[4];

System.out.println(arr[0]);    // valid
System.out.println(arr[10]);   // RuntimeException: ArrayIndexOutOfBoundsException
System.out.println(arr[-10]);  // RuntimeException: ArrayIndexOutOfBoundsException
```
##### NullPointerException

- It is a child class of `RuntimeException`; hence, it is an unchecked exception.
- It is raised automatically by the JVM whenever we try to perform any operation on a null reference.

🔴 Example :-
```java
String s = null;
System.out.println(s.length()); // RuntimeException: NullPointerException
```

##### ClassCasedException

- It is a child class of `RuntimeException`; hence, it is an unchecked exception.
- It is raised automatically by the JVM whenever we try to typecast a parent object to a child type.

🟢 Example :-
```java
String string = new String("Raj");
Object obj = (Object) string;
```
🔴 Example :-
```java
Object obj = new Object();
String s = (String) obj; // RuntimeException: ClassCastException
```
🟢 Example :-
```java
Object obj = new String("Raj");
String s = (String) obj;
```

##### StackOverFlowError

- It is a child class of `Error`; hence, it is an unchecked throwable.
- It is raised automatically by the JVM whenever we try to perform infinite or deep recursive method calls, which exhaust the call stack.

🔴 Example :-
```java
class Test{
    public static void m1(){
        m2();
    }
    public static void m2(){
        m1();
    }
    public static void main(String[]args){
        m1();
    }
}
```
Output :-
```output
Exception in thread "main" java.lang.StackOverflowError

```
#####  NoClassDefFoundError

- It is a child class of `Error`; hence, it is an unchecked throwable.

- It is raised automatically by the JVM whenever the JVM is unable to find the required `.class` file.

##### ExceptionInInitializerError

- It is a child class of `Error`; hence, it is an unchecked throwable
- It is raised automatically by the JVM if any exception occurs while executing **static variable initialization** or **static blocks**.

🔴 Example :-
```java
class Test{
    static int x = 10/0;
}
```
Output :-
```output
RE: Exception in thread "main" java.lang.ExceptionInInitializerError
Caused by: java.lang.ArithmeticException: / by zero

```

🔴 Example :-
```java
class Test{
    static {
        String s = null;
        System.out.println(s.length());
    }
}
```
Output :-
```output
RE: Exception in thread "main" java.lang.ExceptionInInitializerError
Caused by: java.lang.NullPointerException
```

##### IllegalArgumentException

- It is a child class of `RuntimeException`; hence, it is an unchecked exception.
- It is raised explicitly either by the programmer or by the API developer to indicate that a method has been invoked with an illegal or invalid argument.

Exaample :-
The valid range of thread priorities is 1 to 10. If we try to set the priority to any other value, a runtime exception (`IllegalArgumentException`) is thrown.
```java
Thread t = new Thread();
t.setPriority(7);   // valid
t.setPriority(15);  // RuntimeException: IllegalArgumentException
```

##### NumberFormateExceptiion

- It is a direct child class of `IllegalArgumentException`, which itself is a child class of `RuntimeException`; hence, it is an unchecked exception.
- It is raised explicitly either by the programmer or by the API developer to indicate that we are trying to convert a string into a number, but the string is not properly formatted.

Example :-
```java
int i = Integer.parseInt("10");
int i = Integer.parseInt("ten"); // RuntimeException: NumberFormateExceptiion
```
##### IllegalStateException

- It is a child class of `RuntimeException`; hence, it is an unchecked exception.
- It is raised explicitly either by the programmer or by the API developer to indicate that a method has been invoked at the wrong time.

Example :-
After starting a thread, we are not allowed to start the same thread again. If we do so, a runtime exception (`IllegalStateException`) is thrown.
```java
Thread t = new Thread();
t.start();

t.start(); // RuntimeException: IllegalStateException

```

##### AssertionError

- It is a child class of `Error`; hence, it is an unchecked throwable.
- It is raised explicitly either by the programmer or by the API developer to indicate that an `assert` statement has failed.
 
Example :-
```java
int x = 5;
assert x > 10;  // AssertionError if the condition is false
```
Output :- If x is not greater than 10, the JVM throws a runtime error:
```output
java.lang.AssertionError
```

[Summary](https://tinyurl.com/2u7p2ws8)


### 1.7 version enhancements

As part of Java 1.7, the following two concepts were introduced in exception handling:
1. [Try-with-Resources](#try-with-resources)
2. [Multi-catch Block](#multi-catch-block)


#### Try-with-Resources

- Up to Java 1.6, it was highly recommended to write a `finally` block to close resources that were opened as part of the `try` block. 

Code :- 1.6 version
```java
BufferedReader br = null;
try {
    br = new BufferedReader(new FileReader("input.txt"));

    // Use BufferedReader as required
}
catch (IOException e) {
    // Handling code
}
finally {
    if (br != null) {
        br.close();
    }
}
```
##### Problems with this Approach
- The programmer is compulsorily required to close resources inside the finally block, which increases programming complexity.

- Writing the finally block is mandatory, which increases code length and reduces readability.

##### Try-with-Resources (Introduced in Java 1.7)

- To overcome the above problems, Sun Microsystems introduced the Try-with-Resources feature in Java 1.7.

##### Advantages of Try-with-Resources
- Any resource opened as part of the `try` block will be closed automatically once control reaches the end of the try block, either normally or abnormally.
- The programmer is not required to close resources explicitly, which reduces programming complexity.
- There is no need to write a `finally` block, so the code length is reduced and readability is improved.

Code :- 1.7 version
```java
try (BufferedReader br = new BufferedReader(new FileReader("input.txt"))) {
    // Use BufferedReader as required
}
catch (IOException e) {
    // Handling code
}
```

##### Conclusion

We can declare multiple resources in a try-with-resources statement, and these resources must be separated by semicolons (`;`).

Synatx :- 
```java
try (Resource1; Resource2; Resource3) {
    // code
}
```

Example :-
```java
try (
    FileWriter fw = new FileWriter("Output.txt");
    FileReader fr = new FileReader("Input.txt")
) {
    // Use FileWriter and FileReader
}
```
- All resources must be AutoCloseable.
- A resource is said to be AutoCloseable if and only if its corresponding class implements the `java.lang.AutoCloseable` interface.
- All I/O-related resources, database-related resources, and network-related resources already implement the AutoCloseable interface.
- As programmers, we are not required to do anything special; we just need to be aware of this fact.
- The `AutoCloseable` interface was introduced in Java 1.7 and contains only one method:
```java
public void close() throws Exception;
```

- All resource reference variables declared in a try-with-resources statement are implicitly `final`.
- Hence, within the `try` block, we cannot reassign these variables; otherwise, we will get a compile-time error.

Code :-
```java
import java.io.*;
class TryWithResources{
    public static void main(String[]args)throws Exception
    {
        try(BufferedReader br = new BufferedReader(new FileReader("input.txt"))){
            br = new BufferedReader(new FileReader("output.txt"));
        }
    }
}
```
Output :-
```output
Compiletime Error: auto-closeable resource br may not be assigned
```
- Until Java 1.6, a `try` block must be associated with either a `catch` block or a `finally` block.
- From Java 1.7 onwards, we can use try-with-resources without writing either `catch` or `finally`.
```java
try (Resource) {
    // code
}
```
- The main advantage of try-with-resources is that we are not required to write a `finally` block explicitly.
- Resources opened inside the `try` block are closed automatically, so we are not responsible for closing them explicitly.
- Hence, until Java 1.6, the `finally` block played a crucial role in closing resources,
but from Java 1.7 onwards, its usage for resource closing has been significantly reduced.


#### Multi-catch Block

- Until Java 1.6, even if multiple different exceptions required the same handling code, we had to write separate catch blocks for each exception.

This increased the length of the code and reduced readability.

code :-
```java
try {
    // code
}
catch (ArithmeticException e) {
    e.printStackTrace();
}
catch (IOException e) {
    e.printStackTrace();
}
catch (NullPointerException e) {
    System.out.println(e.getMessage());
}
catch (InterruptedException e) {
    System.out.println(e.getMessage());
}
``` 
- To overcome this problem, Sun Microsystems introduced the multi-catch block in Java 1.7.
- Using multi-catch, a single catch block can handle multiple different exception types that require the same handling logic.

```java
try {
    // code
}
catch (ArithmeticException | IOException e) {
    e.printStackTrace();
}
catch (NullPointerException | InterruptedException e) {
    System.out.println(e.getMessage());
}
```
- The main advantage of this approach is that the length of the code is reduced and readability is improved.

Example :- 
```java
import java.io.*;
class MultiCatchBlock{
    public static void main(String[]args){
        try{
            System.out.println(10/0);
            String s = null;
            System.out.println(s.length());
        }
        catch(ArithmeticException | NullPointerException e ){
            System.out.println(e);
        }
    }
}
```
- In the above example, whether the raised exception is an ArithmeticException or a NullPointerException, the same catch block will be executed.

- In a multi-catch block, there must not be any relationship between the exception types
(parent–child, child–parent, or same type).

Otherwise, we will get a compile-time error.
```java
try{
    // risky code
}
catch(ArithmeticException | Exception e){
    e.printStackTrace();
}

```
Output :-
```output
Compile-time error:
Alternatives in a multi-catch statement cannot be related by subclassing
```


#### Exception Propagation

Inside a method, if an exception is raised and it is not handled, the exception object is automatically propagated to the caller method.
The caller method is then responsible for handling the exception.
This process is called Exception Propagation.

#### Re-throwing Exception
Using this approach, we can catch one exception and throw another exception, thereby converting one exception type into another exception type.
```java
try{
    System.out.println(10/0);
}
catch(ArithmeticException e){
    throw new NullPointerException();
}
```
