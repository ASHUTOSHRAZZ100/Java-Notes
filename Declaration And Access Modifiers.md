## Declaration And Access Modifiers
1. [Java Source File Structure](#java-source-file-structure)
2. [Class Level Modifiers](#class-level-modifiers)
3. [Member Level Modifiers](#member-modifiers-method-or-variable-level-modifiers)
4. [Interfaces](#interfaces)

### Java Source File Structure

A java Can contain any nunber of a class but at most one class as public. If there is public class then name of the programme and the name of the public class must be matched otherwise we will get compile time error.

1. **Example**
```java
class A{}
class B{}
class C{}
```
#### Case
<details>
<summary>
Case 1
</summary>

If there is no public class, we can give any name to the source file there is no restriction.

Example: `A.java`, `B.java`, `C.java`, `Durga.java`.
</details>

<details>
<summary>
Case 2
</summary>

If class `B` is public, then the name of the program file must be `B.java`. Otherwise, we will get a compile-time error saying:
`Class B is public, should be declared in a file named B.java.`
</details>

<details>
<summary>
Case 3
</summary>

If both classes `B` and `C` are declared as public and the program file is named `B.java`, then we will get a compile-time error saying:
`Class C is public, should be declared in a file named C.java.`
</details>


2. **Example :-** file name Durga.java

```java
class A{
    public static void main(String[] args) {
        System.out.println("A class main method");
    }
}

class B{
    public static void main(String[] args) {
        System.out.println("B class main method");
    }
}

class C{
    public static void main(String[] args) {
        System.out.println("C class main method");
    }
}
class D{
}
```
javac Durga.java if we compile it will give A.class, B.class, C.class, D.class

Output:-
- Command: `java A`
```output
A class main method
```
- Command: `java B`
```output
B class main method
```
- Command: `java C`
```output
C class main method
```
- Command: `java D`
```java
RuntimeError NoSuchMethodError: Main
```
- Command: `java Durga`
```output
RuntimeError NoClassDefFoundError : Durga
```
#### Conclusion

<details>
<summary>
Conclusion 1
</summary>

Whenever we compile a Java program, a separate `.class` file will be generated for every class present in the program.
</details>

<details>
<summary>
Conclusion 2
</summary>

We compile a Java program (source file), but we run a Java `.class` file.
</details>

<details>
<summary>
Conclusion 3
</summary>

Whenever we execute a Java class, the corresponding class’s main method will be executed.
    - If the class does not contain a main method, we will get a runtime exception: `NoSuchMethodError: main`.
    - If the corresponding .class file is not available, we will get a runtime exception: `NoClassDefFoundError`.
</details>

<details>
<summary>
Conclusion 4
</summary>

It is not recommended to declare multiple classes in a single source file. It is highly recommended to declare only one class per source file, and the name of the program file should be the same as the class name.
</details>

### Types of Import statements
1. [Explicit class Import](#explicit--class-import)
2. [Implicit class Import](#implicit-class-import)

### Explicit  Class Import

**Syntax** :- `Packagename.ClassName;`

**Example** :- `import java.util.ArrayList;`  
It is highly recommended to use an explicit class import because it improves the readability of the code. This approach is best suited for professional environments where readability and maintainability are important.

### Implicit class Import

**Syntax** :- `Packagename.*;`

**Example** :- `import java.util.*;`  
It is not recommended to use the wildcard import because it reduces the readability of the code.  
It is more suitable in situations where typing convenience is more important than code clarity.

<details>
<summary>
Case 1
</summary>

| Which of the following statements are meaningful? | Status    |
| --------- | --------- |
| `import java.util.ArrayList;`                     | ✅ Valid   |
| `import java.util.ArrayList.*;`                   | ❌ Invalid |
| `import java.util.*;`                             | ✅ Valid   |
| `import java.util;`                               | ❌ Invalid |
</details>

<details>
<summary>
Case 2
</summary>

Consider the following code:
```java
class MyObject extends java.rmi.server.UnicastRemoteObject {

}

```
The code compiles successfully even though we are not writing an `import` statement because we have used the fully qualified name (`java.rmi.server.UnicastRemoteObject`).

> **NOTE :-** Whenever we use a fully qualified name, it is not required to write an `import` statement.
>Similarly, whenever we write an `import` statement, it is not required to use the fully qualified name.
</details>

<details>
<summary>
Case 3
</summary>

```java
import java.util.*;
import java.sql.*;

class Test {
    public static void main(String[] args) {
        Date d = new Date();
    }
}
```
Output :-
```output
Compile-time error: reference to Date is ambiguous
```

> **NOTE :-** Even in the case of `List`, we may get the same ambiguity problem because it is available in both the `java.util` and `java.awt` packages.
> - `java.util.List` (Interface)
> - `java.awt.List` (Class) 
</details>


<details>
<summary>
Case 4
</summary>

While resolving class names, the compiler always gives precedence in the following order:
- Explicit class import
- Class present in the current package (current working directory / default package)
- Implicit class import (`java.lang.*`)

Example :-
```java
import java.util.Date;
import java.sql.*;

class Test {
    public static void main(String[] args) {
        Date d = new Date();
        System.out.println(d.getClass().getName());
    }
}
```
Output :-
```output
java.util.Date
```
In the above example, the compiler selects the `Date` class from the `java.util` package.
</details>

<details>
<summary>
Case 5
</summary>

Whenever we import a Java package, all the classes and interfaces present in that package become available by default.
However, subpackage classes are not imported automatically.  
If we want to use a class from a subpackage, we must write the `import` statement up to the subpackage level.
```css
java
 └── util
      └── regex
           └── Pattern
```
To use the Pattern class in our program, which import statement is required?

1. import java.*; ❌
2. import java.util.*; ❌
3. import java.util.regex.*; ✅
4. No import required ❌
</details>

<details>
<summary>
Case 6
</summary>

All classes and interfaces present in the following packages are available by default to every Java program. Hence, we are not required to write an `import` statement:
1. `java.lang` package
2. Current package (current working directory)
</details>

<details>
<summary>
Case 7
</summary>

import statements are totally a compile-time-related concept.
If there are more import statements, the compile time may increase slightly, but there is no effect on execution time (runtime).
</details>

<details>
<summary>
Case 8
</summary>

Difference between C language #include and Java import statement 
- In the case of the C language, `#include` loads the required header files at the beginning (during translation time). Hence, it is considered a static include.
- In the case of Java, the `import` statement does not load any `.class` file at the beginning.  
Whenever we use a particular class, only then is the corresponding `.class` file loaded.  
This is called dynamic loading, load on demand, or load on the fly.
</details>

> **NOTE :-** Java 1.5 version new features
> 1. Enhanced for-loop (for-each loop)
> 1. Var-args methods (variable-length argument methods)
> 1. Autoboxing & Autounboxing
> 1. Generics
> 1. Covariant return types
> 1. Queue interface
> 1. Annotations
> 1. enum types
> 1. [Static import](#static-import)

### Static Import

- Introduced in Java 1.5.
- According to Sun Microsystems, the usage of `static import` reduces the length of the code and can improve readability.
- However, according to worldwide programming experts, excessive use of `static import` can create confusion and reduce readability.
- Recommendation: Use `static import` only when there is a specific requirement.

Example :- Without static import
```java
class Test {
    public static void main(String[] args) {
        System.out.println(Math.sqrt(4));
        System.out.println(Math.max(4, 9));
        System.out.println(Math.random());
    }
}
```
Output :-
```output
2.0
9
0.23456789012345678   // Example random value
```

Example :- With static import
```java
import static java.lang.Math.sqrt;
import static java.lang.Math.*;  // Imports all static members of Math

class Test {
    public static void main(String[] args) {
        System.out.println(sqrt(4));
        System.out.println(max(4, 9));
        System.out.println(random());
    }
}
```
Output :-
```output
2.0
9
0.23456789012345678   // Example random value
```

Usually, we access static members by using the class name.
However, when we use static import, we can access static members directly without using the class name.

#### Explain About `System.out.println()`

First, let us understand it using a simple example.

Example 1:
```java
class Test {
    static String s = "java";
}
```
```text
Test.s.length()
```
Explanation:
- `Test` → `Test` is the class name.
- `s` → `s` is a static variable present in the `Test` class of type `java.lang.String`.
- `length()` → `length()` is a method present in the `String` class.


Now, let us understand `System.out.println()`.

Simplified Representation:
```java
class System {
    static PrintStream out;
}
```
```text
System.out.println()
```
Explanation:
- `System` → `System` is a class present in the `java.lang` package.
- `out` → `out` is a static variable present in the `System` class of type `PrintStream`.
- `println()` → `println()` is a method present in the `PrintStream` class.

`out` is a static variable present in the `System` class. Hence, we can access it by using the class name `System`.  
However, when we use static import, it is not required to use the class name. We can access `out` directly.

🟢Example :-  
```java
import static java.lang.System.out;

class Test {
    public static void main(String[] args) {
        out.println("Hello");
        out.println("Hii...");
    }
}
```
Output :-
```output
Hello
Hii...
```

🔴Example :-
```java
import static java.lang.Integer.*;
import static java.lang.Byte.*;

class Test {
    public static void main(String[] args) {
        System.out.println(MAX_VALUE);
    }
}
```
Output :-
```output
Compile-time error: reference to MAX_VALUE is ambiguous
```

While resolving static members, the compiler always gives precedence in the following order:
- Current class static members
- Explicit static import
- Implicit static import

Example :-
```java
import static java.lang.Integer.MAX_VALUE;  // (2)
import static java.lang.Byte.*;

class Test {
    static int MAX_VALUE = 999;  // (1)

    public static void main(String[] args) {
        System.out.println(MAX_VALUE);
    }
}
```
Output :-
- Since the current class Test contains MAX_VALUE = 999, it has the highest priority.
```output
999
```
- If we `comment line (1)`, then the explicit static import will be considered. Hence, `Integer.MAX_VALUE` will be used, and in this case, the output will be `2147483647`.
```output
2147483647
```
- If we `comment both lines (1) and (2)`, then the implicit static import will be considered. In this case, the output will be `127` (`Byte.MAX_VALUE`).
```output
127
```

| **Normal Import**  | **Static Import**      |
| --------- | ---------------- |
| **Explicit Import**<br>Syntax: `import package.ClassName;`<br>Example: `import java.util.ArrayList;`   | **Explicit Static Import**<br>Syntax: `import static package.ClassName.staticMember;`<br>Example: `import static java.lang.Math.sqrt;`<br>`import static java.lang.System.out;`          |
| **Implicit Import (Wildcard Import)**<br>Syntax: `import package.*;`<br>Example: `import java.util.*;` | **Implicit Static Import (Wildcard Static Import)**<br>Syntax: `import static package.ClassName.*;`<br>Example: `import static java.lang.Math.*;`<br>`import static java.lang.System.*;` |


| Which of the following import statements are valid? | Status    | Reason     |
| --------- | --------- | ------------ |
| `import java.lang.Math.*;`                          | ❌ Invalid | `Math` is a class, not a package. Wildcard (`*`) can be used only with packages.  |
| `import static java.lang.Math.*;`                   | ✅ Valid   | Correct syntax for wildcard static import (imports all static members of `Math`). |
| `import java.lang.Math.sqrt;`                       | ❌ Invalid | Normal import works only for classes/interfaces, not for methods or variables.    |
| `import static java.lang.Math.sqrt();`              | ❌ Invalid | Parentheses are not allowed. Static import is for members, not method calls.      |
| `import java.lang.Math.sqrt.*;`                     | ❌ Invalid | `sqrt` is a method, not a package or class. Wildcard cannot be applied.           |
| `import static java.lang.Math.sqrt;`                | ✅ Valid   | Correct explicit static import of the `sqrt` method.                              |
| `import java.lang;`                                 | ❌ Invalid | Must specify a class name or use `*`. Cannot import only a package name.          |
| `import static java.lang;`                          | ❌ Invalid | Static import requires a class name and its static members.                       |
| `import java.lang.*;`                               | ✅ Valid   | Correct wildcard import of all classes in `java.lang` package.                    |
| `import static java.lang.*;`                        | ❌ Invalid | Static import requires a class name before `.*`.                                  |

- Two packages containing a class or interface with the same name is very rare. Hence, the ambiguity problem is also rare in normal imports.
- However, two classes or interfaces containing a variable or method with the same name is very common. Therefore, the ambiguity problem is also very common in static imports.
- The usage of static import may reduce readability and create confusion. Hence, if there is no specific requirement, it is not recommended to use static import.

**Difference Between Normal Import and Static Import**

- We use normal import to import classes and interfaces of a particular package.
- When we write a normal import statement, it is not required to use the fully qualified name. We can use the short class name directly.
- We use static import to import static members (variables and methods) of a particular class.
- When we write a static import statement, it is not required to use the class name to access static members. We can access them directly.

### Packages

A package is an encapsulation mechanism used to group related classes and interfaces into a single unit.

**Example 1**: All classes and interfaces required for database operations are grouped into a single package called the `java.sql` package.

**Example 2**: All classes and interfaces that are useful for file I/O operations are grouped into a separate package called the `java.io` package.

The main advantages of packages are:
- They help to resolve naming conflicts (provide unique identification for components).
- They improve modularity of the application.
- They improve maintainability of the application.
- They provide security for our components (access protection).

There is one universally accepted naming convention for packages:  
**use the internet domain name in reverse order.**

Example :- `com.icicibank.loan.housing.Account`
  
Explanation:
- `com.icicibank`  -> Client's internet domain name in reverse
- `loan`           -> Module name
- `housing`        -> Sub-module name
- `Account`        -> Class name

Example :-
```java
package com.durgasoft.scjp;

public class Test {
    public static void main(String[] args) {
        System.out.println("pkg demo");
    }
}
```
Command :-
- `javac Test.java`  
 The generated `.class` file will be placed in the Current Working Directory (CWD).  
 Package folder structure will NOT be created automatically.
```text
CWD (Current Working Directory)
 └── Test.class
```
- `javac -d . Test.java`
  - `-d` → Specifies the destination directory to place generated `.class` files.
  - `.` → Represents the Current Working Directory (CWD).  
The compiler automatically creates the corresponding package directory structure.  
The `.class` file is placed inside the package folders.
```text
CWD (Current Working Directory)
 └── com
      └── durgasoft
           └── scjp
                └── Test.class

```
- If the corresponding package structure is not already available, the javac -d command itself will automatically create the required package directories.
- Instead of . (Current Working Directory), we can specify any valid directory as the destination.

- `javac -d F: Test.java`
  - `-d` → Destination directory where generated `.class` files will be placed
  - `F:` → Target drive/location.
- The compiler creates the package folders automatically inside the given destination
```text
F:
 └── CWD
      └── com
           └── durgasoft
                  └── scjp
                        └── Test.class

```
- `javac -d Z: Test.java`
  - `-d` → Destination directory where generated `.class` files will be placed
  - `Z:` → Target drive/location.  
If the specified destination directory is not already available, then the compiler will generate a compile-time saying `error: directory not found: Z:`

- Important Interview / Exam Point
  - Without `-d` → `.class` file goes to CWD.
  - With `-d`  → Compiler creates package folders automatically.

- At the time of execution, we have to use the fully qualified class name: `java com.durgasoft.scjp.Test`.

<details>
<summary>
Conclusion 1
</summary>

In a Java source file, there can be at most one `package` statement.  
Writing more than one `package` statement is not allowed. Otherwise, we will get a compile-time error.

Example :-
```java
package pack1;
package pack2;

public class A {
}

```
Output :-
```output
Compile-time Error: class, interface, or enum expected
```
</details>

<details>
<summary>
Conclusion 2
</summary>


In any Java program, the first non-comment statement must be the `package` statement (if it is present).  
If we place any statement before the `package` statement, we will get a compile-time error.

```java
import java.util.*;
package pack1;

public class A {

}
```
Output:-
```output
Compile-time Error: class, interface, or enum expected
```
</details>

The correct order of statements in a Java source file should be:
- Package statement → At most one
- Import statements → Any number
- Class / Interface / Enum declarations → Any number

An empty source file is also considered a valid Java program.  
Hence, all of the following are valid Java source files:
- **Empty Source File**
```java
// Test.java (empty file)
``` 
- **Only Package Statement**
```java
// Test.java
package pack1;
``` 
- **Only Import Statement**
```java
// Test.java
import java.util.*;
``` 
- **Package + Import Statements**
```java
// Test.java
package pack1;
import java.util.*;
``` 
- **Only Class Declaration**
```java
// Test.java
class Test {

}
``` 

### Class Level Modifiers

Whenever we create our own classes, we must provide some information about the class to the JVM, such as:

- Whether the class is accessible from everywhere or not
- Whether child class creation (inheritance) is allowed or not
- Whether object creation is allowed or not
- Other behavioral restrictions of the class

This information is specified by using appropriate modifiers.

A **top-level class** means a class that is not declared inside another class.

Only the following modifiers are applicable:
- [public](#public-classes) 
- [default](#default-classes) (no modifier)
- [final](#final-modifier)
- [abstract](#abstract-modifier)
- [strictfp](#strictfp-strict-floating-point)

👉 Modifiers like `private`, `protected`, and `static` are not allowed for top-level classes.

But an **inner class** is a class declared inside another class.

The following modifiers are allowed:
- `public` 
- `default` (no modifier)
- `final`
- `abstract`
- `strictfp`
- `private`
- `protected`
- `static`

Example :-
```java
private class Test{
    public static void main(String[] args){
        System.out.println("Hello");
    }
}
```
Output :-
```output
compileTime Error: modifier private not allowed here
``` 

#### Access specifiers Vs Access Modifiers

In some older programming languages like C++, keywords such as:
- public
- private
- protected
- default

are called **specifiers**, while the remaining keywords are called **modifiers**.

⚠️ But this rule is NOT applicable in Java.

In Java, there is no separate term called **specifier**.

👉 All keywords that change the behavior or accessibility of a class, method, or variable are called **modifiers**.

Example :-
```java
private class Test{

}
```
Output :-
```output
compileTime Error: modifier private not allowed here
``` 

#### Public classes

If a class is declared as public, then we can access that class from anywhere, even from another package.

Example :-

`A.java`
```java
package pack1;

public class A {
    public void m1() {
        System.out.println("Hello");
    }
}
```
`B.java`
```java
package pack2;

import pack1.A;

public class B {
    public static void main(String[] args) {
        A a = new A();
        a.m1();
    }
}
```
Compilation and Execution

```bash
javac -d . B.java
java pack2.B
```
Output :-

```output
Hello
```

If class A is not declared as public, then while compiling class B, we will get a compile-time error saying: `pack1.A is not public in pack1; cannot be accessed from outside package`


#### Default classes

If a class is declared with default access (no access modifier), then it can be accessed only within the same package.

It cannot be accessed from outside the package. Hence, default access is also known as package-level access.

Example :-

`A.java`
```java
package pack1;

class A {
    public void m1() {
        System.out.println("Hello");
    }
}
```
`B.java`
```java
package pack2;

import pack1.A;

public class B {
    public static void main(String[] args) {
        A a = new A();
        a.m1();
    }
}
```

Compilation and Execution
```bash
javac -d . B.java
java pack2.B
```
Output
```output
Compile-time error:
pack1.A is not public in pack1; cannot be accessed from outside package
```

#### Final Modifier

`final` is a modifier applicable to **classes**, **methods**, and **variables**.

##### Final method

Whatever methods a parent class has are, by default, available to the child class through inheritance.

If the child class is not satisfied with the parent class method implementation, then the child is allowed to redefine that method according to its requirement. This process is called method **overriding**.

If a parent class method is declared as `final`, then we cannot override that method in the child class because its implementation is final.

Example :-
```java
class Parent {
    public void property() {
        System.out.println("Cash " + "Gold " + "Land");
    }

    public final void marry() {
        System.out.println("Rani");
    }
}

class Child extends Parent {
    public final void marry() {
        System.out.println("Ankita");
    }
}
```
Output :-
```output
Compile-time error:
marry() in Child cannot override marry() in Parent;
overridden method is final
```

##### Final class

If a class is declared as `final`, we cannot extend the functionality of that class.

That means we cannot create a child class for a final class. Hence, inheritance is not possible for final classes.

Example :-
```java
final class Parent {}

class Child extends Parent {}
```
Output :-
```output
Compile-time error:
cannot inherit from final Parent
```
> **NOTE :-** Every method present inside a final class is implicitly final by default, but every variable present inside a final class need not be final.  
> The main **advantage** of the `final` keyword is that it helps achieve security and allows us to provide a fixed (unique) implementation.  
> but **disadvantage** of the `final` keyword is that we miss some key benefits of OOP, such as inheritance (because of final classes) and polymorphism (because of final methods). Hence, if there is no specific requirement, it is not recommended to use the `final` keyword unnecessarily.

#### Abstract Modifier

Abstract is the modifier applicable for classes and methods but not for variables 

##### Abstract Method

Even though we do not know the implementation, we can declare a method using the `abstract` modifier.

For abstract methods, only the declaration is available, not the implementation. Hence, an abstract method declaration must end with a semicolon (`;`).

Example :- 

`public abstract void m1();`   // ✅ Valid  
`public abstract void m1(){}` // ❎ Invalid

The child class is responsible for providing the implementation of the parent class's abstract methods.

Example :
```java
abstract class Vehicle {
    abstract public int getNumberOfWheels();
}

class Bus extends Vehicle {
    public int getNumberOfWheels() {
        return 7;
    }
}

class Auto extends Vehicle {
    public int getNumberOfWheels() {
        return 3;
    }
}
```

By declaring an abstract method in the parent class, we provide guidelines (a contract) that child classes must implement specific methods.

An abstract method never talks about implementation; it only provides a declaration.

If any modifier indicates or requires an implementation, then it forms an illegal combination with the `abstract` modifier.

- `final` + `abstract method` ❎ (invalid)
- `native` + `abstract method` ❎ (invalid)
- `synchronized` + `abstract method` ❎ (invalid)
- `static` + `abstract method` ❎ (invalid)
- `private` + `abstract method` ❎ (invalid)
- `strictfp` + `abstract method` ❎ (invalid)

Example :
```java
abstract class Test{
    abstract final void m1();
}
```
Output :-
```output
compileTime error: illegal combination of modifiers abstract and final.
```

| Modifier         | Why it cannot be combined with `abstract`  | Example (Invalid Code)  | Reason   |
| ---------------- | ------- | -------- | ------- |
| **final**        | `final` methods cannot be overridden, but abstract methods must be overridden by child classes. | `abstract class Test { abstract final void m1(); }`| Abstract requires overriding, but final prevents overriding.|
| **native**| `native` methods already have implementation provided in another language (like C/C++).| `abstract class Test { abstract native void m1(); }`| Native implies implementation exists externally, while abstract means no implementation. |
| **synchronized** | `synchronized` applies to method implementation (thread locking).| `abstract class Test { abstract synchronized void m1(); }` | Synchronization requires a method body, which abstract methods do not have.   |
| **static**| Static methods belong to the class and cannot be overridden.  | `abstract class Test { abstract static void m1(); }` | Abstract methods rely on overriding, but static methods cannot be overridden. |
| **private**| Private methods are not visible to child classes.| `abstract class Test { private abstract void m1(); }`| Child classes cannot access private methods to provide implementation.|
| **strictfp**| `strictfp` controls floating-point implementation details.| `abstract class Test { abstract strictfp void m1(); }`| strictfp affects implementation, but abstract methods have no implementation.|

##### Abstract Class

If, for any Java class, we are not allowed to create an object (because it contains partial or incomplete implementation), then such a class must be declared with the `abstract` modifier. Such a class is called an **abstract class**.

Hence, instantiation of an abstract class is not possible.

Example :-
```java
abstract class Test{
    public static void main(String[] args){
        Test t = new Test();
    }
}
```
Output :-
```output
compileTime Error: Test is abstract; cannot be instantiated
```

**Abstract class Vs Abstract method**

- If a class contains at least one abstract method, then it is compulsory to declare the class as `abstract`; otherwise, we will get a compile-time error.   
**Reason**: :  
 If a class contains at least one abstract method, its implementation is incomplete. Hence, it is not recommended to create objects of such a class. To restrict object instantiation, the class must be declared as abstract.

- Even if a class does not contain any abstract methods, we can still declare the class as abstract if we do not want object creation.

👉 An abstract class can contain zero abstract methods

**Example** 1: HttpServlet class is abstract even though it does not contain any abstract methods.

**Example** 2: Adapter classes are usually declared as abstract even though they may not contain abstract methods.

🔴Example 
```java
class Parent{
    public void m1();
}
```
Output :-
```output
compileTime error: missing method body, or declare abstract
```
🔴Example 
```java
class Parent{
    public abstract void m1(){}
}
```
Output :-
```output
compileTime error: abstract method cannot have a body
```
🔴Example 
```java
class Parent{
    public abstract void m1();
}
```
Output :-
```output
compileTime error: Parent is not abstract and does not override abstract method m1() in Parent
```
- If we extend an abstract class, then we must provide implementations for each and every abstract method of the parent class. Otherwise, we must declare the child class as `abstract`. In that case, the next-level child class becomes responsible for providing the implementation.

🔴Example 
```java
abstract class Parent{
    public abstract void m1(); 
    public abstract void m2(); 
}

class Child extends Parent{
    public void m1(){}
}
```
Output :-
```output
compileTime error: child is not abstract and does not override abstract method m2() in Parent
```

**Final Vs Abstract**

- An abstract method must be overridden in the child class to provide an implementation, whereas a final method cannot be overridden.  
Hence, the combination final abstract is an illegal combination for methods.

- For a final class, we cannot create a child class (inheritance is not allowed).  
For an abstract class, we must create a child class to provide implementations for abstract methods.  
Therefore, the combination `final abstract` is also an illegal combination for classes.

- An abstract class can contain final methods But, a final class cannot contain abstract methods.

**Example** : ✅ Valid: **Abstract Class with Final Method**
```java
abstract class Test {
    public final void m1() {
        // implementation
    }
}
```
**Example** : ❎ Invalid: **Final Class with Abstract Method**
```java
final class Test{
    public abstract void m1(){}
}
```
> **NOTE :-** It is highly recommended to use the abstract modifier because it promotes several OOP features such as inheritance and polymorphism.

#### Strictfp (Strict floating Point)

- The `strictfp` modifier was introduced in Java 1.2
- We can use `strictfp` with classes and methods, but not with variables.
- Usually, the result of floating-point arithmetic may vary from platform to platform due to hardware differences.
- If we want platform-independent results for floating-point calculations, we should use the `strictfp` modifier.

##### Strictfp method

- If a method is declared as `strictfp`, all floating-point calculations inside that method must follow the IEEE 754 standard, ensuring platform-independent results.

Example :
```java
strictfp class Test {
    public strictfp void calculate() {
        double result = 10.0 / 3.0;
        System.out.println(result);
    }
}
```

**abstract vs strictfp in method Combination**
- The abstract modifier never talks about implementation.
- The strictfp modifier always affects the implementation (floating-point calculation rules).

Hence, the combination `abstract strictfp` is an illegal combination for methods.

Example :
```java
abstract class Test {
    abstract strictfp void m1(); // ❌ Illegal
}
```

##### Strictfp class

- If a class is declared as `strictfp`, then every floating-point calculation present in its concrete methods must follow the IEEE 754 standard, so that we get platform-independent results.

**abstract and strictfp in class Combination**
- The combination `abstract strictfp` is legal for **classes**.
- The combination `abstract strictfp `is illegal for **methods**.

**Reason:**
- `abstract` methods do not contain implementation.
- `strictfp` affects the implementation of floating-point calculations.
- Since abstract methods have no implementation, this combination is not allowed for methods.

**Example** : ✅ Valid: Abstract Class + Strictfp Class Combination
```java
abstract strictfp class Test {

}
```
**Example** : ❎ Invalid: Abstract Method + Strictfp Method Combination
```java
abstract strictfp void m1();
```
Output :
```output
Compile-time error:
illegal combination of modifiers: abstract and strictfp
```

### Member Modifiers (method or variable level modifiers)

#### Public Members

- If a member is declared as public, then we can access that member from anywhere, but the corresponding class should be visible. That means before checking member visibility, we have to check class visibility.

Example :

`A.java`
```java
package pack1;

class A{
    public void m1(){
        System.out.println("A class method");
    }
}
```
`B.java`
```java
package pack2;
import pack1.A;

class A{
    public static void main(String[] args){
        A a = new A();
        a.m1();
    }
}
```
Output
```output
compile-time error: pack1.A is not public in pack1; cannot be accessed from outside package
```
In the above example, even though the `m1()` method is public, we cannot access it from outside the package because the corresponding class `A` is not public. That is, only when both the class and the method are public can we access the method from outside the package.

#### Default Members

If a member is declared as default, then we can access that member only within the current package. From outside the package, we cannot access it. Hence, default access is also known as package-level access.

Example :

`A.java`
```java
package pack1;

public class A {
    void m1() {
        System.out.println("Default method");
    }
}
```
`B.java`
```java
package pack1;
import pack1.A;

public class B {
    public static void main(String[] args) {
        A a = new A();
        a.m1();
    }
}
```
Output
```output
compile-time error: A is not public in pack1; cannot be accessed from outside package
```

#### Private Members

- If a member is declared as private, then we can access that member only within the class. From outside the class, we cannot access it. Hence, private access is also known as class-level access.
- An abstract method should be available to child classes to provide implementation, whereas private methods are not available to child classes. Hence, the private–abstract combination is illegal for methods.

#### Procted Members

- If a member is declared as protected, then we can access that member anywhere within the current package and also in child classes outside the package.

- We can access protected members within the current package anywhere, either by using a parent reference or a child reference.
- But we can access protected members in an outside package only in child classes, and we should use a child reference only. That is, a parent reference cannot be used to access protected members from outside the package.

Example 1: valid

```java
package pack1;

public class A{
    protected void m1(){
        System.out.println("The most misunderstood modifier");
    }
}

class B extends A{
    public static void main(String[] args){
        A a = new A();
        a.m1();

        B b = new B();
        b.m1();

        A a1 = new B();
        a1.m1();
    }
}
```
Output:
```output
The most misunderstood modifiers
The most misunderstood modifiers
The most misunderstood modifiers
```

Example :

`A.java`
```java
package pack1;

public class A{
    protected void m1(){
        System.out.println("The most misunderstood modifier");
    }
}
```
`C.java`
```java
package pack2;

import pack1.A;

class C extends A{
    public static void main(String[] args){
        A a = new A(); // Invalid
        a.m1();

        C b = new C(); // Valid
        b.m1();

        A a1 = new C(); // Invalid
        a1.m1();
    }
}
```

Output :
```output
compile-time error: m1() has protected access in pack1.A
```

- We can access protected members from outside the package only in a child class, and we should use that child class reference only. For example, from class `D`, if we want to access the protected member, we should use a `D` class reference only.

Example :

`A.java`
```java
package pack1;

public class A{
    protected void m1(){
        System.out.println("The most misunderstood modifier");
    }
}
```
```java
class C extends A
{

}

class D extends C{
    public static void main(String[] args){
        A a = new A(); // invalid
        a.m1();

        C c = new C(); // invalid
        c.m1();

        D d = new D(); // valid
        d.m1();

        A a1 = new C(); // invalid
        a1.m1();

        A a2 = new D(); // invalid
        a2.m1();

        C c1 = new D(); // invalid
        c1.m1();
    }
}
```
```output
compile-time error: m1() has protected access in pack1.A
```

#### Summary Table of Private Default Protected Public modifiers

| Visibility                                  | Private | Default | Protected                                | Public |
| ------------------------------------------- | ------- | ------- | ---------------------------------------- | ------ |
| Within the same class                       | ✅       | ✅       | ✅                                        | ✅      |
| From child class in the same package        | ❎       | ✅       | ✅                                        | ✅      |
| From non-child class in the same package    | ❎       | ✅       | ✅                                        | ✅      |
| From child class in a different package     | ❎       | ❎       | ✅ (we should use a child reference only) | ✅      |
| From non-child class in a different package | ❎       | ❎       | ❎                                        | ✅      |


- The most restricted access modifier is private.
- The most accessible modifier is public.

`private < default < protected < public`

> **NOTE :-** 
> - The recommended modifier for data members (variables) is private.
> - The recommended modifier for methods is public.

#### Final

##### Final instance variable

- If the value of a variable varies from object to object, such types of variables are called **instance variables**.
- For every object, a separate copy of instance variables will be created.
- For instance variables, we are not required to perform initialization explicitly. The JVM always provides default values.

Example :
```java
class Test{
    int x;
    public static void main(String[] args){
        Test t = new Test();
        System.out.println(t.x);
    }
}
```
Output:
```output
0
```
- If the instance variable is declared as `final`, then we must compulsorily perform initialization explicitly, whether we use it or not, and the JVM will not provide a default value.

Example :-
```java
class Test{
    final int x;
}
```
Output
```output
compile-time error: variable x might not have been initialized
```

**RULE FOR FINAL INSTANCE VARIABLES**

For final instance variables, we must perform initialization before constructor completion. The following are the possible places for initialization:

1. At the time of declaration
```java
class Test{
    final int x = 10;
}
```
1. Inside an instance block
```java
class Test{
    final int x;
    {
        x = 10;
    }
}
```
1. Inside a constructor
```java
class Test{
    final int x;
    Test(){
        x = 10;
    }
}
```
These are the only possible places to perform initialization for final instance variables. If we try to perform initialization anywhere else, then we will get a compile-time error.

Example :
```java
class Test{
    final int x;
    public void m1(){
        x = 10;
    }
}
```
Output
```output
compile-time error: cannot assign a value to final variable x
```

##### Final static variables

- If the value of a variable does not vary from object to object, such types of variables are not recommended to be declared as instance variables. We should declare those variables at the class level by using the static modifier.
- In the case of instance variables, a separate copy will be created for every object, but in the case of static variables, a single copy will be created at the class level and shared by every object of that class.
- For static variables, it is not required to perform initialization explicitly. The JVM will always provide default values.
  
```java
class Test{
    static int x;
    public static void main(String[] args){
        System.out.println(x);
    }
}
```
- If a static variable is declared as `final`, then we must compulsorily perform initialization explicitly; otherwise, we will get a compile-time error, and the JVM will not provide any default values.

```java
class Test{
    final static int x;
}
```
Output
```output
compile-time error: variable x might not have been initialized
```

**Rules for Final Static Variables**

For final static variables, we must perform initialization before class loading completion. The following are the possible places for initialization:

1. At the time of declaration
```java
class Test{
    final static int x = 10;
}
```
2. Inside a static block
```java
class Test{
    final static int x;
    static{
        x = 10;
    }
}
```

These are the only possible places to perform initialization for final static variables. If we try to perform initialization anywhere else, then we will get a compile-time error.

Example
```java
class Test{
    final static int x;
    public void m1(){
        x = 10;
    }
}
```
```output
compile-time error: cannot assign a value to final variable x
```

##### Final local Variables

- To meet the temporary requirements of programmers, we declare variables inside a method, block, or constructor. Such types of variables are called local variables, temporary variables, stack variables, or automatic variables.

- For local variables, the JVM will not provide any default values. We must compulsorily perform initialization explicitly before using a local variable. If we are not using it, then initialization is not required.

Example :
```java
class Test{
    public static void main(String[] args){
        int x;
        System.out.println("Hello");
    }
}
```
Output
```output
Hello
```
Example :
```java
class Test{
    public static void main(String[] args){
        int x;
        System.out.println(x);
    }
}
```
Output
```output
compile-time error: variable x might not have been initialized
```
- Even if a local variable is declared as `final`, we need to initialize it only before using it. If we are not using it, initialization is not required even though it is `final`.

Example :
```java
class Test{
    public static void main(String[] args){
        final int x;
        System.out.println("Hello");
    }
}
```
Output
```output
Hello
```
The only applicable modifier for a local variable is `final`. If we try to apply any other modifier, we will get a compile-time error

Example :

```java
class Test{
    public static void main(String[] args){
        public int x = 10;     // invalid
        private int x = 10;    // invalid
        protected int x = 10;  // invalid
        static int x = 10;     // invalid
        transient int x = 10;  // invalid
        volatile int x = 10;   // invalid
        final int x = 10;      // valid
    }
}
```
Output
```output
compile-time error: illegal start of expression
```

> **NOTE :-** If we do not declare any modifier, it is considered default by default. However, this rule is applicable only for instance and static variables, not for local variables.

##### Formal Parameters

- Formal parameters of a method act as local variables of that method. Hence, formal parameters can be declared as `final`.
- If formal parameters are declared as `final`, then within the method we cannot perform reassignment.

Example 

```java
class Test{
    public static void main(String[] args){
        m1(10, 20);
    }

    public static void m1(final int x, int y){
        x = 100;
        y = 200;
        System.out.println(x + " .... " + y);
    }
}
```
Output
```output
compile-time error: cannot assign a value to final variable x
```

#### Static modifiers

- `static` is a modifier applicable to methods and variables but not to top-level classes. We cannot declare a top-level class with the `static` modifier, but we can declare an inner class as `static`. Such types of inner classes are called static nested classes.

- In the case of instance variables, a separate copy will be created for every object, but in the case of static variables, a single copy will be created at the class level and shared by every object of that class

Example :
```java
class Test{
    static int x = 10;
    int y = 20;

    public static void main(String[] args){
        Test t1 = new Test();
        t1.x = 888;
        t1.y = 999;

        Test t2 = new Test();
        System.out.println(t2.x + " ... " + t2.y);
    }
}
```

- We cannot access instance members directly from a static area, but we can access them directly from an instance area.
- We can access static members directly from both instance and static areas.

Consider the following declarations:

```java
class Test{
    int x = 10;              // (1)
    static int x = 10;       // (2)

    public void m1(){        // (3)
        System.out.println(x);
    }

    public static void m1(){ // (4)
        System.out.println(x);
    }
}
```
Within the same class, which of the above declarations can be taken simultaneously?
- `1 & 3` ✅
- `1 & 4` ❎ → `compile-time error: non-static variable x cannot be referenced from a static context`
- `2 & 3` ✅
- `2 & 4` ✅
- `1 & 2` ❎ → `compile-time error: variable x is already defined in Test`
- `3 & 4` ❎ → `compile-time error: m1() is already defined in Test`

<details>
<Summary>
Case 1
</Summary>

The overloading concept is applicable to static methods, including the `main` method, but the JVM can always call only the `main` method with the `String[]` argument.

Example :
```java
class Test{
    public static void main(String[] args){
        System.out.println("String[]");
    }

    public static void main(int[] args){
        System.out.println("int[]");
    }
}
```
Output :
```output
String[]
```
Other overloaded methods must be called just like normal method calls.
</details>

<details>
<summary>
Case 2
</summary>

The inheritance concept is applicable to static methods, including the `main()` method. Hence, while executing a child class, if the child class does not contain a `main()` method, then the parent class `main()` method will be executed.

```java
class Parent{
    public static void main(String[] args){
        System.out.println("parent main");
    }
}

class Child extends Parent{

}
```
Output
- Command: `java Parent`
```output
parent main
```
- Command: `java Child`
```output
parent main
```
</details>

<details>
<summary>
Case 3
</summary>

It seems that the overriding concept is applicable to static methods, but it is not overriding; it is method hiding.

Example :
```java
class Parent{
    public static void main(String[] args){
        System.out.println("Parent main");
    }
}

class Child extends Parent{
    public static void main(String[] args){
        System.out.println("Child main");
    }
}
```
Output
- Command: `java Parent`
```output
Parent main
```
- Command: `java Child`
```output
Child main
```
> **NOTE:** For static methods, overloading and inheritance concepts are applicable, but the overriding concept is not applicable. Instead of overriding, the method hiding concept is applicable.
</details>

- If inside a method implementation we are using at least one instance variable, then that method talks about a particular object. Hence, we should declare such a method as an instance method.

- If inside a method implementation we are not using any instance variable, then that method is not related to any particular object. Hence, we should declare such types of methods as static methods, irrespective of whether we are using static variables or not.

Example :

```java
class Student{
    String name;
    int rollno;
    int marks;
    static String collegeName;

    String getStudentInfo(){
        return (name + " .... " + marks);
    }

    static String getCollegeInfo(){
        return (collegeName);
    }

    static float getAverage(int x, int y){
        return (x + y) / 2.0f;
    }

    String getCompleteInfo(){
        return (name + " .... " + rollno + " .... " + marks + " .... " + collegeName);
    }
}
```
- For a static method, implementation should be available, whereas for an abstract method, implementation is not available. Hence, the abstract–static combination is illegal for methods.


#### Synchronized modifier

- `synchronized` is a modifier applicable to methods and blocks, but not to classes and variables.

- If multiple threads try to operate simultaneously on the same Java object, then there may be a chance of a data inconsistency problem. This is called a race condition.
- We can overcome this problem by using the `synchronized` keyword.
- If a method or block is declared as `synchronized`, then at a time only one thread is allowed to execute that method or block on the given object, so that the data inconsistency problem will be resolved.
- The main disadvantage of the `synchronized` keyword is that it increases the waiting time of threads and creates performance problems. Hence, if there is no specific requirement, it is not recommended to use the `synchronized` keyword.

- A synchronized method must compulsorily contain implementation, whereas an abstract method does not contain any implementation. Hence, the abstract–synchronized combination is an illegal combination of modifiers for methods.

#### Native modifier

- `native` is a modifier applicable only to methods, and we cannot apply it anywhere else.
- The methods that are implemented in non-Java languages (mostly C or C++) are called native methods or foreign methods.

- The main objectives of the `native` keyword are:
  - To improve the performance of the system
  - To achieve machine-level or memory-level communication
  - To use already existing legacy non-Java code

##### Pseudo code to use the native keyword in Java

```java
class Native{
    static{
        System.loadLibrary("native library path"); // Load native libraries
    }

    public native void m1(); // Declare a native method
}

class Client{
    public static void main(String[] args){
        Native n = new Native();
        n.m1(); // Invoke a native method
    }
}
```
- For a native method, implementation is already available in older languages like C or C++, and we are not responsible for providing the implementation. Hence, a native method declaration should end with a semicolon (`;`).

Example :
```java
public native void m1();   // valid
public native void m1(){}  // invalid
```

- For native methods, implementation is already available in another language, whereas for abstract methods, implementation should not be available. Hence, we cannot declare a native method as abstract. Therefore, the native–abstract combination is an illegal combination for methods.

- We cannot declare a native method as `strictfp` because there is no guarantee that the older language follows the IEEE 754 standard. Hence, the native–strictfp combination is an illegal combination for methods.

- The main advantage of the `native` keyword is that performance will be improved, but the main disadvantage is that it breaks the platform-independent nature of Java.

#### Transient modifier

- `transient` is a modifier applicable only to variables.
- We can use the `transient` keyword in the serialization context.

- At the time of serialization, if we do not want to save the value of a particular variable due to security constraints, then we should declare it as `transient`.

- During serialization, the JVM ignores the original value of a transient variable and saves the default value to the file. Hence, `transient` means not to serialize.

[Image](https://tinyurl.com/2fzpbuu4)

#### Volatile modifier 

- volatile is a modifier applicable only to variables, and we cannot apply it anywhere else.

- If the value of a variable keeps changing due to multiple threads, then there may be a chance of a data inconsistency problem. We can overcome this problem by using the `volatile` modifier.

- If a variable is declared as `volatile`, then every thread accesses the latest updated value directly, instead of using a cached copy.

- The main advantage of `volatile` is that it helps overcome data inconsistency problems.

- The main disadvantage of the `volatile` keyword is that managing visibility between multiple threads may increase programming complexity and can create performance issues. Hence, if there is no specific requirement, it is not recommended to use the `volatile` keyword.

- A `final` variable means the value never changes, whereas a `volatile` variable means the value may keep changing.  
   Hence, the volatile–final combination is an illegal combination for variables.

| Modifier                  | Outer Class | Inner Class | Method | Variable | Block | Outer Interface | Inner Interface | Outer Enum | Inner Enum | Constructor |
| ------------------------- | ----------- | ----------- | ------ | -------- | ----- | --------------- | --------------- | ---------- | ---------- | ----------- |
| **public**                | ✔           | ✔           | ✔      | ✔        | ❌     | ✔               | ✔               | ✔          | ✔          | ✔           |
| **private**               | ❌           | ✔           | ✔      | ✔        | ❌     | ❌               | ✔               | ❌          | ✔          | ✔           |
| **protected**             | ❌           | ✔           | ✔      | ✔        | ❌     | ❌               | ✔               | ❌          | ✔          | ✔           |
| **default (no modifier)** | ✔           | ✔           | ✔      | ✔        | ❌     | ✔               | ✔               | ✔          | ✔          | ✔           |
| **final**                 | ✔           | ✔           | ✔      | ✔        | ❌     | ❌               | ❌               | ❌          | ❌          | ❌           |
| **abstract**              | ✔           | ✔           | ✔      | ❌        | ❌     | ✔    | ✔    | ❌          | ❌          | ❌           |
| **static**                | ❌           | ✔           | ✔      | ✔        | ✔     | ❌               | ✔               | ❌          | ✔          | ❌           |
| **synchronized**          | ❌           | ❌           | ✔      | ❌        | ✔     | ❌               | ❌               | ❌          | ❌          | ❌           |
| **native**                | ❌           | ❌           | ✔      | ❌        | ❌     | ❌               | ❌               | ❌          | ❌          | ❌           |
| **strictfp**              | ✔           | ✔           | ✔      | ❌        | ❌     | ✔               | ✔               | ✔          | ✔          | ❌           |
| **transient**             | ❌           | ❌           | ❌      | ✔        | ❌     | ❌               | ❌               | ❌          | ❌          | ❌           |
| **volatile**              | ❌           | ❌           | ❌      | ✔        | ❌     | ❌               | ❌               | ❌          | ❌          | ❌           |


- The only applicable modifier for a local variable is `final`.
- The only applicable modifiers for constructors are `public`, `private`, `protected`, and `default`.
- The modifier which is applicable only to methods is `native`.
- The modifiers which are applicable only to variables are `volatile` and `transient`.
- The modifier which is applicable only to classes but not to interfaces is `final`.
- The modifiers which are applicable only to classes but not to enums are `final` and `abstract`.


### Interfaces

1. [Introduction](#introduction)
2. [Interface Declaration & Implementation](#interface-declaration--implementation)
3. [extends vs implements](#extends-vs-implements)
4. [Interface Methods](#interface-methods)
5. [Interface Variables](#interface-variables)
6. [Interface Naming Conflicts](#interface-naming-conflicts)
   1. [Method Naming Conflicts](#method-naming-conflicts)
   2. [Variable Naming Conflicts](#variable-naming-conflicts)
7. [Marker Interface](#marker-interface)
8. [Adapter Classes](#adapter-classes)
9. [Interface vs Abstract Class vs Concrete Class](#interface-vs-abstract-class-vs-concrete-class)
10. [Difference Between Interface and Abstract Class](#difference-between-interface-and-abstract-class)

#### Introduction

**Definition-1**

- Any Service Requirement Specification (SRS) is considered an interface.

Example : The JDBC API acts as a requirement specification to develop database drivers, and the database vendor is responsible for implementing the JDBC API.
```diagram
      Sun
       |
     JDBC API
        |
   -----------------
   |       |       |
 Oracle   MySQL    DB2
 Driver   Driver   Driver
```

Example : The Servlet API acts as a requirement specification to develop a web server. The web server vendor is responsible for implementing the Servlet API.
```diagram
       Sun
        |
     Servlet API
         |
-------------------------------------------------
|                 |                            |
Apache Tomcat   Oracle WebLogic           IBM WebSphere
   Server           Server                    Server
```

**Definition-2**

- From the client’s point of view, an interface defines the set of services that the client is expecting. From the service provider’s point of view, an interface defines the set of services that the provider is offering. Hence, any contract between a client and a service provider is considered an interface.

Example: Through the bank ATM GUI screen, bank authorities highlight the set of services they are offering. At the same time, the GUI screen presents the set of services that customers expect. Hence, this GUI screen acts as a contract between customers and bank authorities.

```diagram
                -----------------
                |               |
                |   Withdraw    |
                |               |
                | Mini Statement|
                |               | <----- Bank authorities
Customer -----> |               |
                |    Balance    |
                |               |
                |               |
                -----------------
                 Bank ATM GUI Screen
```

**Definition-3**

- Inside an interface, every method is always abstract whether we declare it or not. Hence, an interface is considered a 100% pure abstract class.

**Summary Definition**

Any service requirement specification, or any contract between a client and a service provider, or a 100% pure abstract class is nothing but an interface.


#### Interface Declaration & Implementation

- Whenever we implement an interface, we must provide implementation for each and every method of that interface. Otherwise, we have to declare the class as `abstract`, and then the next-level child class is responsible for providing the implementation.
- Every interface method is always `public` and `abstract`, whether we declare it or not. Hence, whenever we implement an interface method, we must compulsorily declare it as `public`; otherwise, we will get a compile-time error.

**Example** : Without `abstract` (Class must implement all methods)  

If a class implements an interface and is not declared abstract, then it must provide implementation for all interface methods.
```java
interface Interf{
    void m1();
    void m2();
}

class ServiceProvider implements Interf{

    public void m1(){
        System.out.println("m1 implementation");
    }

    public void m2(){
        System.out.println("m2 implementation");
    }
}
```

**Example** : With `abstract` (Partial implementation allowed)

If a class implements an interface but does not implement all methods, then the class must be declared `abstract`. The remaining implementation will be provided by the child class.
```java
interface Interf{
    void m1();
    void m2();
}

abstract class ServiceProvider implements Interf{
    public void m1(){
        System.out.println("m1 implementation");
    }
}

class SubServiceProvider extends ServiceProvider{
    public void m2(){
        System.out.println("m2 implementation");
    }
}
```

#### extends vs implements

- A class can extend only one class at a time.
- An interface can extend any number of interfaces simultaneously.

Example :-
```java
interface A{
    
}

interface B{

}

interface C extends A, B{

}
```
- A class can implement any number of interfaces simultaneously. 
- A class can extend another class and can implement any number of interfaces simultaneously.

Example
```java
class A extends B implements C, D, E{

}
```
| Statement   | Valid / Invalid | Reason         |
| ----------- | --------------- |------- |
| A class can extend any number of classes at a time                                      | ❌ Invalid       | Java does not support multiple inheritance for classes. A class can extend only one class. |
| A class can implement only one interface at a time                                      | ❌ Invalid       | A class can implement multiple interfaces simultaneously.                                  |
| An interface can extend only one interface at a time                                    | ❌ Invalid       | An interface can extend multiple interfaces simultaneously.                                |
| An interface can implement any number of interfaces simultaneously                      | ❌ Invalid       | Interfaces do not implement other interfaces; they only extend interfaces.                 |
| A class can extend another class or implement an interface, but not both simultaneously | ❌ Invalid       | A class can extend one class and implement multiple interfaces at the same time.           |

**Q.** Consider the following expression: `X extends Y`.
For which of the following possibilities of X and Y is the above expression valid?

| Option | Statement | Valid / Invalid | Explanation  |
| ------ | ----- | --------------- | ------------ |
| 1      | Both X and Y should be classes                   | ❌ Invalid       | A class extends a class, but an interface can also extend an interface. So this is not the only possibility. |
| 2      | Both X and Y should be interfaces                | ❌ Invalid       | Classes can also use `extends` with other classes.                                                           |
| 3      | Both X and Y can be either classes or interfaces | ✅ Valid         | A class can extend a class, and an interface can extend an interface.                                        |
| 4      | No restriction                                   | ❌ Invalid       | A class cannot extend an interface, so restrictions exist.                                                   |

**Q.** Consider the following expression: `X extends Y,Z`.
For which of the following possibilities of X, Y and Z is the above expression valid?

**Ans** `X,Y,Z should be interface`

**Q.** Consider the following expression: `X implements Y,Z`.
For which of the following possibilities of X, Y and Z is the above expression valid?

**Ans** `X -> class; Y,Z -> interface`

**Q.** Consider the following expression: `X extends Y implements Z`.
For which of the following possibilities of X, Y and Z is the above expression valid?

**Ans** `X,Y -> class; Z -> interface`

**Q.** Consider the following expression: `X implements Y extends Z`.
For which of the following possibilities of X, Y and Z is the above expression valid?

**Ans** `Compile-time error : because we have to take extends first followed by interface`

#### Interface Methods

- Every method present inside an interface is always `public` and `abstract`, whether we declare it explicitly or not.

```java
interface Interf{
    void m1();
}
```
**Q.** Why Interface Methods Are Always public and abstract?

- public : to make this method available to every implementation class.
- abstarct : Implementation class is responsible to provide implemenattion

Hence, inside an interface, the following method declarations are equal:

```java
void m1();
public void m1();
abstract void m1();
public abstract void m1();
```
- As every interface method is always public and abstract, we cannot declare an interface method with the following modifiers:
  - private
  - protected
  - static
  - final
  - synchronized
  - strictfp
  - native

**Q.** Which of the Following Method Declarations Are Allowed Inside an Interface?

| Method Declaration | Allowed / Not Allowed | Reason        |
| ----------------- | --------------------- | -------- |
| `public void m1(){}`                | ❌ **Not Allowed**     | Interface methods cannot have a body (unless `default` or `static` in Java 8+). Missing `default/static`.                         |
| `private void m1();`                | ❌ **Not Allowed**     | `private` methods must have a body (Java 9+). Abstract private methods are illegal.                                               |
| `protected void m1();`              | ❌ **Not Allowed**     | Interface methods cannot be `protected`. They are always `public`.                                                                |
| `public abstract native void m1();` | ❌ **Not Allowed**     | `native` methods require implementation outside Java, but interface methods are abstract contracts — this combination is illegal. |
| `abstract public void m1();`        | ✅ **Allowed**         | Valid declaration. Order of modifiers does not matter. Equivalent to `public abstract void m1();`                                 |



#### Interface Variables

- An interface can contain variables. The main purpose of interface variables is to define requirement-level constants.

- Every interface variable is always `public`, sta`tic, and `final`, whether we declare these modifiers explicitly or not.

```java
interface Interf{
    int x = 10;
}
```
**Q.** Why are interface variables always `public`, `static`, and `final`?

- `public`: To make the variable available to every implementation class.
- `static`: So that implementation classes can access this variable without creating an object.
- `final`: If one implementation class changes the value, then the remaining implementation classes will be affected. To restrict this, every interface variable is always `final`.

Hence, within an interface, the following variable declarations are equivalent:
```java
int x = 10;
public int x = 10;
static int x = 10;
final int x = 10;
public static int x = 10;
public final int x = 10;
static final int x = 10;
public static final int x = 10;
```
- Since every interface variable is always `public`, `static`, and `final`, we cannot declare interface variables with the following modifiers:
  - `private`
  - `protected`
  - `transient`
  - `volatile`

- For interface variables, we must compulsorily perform initialization at the time of declaration; otherwise, we will get a compile-time error.

Example :
```java
interface Interf{
    int x;
}
```
Output
```output
compile-time error: = expected
```

Which of the following variable declarations are allowed inside an interface?

| Variable Declaration        | Allowed / Not Allowed | Reason         |
| --------------- | --------------------- | --------------- |
| `int x;`                    | ❌ Not Allowed         | Interface variables must be initialized at the time of declaration.  |
| `private int x = 10;`       | ❌ Not Allowed         | Interface variables cannot be `private`; they are always `public`.   |
| `protected int x = 10;`     | ❌ Not Allowed         | Interface variables cannot be `protected`; they are always `public`. |
| `volatile int x = 10;`      | ❌ Not Allowed         | `volatile` modifier is not allowed for interface variables.          |
| `transient int x = 10;`     | ❌ Not Allowed         | `transient` modifier is not allowed for interface variables.         |
| `public static int x = 10;` | ✅ Allowed             | Interface variables are implicitly `public`, `static`, and `final`.  |


- Inside an implementation class, we can access interface variables, but we cannot modify their values.

Example :
```java
interface Interf{
    int x = 10;
}

class Test implements Interf{
    public static void main(String[] args){
        x = 777;
        System.out.println(x);
    }
}
```
Output
```output
compile-time error: cannot assign a value to final variable x
```

Example :
```java
interface Interf{
    int x = 10;
}

class Test implements Interf{
    public static void main(String[] args){
        int x = 777;
        System.out.println(x);
    }
}
```
Output
```output
777
```

#### Interface Naming Conflicts

##### Method Naming Conflicts

**Case -1**

If two interfaces contain methods with the same signature and the same return type, then in the implementation class we have to provide implementation for only one method.

Example
```java
interface Left{
    public void m1();
}

interface Right{
    public void m1();
}

class Test implements Left, Right{
    public void m1(){
        // implementation
    }
}
```

**Case -2**

If two interfaces contain methods with the same name but different argument types, then in the implementation class we have to provide implementations for both methods. These methods act as overloaded methods.

Example
```java
interface Left{
    public void m1();
}

interface Right{
    public void m1(int i);
}

class Test implements Left, Right{
    public void m1(){
        // implementation
    }

    public void m1(int i){
        // implementation
    }
}
```

**Case -3**

If two interfaces contain methods with the same signature but different return types, then it is impossible to implement both interfaces simultaneously (even if the return types are not compatible).

Example
```java
interface Left{
    public void m1();
}

interface Right{
    public int m1();
}
```
We cannot write any Java class that implements both interfaces simultaneously because the method signatures are the same but the return types are different.

**Q.** Can a Java class implement any number of interfaces simultaneously?

**Ans.** Ans.
Yes, a Java class can implement multiple interfaces simultaneously because Java supports multiple inheritance through interfaces.

However, there is one exception: if two interfaces contain methods with the same method signature but different return types, then a class cannot implement both interfaces at the same time because Java cannot resolve which method implementation to use. This results in a compilation error.

Example
```java
interface A {
    int show();
}

interface B {
    String show();
}

// Compilation Error
class Test implements A, B {
    public int show() {
        return 10;
    }
}
```
👉 Here, both interfaces declare show() with the same parameters but different return types, which is not allowed.

##### Variable Naming Conflicts

- Two interfaces can contain variables with the same name. This may create a naming conflict, but the problem can be resolved by referring to the variables using the interface name.

In Java, all variables declared inside an interface are public, static, and final by default. Therefore, they must be accessed using the interface name when ambiguity occurs.

Example

```java
interface Left {
    int x = 777;
}

interface Right {
    int x = 888;
}

class Test implements Left, Right {
    public static void main(String[] args) {

        System.out.println(Left.x);
        System.out.println(Right.x);

        // System.out.println(x);  // Compilation Error (Ambiguous reference)
    }
}
```
Output
- System.out.println(Left.x);
```output
777
```
- System.out.println(Right.x);
```output
888
```
- System.out.println(x);
```output
Compilation Error: reference to x is ambiguous
```

#### Marker Interface

If an interface does not contain any methods, and by implementing that interface an object gets some special ability or behavior, then such an interface is called a **Marker Interface** or **Ability Interface** or **Tag Interface**.

- Some commonly used marker interfaces in Java are:
    - `Serializable Interface`
    - `Cloneable Interface`
    - `RandomAccess Interface`
    - `SingleThreadModel Interface` (used in older Servlet versions)

Example 1: By implementing the Serializable interface, objects of a class can:
- be saved into a file (serialization)
- travel across a network

Example 2: By implementing the Cloneable interface, an object becomes capable of creating an exact copy (clone) of itself.

**Q** Without having any methods, how do objects get ability in marker interfaces?

**Answer:** Even though marker interfaces do not contain any methods, objects get ability because internally the JVM (or Java API classes) provides the required functionality.  
When a class implements a marker interface, the JVM checks whether the object belongs to that interface using runtime checking (instanceof). Based on this check, special behavior is enabled.

**Q** Why does the JVM provide special ability for marker interfaces? 

**Answer:** The JVM provides the required ability for marker interfaces:
- To reduce the complexity of programming
- To make the Java language simple and easy to use
- To allow enabling special features without forcing programmers to implement unnecessary methods

**Q** Is it possible to create our own marker interface? 

**Answer:** Yes, it is possible to create a custom marker interface.





#### Adapter Classes

An Adapter class is a simple Java class that implements an interface and provides empty implementations for all the methods of that interface.

```java
interface X{
    void m1();
    void m2();
    void m3();
    void m4();
    void m5();
    void m6();
    ...
    void m1000();
}

abstract class AdapterX implements X{
    public void m1(){}
    public void m2(){}
    public void m3(){}
    public void m4(){}
    public void m5(){}
    public void m6(){}
    ...
    public void m1000(){}
}
```
If we directly implement an interface, then we must provide implementations for every method, whether required or not.
```java
class Test implements X{
    public void m3(){
        System.out.println("Line 3");
    }

    public void m1(){}
    public void m2(){}
    public void m4(){}
    public void m5(){}
    public void m6(){}
    ...
    public void m1000(){}
}
```
The adapter class provides empty (default) implementations for all interface methods.  

Problem in this approach:
- Increases the length of the code
- Reduces readability
- Adds many unnecessary method implementations

we can solve this problem by using Adapter classes  
Instead of implementing the interface directly, we extend the adapter class.
```java
class Test extends AdapterX{
    public void m3(){
        System.out.println("Line 3");
    }
}

class Sample extends AdapterX{
    public void m7(){
        System.out.println("Line 7");
    }
}

class Demo extends AdapterX{
    public void m1000(){
        System.out.println("Line 1000");
    }
}
```
[Image](https://tinyurl.com/2jzbtsn3)

We can develop a servlet in the following three ways:
1. By implementing the Servlet interface
2. By extending GenericServlet
3. By extending HttpServlet

[Image](https://tinyurl.com/34a5zedr)

If we implement the Servlet interface directly, then we must provide implementations for each and every method of that interface.  
This increases the length of the code and reduces readability.

Instead of implementing the Servlet interface directly, if we extend GenericServlet, we only need to provide an implementation for the service() method. For the remaining methods, we are not required to provide implementations.

Hence, GenericServlet acts more or less like an adapter class for the Servlet interface.

> **NOTE:** Marker interfaces and adapter classes simplify the complexity of programming. These are very useful utilities for programmers, and they make a programmer’s life easier.

#### Interface vs Abstract Class vs Concrete Class

- If we don’t know anything about the implementation and only have a requirement specification, then we should go for an interface.

Example : Servlet

- If we are talking about implementation but not completely (partial implementation), then we should go for an abstract class.

Example : GenericServlet, HttpServlet

- If we are talking about complete implementation and the class is ready to provide service, then we should go for a concrete class.

Example : MyOwnServlet

[Image](https://tinyurl.com/j8rd354p)


#### Difference Between Interface and Abstract Class

| Interface        | Abstract Class      |
| ------- | ------- |
| If we don’t know anything about the implementation and only have requirement specifications, then we should go for an interface.     | If we are talking about implementation but not completely (partial implementation), then we should go for an abstract class. |
| Inside an interface, every method is always **public** and **abstract**, whether we declare it or not. Hence, an interface is considered a **100% pure abstract class**.   | Methods inside an abstract class need not be public or abstract; we can also have concrete methods.     |
| Since interface methods are always public and abstract, we cannot declare them with the following modifiers: **private, protected, final, static, synchronized, native,** or **strictfp**. | There are no such restrictions on abstract class method modifiers.   |
| Every variable inside an interface is always **public, static, and final**, whether we declare it or not.    | Variables inside an abstract class need not be public, static, or final.  |
| Since interface variables are always public, static, and final, we cannot declare them with **private, protected, volatile,** or **transient** modifiers.      | There are no restrictions on abstract class variable modifiers.    |
| Interface variables must be initialized at the time of declaration; otherwise, a compile-time error occurs.     | Abstract class variables are not required to be initialized at the time of declaration.     |
| Inside an interface, we cannot declare static or instance blocks.     | Inside an abstract class, we can declare static and instance blocks.     |
| Interfaces cannot have constructors.  | Abstract classes can have constructors.  |

**Q** We cannot create an object of an abstract class, but the class can contain a constructor. What is the need for it?

An abstract class constructor is executed whenever we create a child class object. It is used to perform initialization of the common properties of the child class object.

Approach 1: Without a constructor in an abstract class
```java
abstract class Person{
    String name;
    int age;
    double weight;
    // ... 100 properties
}

class Student extends Person{
    int rollNo;

    Student(String name, int age, double weight, int rollNo){
        this.name = name;
        this.age = age;
        this.weight = weight;
        this.rollNo = rollNo;
    }
}

class Teacher extends Person{
    String subject;

    Teacher(String name, int age, double weight, String subject){
        this.name = name;
        this.age = age;
        this.weight = weight;
        this.subject = subject;
    }
}
```
👉 Problem:
Initialization code for common properties (`name`, `age`, `weight`, etc.) is repeated in every child class, which increases code duplication.

Approach 2: With a constructor in an abstract class
```java
abstract class Person{
    String name;
    int age;
    double weight;
    // ... 100 properties

    Person(String name, int age, double weight){
        this.name = name;
        this.age = age;
        this.weight = weight;
    }
}

class Student extends Person{
    int rollNo;

    Student(String name, int age, double weight, int rollNo){
        super(name, age, weight);
        this.rollNo = rollNo;
    }
}

class Teacher extends Person{
    String subject;

    Teacher(String name, int age, double weight, String subject){
        super(name, age, weight);
        this.subject = subject;
    }
}
```

> **NOTE:** either directly or indirectly we can't create object for abstract class

**Q** Anyway, we cannot create objects for an abstract class or an interface, but an abstract class can contain a constructor whereas an interface cannot. What is the reason?

The main purpose of a constructor is to perform initialization of instance variables.  

An abstract class can contain instance variables that are required by child class objects. To initialize these instance variables, a constructor is required in the abstract class. When a child class object is created, the abstract class constructor is automatically executed to initialize the common properties.  

However, every variable present inside an interface is always public, static, and final, whether we declare it explicitly or not. Since interfaces do not contain instance variables, there is no need for object-level initialization. Therefore, the constructor concept is not required in interfaces.

**Q** Whenever we create a child class object, the parent object is not created separately; only the parent class constructor is executed for initializing the child object.

```java
class P {
    P() {
        System.out.println(this.hashCode());
    }
}

class C extends P {
    C() {
        System.out.println(this.hashCode());
    }
}

class Test {
    public static void main(String[] args) {
        C c = new C();
        System.out.println(c.hashCode());
    }
}
```

**Q** Inside an interface every method is abstract, and we can also have only abstract methods in an abstract class. Then what is the difference between an interface and an abstract class? Is it possible to replace an interface with an abstract class?

Yes, we can replace an interface with an abstract class, but it is not a good programming practice. It is similar to recruiting an IAS officer for sweeping work.  

If everything is abstract, then it is highly recommended to use an interface instead of an abstract class.

Approch 1: Using Abstract Class
```java
abstract class X {

}

class Test extends X {

}
```
- When extending an abstract class, it is not possible to extend any other class because Java does not support multiple inheritance with classes. Hence, we may lose inheritance benefits.

- in this case object creation is costly Example: Test t = new Test(); // 2 min

Approch 2: Using Interface
```java
interface X {

}

class Test implements X {

}
```
- When implementing an interface, we can still extend another class. Hence, we do not lose inheritance benefits.
- in this case object creation is not costly Example: Test t = new Test(); // 2 sec

<hr/>

#### Question

<details>
<summary> 
Roles of new and Constructor Operator?
</summary>

- **new :-** The main objective of new operator is to create an object.
- **Constructor :-** The main purpose of constructor is to initialize object.
- First object will be created by using new operator and the then initialization will be performed by Constructor.
</details>

<details>
<summary>
Whenever we are creating child classs object, what is the need of executing Parent class Constructor? 
</summary>

 Whenever we create a child class object, the parent constructor is automatically executed to initialize the instance variables inherited from the parent.
[image](https://tinyurl.com/ChildConstructorParent)
```java
class Person{
    int age;String name;
    Person(String name,int age){
        this.name = name;
        this.age = age;
    }
}
class Student extends Person{
    int rollNo;int marks;
    Student(String name,int age,int rollNo,int marks){
        super(name,age); // Here, super calls the parent class constructor, and the parent class is Person.
        this.rollNo = rollNo;
        this.marks = marks;
    }
}

class Main{
    public static void main(String [] args){
        Student student = new Student("Raj",22,3779,86);
    }
}
```

In the above programme both parent and child constructor executed for child object initialization only.
</details>

<details>
<summary>
Whenever we are creating child class object whether Parent object will be created or not?
</summary>


Whenever we create a child class object, the parent constructor will be executed, but a parent object will not be created
```java
class Parent{
    Parent(){
        System.out.println(this.hashCode());
    }
}
class Child extends Parent{
    Child(){
        System.out.println(this.hashCode());
    }
}
class Main{
    public static void main(String []args){
       Child child = new Child();
       sout(child.hashCode()); 
    }
}
```
In the above example, we created only a child class object, but both the parent and child constructors were executed for that child object.
</details>

<details>
<summary>
Anyway we cannot create object for abstract class either directly or indirectly, But abstract class can contain constructor. What is the need?
</summary>


We cannot create an object of an abstract class either directly or indirectly, but an abstract class can still have a constructor. The main purpose of an abstract class constructor is to initialize the instance variables that are inherited by the child class. Whenever we create a child class object, the abstract class constructor is automatically executed to initialize the instance variables inherited from the abstract class. This ensures code reusability.

- Without Constructor in Abstract Class
```java
abstract class Person{
    String name;
    int age;
}
class Student extends Person{
    int rollNo;
    int marks;
    Student(String name,int age,int rollNo,int marks ){
        this.name = name;
        this.age = age;
        this.rollNo = rollNo;
        this.marks = marks;
    }
}
class Teacher extends Person{
    double salary;
    String subject;
    Teacher(String name,int age,double salary,String subject){
        this.name = name;
        this.age = age;
        this.salary = salary;
        this.subject = subject;
    } 
}
class Main{
    public static void main(String []args){
       Student student = new Student("Raj",48,101,90);
       Teacher teacher = new Teacher("Rahul",54,25,"JAVA"); 
    }
}
```
- With Constructor in Abstract Class
```java
abstract class Person{
    String name;
    int age;
    Person(String name,int age){
        this.name = name;
        this.age = age;
    }
}
class Student extends Person{
    int rollNo;
    int marks;
    Student(String name,int age,int rollNo,int marks ){
        super(name,age);
        this.rollNo = rollNo;
        this.marks = marks;
    }
}
class Teacher extends Person{
    double salary;
    String subject;
    Teacher(String name,int age,double salary,String subject){
        super(name,age);
        this.salary = salary;
        this.subject = subject;
    } 
}
class Main{
    public static void main(String []args){
       Student student = new Student("Raj",48,101,90);
       Teacher teacher = new Teacher("Rahul",54,25,"JAVA"); 
    }
}
```
</details>

<details>
<summary>
Anyway we cannot create object for Abstract class and interface.Abstract class can contain constructor but interface does not. Why?
</summary>

- The main purpose of a constructor is to initialize an object, that is, to provide values for its instance variables. 
- An abstract class can contain instance variables that are required by the child class object. To initialize these instance variables, a constructor is needed inside the abstract class.
- But Every variable in an interface is always public, static, and final, whether we explicitly declare it or not. Additionally, all interface variables must be initialized at the time of declaration. Therefore, there cannot be any instance variables in an interface.
- Because of this, the concept of initializing instance variables is not applicable to interfaces.
- Hence, the concept of a constructor is not required for an interface.

- With Abstract Class
```java
abstract class Person{
    String name;
    int age;
    Person(){
        this.name = name;
        this.age = age;
    }
}
```
- With Interface
```java
interface Person{
    // In an interface, variables are always public, static, and final, whether we declare them explicitly or not.
    long phoneNo = 767957832;
}
```
</details>

<details>
<summary>
Inside interface we can take only Abstract Methods. But in Abstract class Also we can take only Abstract Methods based on our requirement. Then what is the need of Interface? i.e. Is it possible to replace Interface Concept with Abstract class?
</summary>
</details>

<details>
<summary>
Inside interface we can take only Abstract Methods. But in Abstract class Also we can take only Abstract Methods based on our requirement. Then what is the need of Interface? i.e. Is it possible to replace Interface Concept with Abstract class?
</summary>

- If everything is abstract, it is highly recommended to use an interface instead of an abstract class. 
- We can replace an interface with an abstract class, but it is not a good programming practice. It is like recruiting an IAS officer for sweeping work.

| Interface | Abstract class |
|----------|----------------|
| <pre><code>interface X {}</code></pre>  | <pre><code>abstract class X {}</code></pre> |
|While implementing an interface, we can still extend another class therefore, we do not lose the benefits of inheritance. <br/>✅example:- <pre><code>class Test extends A ,implement X{}</code></pre> | While extending an abstract class, we cannot extend any other class; hence, we miss the benefit of multiple inheritance.<br/>❎example:- <pre><code>class Test extends A ,implements X{}</code></pre> |
| In this case, object creation is not costly.<br/><pre><code>class Test implements X{}</code><code>Test K = new Test(); //-> 2 sec</code></pre> | In this case, object creation is costly. <br/><pre><code>class Test extends X{}</code><code>Test K = new Test(); //-> 2 min</code></pre> |

</details>

<details>
<summary>
Which of the following are valid?
</summary> 

1. The Purpose of constructor is to create an object.❎
2. The Purpose of constructor is to initialize an object but not to create object.✅
3. Once constructor completes then only object creation completes.❎
4. Frst object will be created and then constructor will be executed.✅
5. The purpose of new key word is to create object and the purpose of constructor is to initialize that object.✅
6. We can't create object for Abstract class Directly but Indirectly we can create.❎ 
7. Whenever we are creating child class object Automatically Parent class object will be created internally.❎
8. Whenever we are creating child class object Automatically Abstract class constructor will be executed.✅
9. Whenever we are creating child class object Automatically Parent object will be created.❎
10. Whenever we are creating child class object Automatically Parent constructor will be executed but Parent object won't be created.✅
11. Either directly or Indirectly we can't create object Abstract class and Hence constructor concept is not applicable for abstract class.❎
12.Interface can contain Constructor.❎
</details>

<hr/>
