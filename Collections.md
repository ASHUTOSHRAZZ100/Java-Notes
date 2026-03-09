# Array

- An array is an indexed collection of a fixed number of homogeneous data elements.

- The main advantage of arrays is that we can represent multiple variables using a single variable, which improves the readability of the code.

## limitations of Arrays

- Arrays are fixed in size. Once an array is created, we cannot increase or decrease its size based on our requirement.  
Because of this, we must know the array size in advance, which is not always possible.

- Arrays can hold only homogeneous data types (elements of the same type).

Example
```java
Student[] s = new Student[10000];

s[0] = new Student();   // Valid
s[1] = new Customer();  // Compile-time error
```
Output
```output
Compile-time Error: incompatible types
found: Customer
required: Student
```

We can solve this problem by using object type arrays.

```java
Object[] a = new Object[10000];

a[0] = new Student();   // Valid
a[1] = new Customer();  // Valid
```
Because Object is the parent class of all classes in Java, it can store any type of object.

- The array concept is not implemented based on any standard data structure, and hence ready-made method support is not available.  
  
For every requirement, we must write the logic explicitly, which increases the complexity of programming.

- To overcome the above problems of arrays, we should use the Collections Framework.

    - Collections are growable in nature, meaning we can increase or decrease the size dynamically based on our requirement.
    - Collections can hold both homogeneous and heterogeneous objects.
    - Every collection class is implemented based on a specific data structure, so ready-made method support is available for many operations.

As programmers, we are responsible for using the provided methods, but we are not responsible for implementing those methods ourselves.

## Diffrences between Array and collection

| **Arrays**                                                                                                                                                                                                                   | **Collections**                                                                                                                                                                                                                          |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Arrays are **fixed in size**. Once we create an array, we cannot increase or decrease its size based on our requirement.                                                                                                     | Collections are **growable in nature**. Based on our requirement, we can increase or decrease the size dynamically.                                                                                                                      |
| With respect to **memory**, arrays are **not recommended** because the size must be defined in advance.                                                                                                                      | With respect to **memory**, collections are **recommended** because they can grow or shrink dynamically.                                                                                                                                 |
| With respect to **performance**, arrays are **recommended** because they have less overhead.                                                                                                                                 | With respect to **performance**, collections are **not always recommended** because they have additional overhead.                                                                                                                       |
| Arrays can hold **only homogeneous data type elements** (same type).                                                                                                                                                         | Collections can hold **both homogeneous and heterogeneous elements**.                                                                                                                                                                    |
| There is **no underlying data structure for arrays**, and hence **ready-made method support is not available**. For every requirement, we must write the code explicitly, which **increases the complexity of programming**. | Every collection class is implemented based on **a specific data structure**, and hence **ready-made method support is available**. As programmers, we can directly use these methods and are **not responsible for implementing them**. |
| Arrays can hold **both primitive types and objects**.                                                                                                                                                                        | Collections can hold **only objects**, not primitive data types (they use wrapper classes instead).                                                                                                                                      |
