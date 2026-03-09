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
# Collection

If we want to represent a group of individual objects as a single entity, then we should go for a Collection.

## Collection Framework

The Collection Framework contains several classes and interfaces that can be used to represent a group of individual objects as a single entity.

| **Java**             | **C++**                         |
| -------------------- | ------------------------------- |
| Collection           | Container                       |
| Collection Framework | STL (Standard Template Library) |

## 9 key interface of collection framework

1. [Collection](#collection-i)
1. [List](#list-i) 
1. [Set](#set-i)
1. [SortedSet](#sortedset-i)
1. [NavigableSet](#navigableset-i)
1. [Queue](#queue-i)
1. Map
1. SortedMap
1. NavigableMap

### Collection (I)

- If we want to represent a group of individual objects as a single entity, then we should go for a Collection.

- The Collection interface defines the most common methods that are applicable to any collection object.

- In general, the Collection interface is considered the root interface of the Collection Framework.

However, there is no concrete class that implements the Collection interface directly. Instead, other interfaces such as List, Set, and Queue extend the Collection interface, and their classes provide implementations.

```diagram
Collection (Interface)    [1.2 version]
   |
   |-- List               [1.2 version]
   |     |-- ArrayList    [1.2 version]
   |     |-- LinkedList   [1.2 version]
   |     |-- Vector       [1.0 version]
   |            |-- Stack [1.0 version]
   |
   |-- Set                [1.2 version]
   |     |-- HashSet      [1.2 version]
   |     |      |-- LinkedHashSet   [1.4 version]
   |     |
   |     |-- SortedSet    [1.2 version]
   |            |-- NavigableSet   [1.6 version]
   |                    |-- TreeSet [1.2 version]
   |
   |-- Queue             [1.5 version]
         |-- PriorityQueue
         |-- BlockingQueue
```
> **NOTE:** The Map interface is part of the Collection Framework but does NOT extend the Collection interface because it stores key-value pairs, not just objects.


## Difference Between Collection and Collections


| **Collection**                                                                                                                                        | **Collections**                                                                                                                                                                               |
| ----------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Collection** is an **interface**. If we want to represent a **group of individual objects as a single entity**, then we should go for a Collection. | **Collections** is a **utility class** present in the `java.util` package that provides several **utility methods** for collection objects (such as **sorting, searching, reversing, etc.**). |

### List (I)

- List is a child interface of the Collection interface.
- If we want to represent a group of individual objects as a single entity where duplicates are allowed and insertion order is preserved, then we should go for a List.

```diagram
List                  [1.2 version]
  |-- ArrayList       [1.2 version]
  |-- LinkedList      [1.2 version]
  |-- Vector          [1.0 version]
         |-- Stack    [1.0 version]
```

>**NOTE:** In Java 1.2, the Vector and Stack classes were re-engineered to implement the List interface.

### Set (I)

- Set is a child interface of the Collection interface.

- If we want to represent a group of individual objects as a single entity where duplicates are not allowed and insertion order is not required, then we should go for the Set interface.

```diagram
Set                  [1.2 version]
  |
  |-- HashSet        [1.2 version]
  |      |
  |      |-- LinkedHashSet   [1.4 version]
  |
  |-- SortedSet      [1.2 version]
         |
         |-- NavigableSet   [1.6 version]
                |
                |-- TreeSet [1.2 version]
```

#### SortedSet (I)

- SortedSet is a child interface of the Set interface.

- If we want to represent a group of individual objects as a single entity where duplicates are not allowed and all objects are stored according to some sorting order, then we should go for a SortedSet.

- The elements in a SortedSet are stored in ascending sorted order by default.

##### NavigableSet (I)

- NavigableSet is a child interface of the SortedSet interface.

- It contains several methods for navigation purposes, such as finding elements closest to a given element.

## Difference Between List and Set

| **List**                          | **Set**                               |
| --------------------------------- | ------------------------------------- |
| **Duplicates are allowed.**       | **Duplicates are not allowed.**       |
| **Insertion order is preserved.** | **Insertion order is not preserved.** |


## Queue (I)

- Queue is a child interface of the Collection interface

- If we want to represent a group of individual objects prior to processing, then we should go for a Queue.

- Usually, a Queue follows the First-In-First-Out (FIFO) order. However, based on our requirements, we can also implement our own priority order

Example : Before sending emails, all email IDs must be stored in some data structure.  
The emails should be delivered in the same order in which they were added. For this requirement, a Queue is the best choice.

```diagram
Queue [1.5 version]
   |
   |-- PriorityQueue
   |
   |-- BlockingQueue
         |
         |-- PriorityBlockingQueue
         |-- LinkedBlockingQueue
```

> **NOTE:** 
> - All the above interfaces (Collection, List, Set, SortedSet, NavigableSet, Queue) are mainly used for representing a group of individual objects.
> If we want to represent a group of objects as key–value pairs, then we should go for the Map interface.

## Map (I)

- Map is not a child interface of the Collection interface.

- If we want to represent a group of objects as key–value pairs, then we should go for a Map.

- Both keys and values are objects.

- Duplicate keys are not allowed, but values can be duplicated.

```diagram
Map (Interface)        [1.2 version]
   |
   |-- HashMap         [1.2 version]
   |      |-- LinkedHashMap   [1.4 version]
   |
   |-- WeakHashMap     [1.2 version]
   |
   |-- IdentityHashMap [1.4 version]
   |
   |-- Dictionary (Abstract Class)  [1.0 version]
            |-- Hashtable       [1.0 version]
                   |-- Properties      [1.0 version]
```

###  Sortedmap (I)

- SortedMap is a child interface of the Map interface.

- If we want to represent a group of key–value pairs according to some sorting order of keys, then we should go for a SortedMap.

- In SortedMap, the sorting is based on keys only, not on values.

#### NavigableMap (I)