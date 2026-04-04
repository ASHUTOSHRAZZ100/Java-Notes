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
1. [Map](#map-i)
1. [SortedMap](#sortedmap-i)
1. [NavigableMap](#navigablemap-i)

### Collection (I)

- If we want to represent a group of individual objects as a single entity, then we should go for a Collection.

- The Collection interface defines the most common methods that are applicable to any collection object.

- In general, the Collection interface is considered the root interface of the Collection Framework.

However, there is no concrete class that implements the Collection interface directly. Instead, other interfaces such as List, Set, and Queue extend the Collection interface, and their classes provide implementations.

```diagram
Collection (Interface)                  [1.2 version]
   |
   |-- List                             [1.2 version]
   |     |-- ArrayList                  [1.2 version]
   |     |-- LinkedList                 [1.2 version]
   |     |-- Vector                     [1.0 version]
   |            |-- Stack               [1.0 version]
   |
   |-- Set                              [1.2 version]
   |     |-- HashSet                    [1.2 version]
   |     |      |-- LinkedHashSet       [1.4 version]
   |     |
   |     |-- SortedSet                  [1.2 version]
   |            |-- NavigableSet        [1.6 version]
   |                    |-- TreeSet     [1.2 version]
   |
   |-- Queue                            [1.5 version]
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
Map (Interface)                         [1.2 version]
   |
   |-- HashMap (Interface)              [1.2 version]
   |      |-- LinkedHashMap             [1.4 version]
   |
   |-- WeakHashMap (Interface)          [1.2 version]
   |
   |-- IdentityHashMap (Interface)      [1.4 version]
   |
   |-- SortedMap (Interface)            [1.2 version]
   |      |-- NavigableMap (Interface)  [1.6 version]
   |             |-- TreeMap            [1.2 version]
   |
   |-- Dictionary (Abstract Class)      [1.0 version]
          |
          |-- Hashtable                 [1.0 version]
                 |-- Properties         [1.0 version]
```

###  SortedMap (I)

- SortedMap is a child interface of the Map interface.

- If we want to represent a group of key–value pairs according to some sorting order of keys, then we should go for a SortedMap.

- In SortedMap, the sorting is based on keys only, not on values.

#### NavigableMap (I)

- NavigableMap is a child interface of the SortedMap interface.

- It defines several methods for navigation purposes.


> **Note:** The following are legacy components present in the Java Collection Framework:
> - Enumeration (Interface)
> - Dictionary (Abstract Class)
> - Vector (Class)
> - Stack (Class)
> - Hashtable (Class)
> - Properties (Class)

[Image](https://tinyurl.com/wsyrn43x)

# Collection (I)

- If we want to represent a group of individual objects as a single entity, then we should go for a Collection.

- The Collection interface defines the most common methods that are applicable to any collection object.

| **Method**                          | **Definition**                                                                               |
| ----------------------------------- | -------------------------------------------------------------------------------------------- |
| `boolean add(Object o)`             | Adds the specified element to the collection.                                                |
| `boolean addAll(Collection c)`      | Adds all elements of the specified collection to this collection.                            |
| `boolean remove(Object o)`          | Removes the specified element from the collection.                                           |
| `boolean removeAll(Collection c)`   | Removes all elements from this collection that are also present in the specified collection. |
| `boolean retainAll(Collection c)`   | Retains only the elements that are also present in the specified collection.                 |
| `void clear()`                      | Removes all elements from the collection.                                                    |
| `boolean contains(Object o)`        | Returns `true` if the collection contains the specified element.                             |
| `boolean containsAll(Collection c)` | Returns `true` if this collection contains all elements of the specified collection.         |
| `boolean isEmpty()`                 | Returns `true` if the collection contains no elements.                                       |
| `int size()`                        | Returns the number of elements present in the collection.                                    |
| `Object[] toArray()`                | Converts the collection into an array.                                                       |
| `Iterator iterator()`               | Returns an **Iterator object** to traverse the elements of the collection.                   |


> **NOTE:** There is no concrete class that implements the Collection interface directly.

# List (I)

- List is a child interface of the Collection interface.
- If we want to represent a group of individual objects as a single entity where duplicates are allowed and insertion order must be preserved, then we should go for a List.
- In a List, insertion order is preserved using an index, and we can differentiate duplicate objects using the index. Hence, the index plays a very important role in List.
-  The List interface defines the following specific methods.

| **Method**                                 | **Definition**                                                                       |
| ------------------------------------------ | ------------------------------------------------------------------------------------ |
| `void add(int index, Object o)`            | Inserts the specified element at the specified position in the list.                 |
| `boolean addAll(int index, Collection c)`  | Inserts all elements of the specified collection starting at the specified position. |
| `Object get(int index)`                    | Returns the element present at the specified index.                                  |
| `Object remove(int index)`                 | Removes and returns the element at the specified index.                              |
| `Object set(int index, Object newElement)` | Replaces the element at the specified index with the new element.                    |
| `int indexOf(Object o)`                    | Returns the index of the first occurrence of the specified element.                  |
| `int lastIndexOf(Object o)`                | Returns the index of the last occurrence of the specified element.                   |
| `ListIterator listIterator()`              | Returns a **ListIterator** to traverse the list elements.                            |

# ArrayList

- The underlying data structure of an ArrayList is a resizable (or growable) array.
- Duplicate objects are allowed.
- Insertion order is preserved.
- Heterogeneous objects are allowed (except in TreeSet and TreeMap, where heterogeneous objects are not allowed because sorting is required)
- Null insertion is possible (multiple null values can be stored).

## Constructors

1. `ArrayList l = new ArrayList();`

Creates an empty ArrayList object with the default initial capacity of 10.

Once the ArrayList reaches its maximum capacity, a new ArrayList object will be created with increased capacity.  
 `newCapacity = (currentCapacity * 3 / 2) + 1 `

2. `ArrayList l = new ArrayList(int initialCapacity);`  

Creates an empty ArrayList object with the specified initial capacity.

3. `ArrayList l = new ArrayList(Collection c);`  

Creates an equivalent ArrayList object for the given Collection.

Example :
```java
import java.util.*;

class ArrayListDemo {
    public static void main(String[] args) {

        ArrayList l = new ArrayList();

        l.add("A");
        l.add(10);
        l.add("A");
        l.add(null);

        System.out.println(l);

        l.remove(2);
        System.out.println(l);

        l.add(2, "M");
        l.add("N");

        System.out.println(l);
    }
}
```
Output
```output
[A, 10, A, null]
[A, 10, null]
[A, 10, M, null, N]
```

- Usually, we use collections to hold and transfer objects from one location to another location (like a container).
- To support this requirement, every collection class by default implements the `Serializable` and `Cloneable` interfaces.
- ArrayList and Vector classes implement the RandomAccess interface, so that any random element can be accessed with the same speed.

## RandomAccess

- RandomAccess is an interface present in the java.util package.
- It does not contain any methods.
- It is a marker interface, where the required ability is provided automatically by the JVM.

Example:

```java
import java.util.*;

class Test {
    public static void main(String[] args) {

        ArrayList l1 = new ArrayList();
        LinkedList l2 = new LinkedList();

        System.out.println(l1 instanceof Serializable);
        System.out.println(l2 instanceof Cloneable);
        System.out.println(l1 instanceof RandomAccess);
        System.out.println(l2 instanceof RandomAccess);
    }
}
```
Output
```output
true
true
true
false
```

- ArrayList is the best choice if our frequent operation is retrieval, because ArrayList implements the `RandomAccess` interface, which allows fast index-based access.
- ArrayList is the worst choice if our frequent operation is insertion or deletion in the middle, because in such cases elements must be shifted, which reduces performance.

## Difference Between ArrayList and Vector

| ArrayList                                                                                                           | Vector                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| Every method present in **ArrayList** is **non-synchronized**.                                                      | Every method present in **Vector** is **synchronized**.                                                   |
| At a time, **multiple threads are allowed** to operate on an ArrayList object, and hence it is **not thread-safe**. | At a time, **only one thread is allowed** to operate on a Vector object, and hence it is **thread-safe**. |
| **Performance is relatively high** because threads are **not required to wait** to operate on an ArrayList object.  | **Performance is relatively low** because threads are **required to wait** to operate on a Vector object. |
| Introduced in **Java 1.2** and it is **not a legacy class**.                                                        | Introduced in **Java 1.0** and it is a **legacy class**.                                                  |

## How to Get a Synchronized Version of an ArrayList Object

- By default, ArrayList is non-synchronized.
- But we can get a synchronized version of an ArrayList object by using the synchronizedList() method of the Collections class.

`public static List synchronizedList(List l)`

Example :
```java
import java.util.*;

class Test {
    public static void main(String[] args) {

        ArrayList l = new ArrayList();
        List l1 = Collections.synchronizedList(l);

    }
}
```
Similarly, we can get synchronized versions of `Set` and `Map` objects by using the following methods of the `Collections` class.

```java
public static Set synchronizedSet(Set s)
public static Map synchronizedMap(Map m)
```

# LinkedList

- The underlying data structure is a doubly linked list.
- Insertion order is preserved.
- Duplicate objects are allowed.
- Heterogeneous objects are allowed.
- Null insertion is possible.
- LinkedList implements the Serializable and Cloneable interfaces, but not the RandomAccess interface.
- LinkedList is the best choice if our frequent operation is insertion or deletion in the middle.
- LinkedList is the worst choice if our frequent operation is retrieval.

## Constructors

1. `LinkedList l = new LinkedList();`  
Creates an empty LinkedList object.
1. `LinkedList l = new LinkedList(Collection c);`  
Creates an equivalent LinkedList object for the given collection.

## LinkedList Class Specific Methods

Usually, we can use LinkedList to develop Stacks and Queues.  
To support this requirement, the LinkedList class defines the following specific methods.

| Method                    | Description                                                     |
| ------------------------- | --------------------------------------------------------------- |
| `void addFirst(Object o)` | Inserts the specified element at the **beginning** of the list. |
| `void addLast(Object o)`  | Inserts the specified element at the **end** of the list.       |
| `Object getFirst()`       | Returns the **first element** of the list.                      |
| `Object getLast()`        | Returns the **last element** of the list.                       |
| `Object removeFirst()`    | Removes and returns the **first element** of the list.          |
| `Object removeLast()`     | Removes and returns the **last element** of the list.           |

Example :
```java
import java.util.*;

class LinkedListDemo {
    public static void main(String[] args) {

        LinkedList l = new LinkedList();

        l.add("durga");
        l.add(30);
        l.add(null);
        l.add("durga");

        l.set(0, "Software");
        l.add(0, "venky");
        l.removeLast();
        l.addFirst("CCC");

        System.out.println(l);
    }
}
```
```output
[CCC, venky, Software, 30, null]
```

## Difference Between ArrayList and LinkedList


| **ArrayList**                                                                                                                                     | **LinkedList**                                                                                                                                     |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| **ArrayList is the best choice if our frequent operation is retrieval**, because it provides **fast index-based access**.                         | **LinkedList is the best choice if our frequent operation is insertion or deletion in the middle**.                                                |
| **ArrayList is the worst choice for frequent insertion or deletion in the middle**, because internally **several shift operations are required**. | **LinkedList is the worst choice if our frequent operation is retrieval**, because elements must be accessed by **traversing nodes**.              |
| In **ArrayList**, elements are stored in **consecutive memory locations**, and hence **retrieval operations become easy and fast**.               | In **LinkedList**, elements are **not stored in consecutive memory locations**, and hence **retrieval operations become slower and more complex**. |


# Vector

- the underline datastructure is resizable array or Grovable array
- Insertion order is preserved
- duplicates are allowed
- hetrogeneous object are allowed
- null inseration is possible
- it implements serilizable , clonable, and  random access interafaces
- every method present in the vector is thread syncorinized and hence vector object is thread safe.

## Constructors

1. `Vector v = new Vector();`  
Creates an empty Vector object with the default initial capacity of 10.  
Once the Vector reaches its maximum capacity, a new Vector object will be created with: `new capacity = current capacity * 2`

1. `Vector v = new Vector(int initialCapacity);`  
Creates an empty Vector object with the specified initial capacity.

1. `Vector v = new Vector(int initialCapacity, int capacityIncrement);`  
Creates an empty Vector object with the specified initial capacity, and the capacity will increase by the specified increment value whenever the Vector reaches its maximum capacity 

1. `Vector v = new Vector(Collection c);`  
Creates an equivalent Vector object for the given Collection.
This constructor is mainly used for interconversion between Collection objects.

## Vector Specific Methods

| **Method**                    | **Defined In / Description**                                          |
| ----------------------------- | --------------------------------------------------------------------- |
| `add(Object o)`               | Defined in **Collection** – Adds an element to the collection.        |
| `add(int index, Object o)`    | Defined in **List** – Inserts an element at the specified index.      |
| `addElement(Object o)`        | **Vector specific** – Adds an element to the end of the Vector.       |
| `remove(Object o)`            | Defined in **Collection** – Removes the specified element.            |
| `removeElement(Object o)`     | **Vector specific** – Removes the specified element from the Vector.  |
| `remove(int index)`           | Defined in **List** – Removes the element at the specified index.     |
| `removeAllElements()`         | **Vector specific** – Removes all elements from the Vector.           |
| `removeElementAt(int index)`  | **Vector specific** – Removes the element at the specified index.     |
| `clear()`                     | Defined in **Collection** – Removes all elements from the collection. |
| `Object get(int index)`       | Defined in **List** – Returns the element at the specified index.     |
| `Object elementAt(int index)` | **Vector specific** – Returns the element at the specified index.     |
| `Object firstElement()`       | **Vector specific** – Returns the first element of the Vector.        |
| `Object lastElement()`        | **Vector specific** – Returns the last element of the Vector.         |
| `int size()`                  | Returns the **number of elements present** in the Vector.             |
| `int capacity()`              | Returns the **current capacity** of the Vector.                       |
| `Enumeration elements()`      | Returns an **Enumeration object to iterate through Vector elements**. |

- Vector contains two types of methods:

   - Collection/List methods → `add()`, `remove()`, `clear()`, `get()`
   - Vector specific methods → `addElement()`, `removeElement()`, `elementAt()`, `capacity()`, `elements()`

```java
import java.util.*;

class VectorDemo1{
    public static void main(String[] args){
        Vector v = new Vector(10);
        System.out.println(v.capacity());
        for(int i=1;i<=10;i++){
            v.addElement(i);
                  }
                  System.out.println(v.capacity());
                  v.addElement("A");
                  System.out.println(v.capacity());
                  System.out.println(v);
    }
}
```

# Stack

- Stack is a child class of Vector.
- It is a specially designed class for Last-In-First-Out (LIFO) order.  
LIFO means the last element inserted will be the first element removed.

## Constructor

`Stack s = new Stack();`

## Methods

| Method                  | Description                                                        |
| ----------------------- | ------------------------------------------------------------------ |
| `Object push(Object o)` | Inserts an element onto the stack.                                 |
| `Object pop()`          | Removes and returns the **top element** of the stack.              |
| `Object peek()`         | Returns the **top element without removing it**.                   |
| `boolean empty()`       | Checks whether the stack is **empty or not**.                      |
| `int search(Object o)`  | Returns the **position of the element from the top of the stack**. |

Example :

```java
import java.util.*;

class StackDemo {
    public static void main(String[] args) {

        Stack s = new Stack();

        s.push("A");
        s.push("B");
        s.push("C");

        System.out.println(s);
        System.out.println(s.search("A"));
        System.out.println(s.search("Z"));
    }
}
```
Output
```output
[A, B, C]
3
-1
```

# The 3 Cursors of Java

If we want to retrieve objects one by one from a collection, then we should go for a cursor.  

A cursor is used to iterate or traverse through the elements of a collection object.

There are three types of cursors available in Java:

1. [Enumeration](#enumeration)
2. [Iterator](#iterator)
3. ListIterator

# Enumeration

- We can use Enumeration to get objects one by one from legacy collection objects such as Vector and Hashtable.

- We can create an Enumeration object by using the elements() method of the Vector class. `public Enumeration elements();`

Example :  
`Enumeration e = v.elements();`

## Methods

| Method                             | Description                                    |
| ---------------------------------- | ---------------------------------------------- |
| `public boolean hasMoreElements()` | Returns `true` if more elements are available. |
| `public Object nextElement()`      | Returns the next element in the collection.    |


Example :
```java
import java.util.*;

class EnumerationDemo {
    public static void main(String[] args) {

        Vector v = new Vector();

        for(int i = 0; i <= 10; i++) {
            v.addElement(i);
        }

        System.out.println(v);

        Enumeration e = v.elements();

        while(e.hasMoreElements()) {
            Integer I = (Integer) e.nextElement();

            if(I % 2 == 0) {
                System.out.println(I);
            }
        }
    }
}
```
Output :
```output
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
0
2
4
6
8
10
```

## Limitations of Enumeration

- We can apply Enumeration only for legacy classes (like Vector and Hashtable), so it is not a universal cursor.
- By using Enumeration, we get only read access to the elements; we cannot perform the remove operation.
- To overcome these limitations, we should go for the **Iterator cursor**.

# Iterator

- We can apply the Iterator concept to any Collection object, and hence it is a universal cursor.
- By using Iterator, we can perform both read and remove operations
- We can create an Iterator object by using the iterator() method of the Collection interface.  
  `public Iterator iterator();`

Example:
```java
// c is any Collection object
Iterator itr = c.iterator();
```
## Methods

| Method                     | Description                                      |
| -------------------------- | ------------------------------------------------ |
| `public boolean hasNext()` | Returns `true` if the next element is available. |
| `public Object next()`     | Returns the next element in the collection.      |
| `public void remove()`     | Removes the current element from the collection. |



Example :

```java
import java.util.*;

class IteratorDemo {
    public static void main(String[] args) {

        ArrayList l = new ArrayList();

        for(int i = 0; i <= 10; i++){
            l.add(i);
        }

        System.out.println(l);

        Iterator itr = l.iterator();

        while(itr.hasNext()){
            Integer I = (Integer) itr.next();

            if(I % 2 == 0){
                System.out.println(I);
            }
            else{
                itr.remove();
            }
        }

        System.out.println(l);
    }
}
```
Output :
```output
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
0
2
4
6
8
10
[0, 2, 4, 6, 8, 10]
```

## Limitations of Iterator

- By using Enumeration and Iterator, we can move only in the forward direction, and we cannot move in the backward direction.  
Hence, they are single-direction cursors, not bi-directional cursors.
- By using Iterator, we can perform only read and remove operations.  
We cannot perform replacement or addition of new objects.
- To overcome the above limitations, we should go for ListIterator.



