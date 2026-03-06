# Enum (Enumeration)
- [Enum (Enumeration)](#enum-enumeration)
  - [Enum Introduction](#enum-introduction)
  - [Internal Implementation of Enum](#internal-implementation-of-enum)
  - [Enum Declaration and Usage](#enum-declaration-and-usage)
  - [Applicable Modifiers for Enum](#applicable-modifiers-for-enum)
  - [Enum vs Switch](#enum-vs-switch)
  - [Enum vs Inheritance](#enum-vs-inheritance)
  - [java.lang.Enum](#javalangenum)
  - [values() Method](#values-method)
  - [ordinal() Method](#ordinal-method)
  - [Specialty of Java Enum](#specialty-of-java-enum)
  - [Enum Vs Constructor](#enum-vs-constructor)
  - [enum Vs Enum Vs Enumeration](#enum-vs-enum-vs-enumeration)

## Enum Introduction
If we want to represent a group of named constants, then we should use enum.

Example
```java
enum Month {
    JAN, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, DEC
}
```
- The semicolon (;) is optional if there are no additional members declared inside the enum.
- The main objective of an enum is to define our own data types, also called **enumerated data types**.
- The enum concept was introduced in Java 1.5. Compared to old languages, Java enums are more powerful.

## Internal Implementation of Enum

- Every enum is internally implemented using the class concept.
- Every enum constant is implicitly `public`, `static`, and `final`.
- Every enum constant represents an object of the enum type.

[Image](https://tinyurl.com/4cefsz82)

## Enum Declaration and Usage

Every enum constant is implicitly `public`, `static`, and `final`. Hence, we can access enum constants by using the enum name.

Example
```java
enum Beer {
    KF, FO, RC
}

class Test {
    public static void main(String[] args) {
        Beer b = Beer.RC;
        System.out.println(b);
    }
}
```
Output
```output
RC
```

> **NOTE:** Inside an enum, the `toString()` method is internally implemented to return the name of the constant.

- We can declare an enum either outside a class or inside a class, but not inside a method.
- If we declare an enum inside a method, we will get a compile-time error saying: `enum types must not be local`.

Examples

- 🟢 Valid: Enum outside a class
```java
enum X {}

class Y {}
```
- 🟢 Valid: Enum inside a class
```java
class Y {
    enum X {}
}
```
- 🔴 Invalid: Enum inside a method
```java
class Y {
    public void m() {
        enum C {}   // Compile-time error
    }
}
```

## Applicable Modifiers for Enum

1. If we declare an enum outside a class, the applicable modifiers are:
    - `public`
    - `default`
    - `strictfp`
2. If we declare an enum inside a class, the applicable modifiers are:
   - `public`
   - `default`
   - `strictfp`
   - `private`
   - `protected`
   - `static`

## Enum vs Switch

- Until Java 1.4, the allowed argument types for the switch statement were:
  - `byte`
  - `short`
  - `int`
- From Java 1.5 onwards, the corresponding wrapper classes (`Byte`, `Short`, `Integer`) and enum types are also allowed.
- From Java 1.7 onwards, `String` types are also allowed in a switch statement.  
Hence, from Java 1.5 onwards, we can pass enum types as arguments to a switch statement.

Example
```java
enum Beer {
    KO, FO, KF, RC
}

class Test {
    public static void main(String[] args) {
        Beer b = Beer.KO;

        switch (b) {
            case KF:
                System.out.println("KF Brand");
                break;

            case KO:
                System.out.println("KO Brand");
                break;

            case FO:
                System.out.println("FO Brand");
                break;

            case RC:
                System.out.println("RC Brand");
                break;

            default:
                System.out.println("Other Brand");
        }
    }
}
```
Output
```output
KO Brand
```
If we pass an enum type as an argument to a switch statement, then every case label must be a valid enum constant. Otherwise, we will get a compile-time error saying: `unqualified enumeration constant name required`

Example:
```java
enum Beer {
    KO, FO, KF, RC
}

class Test {
    public static void main(String[] args) {
        Beer b = Beer.KF;

        switch (b) {
            case KF:
                System.out.println("KF Brand");
                break;

            case KO:
                System.out.println("KO Brand");
                break;

            case FO:
                System.out.println("FO Brand");
                break;

            case Desi:   // Compile-time error (invalid enum constant)
                System.out.println("Desi Brand");
                break;

            default:
                System.out.println("Other Brand");
        }
    }
}
```
**Reason for error:**
Desi is not declared in the Beer enum, so the compiler throws a compile-time error.

## Enum vs Inheritance

- Every enum is always a direct child of `java.lang.Enum`. Hence, our enum cannot extend any other class (because Java does not support multiple inheritance for classes).
- Every enum is implicitly final, and therefore we cannot create a child enum.

Because of the above reasons, we can conclude that the inheritance concept is not applicable to enums, and we cannot use the extends keyword with enums.  

Example

- 🔴 Invalid: Enum extending another Enum
```java
enum X {}

enum Y extends X {}   // Compile-time error
```
**Reason**:  
An enum cannot extend another enum because it already extends java.lang.Enum.

- 🔴 Invalid: Enum extending java.lang.Enum explicitly
```java
enum X extends java.lang.Enum {}   // Compile-time error
```
**Reason**:
Every enum implicitly extends java.lang.Enum, so explicitly extending it is not allowed.

- 🔴 Invalid: Enum extending a Class
```java
class X {}

enum Y extends X {}   // Compile-time error
```
**Reason**:
An enum cannot extend any class, because it already extends java.lang.Enum.

- 🔴 Invalid: Class extending an Enum
```java
enum X {}

class Y extends X {}   // Compile-time error
```
**Reason**:
An enum is implicitly final, so no class can extend an enum.

- However, an enum can implement any number of **interfaces**.

Example 
```java
interface X {}

enum Y implements X {
}
```
In this example, the enum Y implements the interface X, which is valid in Java.

## java.lang.Enum

- Every enum in Java is a direct child class of `java.lang.Enum`. Hence, this class acts as the base class for all Java enums.
- It is an abstract class and a direct child class of `Object`.
- The `java.lang.Enum` class implements the following interfaces:
  - `Serializable`
  - `Comparable`

## values() Method

Every enum implicitly contains the values() method, which is used to list all the values present inside the enum.

Example
```java
Beer[] b = Beer.values();
```
> **Note:** 
> - The `values()` method is not present in `java.lang.Enum` or the `Object` class.
> - The `enum` keyword implicitly provides this method for every enum type.

## ordinal() Method

- Inside an enum, the order of constants is important, and we can represent this order by using the ordinal value.
- We can find the ordinal value of an enum constant by using the `ordinal()` method.

Method Declaration:
```java
public final int ordinal();
```
The ordinal value is 0-based, just like an array index.

Example
```java
enum Beer {
    KO, FO, RC, KF
}

class Test {
    public static void main(String[] args) {
        Beer[] b = Beer.values();

        for (Beer b1 : b) {
            System.out.println(b1 + " ......... " + b1.ordinal());
        }
    }
}
```
Output:
```output
KO ......... 0
FO ......... 1
RC ......... 2
KF ......... 3
```
## Specialty of Java Enum

- In old programming languages, enums could contain only constants.  
But in Java, enums can contain constants, methods, constructors, and normal variables.  

Hence, Java enums are more powerful than enums in older languages.

- Even in Java enums, we can declare a main() method, and we can run the enum directly from the command prompt.

Example
```java
enum Fish {
    STAR, GOLD, RUHI, KATAL;

    public static void main(String[] args) {
        System.out.println("Enum Fish");
    }
}
```
Output
```output
Enum Fish
```
> **Notes:**
> - If we declare extra members inside an enum (like methods, variables, or constructors), then the list of constants must appear first and must end with a semicolon (`;`).
> Inside an enum, if we include additional members, the first line must contain the list of constants followed by a semicolon.

Example

- 🟢 valid 
```java
enum Fish{
    STAR,GUPPY;

    public void m1(){}
}
```
**Reason**: Enum constants are declared first and end with ; because a method is defined.

- 🔴 Invalid
```java
enum Fish{
    STAR,GUPPY;

    public void m1(){}
}
```
**Reason**: Missing semicolon (;) after enum constants when additional members (methods) are declared.

- 🔴 Invalid 
```java
enum Fish{
    public void m1(){}
    STAR,GUPPY;
}
```
**Reason**: Enum constants must be declared before methods or other members.

- 🔴 Invalid
```java
enum Fish{
    public void m1(){}
}
```
**Reason**: If an enum has no constants, a semicolon (;) must appear before other members.

- 🟢 valid 
```java
enum Fish{
    ;
    public void m1(){}
}
```
**Reason**: Empty enum is valid and the semicolon separates the constant section from members.

- An empty enum is also valid Java syntax.
```java
enum Fish {
}
```

## Enum Vs Constructor

- An enum can contain constructors.
- The enum constructor will be executed separately for every enum constant at the time of enum class loading automatically.

Example :
```java
enum Beer7 {
    KF, KO, FO, RC;

    Beer7() {
        System.out.println("Constructor");
    }
}

class Test {
    public static void main(String[] args) {
        Beer7 b = Beer7.RC;   // Line 1
        System.out.println("Hello");
    }
}
```
Output:
- Test.class
```output
Constructor
Constructor
Constructor
Constructor
Hello
```
 - If Line 1 is commented, the output will be:
```output
Hello
```

- We cannot create enum objects directly, and hence we cannot invoke enum constructors directly.

Example :
```java
Beer b = new Beer();
```
Compile-time error: `enum types may not be instantiated`

Example : with Parameters in Enum Constructor
```java
enum Beer {
    KF(70), KO(80), RC(90), FO;

    int price;

    Beer(int price) {
        this.price = price;
    }

    Beer() {
        this.price = 65;
    }

    public int getPrice() {
        return price;
    }
}

class Test {
    public static void main(String[] args) {
        Beer[] b = Beer.values();

        for (Beer b1 : b) {
            System.out.println(b1 + "....." + b1.getPrice());
        }
    }
}
```

Output
```output
KF.....70
KO.....80
RC.....90
FO.....65
```

> **NOTE:** 
> - KF is internally treated as: `public static final Beer KF = new Beer();`
> - KF(70) is internally treated as: `public static final Beer KF = new Beer(70);`
> - Inside an enum, we can declare methods, but they must be concrete methods. Abstract methods cannot be declared inside enums.

**Case-1**

- Every enum constant represents an object of the enum type. Hence, whatever methods we can apply to normal Java objects can also be applied to enum constants.

Example :
```java
Beer.KF.equals(Beer.RC);                 // Valid
Beer.KF.hashCode() > Beer.RC.hashCode(); // Valid
Beer.KF < Beer.RC;                       // Invalid
Beer.KF.ordinal() < Beer.RC.ordinal();   // Valid
```

**Case-2**

- If we want to use any class or interface directly from another package, the required import is a normal import.

- If we want to access static members without using the class name, the required import is a static import.

Example : (Normal Import + Static Import)
```java
import static java.lang.Math.sqrt;
import java.util.ArrayList;

class Test {
    public static void main(String[] args) {
        ArrayList l = new ArrayList();

        System.out.println(sqrt(4));
    }
}
```
**Reason**:

- ArrayList requires a normal import.

- sqrt() is a static method, so we can use static import to call it without Math.sqrt().


Example : with Enum in Different Packages
```java
package pack1;

public enum Fish {
    STAR, GUPPY
}
```
```java
package pack2;

// Required import
// import pack1.Fish;
// or
// import pack1.*;

import pack1.Fish;

public class Test1 {
    public static void main(String[] args) {
        Fish f = Fish.GUPPY;
        System.out.println(f);
    }
}
```
**Reason**:
We use normal import to access the enum type from another package.

```java
package pack3;

// Required import
// import static pack1.Fish.STAR;
// or
// import static pack1.Fish.*;

import static pack1.Fish.STAR;

public class Test2 {
    public static void main(String[] args) {
        System.out.println(STAR);
    }
}
```
**Reason**:
We use static import to access the enum constant directly without using Fish.STAR.

```java
package pack3;

import pack1.Fish;
import static pack1.Fish.STAR;

public class Test3 {
    public static void main(String[] args) {

        Fish f = Fish.GUPPY;

        System.out.println(STAR);
    }
}
```
**Reason**:

- `import pack1.Fish;` → used to access the enum type.

- `import static pack1.Fish.STAR;` → used to access the enum constant directly.


**Case-3**

Example 
```java
enum Color {
    BLUE, RED, GREEN;

    public void info() {
        System.out.println("Universal color");
    }
}

class Test {
    public static void main(String[] args) {
        Color[] c = Color.values();

        for (Color c1 : c) {
            c1.info();
        }
    }
}
```
Output
```output
Universal color
Universal color
Universal color
```
**Reason**:

All enum constants use the same info() method defined in the enum

Example 2
```java
enum Color {
    BLUE,
    RED {
        public void info() {
            System.out.println("Dangerous color");
        }
    },
    GREEN;

    public void info() {
        System.out.println("Universal color");
    }
}

class Test {
    public static void main(String[] args) {
        Color[] c = Color.values();

        for (Color c1 : c) {
            c1.info();
        }
    }
}
```
Output
```output
Universal color
Dangerous color
Universal color
```
**Reason**:

The RED enum constant overrides the info() method, while BLUE and GREEN use the default implementation defined in the enum.

## enum Vs Enum Vs Enumeration

| **enum**                                                                       | **Enum**                                                                                                                         | **Enumeration**                                                                      |
| ------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| `enum` is a **keyword in Java** used to define a **group of named constants**. | `Enum` is a **class in Java** present in the **`java.lang` package**.                                                            | `Enumeration` is an **interface** present in the **`java.util` package**.            |
| It is used to **declare enumerated types** in Java.                            | Every enum in Java is a **direct child class of `java.lang.Enum`**, so this class acts as the **base class for all Java enums**. | We can use an **`Enumeration` object to get elements one by one from a collection**. |
| Example: `enum Day { MON, TUE, WED }`                                          | Example: `java.lang.Enum`                                                                                                        | Example: `Enumeration e = v.elements();`                                             |

