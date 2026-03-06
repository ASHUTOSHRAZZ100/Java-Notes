## OOPs

1. [Data Hiding](#data-hiding)
1. [Abstraction](#abstraction)
1. [Encapsulation](#encapsulation)
1. [Tightly Encapsulated class](#tightly-encapsulated-class)
1. [Is-A Relationship](#is-a-relationship)
1. [Has-A Relationship](#has-a-relationship)
1. [Method Signature](#method-signature)
1. [Overloading](#overloading)
1. [Overriding](#overriding)
1.  [Static Control flow](#static-control-flow)
1.  [Instance Control flow](#instance-control-flow)
1.  [Constructors](#constructors)
1.  [Copuling](#coupling) 
1.  [Cohesion](#cohesion)
1.  [Type-casting](#object-type-casting)

### Data Hiding

- External entities should not have direct access to the internal data of a class, and the internal data should not be exposed directly. This principle in OOP is referred to as **data hiding**.
- After validation, an outside person can access our internal data.
- By declaring data members (variables) as private, we can achieve data hiding.
- The main advantage of data hiding is security.

> **NOTE :-** It is highly recommended to declare data members (variables) as private.

```java
public class Account{
    private double balance;

    public double getBalance(){
        // check for validation
        return balance;
    }
}
```

<details>
<summary>
Example
</summary>

1. After providing the proper username and password, we can access our Gmail information.
2. Even though we are valid customers of the bank, we can access only our own account information, and we cannot access anyone else’s account information.
</details>

### Abstraction

- Abstraction is the concept of hiding internal implementation details while exposing only the essential services to the user.
- We can implement abstraction using **Interfaces** and **Abstract classes**.

<details>
<summary>
The main advantages of abstraction are:
</summary>

1. We can achieve security because we are not exposing our internal implementation.
2. We can make any kind of changes to our internal system without affecting external users, which makes enhancement easier.
3. It improves the maintainability of the application.
4. It makes the system easier to use.
</details>

<details>
<summary>
Example :- 
</summary>
Using the bank’s ATM GUI (Graphical User Interface), customers can view the available banking services, while the internal implementation remains hidden.
</details>

### Encapsulation

- The process of binding data and the corresponding methods into a single unit is called encapsulation.
- Example:- 
```text
class Student {
    Data Member
        +
    Methods (Behaviour)
}
```
- If any component follows data hiding and abstraction, such a component is said to be an encapsulated component.<br/>
Encapsulation = Data Hiding+ Abstraction

```java
public class Account{
    private double balance;

    public double getBalance(){
        // check validation

        return balance;
    }

    public void setBalance(double balance){
        // check validation

        this.balance = balance;
    }
}
```

<details>
<summary>
The main advantages of encapsulation are:
</summary>

1. We can achieve security.
2. Enhancements become easier.
3. It improves the maintainability of the application
</details>
<details>
<summary>
The main Disadvantages of encapsulation are:
</summary>

1. It increases the length of the code and slows down execution.
</details>

### Tightly Encapsulated class

- A class is said to be tightly encapsulated if and only if all its variables are declared as private.
- We do not need to check whether a class contains the corresponding getter and setter methods or whether these methods are declared as public.

- Example:- 
```java
public class Account{
    private double balance;
    public double getBalance(){
        // check validation
        return balance;
    }
}
```
<details>
<summary>
which of  the following classes are Tightly Encapsulated?
</summary>

```java 
// ✅ Tightly Encapsulated class
class A{
    private int x = 10;
}

// ❎ Tightly Encapsulated class
class B extends A{
     int y = 20;
}

// ✅ Tightly Encapsulated class
class C extends A{
    private int z = 30;
}
```
```java 
// ❎ Tightly Encapsulated class
class A{
    int x = 10;
}

// ❎ Tightly Encapsulated class
class B extends A{
     int y = 20;
}

// ❎ Tightly Encapsulated class
class C extends B{
    private int z = 30;
}
```
> **NOTE :-** If the parent class is not Tightly Encapsulated then no child class is Tightly Encapsulated.
</details>

### Is-A Relationship

- It is also Know as **Inheritance**.
- The main advantage is code Reusability.
- By using **extends** keyword, we can implement an Is-A relationship.

```java
class Parent{
    public void m1(){
        System.out.println("Call Parent")
    }
}
class Child extends Parent{
    public void m2(){
        System.out.println("Call Child")
    }
}
class Main {
    public static void main(String [] args){
        // case 1
       Parent parent = new Parent();
       parent.m1();//✅
       parent.m2();//❎ Compiler Error: cannot find symbol: method m2() location: class Parent

        // case 2
       Child child = new Child();
       child.m1();//✅
       child.m2();//✅

        // case 3
       Parent parent = new child();
       parent.m1();//✅
       parent.m2();//❎ Compiler Error: cannot find symbol: method m2() location: class Parent

        // case 4
       Child child = new Parent();//❎ Compiler Error: incompatible types found: Parent required:Child
    }
}
```
<details>
<summary>
Conclusion
</summary>

- All methods that the parent has are by default available to the child, so using the child reference, we can call both parent and child class methods.

- Methods specific to the child are not available to the parent, so using the parent reference, we cannot call child-specific methods.

- A parent reference can hold a child object, but using that reference, we cannot call child-specific methods; we can only call methods present in the parent class.

- A parent reference can hold a child object, but a child reference cannot hold a parent object.
</details>

- Without Inheritence
```java
class HomeLone{
    300 methods
}
class PersonalLone{
    300 methods
}
class FarmLone{
    300 methods
}
```
- With Inheritence
```java
class Lone{
    250 methods
}
class HomeLone extends Lone{
    50 methods
}
class PersonalLone extends Lone{
    50 methods
}
class FarmLone extends Lone{
    50 methods
}
```
> **NOTE :-** Most comman methods which are applicable for any type of child, we have to define in the parent class.<br/>
> The specific methods which are applicable for a particular child we have to define in child class.

- The entire Java API is implemented based on the concept of inheritance. The most common methods applicable to any Java object are defined in the Object class. Therefore, every class in Java is a child of the Object class, either directly or indirectly. This means the methods of the Object class are automatically available to every Java class without rewriting them. Thus, the Object class acts as the root of all Java classes.
- Throwable defines the most common methods required by all exception and error classes; therefore, this class acts as the root of the exception hierarchy.<br/>
[image](https://tinyurl.com/4arsahjr)

### Multiple Inheritance

- A java class can't extend more than one class at a time hence java won't provide support for multiple inheritance in classes.

```java
// Compile Error we get for this classes 
class A extends B,C{

}
```
> **NOTE :-** If our class doesn't extend any other class then only our class is direct child class of object.

```java
class A{}
// object <----- A
```
> **NOTE :-** If our class extends any other class then our class is indirect child class of object.
```java
class A extends B{}
// object <----- B <------ A
```
[Image](https://tinyurl.com/4fe8mkmy)

> **NOTE :-** Either directly or indirectly java won't provide support for inheritance with respect to classes.

<details>
<summary>
Why Java won't provide support for multiple inhertance?
</summary>

- There may be chance of ambiguity problem hence a java won't provide support for multiple inheritance.

- [Image](https://tinyurl.com/26j36b44)<br/>
If class C extends both P1 and P2, and both P1 and P2 contain the m1 method, then calling m1 on the child object may cause ambiguity.
- But an interface can extend any number of interfaces simultaneously; therefore, Java provides support for multiple inheritance with respect to interfaces.

```java
interface A{}
interface B{}
interface C extends A,B{}
```
</details>

<details>
<summary>
Why ambiguity problem won't be there in Interfaces
</summary>

- [Image](https://tinyurl.com/3hy5ee35)<br/>
Even though multiple method declarations are available, the implementation is unique; therefore, there is no chance of ambiguity in interfaces.
> **NOTE :-** Strictly speaking, interfaces do not provide inheritance.
</details>

### Cyclic Inhertance

- Cyclic Inhertance is not allowed in java of course it is not required.
- Example:- [Image](https://tinyurl.com/485zahhc)
```java
//  Compile Error : Cyclic Inhertance involving A
class A extends A{
}
```
```java
//  Compile Error : Cyclic Inhertance involving A
class A extends B{
} 
class B extends A{
}
```
> **Important :-** In both example we get Compile Error : Cyclic Inhertance involving A

### Has-A Relationship

- A Has-A relationship is also known as composition or aggregation.
- There is no specific keyword to implement a Has-A relationship, but most of the time we depend on the **new** keyword.
- The main advantage of a Has-A relationship is code reusability.
- Example:- 
```java
class Engine {
        // ENgine specific functionality
}
class Car{
    Engine engine = new Engine();
}
```
- Car Has-A Engine Reference.

<details>
<summary>
Difference between Composition and Aggregation
</summary>

|   Composition | Aggregation|
|---------------|------------|
|If there is no chance for the contained object to exist without the container object, then the container and contained objects are strongly associated. This strong association is known as composition.| If the contained object can exist even without the container object, then the container and contained objects are weakly associated. This weak association is known as aggregation. |
| Example: A university consists of several departments. Without the existence of the university, there is no chance for the departments to exist. Hence, the university and its departments are strongly associated, and this strong association is known as composition. | A department consists of several professors. Even without the existence of the department, there may still be a chance for professor objects to exist. Hence, the department and professor objects are weakly associated, and this weak association is known as aggregation. |
|[Digram](https://tinyurl.com/bdme7dcx)|[Digram](https://tinyurl.com/5t2h87bt)|


> **NOTE :-** In composition, objects are strongly associated, whereas in aggregation, objects are weakly associated.<br/>
> In composition container object holds directly contined object where as in aggregation container object holds just references of contained objects.  
</details>

<details>
<summary>
Is-A Relationship VS Has-A Relationship
</summary>

|Is-A Relationship | Has-A Relationship|
| ---------- | --------------|
| If we want all the functionalities automatically, then we should go for an Is-A relationship.| If we want part-of functionality, then we should go for a Has-A relationship|
|Example :- [Digrame](https://tinyurl.com/bdcc8c3u) |Example :- [Digrame](https://tinyurl.com/bbeerbe8) |

</details>

### Method Signature

In Java, the method signature is defined by the method name and its parameter types.
- Example :-
```java
 public static int m1(int i, float f) {} // from this  m1(int,float) is a Method Signature
```

> **NOTE :-** Return type is not part of Method Signature in java.

- Compiler will use Method Signature to resolve method calls.

```java
class Test{
    public void m1(int i){}
    public void m2(String s){}
}
class Main{
    public static void main(String [] args){
        Test t = new Test();
        t.m1(10);//✅
        t.m2("Raaz");//✅
        t.m3(10.5);//❎ Compiler Error: can't find symbol: method m3(double) location: class Test 
    }
}
```
- Within a class, having two methods with the same signature is not allowed
```java
class Test{
    public void m1(int i){}
    public int m1(int x){
        return x;
    }
}
class Main{
    public static void main(String [] args){
        Test t = new Test();
        t.m1(10);// ❎ compiler Error: m1(int) is already defined in Test
    }
}
```

### Overloading

Two methods are said to be overloaded only if both methods have the same name but different argument types.

- In the C language, the concept of method overloading is not available; therefore, we cannot declare multiple functions with the same name but different argument types.
- If there is a change in argument type, we must use a new method name, which increases the complexity of programming

```C
abs(int i)
labs(long i)
fabs(float i)
```
- But in Java, we can declare multiple methods with the same name but different argument types. Such methods are called overloaded methods.
```java
abs(int i)
abs(long i)
abs(float i)
```
- Having the concept of overloading in Java reduces the complexity of programming.

```java
class Test{
    public void m1(){
        System.out.println("no-argument")
    }
    public void m1(int i){
        System.out.println("int-argument")
    }
    public void m1(double i){
        System.out.println("double-argument")
    }
    public static void main(String [] args){
        Test t = new Test();
        t.m1();// no-argument
        t.m1(10);// int-argument
        t.m1(12.3);// double-argument
    } 
}
```
- In overloading, method resolution is always handled by the compiler based on the reference type. Hence, overloading is considered compile-time polymorphism, static polymorphism, or early binding.

<details>
<summary>
Case 1
</summary>

- Automatic promotion in overloading occurs while resolving overloaded methods. If an exact matching method is not available, we do not get a compile-time error immediately. First, the argument is promoted to the next level, and the compiler checks whether a matching method is available. If a match is found, that method is considered. If not, the compiler again promotes the argument to the next level. This process continues through all possible promotions, and if no suitable method is found, then a compile-time error will be raised.
- The following are the possible promotions in method overloading: 
    - >byte → short → int → long → float → double
    - >char → int → long → float → double

This process is called automatic promotion in overloading.
```java
        class Test{
            public void m1(int i){
                System.out.println("int-argument");
            }
            public void m1(float i){
                System.out.println("float-argument");
            }
            public static void main(String []args){
                Test t = new Test();
                t.m1(10);//✅ int-argument
                t.m1(10.5f);//✅ float-argument
                t.m1('a');//✅ int-argument
                t.m1(10l);//✅ float-argument
                t.m1(10.5);//❎ compile Error: cannot find symbol: method m1(double) location: class Test
            }
        }
```
</details>

<details>
<summary>
Case 2
</summary>

```java
class Test{
    public void m1(String s){
        System.out.println("String version");
    }
    public void m1(Object o){
        System.out.println("object version");
    }
    public static void main(String []args){
    Test t = new Test();
       t.m1(new Object());// Object version
       t.m1("Raj");// String version
       t.m1(null);// String version
    }
}
```

> **NOTE :-** While resolving overloaded  meathod compiler will always gives the precendence for child type argument then compare with parent type argument.

</details>

<details>
<summary>
Case 3
</summary>

```java
class Test{
    public void m1(String s){
        System.out.println("String version");
    }
    public void m1(StringBuffer s){
        System.out.println("StringBuffer version");
    }
    public static voidmain(String []args){
        Test t= new Test();
        t.m1("Raj");// string version
        t.m1(new StringBuffer("Ashu"));// stringBuffer version
        t.m1(null);// Compile Error: reference to m1() is ambiguous
    }
}
```
</details>

<details>
<summary>
Case 4
</summary>

```java
class Test{
    public void m1(int i, float f){
        System.out.println("int-float version")
    }
    public void m1(float i, int f){
        System.out.println("float-int version")
    }
    public static voidmain(String []args){
        Test t= new Test();
        t.m1(10,10.5f);// int-float version
        t.m1(10.5f,10);// float-int version
        t.m1(10,10);// Compile Error: reference to m1() is ambiguous.
        t.m1(10.5f,10.5f);// Compile Error: can't find symbol: method m1(float,flaot) location: class Test.
    }
}
```
</details>

<details>
<summary>
Case 5
</summary>

```java
class Test{
    public void m1(int i){
        System.out.println("General Method")
    }
    public void m1(int... x){
        System.out.println("var-arg Method")
    }
    public static voidmain(String []args){
        Test t= new Test();
        t.m1();// var-arg Method
        t.m1(10,20);// var-arg Method
        t.m1(10);// General Method
        t.m1(10.5f,10.5f);// Compile Error: can't find symbol: method m1(float,flaot) location: class Test.
    }
}
```
- In general, a var-arg method gets the least priority; that is, it is considered only if no other method matches. It is exactly like the default case in a switch statement.
</details>

<details>
<summary>
Case 5
</summary>

```java
class Animal{

}
class Monkey extends Animal{

}

class Test{
    public void m1(Animal a){
        System.out.println("Animal version");
    }
    public void m1(Monkey m){
        System.out.println("Monkey version");
    }
    public static void main(String []args){
        Test t = new Test();
        //case1
        Animal a = new Animal();
        t.m1(a);// Animal version
        //case2
        Monkey m = new Monkey();
        t.m1(m); // Monkey version
        // case3
        Animal a1 = new MOnkey();
        t.m1(a1);// Animal version
    }
}
```
> **NOTE :-** In overloading, method resolution is always handled by the compiler based on the reference type. In overloading, the runtime object does not play any role.
</details>

### Overriding

- Whatever methods the parent has are by default available to the child through inheritance. If the child class is not satisfied with the parent class implementation, then the child is allowed to redefine that method based on its requirement. This process is called overriding.

- The parent class method that is overridden is called the overridden method, and the child class method that overrides it is called the overriding method.

- In overriding, method resolution is always handled by the JVM based on the runtime object. Hence, overriding is also considered runtime polymorphism, late binding, or dynamic polymorphism.

```java
class Parent{
    public void property(){
        System.out.println("cash-land-gold");
    }
    // Overridden method
    public void marry(){
        System.out.println("Parent choose Girl");
    }
}
class Child extends Parent{
    // overriding method
    public void marry(){
        System.out.println("My choose Girl");
    }
}
class Test{
    public static void main(String [] args){
        Parent p = new Parent();
        p.marry();// run Parent method
        Child c = new Child();
        c.marry(); // run child method
        Parent p1 = new Child();
        p1.marry(); // run child method
    }
}
```

#### Rules for overriding
<details>
<summary>
Rules 1
</summary>

1. In overriding, method names and argument types must match; i.e., the method signature must be the same.
2. In overriding, the return type must be the same, but this rule applied only until JDK 1.4. From JDK 1.5 onwards, we can use [co-variant return types](#co-variant-return-types). According to this, the child class method’s return type need not be exactly the same as the parent method’s return type; a subtype of the parent return type is also allowed.
```java
// It is invalid in 1.4 version but from 1.5 version onwards it is valid.
class P{
    public Object m1(){
        return null;
    }
}
class C extends P{
    public String m1(){
        return null;
    }
}
```
</details>

<details>
<summary>
Rules 2
</summary>

3. Private methods are NOT inherited, because they are not visible outside the parent class. Since overriding requires inheritance + same signature + visibility to child, overriding is NOT applicable for private methods.
4. Based on our requirement we can deffine exactly same private method in child class it is valid but not overriding.
```java
// It is valid but not overriding
class P{
    private void m1(){
        System.out.println("Parent methods");
    }
}
class C extends P{
    private void m1(){
        System.out.println("Child methods");
    }
}
```
</details>

<details>
<summary>
Rules 3
</summary>

5. If a method in the parent class is declared as final, it cannot be overridden in the child class.<br/>
If we try to override it, the compiler will throw a compile-time error.
```java
// Compiler Error: m1() in C cannot override m1() in P, override method is final 
class P{
    public final void m1(){}
}
class C extends P{
    public void m1(){}
}
```
</details>

<details>
<summary>
Rules 4
</summary>

6. If a parent class has abstract methods, then a non-abstract child class must override them and provide implementation.
```java
abstract class P{
    public abstract void m1();
}
class C extends P{
    public void m1(){

    }
}
```
7. we can override non abstract method as abstract.
```java
class P{
    public void m1(){}
}
abstract class C extends P{
    public abstract void m1();
}
```
The main advantage of this approach is that we can stop the availability of the parent method implementation to the next-level child class.
</details>

<details>
<summary>
Rules 5
</summary>

8. In overriding, the following modifiers won’t impose any restrictions. [Image](https://tinyurl.com/3449s9tm) 
    - Synchronized
    - Native
    - Strictfp

9. While overriding, we cannot reduce the scope of the access modifier, but we can increase it. [Image](https://tinyurl.com/3449s9tm)
```text
private < default < protected < public
```
```java
// Compile Error: m1() in C cannot averride m1() in P, attemptions to assign weaker access privleges, was public. 
class P{
    public void m1(){
    }
}
class C extends P{
    void m1(){}
}
```
> **NOTE :-** Overriding cocept not applicable for private methods.
</details>


<details>
<summary>
Rules 6
</summary>

10. If a child class method throws any checked exception, then the parent class method must also declare the same checked exception or its parent exception; otherwise, we get a compile-time error. However, there is no such restriction for unchecked exceptions.
    - <details>
        <summary>Options are:-
        </summary>

        1. >P: public void m1() throws Exception <br/> C: pubic void m1() <br/> this opition is ✅

        2. >P: public void m1()  <br/> C: pubic void m1() throws Exception <br/> this opition is ❎

        3. >P: public void m1() throws Exception <br/> C: pubic void m1() throws IOException <br/> this opition is ✅

        4. >P: public void m1() throws IOException <br/> C: pubic void m1() throws Exception <br/> this opition is ❎

        5. >P: public void m1() throws IOException <br/> C: pubic void m1() throws FileNotFoundException, EOFException <br/> this opition is ✅

        6. >P: public void m1() throws IOException <br/> C: pubic void m1() throws EOFException, InterruptedException<br/> this opition is ❎

        7. >P: public void m1() throws IOException <br/> C: pubic void m1() throws AE,NPE,CCE <br/> this opition is ✅

        </details>

Example :-

```java

// Compiler Error m1() in cannot override m1() in P; overridden method doesn't throw java.lang.InterruptedException
import java.io.*;

class P{
    public void m1()throws IOException{}
}
class C extends p{
    public void m1()throws EOFException,InterruptedException
}
```

</details>

#### Co-variant return types

- [Image](https://tinyurl.com/2dp3ns2b) 
- Co-variant return type applies only to object/reference types, not primitive types. <br/>
So in overriding, the child method can return a subclass of the parent method’s return type only when the return type is a class/interface type.
- Example (Valid – Object Types)
```java
class Parent {
    Number m1() {
        return 10;
    }
}

class Child extends Parent {
    Integer m1() {   // Integer is a subtype of Number → Allowed
        return 10;
    }
}
```
❌ Not Allowed for Primitive Types

```java
class Parent {
    int m1() { return 10; }
}

class Child extends Parent {
    long m1() { return 10; }  // Not allowed – primitives don't support covariance
}
```
Primitive types must match exactly in overriding.

#### Overriding with respect to static methods

<details>
<summary>
Case 1
</summary>

We cannot override a static method as a non-static method; otherwise, we will get a compile-time error.

 ```java
 // Compile error: m1() in C can't override in P; overridden method is static
class P{
    public static void m1(){}
}
class C extends P{
    public void m1(){}
}
 ```
 Output:-
 ```output
Compile error: m1() in C can't override in P; overridden method is static
 ```
</details>

<details>
<summary>
Case 2
</summary>

Similarly, we cannot override a non-static method as static.
```java
 // Compile error: m1() in C can't override in P; overriding method is static
class P{
    public  void m1(){}
}
class C extends P{
    public static void m1(){}
}
 ```
  Output:-
 ```output
Compile error: m1() in C can't override in P; overriding method is static
 ```
</details>

<details>
<summary>
Case 3
</summary>

If both the parent and child class methods are static, then we won’t get any compile-time error. It may seem like overriding is applicable for static methods, but it is not overriding; it is called [method hiding](#method-hiding).
```java
// it is method hiding not overriding
class P{
    public static void m1(){}
}
class C extends P{
    public static void m1(){}
}
 ```
</details>

#### Method Hiding

All rules of method hiding are exactly the same as overriding, except for the following differences.

<details>
<summary>
Method hiding Vs Overriding
</summary>

| Method hiding | Overriding |
| ------------- | ----------- |
| Both the parent and child class methods must be static. | Both the parent and child class methods must be Non-static.|
| The compiler is responsible for method resolution based on the reference type. | The JVM is always responsible for method resolution based on the runtime object. |
| It is also known as compile-time polymorphism, static polymorphism, or early binding. | It is also known as runtime polymorphism, dynamic polymorphism, or late binding.|
</details>

```java
// It is method hiding but not overriding 
class P{
    public static void m1(){
        Systemout.println("Parent");
    }
}
class C extends P{
    public static void m1(){
        Systemout.println("Child");
    }
}
class Test{
    public static void main(String[] args){
        P p = new P();
        p.m1(); // Parent methods

        C c = new C();
        c.m1(); // Child methods

        P p1 = new C();
        p1.m1();// Parent method

    }
}
```
Output:- 
```output
Parent
child
Parent
```
If both parent and child class methods are non-static, then it is considered overriding. In this case, above code the output is :-

Output:-

```output
 Parent
 Child
 Child
```

#### Overriding with var-arg methods

- We can override a var-arg method only with another var-arg method.<br/>
If we try to override it using a normal (non–var-arg) method, then it will not be treated as overriding; instead, it will be considered method overloading, not overriding.
```java
// It is overrloading but not overriding
class P{
    public void m1(int...x){
        System.out.println("Parent");
    }
}
class C extends P{
    public void m1(int x){
        System.out.println("Child");
    }
}
class Test{
    public static void main(String[]args){
        P p = new P();
        p.m1(10);
        C c = new C();
        c.m1(10);

        P p1 = new C();
        p1.m1(10);
    }
}
```
Output:- 
```output
Parent
child
Parent
```
- In the above program, if we replace the child method with a var-arg method, then it will become overriding.
```java
// It is overriding but not overloading
class P{
    public void m1(int...x){
        System.out.println("Parent");
    }
}
class C extends P{
    public void m1(int... x){
        System.out.println("Child");
    }
}
class Test{
    public static void main(String[]args){
        P p = new P();
        p.m1(10);
        C c = new C();
        c.m1(10);

        P p1 = new C();
        p1.m1(10);
    }
}
```
Output:- 
```output
Parent
child
Child
```

#### Overrding with respect to variables

Variable resolution is always taken care of by the compiler based on the reference type, irrespective of whether the variable is static or non-static. (Overriding concept is applicable only for methods, but not for variables.)

```java
class P{
    int x=888;
}
class C extends P{
    int x = 999;
}
class Main{
    public static void main(String []args){
        P p =new P();
        System.out.println(p.x);
        C c =new C();
        System.out.println(c.x);
        P p1 =new C();
        System.out.println(p1.x);
    }
}
```
Output:-
```output
888
999
888
```
This table is based on above Code Output
| P-> non-static <br/> C-> non-static | P-> static <br/> C-> non-static  | P-> non-static <br/> C-> static | P-> static <br/> C-> static | 
|------|-----|------|------|
| 888 |888 | 888 | 888 |
| 999 |999 | 999 | 999 |
| 888 |888 | 888 | 888 |

#### Overrding Vs overloading

| Property | Overloading | Overidding|
|----------|-------------|-----------|
| methods Names | must be same | must be same  |
| Argument Types | must be different[atleast oeder] | must be same[including order] |
| Return types | No Restrictions | must be same until 1.4 version but from 1.5 version onward co-varient return types also allowed |
|pivate, static, final methods |can be overloaded|  can't be overridden |
| Access modifiers | No Restrictions | we can't reduce the scope of access modifier but we can increase it |
| throws Clause | No Restrictions | if child class method throws any checked exception compulsary parent class method should throw the same checked exception our it's parent but no restrictions for unchecker exception |
| method Resolution | Always taken care by Compiler based on Reference type | Always takes care by JVM based on runtime object |
| It is also known as| Compiletime polymorphism or static polymorphism or early binding | Runtime polymorphism or late binding, or dynamic polymorphism |

> **NOTE :-** 
> - In overloading we have to check only method names (must be same and argument must be different) 
> - we are not required to check remaning like return types, access modifiers etc
> - But in overriding everything we have to check method name, argument types, return types, access modifiers, throws class etc.


<details>
<summary>
Valid Method Declarations in Child Class
</summary>

Consider the following method in the parent class:
```java 
public void m1(int x) throws IOException
``` 
In the child class, which of the following methods can we take?
- ```public void m1(int i)``` — Correct, based on overriding.
- ```public static void m1(long i)``` — Correct, but this is based on overloading, not overriding.
- ```public static void m1(int i)``` — Wrong, with respect to overriding.
- ```public void m1(int i) throws Exception``` — Wrong, because in overriding we cannot throw a broader checked exception than the parent method.
- ```public static abstract void m1(double i)``` This will cause a compile-time error because static and abstract is an illegal combination of modifiers.
</details>

### Polymorphism

One name but multiple forms is the concept of polymorphism.
-If the method name is the same but we use different types of arguments, the concept is called overloading.<br/>
Example:-
```java
// overloading
abs(int)
abs(long)
abs(float)
```
- When the method signature is the same, but the parent class has one implementation and the child class has another implementation, this concept is called method overriding.
Example:-
```java
// overriding
class P{
    void marry(){
        System.out.println("Parent chosse girl");
    }
}
class C extends P{
    void marry(){
        System.out.println("My chosse girl");
    }
}
```
- Using a parent reference to hold a child object is the concept of polymorphism.<br/>
Example:-
```java
List l = new ArrayList();
List l = new LinkedList();
List l = new Stack();
List l = new Vector();
```
- Parent class Refrence can be used to hold child object but by using that refernce we can call only the methods valiable in parent class and we can't call child specific methods.
```text
P -> m1()
|
|
C -> m2()

P p = new C()

p.m1() ✅
p.m2() ❎ CompileTime error: can't find symbole: method m2() location: class P
```
But by using child refrence we can call both parent and child class methods
```text
C c = new C()
c.m1() ✅ 
c.m2() ✅ 
```
- When should we use a parent reference to hold a child object?
    - If we don’t know the exact runtime type of the object, then we should use a parent reference. For example, the first element present in an ArrayList can be of any type. It may be a Student object, Customer object, String object, or StringBuffer object. Hence, the return type of the get() method is Object, which can hold any type of object.
    ```java
    Object o = l.get(0)
    ```

|C c = new C()| P p = new C()|
|--------------| ------------|
|Example:- ```ArrayList l= new ArrayList()``` |Example:- ```List l= new ArrayList()``` |
| We can use this approach if we know the exact runtime type of the object. | We can use this approach if we don’t know the exact runtime type of the object. |
| By using a child reference, we can call both parent class and child class methods. (This is an advantage of this approach.) |  By using a parent reference, we can call only the methods available in the parent class; we cannot call child-specific methods. (This is a disadvantage of this approach.)|
| We can use a child reference to hold only a particular child class object. (This is a disadvantage of this approach.) | We can use a parent reference to hold any child class object. (This is an advantage of this approach.) |

[Image](https://tinyurl.com/2jmxt8u5)

### Three Pillars Of OOPs 
[Image](https://tinyurl.com/mr3kdudn)
- Polymorphism
- Encapsulation
- Inheritance

### Coupling

- The degree of dependence between components is called coupling.
- If the dependence is high, it is considered tightly coupled.
- If the dependence is low, it is considered loosely coupled.
- Example:-
```java
class A{
    static int i = B.j;
}
class B{
    static int j = C.k;
}
class C{
    static int k =D.m1();
}
class D{
   public static int m1(){
    return 10;
   }
}
```
The above components are said to be tightly coupled with each other because the dependence between the components is high. 
- Tight coupling is not a good programming practice because it has several serious disadvantages:
    - We cannot modify any component without affecting the remaining components; hence enhancement becomes difficult.
    - It suppresses reusability.
    - It reduces the maintainability of the application.
    - Hence, we have to keep the dependency between components as low as possible; therefore, loosely coupling is considered good programming practice.

### Cohesion

- For every component, if a clear and well-defined functionality is specified, then that component is said to follow high cohesion. [Image](https://tinyurl.com/38mcc5w8)

- High cohesion is always good programming practice because it has several advantages:
     
    - Without affecting the remaining components, we can modify any component; hence enhancement becomes easy.
    - It promotes reusability of code (wherever validation is required, we can reuse the same validation servlet without rewriting).
    - It improves the maintainability of the application.

    > **NOTE :-** Loose coupling and high cohesion are good programming practices.

### Object Type-casting

- We can use a parent reference to hold a child object. Example:- ```Object o = new String("Raj")```
- We can use an interface reference to hold an implementing class object. Example :- ```Runnable r = new Thread();``` 

Syntax :- ```A b = (C) d```
```
    A = class/interface Name
    b = Name of Refrence variable
    C = class/interface Name
    d = Refrence variable Name
```
<details>
<summary>
Mantra 1 (Compile-time Checking 1)
</summary>

The types of ```d``` and ```C``` must have some relationship—either parent-to-child, child-to-parent, or the same type. Otherwise, we will get a ```compile-time error saying inconvertible types: found d, required C```.<br/>
Example 1 :- ✅ Correct
```
Object o = new String("Raj");
StringBuffer sb = (StringBuffer) o;
```
Example 2 :- ❎ Wrong
```
String s = new String("Raj");
StringBuffer sb = (StringBuffer) s;
```
Output :- 
```output
CompileTime error: inconvertible types found : java.lang.String required: java.lang.StringBuffer
```
</details>

<details>
<summary>
Mantra 2 (Compile-time Checking 2)
</summary>

```C``` must be either the same type as ```A``` or a derived type of ```A```; otherwise, we will get a ```compile-time error saying “incompatible types: found C, required A```.<br/>
Example 1 :- ✅ Correct
```
Object o = new String("Raj");
StringBuffer sb = (StrinBuffer) o;
```
Example 2 :- ❎ Wrong
```
Object o = new String("Raj");
StringBuffer sb = (String) o;
```
Output :- 
```output
Compile time error incompatible types found: java.lang.String required: java.lang.StringBuffer
```
</details>

<details>
<summary>
Mantra 3 (Run-time Checking)
</summary>

The runtime object type of ```d``` must be either the same as ```C``` or a derived type of ```C```; otherwise, we will get a ```runtime exception saying ClassCastException```.<br/>
Example 1 :- ❎ Wrong
```java
Object o = new String("Raj");
StringBuffer sb = (StringBuffer) o;
```
Output:- 
```output
runtime exception ClassCastException: java.lang.String can't be cast to java.lang.StringBuffer
```
Example 2 :- ✅ Correct
```java
Object o = new String("Raj");
Object o1 = (String) o;
```
</details>

- [Image](https://tinyurl.com/3pfa48st)

```Base2 b = new Der4();``` these are the options are correct and wrong  
``` 1. Object o = (Base2) b; ```✅  
``` 2. Object o = (Base2) b;```❎ compile-time error  
``` 3. Object o = (Base2) b;```❎ Run-time error  
``` 4. Object o = (Base2) b;```❎ compile-time error  
``` 5. Object o = (Base2) b;```❎ compile-time error  
``` 6. Object o = (Base2) b;```❎ compile-time error  

- Strictly speaking, through type casting we are not creating any new object.
-  For the existing object, we are only providing another type of reference variable. That means we are performing type casting, not object casting.

Example :- [Image](https://tinyurl.com/43kxhdky)
```
String s = new String("Raj")
Object o = (Object) s;
```
Example 1 :- [Image](https://tinyurl.com/29e28zfc)

> **NOTE :-** [Image](https://tinyurl.com/3m6zndtr)

Example 2 :- A parent reference can be used to hold a child object, but by using that reference we cannot call child-specific methods; we can call only the methods available in the parent class. [Image](https://tinyurl.com/bdc2v2bh)

Example 3 :- This is overriding, and method resolution is always based on the runtime object. [Image](https://tinyurl.com/mx8z8nse)

Example 4 :- This is method hiding, and method resolution is always based on refrench type. [Image](https://tinyurl.com/4a788cpf)

Example 5 :- Variable resolution is always based on the reference type but not on the runtime object.[Image](https://tinyurl.com/356a8pud)

### Static Control Flow

Whenever we execute a Java class, the following sequence of steps will be executed as part of static control flow:
- Identification of static members from top to bottom.
- Execution of static variable assignments and [static blocks](#static-block) from top to bottom.
 - Execution of the main() method.

[Image](https://tinyurl.com/2mmd5np2)
 ```java
 class Base{
     static int i = 10
     static{
        m1();
        System.out.println("First static Block");
     }
     public static void main(String[] args){
        m1();
        System.out.println("Main Block");
     }
     public static void m1(){
        System.out.println("j -> "+j);
     }
     static{
        System.out.println("Second static Block");
     }
     static int j = 20;
 }
 ```
 Output :-
 ```output
0
First static Block
Second static Block
20
Main Block
 ```

#### Read Indirectly and Write Only (RIWO) state

- Inside a static block, if we try to read a variable directly, that operation is called **Direct Read**.
- If we call a method, and within that method we try to read a variable, that operation is called **Indirect Read**.

```java
class Test{
    static int i = 10;
    static{
        m1();
        System.out.println(i);// Direct Read
    }
    public static void m1(){
        System.out.println(i);// Indirect Read
    }
}
```
- If a variable is just identified by the JVM but its original value is not yet assigned, then the variable is said to be in Read Indirectly and Write Only (RIWO) state.
- If a variable is in Read Indirectly and Write Only (RIWO) state, then we cannot perform a direct read, but we can perform an indirect read.
- If we try to read it directly, we will get a ```compile-time error saying Illegal forward reference```.
Example 1 :-
```java
class Test{
    static int x = 10;
    static{
        System.out.println(x);
    }
}
```
Output:-
```output
10
Run-Time error : NoSuchMethodError: main
```
Example 2 :-
```java
class Test{
    static{
        System.out.println(x);
    }
    static int x = 10;
}
```
Output:-
```output
Compile-time Error: illegal Forward refrence
```
Example 3 :-
```java
class Test{
    static{
        m1();
    }
    public static void m1(){
        System.out.println(x);
    }
    static int x = 10;
}
```
Output:-
```output
0
Run-Time error : NoSuchMethodError: main
```

#### Static Block 

- A static block will be executed at the time of class loading. Hence, if we want to perform any activity at the time of class loading, we must define it inside the **Static Block**.

Example 1 :- 

At the time of Java class loading, the corresponding native library should be loaded; hence, we have to define this activity inside the static block.

```java
class Test{
    static{
        System.loadLibrary("native library path");
    }
}
```
Example 2 :-  

After loading every database driver class, we have to register the driver class with the DriverManager. However, inside the database driver class, there is a static block to perform this activity automatically, so we are not responsible for registering it explicitly.

```java
class DbDriver{
    static{
        Register this Driver with DriverManager;
    }
}
```
> **NOTE :-** Within a class, we can declare any number of static blocks, and all these static blocks will be executed from top to bottom.

<details>
<summary>
Without writing the main method, is it possible to print some statements to the console?
</summary>

Yes, by using a static block.

Example 1:- 
```java
class Tetst{
    static{
        System.out.println("Hello Ashutosh");
        System.exit(0);
    }
}
```
Output:-
```output
Hello Ashutosh
```
Example 2:- 
```java
class Tetst{
    static{
        System.out.println("Hello Ashutosh");
        // System.exit(0);
    }
}
```
Output:-
```output
Hello Ashutosh
Compile Time error main java.lang.NoSuchMethodError: main method
```
</details>

<details>
<summary>
Without writing the main method and static block, is it possible to print some statements to the console?
</summary>

Yes, of course. There are multiple ways. 
```java
class Test{
    static int x = m1();
    public static int m1(){
        System.out.println("Hello");
        System.exit(0);
        return 10;
    }
}
```
Output:-

```output
Hello
```
```java
class Test{
    static Test t = new Test();
    {
    System.out.println("Hello1");
    System.exit(0);
    }
}
```
Output:-

```output
Hello1
```
```java
class Test{
    static Test t = new Test();
    Test(){
        System.out.println("Hello2");
        System.exit(0);
    }
}
```
Output:-

```output
Hello2
```
</details>

> **NOTE:-** From Java 1.7 onwards, the main method is mandatory to start program execution. From Java 1.7 onwards, without writing the main method, it is impossible to print any statements to the console.

#### Static Control flow Parent to Child

Whenever we execute the child class, the following sequence of events will occur automatically as part of static control flow:
    - Identification of static members from parent to child.
    - Execution of static variable assignments and static blocks from parent to child.
    - Execution of only the child class main() method
[Image-1](https://tinyurl.com/2vj3u9vc) [Image-2](https://tinyurl.com/3js4kt93)
```java
class Base{
    static int i = 10;
    static{
        m1();
        System.out.println("Base static Block");
    }
    public static void main(String[]args){
        m1();
        System.out.println("Base main");
    }
    public static void m1(){
        System.out.println(j);
    }
    static int j = 20;
}
class Derived extends base{
    static int x = 100;
    static{
        m2();
        System.out.println("Derived First static Block");
    }
    public static void main(String[] args){
        m2();
        System.out.println("Derived main Block");
    }
    static{
        System.out.println("Derived Second static Block");
    }
    static int y = 200;
}
```
Output:- ```javac Base.java``` will make two class one Base.class and another one is Derived.class. but here we will run ```Java Derived```
```output
0
Base static Block
0
Derived First static Block
Derived Second static Block
200
Derived main
```
> **NOTE :-** Whenever a child class is loaded, its parent class is automatically loaded. However, when the parent class is loaded, the child class is not loaded.
(This is because parent class members are by default available to the child class, whereas child class members are not by default available to the parent class).

### Instance Control flow

- Whenever we execute a Java class, the [static control flow](#static-control-flow) is executed first.
- If, during static control flow, an object is created, then the following sequence of events will be executed as part of instance control flow:
    - Identification of instance members from top to bottom.
    - Execution of instance variable assignments and instance blocks from top to bottom.
    - Execution of the constructor.

[Image](https://tinyurl.com/4jckyxt2)
```java
class Test{
    int i = 10;
    {
        m1();
        System.out.println("First Instance Block");
    }
    Test(){
        System.out.println("Constructor");
    }
    public static void main(String []args){
        Test t = new Test();
        System.out.println("Main Block");
    }
    public void m1(){
        System.out.println("j -> "+j);
    }
    {
        System.out.println("Second Instance Block");
    }
    int j = 20;
}
```
Output:-
```output
0
First Instance Block
Second Instance Block
Constructor
Main Block
```
If we comment out the line ```Test t = new Test();```, then the output of the above code will be ```"Main Block"```.

> **NOTE :-** 
> - Static control flow is a one-time activity that is performed at the time of class loading, whereas instance control flow is not a one-time activity; it is performed for every object creation.
> - Object creation is one of the most costly operations. If there is no specific requirement, then it is not recommended to create an object.

#### Instance Control flow Parent to child relationship

- Whenever we create a child class object, the following sequence of events will be performed automatically as part of the instance control flow:
    - Identification of instance members from parent to child.
    - Execution of instance variable assignments and instance blocks in the parent class.
    - Execution of the parent constructor.
    - Execution of instance variable assignments and instance blocks in the child class.
    - Execution of the child constructor.

[Image-1](https://tinyurl.com/2s3dh7nb) [Image-2](https://tinyurl.com/33shv8mj)
```java
class Parent{
    int i = 10;
    {
        m1();
        System.out.println("Parent Instance Block");
    }
    Parent(){
        System.out.println(" Parent Constructor");
    }
    public static void main(String[]args){
        Parent p = new Parent();
        System.out.println("Parent main Block");
    }
    public void m1(){
        System.out.println(j);
    }
    int j = 10;
}
class Child extends Parent{
    int x = 100;
    {
        m2();
        System.out.println("Child first Instance Block");
    }
    Child(){
        System.out.println(" Child Constructor");
    }
    public static void main(String[]args){
        Child c = new Child();
        System.out.println("Child main Block");
    }
    public void m2(){
        System.out.println(y);
    }
    {
        System.out.println("Child second Instance Block");
    }
    int y = 200;
}
```
Output:-
```output
0
Parent Instance Block
Parent Constructor
0
Child first Instance Block
Child second Instance Block
Child Constructor
Child main Block
``` 
#### Instance and Static Control Flow Example
Example :-
```java
class Tets{
    {
        System.out.println("First Instance Block ");
    }
    static{
        System.out.println("First static Block ");
    }
    Test(){
        Sysem.out.println("Constructor Block");
    }
    public static void main(String[]args){
        Test t = new Test();
        System.out.println("Main Block ");
        Test t1 = new Test();
    }
    static {
        System.out.println("Second static Block ");
    }
    {
        System.out.println("Second Instance Block ");
    }
}
```
Output:-
```output
First static Block 
Second static Block 
First Instance Block 
Second Instance Block
Constructor Block
main
First Instance Block 
Second Instance Block
Constructor Block
```

Example :-
```java
public class Initialization{
    public static String m1(String value){
        System.out.println(value);
        return value;
    }
    public Initialization(){
        m = m1("1");
    }
    {
        m = m1("2");
    }
    String m = m1("3");
    public static void main(String []args){
        Object o = new Initialization() 
    }
}
```
Output :-
```output
2
3
1
```

Example :-
```java
public class Initialization2{
    private static String m1(String value){
        System.out.println(value);
        return value;
    }
    
    static String m = m1("1");
    {
        m = m1("2");
    }
    static{
     m = m1("3");
    }
    public static void main(String []args){
        Object o = new Initialization2() 
    }
}
```
Output :-
```output
1
3
2
```
Example :-
```java
class Test{
    int x = 10;
    public static void main(String []args){
        System.out.println(x);
    }
}
```
Output :-
```output
Complie error: non-static variable x cannot be reference from a static content
```
Example :-
```java
class Test{
    int x = 10;
    public static void main(String []args){
        Test t = new Test();
        System.out.println(t.x);
    }
}
```
Output :-
```output
10
```
> **NOTE :-** From a static area, we cannot access instance members directly because while executing the static area, the JVM may not have created the object yet, so instance members may not be available.

<details>
<summary>
In how many ways we can create an object in java or In how many ways we can get object in java?
</summary>

1. By using new operator  ```Test t = new Test();```
2. By using newInstance() method ```Test t = (Test)class.forName("Test").newInstance();```
3. By using factory method ```Runtime r = Runtime.getRuntime(); ```
4. By using clone() method
```
Test t1 = new Test();
Test t2 = (Test)t1 clone();
```
5. By using Deseralization 
```
FileInputStream fir = new FileInputStream();
ObjectInputStream oir = new ObjectInputStream();
Dog dg = (Dog)oir.readObject();
```
</details>

### Constructors

Once we create an object, we should perform initialization; only then is the object in a position to respond properly.

Whenever we create an object, some part of the code is executed automatically to perform initialization of the object. This part of the code is called a constructor. Hence, the main purpose of a constructor is to initialize an object.

Example :-
```java
class Student{
    String name;
    int rollNo;

    // Constructor
    Student(String name,introllNo){
        this.name = name;
        this.rollNo = rollNo;
    }
    public static  void main(String[]args){
        Student s1 = new Student("Raj",3090);
        Student s2 = new Student("Kumar",3779);
    }
}
```
> **NOTE :-** The main purpose of a constructor is to perform initialization of an object, not to create the object.

#### Constructor Vs Instance block

- The main purpose of a constructor is to perform the initialization of an object.
- Other than initialization, if we want to perform any activity for every object creation, then we should use an instance block (for example, updating an entry in the database for every object creation or incrementing a count value for every object creation, etc.)
- Both the constructor and the instance block have their own different purposes, and replacing one concept with the other may not always work.

- Both the constructor and the instance block are executed for every object creation, but the instance block executes first, followed by the constructor.

Example :-
```java
class Test{
    static int count = 0;
    // improve code  this part of code
    // Test(){
    //     count++;
    // }
    // Test(int i){
    //     count++;
    // }
    // Test(double d){
    //     count++;
    // }
    {
        count++;
    }
    Test(){}
    Test(int i){}
    Test(double d){}
    public static void main(String []args){
        Test t1 = new Test();
        Test t2 = new Test(10);
        Test t3 = new Test(10.5);
        System.out.println("The no. of object created "+count)
    }
}
```
A demo program to print the number of objects created for a class.

#### Rules of Writing constructor

Name of the class and name of the constructor much be matched.
<details>
<summary>
Rule 1
</summary>
Name of the class and name of the constructor much be matched.
</details>

<details>
<summary>
Rule 2
</summary>
Return type concept not applicable for constructor even void also.
</details>

<details>
<summary>
Rule 3
</summary>

By mistake, if we try to declare a return type for a constructor, we won’t get any compile-time error because the compiler treats it as a method.
```java
class Test{
    void Test(){
        System.out.println("Method not constructor");
    }
    public static void main(){
        Test t = new Test();
        t.Test();
    }
}
```
Output:-
```output
Method not constructor
```
Hence, it is legal (but stupid to have a method whose name is exactly the same as the class name).

</details>

<details>
<summary>
Rule 4
</summary>

The only applicable modifiers for constructors are ```public, private, protected, and default```. If we try to use any other modifier, we will get a compile-time error.
```java
class Test{
    static Test(){}
}
```
Output :-
```output
CompileTime Error: modifier static not allowed here
```
</details>

#### Default constructor

- The compiler is responsible for generating the default constructor (not the JVM).
- If we do not write any constructor, only then will the compiler generate a default constructor. That is, if we write at least one constructor, the compiler will not generate the default constructor. Hence, every class in Java contains a constructor—either a default constructor generated by the compiler or a customized constructor explicitly provided by the programmer—but not both simultaneously.

##### Prototype of Default Constructor

- It is always a no-argument constructor.
- The access modifier of the default constructor is exactly the same as the access modifier of the class (this rule is applicable only for public and default access).
- It contains only one line: super(); — which is a no-argument call to the superclass constructor.

|Programmers Code|Compiler Code|
| --------------- | --------------|
| <pre><code> class Test{}</code></pre>|<pre><code> class Test{***Test(){super();}***}</code></pre> |
| <pre><code> public class Test{}</code></pre>|<pre><code> public class Test{***public Test(){super();}***}</code></pre> |
| <pre><code> public class Test{void Test(){}}</code></pre>|<pre><code> public class Test{***public Test(){super();}*** void Test(){}}</code></pre> |
| <pre><code> class Test{Test(){}}</code></pre>|<pre><code> class Test{Test(){***super();***}}</code></pre> |
| <pre><code> class Test{Test(int i){super();}}</code></pre>|<pre><code> class Test{ Test(int i){super();}}</code></pre> |
| <pre><code> class Test{ Test(){this(10)} Test(int i){}}</code></pre>|<pre><code> class Test{ Test(){this(10);} Test(int i){***super();***}}</code></pre> |

- The first line inside every constructor should be either ```super()``` or ```this()```. If we do not write anything, the compiler will automatically insert ```super();```.

<details>
<summary>
Case 1
</summary>

We can use ```super()``` or ```this()``` only as the first line of a constructor. If we try to use them anywhere else, we will get a compile-time error.

Example :-
```java
class Test{
    Test(){
        System.out.println("Constructor");
        super();
    }
}
```
Output :-
```output
Compile-Time Error : call to super must be first satement in constructor
```
</details>

<details>
<summary>
Case 2
</summary>

Within a constructor, we can use either ```super()``` or ```this()```, but not simultaneously.

Example :-
```java
class Test{
    Test(){
        super();
        this();
    }
}
```
Output :-
```output
Compile-Time Error : call to this must be first satement in constructor
```
</details>

<details>
<summary>
Case 3
</summary>

We can use ```super()``` or ```this()``` only inside a constructor. If we try to use them outside a constructor, we will get a compile-time error. That is, a constructor can be called directly only from another constructor.

Example :-
```java
class Test{
    public void m1(){
        super();
        System.out.println("Hello");
    }
}
```
Output :-
```output
Compile-Time Error : call to super must be first satement in constructor
```
</details>

[Summary of Case](https://tinyurl.com/3w2tsvek) 

##### super(), this() Vs super, this

| `super()`, `this()` | `super`,`this` |
| --------------------| -------------|
| These are **constructor calls** used to invoke superclass or current-class constructors. | These are **keywords** used to refer to superclass and current-class instance members. |
| They can be used **only in constructors** and **only as the first line**.                | They can be used **anywhere**, except in a static context.                             |
| They can be used **only once** in a constructor.                                         | They can be used **any number of times**.                                              |

Example :- 
```java
class Tets{
    public static void main(String []args){
        System.out.println(super.hashCode());
    }
}
```
Output:-
```output
Compile -time Error non-static variable super cannot be referenced from a static content
```

#### Overloaded Constructor

With in a class we can declare mutipule constructor all these constructor having same name but different type of arguments hence all these constructor are consider as overloaded constructors.hence overloading constructor concept applicable for constructors. [Image](https://tinyurl.com/2twte86h)

```java
class Test{
    Test(){
        this(10);
        System.out.println("No-args");
    }
    Test(int i){
        this(10.5);
        System.out.println("Int-args");
    }
    Test(double d){
        System.out.println("Double-args");
    }
    public static void main(String[]args){
        Test t1 = new Test();
        Test t2 = new Test(10);
        Test t3 = new Test(10.5);
        Test t4 = new Test(10l);
    }
}
```
Output :-
```output
Double-args
Int-args
No-args
Double-args
Int-args
Double-args
Double-args
```

- For constructors, inheritance and overriding concepts are not applicable, but the overloading concept is applicable.
- Every class in Java, including abstract classes, can contain constructors, but **interfaces** cannot contain constructors.

Example :- ✅
```java
class Test{
    Test(){}
}
```
Example :- ✅
```java
abstract class Test{
    Test(){}
}
```
Example :- ❎
```java
interface Test{
    Test(){}
}
```

#### Case

<details>
<summary>
Case 1
</summary>

- A recursive method call can cause a runtime exception called StackOverflowError.
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
       System.out.println("Hello");
    }

}
```
Output :-
```output
Run-time error: StackOverflow source
```
- However, if there is a chance of recursive constructor invocation in a program, the code will not compile, and we will get a compile-time error.
```java
class Test{
    Test(){
        this(10);
    }
    Test(int i){
        this();
    }
    public static void main(String[]args){
       System.out.println("Hello");
    }

}
```
Output :-
```output
Compile Error: Recursive constructor invocation
```
</details>

<details>
<summary>
Case 2
</summary>

 Example :- [Image](https://tinyurl.com/bdehawxm)

 > **NOTE :-**
 > - If the parent class contains any argument constructor, then while writing the child class we must take special care with respect to constructors.
> - Whenever we write an argument constructor, it is highly recommended to also write a no-argument constructor also.

</details>

<details>
<summary>
Case 3
</summary>

[Image](https://tinyurl.com/4uynknvt)

Example :- ❎
```java
class P{
    p() throws IOException{

    }
}
class C extends P{
    c(){
        super();
    }
}
```
Output :-
```output
compiler error: unreputted exception java.io.IoException in default Constructor.
```
Example :- ✅
```java
class P{
    p() throws IOException{

    }
}
class C extends P{
    c() throws IOException{
        super();
    }
}
```
If a parent class constructor throws any checked exception, the child class constructor must compulsorily throw the same checked exception or its parent; otherwise, the code will not compile.

</details>

#### Which of the following is valid

| Statement | Status |
|----------|--------|
| The main purpose of a constructor is to create an object | ❌ |
| The main purpose of a constructor is to perform initialize of an object | ✅ |
| The name of the constructor need not be same as class name | ❌ |
| Return type concept applicable for constructor but only void | ❌ |
| we can apply any modifiers for constructor | ❌ |
| Default constructor genrated by JVM | ❌ |
| Compiler is responsible for generating the default constructor| ✅ |
| Compiler will always generates a default constructor | ❌ |
| If we do not write a no-argument constructor, the compiler will generate a default constructor | ❌ |
| Every no argument constructor is default constructor| ❌ |
| Default constructor is always no argument constructor | ✅ |
| The first line inside every constructor should be either super() or this() if we are not writing anything then compiler will gentrates super() | ✅ |
| For constructors both overlading and overriding concepts are applicable | ❌ |
| For constructors inheritance concept applicable but not overriding | ❌ |
| Only concrete classes can contain constructor but abstract class can't | ❌ |
| Interface can contain constructors  | ❌ |
| Recursive constructor invocation is a runtime exception | ❌ |
| if parent class constructor throws some checked exception then compulsory child class constructor should throw the same checked exception or it's child | ❌ |

#### Singleton class

For any Java class, if we are allowed to create only one object, such a class is called a singleton class.

Example :- Runtime, BusinessDelegate, ServiceLocator

#### Advantage of Singleton class

- If several people have the same requirement, it is not recommended to create a separate object for every requirement.
- We should create only one object and reuse the same object for every similar requirement so that performance and memory utilization are improved.
- This is the central idea of singleton classes.

Example :- [Image](https://tinyurl.com/4b6dvcny)

#### How to create Our own singletone class

We can create our own singleton classes by using a private constructor, a private static variable, and a public factory method.

- Approach - 1 :- [Image](https://tinyurl.com/mw7tddcr)
```java
class Test{
    private static Test test = new Test();
    
    private Test(){}

    public static Test getTest(){
        return test;
    }
}
class Main{
    public static void main(String[] args){
        Test t1 = Test.getTest();
        Test t2 = Test.getTest();
        Test t3 = Test.getTest();
    }
}
```
> **NOTE :-** The Runtime class is internally implemented using this approach.

- Approach - 2 :- [Image](https://tinyurl.com/4arkse2a)
```java
class Test{
    private static Test test = null;
    
    private Test(){}

    public static Test getTest(){
        if(test==null){
            test = new Test();
        }
        return test;
    }
}
class Main{
    public static void main(String[] args){
        Test t1 = Test.getTest();
        Test t2 = Test.getTest();
        Test t3 = Test.getTest();
    }
}
```
At any point in time, for the ```Test``` class we can create only one object; hence, the ```Test``` class is a singleton class.

#### Class is not finall but we are not allowed to create child classes

By declaring every constructor as private, we can restrict child class creation.

Example :-
```java
class P{
    private P(){}
}
```
For the above class, it is impossible to create a child class.

<hr/>

