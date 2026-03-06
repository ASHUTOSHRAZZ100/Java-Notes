## Language Fundamentals
1. [Identifiers](#identifiers) 
1. [Reserved words](#reserved-words) 
1. [Data type](#data-type) 
1. [Literals](#literals) 
1. [Arrays](#arrays) 
1. [Types of variable](#types-of-variable) 
1. [Var-arg method](#var-arg-method-variable-argument-methods) 
1. [Main method](#main-method) 
1. [Command line arguments](#command-line-arguments)
1. [Java coding standards](#java-coding-standards)

### Identifiers

Example :- [Image](https://tinyurl.com/yjdwuj43)
```java
class Test{
    public static void main(String[]args){
        int x = 10;
    }
}
```
#### Rules for java Identifiers

<details>
<summary>
Rule 1
</summary>

Only the following characters are allowed in Java identifiers:
- `a-z`
- `A-Z`
- `0-9`
- `$`
- `_`

If we use any other character, we will get a compile-time error.

Example:
```text
total_number  ✅
total#        ❌
```
> **NOTE :-** (hyphen) is not allowed in Java identifiers; _ (underscore) is allowed.
</details>

<details>
<summary>
Rule 2
</summary>

Identifiers can't start with digits.

Example:-
```text
total123 ✅
123total ❎
```
</details>

<details>
<summary>
Rule 3
</summary>

Java identifiers are case-sensitive. Of course, the Java language itself is a case-sensitive programming language.
Example :-
```java
class Test{
    int number = 10;
    int Number = 10;
    int NUMBER = 10;
}
```
</details>

<details>
<summary>
Rule 4
</summary>
There is no length limit for Java identifiers, but it is not recommended to use very lengthy identifiers.
</details>

<details>
<summary>
Rule 5
</summary>

We cannot use reserved words as identifiers.

Example :-
```text
int x = 10; ✅
int if = 20; ❎
```
</details>

<details>
<summary>
Rule 6
</summary>

all Predefine java class names and interface names use as identifiers
```java
class Test{
    public static void main(String[args]){
        int String = 888;
        int Runnable = 999;

        System.out.println(String);
        System.out.println(Runnable);
    }
}
```
Output :-
```output
888
999
```
Even though it may be valid, it is not good programming practice because it reduces readability and creates confusion.
</details>

#### Which of the followiung are valid Identifiers

| Identifiers | status |
|--------|----------|
|total_number | ✅ |
|total# | ❎ |
|123total | ❎ |
|total123 | ✅ |
|ca$h | ✅ |
|`_$_$_$_$` | ✅ |
|all@hands | ❎ |
|java2Share | ✅ |
|Integer | ✅ |
|Int | ✅ |
|int | ❎ |

### Reserved words 

In Java, some words are reserved for specific meanings or functionality; such words are called reserved words.

#### Types of Reserved words (53)
- Keywords (50)
    - used Keywords (48)
    - unused Keywords (2)
        - goto
        - const
- Reserved Literals (3)
    - true
    - false
    - null

#### Keywords for Data Types (8)

- ```byte```
- ```short```
- ```int```
- ```long```
- ```float```
- ```double```
- ```boolean```
- ```char```

#### Keywords for Flow control (11)

- ```if```
- ```else```
- ```switch```
- ```case```
- ```default```
- ```while```
- ```do```
- ```for```
- ```break```
- ```continue```
- ```return```

#### Keywords for modifiers (11)

- ```public```
- ```private```
- ```protected```
- ```static```
- ```find```
- ```abstract```
- ```synchronised```
- ```native```
- ```strictfp(1.2 version)```
- ```transient```
- ```volatile```

#### Keywords for Exception Handling (6)

- ```try```
- ```catch```
- ```finally```
- ```throw```
- ```throws```
- ```assert (1.4 version)```

#### Class related Keywords (6)

- ```class```
- ```interface```
- ```extends```
- ```implements```
- ```package```
- ```import```

#### Object related Keywords (4)

- ```new```
- ```instanceof```
- ```super```
- ```this```

#### Void return type Keyword (1)

- ```void```

- In Java, the return type is mandatory. If a method does not return anything, then we have to declare that method with the ```void``` return type.
- But in the ```C language```, the return type is optional, and the default return type is ```int```.

#### Unused Keyword (2)

- ```goto``` The use of goto created several problems in older languages; hence, Sun engineers banned this keyword in Java.
- const Use final instead of const.

> **NOTE :-** goto and const are unused keywords, and if we try to use them, we will get a compile-time error

#### Reserved Literals (3)

- ```true```, ```false``` values for boolean data types
- ```null``` default value for object refrence.

#### Enum Keyword (1)

- ```enum (1.5 version)``` We can use enum to define a group of named constants

Example :-
```java
enum Month{
    JAN, FEB, ... Dec;
}
enum Beer{
   KF,KO,RC,FO;
}
```
#### Conclusion

<details>
<summary>
Conclusion 1
</summary>

All 53 reserved words in Java contain only lowercase alphabet symbols.
</details>

<details>
<summary>
Conclusion 2
</summary>

In Java, we have the ```new``` keyword, but there is no ```delete``` keyword because the ```destruction``` of unused objects is the responsibility of the garbage collector.
</details>

<details>
<summary>
Conclusion 3
</summary>

- The following are new keywords in Java:
    - ```strictfp``` was introduced in Java 1.2
    - ```assert``` was introduced in Java 1.4
    - ```enum``` was introduced in Java 1.5
</details>

<details>
<summary>
Conclusion 4
</summary>

- strictfp butnot strictFp
- instanceof butnot instanceOf
- synchronised butnot synchronise
- extends butnot extend
- implements butnot implements
- import butnot imports
- const butnot constant
</details>

### Data Type 

 in java every variable and every expression has some type
 - each and every data type is clearly defined
 - every assignment should be checked by compiler for type compact ability
 - because of above reason we can conclude java language is strongly typed programming language.

- java is not consider as pure Object oriented programming language because several oop features are not satisfied by java like operator overloading and multiple inheritance etc.
- More over we are dependeing on perimitive data types which are non objects.

#### Primitive data types

there are 2 types in primitive data type
1. Numeric data type
   1. Integral data type
      1. [byte](#byte)
      2. [short](#short)
      3. [int](#int)
      4. [long](#long)
   2. floating point data type
      1. [float](#float)
      2. [double](#double)
2. Non-Numeric data type
   1. [char](#char)
   2. [boolean](#boolean)

Except boolean and char remaining data type consider as signed data types because we can represent both positive and negative numbers. 

##### Byte

`size -> 1 byte(8 bit)`
 
`Range -> -2^(8-1) to 2^(8-1)-1`

```java
byte b = 128;
```
Output
```output
compile time error possible loss of precision
found : int
required : byte
```
```java
byte b = true;
```
Output
```output
compile time error incompatible type
found : Boolean
required : byte
```
- byte is the best choice if we want to handle data in terms of streams either from the file or from the Network( file suppoted from or network suppoted from is byte).

##### Short

`size -> 2 bytes (16 bits)`

`Range -> -2^(15) to 2^(15)-1 or [-32768 to 32767]`
```java
short s = 32768;
```
Output
```output
compile time error possible loss of precision
found : int
required : short
```
```java
short s = true;
```
Output
```output
compile time error incompatible type
found : Boolean
required : short
```
- short data type best suitable for 16bit processor like 8085 but these processor are completely outdated and hence corresponding short data type is also outdated data type.

##### Int

`size -> 4 bytes (32 bits)`

`Range -> -2^(31) to 2^(31)-1 or [-2147483648 to 2147483647]`

```java
int i = 2147483648;
```
Output
```output
compile time error integer number to large

```
```java
int i = 2147483648l;
```
Output
```output
compile time error possible loss of precision
found : long
required : int
```
```java
int i = true;
```
Output
```output
compile time error incompatible type
found : Boolean
required : int
```

##### Long

`size -> 8 bytes (64 bits)`

`Range -> -2^(63) to 2^(63)-1`

- the number of characters present in the big file may exceed int range hence the return type of length method is long but not int `long l = f.length()`

#### floating point data type

| float | double |
|------| -------|
| if we want 5 to 6 decimal places of accuracy then we should go for float| if we want 14 to 15 decimal places of accuracy then we should go for double|
|float follows single precision|double follows double precision|
|size -> 4 bytes | size -> 8 bytes|
|Range -> -3.4e38 to 3.4e38 | Range -> -1.7e38 to 1.7e38|

##### Char

old languages (c/c++) or ASCI code based and number of diffrent allowed ASCI code character are <=256 to represent these 256 characters 8 bits are enough hence the size of char in old languages is 1 byte
java is UNI code based and the number of diffrent unicode characters are > 256 and <= 65536 
to represent these many charcter 8 bites amy not enough compulsory we should go for 16 bites hence the size of char in java is 2 bytes

size -> 2 bytes
Range -> 0 to 65535 


##### Boolean

size -> not applicable [vartual machine dependent]

Range -> Not applicable [but allowed value are: true/ false]

```java
boolean b = 0;
```
Output
```output
compile time error incompatible type
found : int
required : boolean
```
```java
boolean b = True;
```
Output
```output
compile time error cannot find symbol
symbol : variable True
location : class Test
```
```java
boolean b = "True";
```
Output :-
```output
compile time error incompatible type
found : java.lang.String
required : boolean
```
#### Summary of java Primitive data types

| Data Type | Size  | Range  | Wrapper Class | Default Value |
| --------- | -------------- | ----- | ------------- | ----- |
| `byte`    | 1 byte         | −2⁷ to 2⁷ − 1         | `Byte`        | `0`                       |
| `short`   | 2 bytes        | −2¹⁵ to 2¹⁵ − 1       | `Short`       | `0`                       |
| `int`     | 4 bytes        | −2³¹ to 2³¹ − 1       | `Integer`     | `0`                       |
| `long`    | 8 bytes        | −2⁶³ to 2⁶³ − 1       | `Long`        | `0L`                      |
| `float`   | 4 bytes        | ~ −3.4E38 to 3.4E38   | `Float`       | `0.0f`                    |
| `double`  | 8 bytes        | ~ −1.7E308 to 1.7E308 | `Double`      | `0.0d`                    |
| `boolean` | Not applicable | `true` / `false`      | `Boolean`     | `false`                   |
| `char`    | 2 bytes        | 0 to 65,535 (Unicode) | `Character`   | `\u0000` (null character) |

> **NOTE :-** 
> - `null` is the default value for object references.
> - We cannot assign `null` to primitive data types.
> - If we try to assign `null` to a primitive type, we will get a compile-time error.

Example :-
```java
char ch = null;
```
Output :-
```output
Compile-time error incompatible types
found   : <nulltype>
required: char
```

### Literals

A constant value that can be assigned to a variable is called a **literal**.

Example :-
```java
int x = 10;
```
#### Integral Literals

For integral data types (byte, short, int, long), we can specify literal values in the following ways:

1. Decimal Form (Base 10)
   - Allowed digits: 0 to 9
```java 
int x = 10;
```
2. Octal Form (Base 8)
   - Allowed digits: 0 to 7
   - Literal value must be prefixed with 0
```java
int x = 010;
```
3. Hexadecimal Form (Base 16)
    - Allowed digits: 0–9, a–f, A–F
    - Prefix with 0x or 0X
    - Java is not case-sensitive for hexadecimal digits
```java
int x = 0x10;
```
- These are the only possible ways to specify integral literals.
- valid and invalid Declarations
```java
1. int x = 10;          // Valid
2. int x = 0786;        // Compile-time error (invalid octal digit 8)
3. int x = 0777;        // Valid
4. int x = 0xFace;      // Valid
5. int x = 0xBeef;      // Valid
6. int x = 0xBeer;      // Compile-time error (r is not a hex digit)
```
Example :-
Programmers can specify values in decimal, octal, or hexadecimal form, but the JVM always prints values in decimal form.
```java
class Test {
    public static void main(String[] args) {
        int x = 10;
        int y = 010;
        int z = 0x10;

        System.out.println(x + " " + y + " " + z);
    }
}
```
Output
```output
10 8 16
```

##### Long Literals

- By default, every integral literal is of type `int`.
- We can explicitly specify a `long` literal using suffix `l` or `L` (recommended: `L`).

Examples :-
```java
int x = 10;
long y = 10L;

int a = 10L;   // Compile-time error: possible loss of precision
```

##### Byte and Short Literals

- There is no direct way to specify byte and short literals.
- If an integral literal is within the range, the compiler automatically treats it as byte or short.

Examples :-
```java
byte b = 10;      // Valid
byte b1 = 127;    // Valid
byte b2 = 128;    // Compile-time error

short s1 = 32767; // Valid
short s2 = 32768; // Compile-time error
```
#### Floating-Point Literals

- By default, every floating-point literal is of type double.
- We cannot assign a double literal directly to a `float`.
- To specify a float literal, use suffix `f` or `F`.

Examples :-
```java
float f = 123.456;    // Compile-time error
float f = 123.456f;   // Valid
double d = 123.456;   // Valid
```

- We can explicitly specify a double literal using `d` or `D` (optional).

Example :-
```java
double d = 123.456D;  // Valid
float f = 223.456d;   // Compile-time error
```

- We can specify floating-point literals only in decimal form.
- We cannot specify floating-point literals in octal or hexadecimal form
- If we try to use octal or hexadecimal notation with floating-point values, we get a compile-time error.

Example :-
```java
double d1 = 123.456;      // Valid (decimal form)

double d2 = 0123.456;     // Compile-time error
double d3 = 0x123.456;    // Compile-time error
```
Output :-
```output
Compile-Time Error malformed floating-point literal
```

- We can assign integral literals directly to floating-point variables (float and double).
- The integral literal can be specified in decimal, octal, or hexadecimal form.
- However, floating-point literals themselves must be in decimal form only.

Examples :- 
```java

double d1 = 0786;     // Compile-time error (invalid octal digit 8)
double d2 = 0xFace;   // Valid

double d3 = 0786.0;   // Compile-time error (floating-point literal cannot be octal)
double d4 = 0xFace.0; // Compile-time error (floating-point literal cannot be hexadecimal)

double d5 = 10;       // Valid (decimal integral literal)
double d6 = 0777;     // Valid (octal integral literal)
```

- We cannot assign floating-point literals to integral data types (byte, short, int, long).

Example :-
```java
double d = 10;   // Valid (integral literal assigned to floating-point variable)

int x = 10.0;    // Compile-time error 
```
Output :-
```output
Compile-Time Error possible lossy conversion from double to int
```

- We can specify floating-point literals in exponential (scientific) notation.
- Exponential notation uses e or E and represents powers of 10.
- By default, a floating-point literal is of type double.

Example :-
```java
double d = 1.2e3;    // Valid → 1.2 × 10³ = 1200.0

float f1 = 1.2e3;    // Compile-time error (double cannot be assigned to float)
float f2 = 1.2e3f;   // Valid
```
Output :-
```output
Compile-Time Error possible lossy conversion from double to float
```

#### Boolean Literals

- The only allowed values for the boolean data type in Java are true and false.
- Java is case-sensitive, so True and False are not valid.
- A boolean value cannot be represented using numbers or strings.

Example :-
```java
boolean b1 = true;     // Valid
boolean b2 = 0;        // Compile-time error
boolean b3 = True;     // Compile-time error
boolean b4 = "true";   // Compile-time error
```
Output :- Compile-Time Errors Explained
- boolean b2 = 0;
```output
incompatible types: int cannot be converted to boolean
```
- boolean b3 = True;
```output
cannot find symbol: variable True
```
- boolean b4 = "true";
```output
incompatible types: String cannot be converted to boolean
```

#### Char Literals

- We can specify a char literal as a single character enclosed within single quotes (' ').
- A char represents exactly one character.

```java
char ch1 = 'a';    // Valid
char ch2 = a;      // Compile-time error
char ch3 = "a";    // Compile-time error
char ch4 = 'ab';   // Compile-time error
```
Output :- Compile-Time Errors Explained
- `char ch2 = a;`
```output
cannot find symbol: variable a
```
- `char ch3 = "a";`
```output
incompatible types: String cannot be converted to char
```
- `char ch4 = 'ab';`
```output
too many characters in character literal
```
- We can specify a char literal using an integral literal, which represents the Unicode value of the character.
- The integral literal can be specified in decimal, octal, or hexadecimal form.
- The allowed range for `char` is `0` to `65535` (unsigned 16-bit value).

Example :-
```java
char ch1 = 97;       // Valid ('a')
char ch2 = 0xFace;   // Valid
char ch3 = 0777;     // Valid
char ch4 = 65535;    // Valid

char ch5 = 65536;    // Compile-time error
```
Output:-
```output
Compile-time error possible lossy conversion from int to char
```

- We can represent a char literal using Unicode representation.
- The Unicode format is \uXXXX, where XXXX is a 4-digit hexadecimal number.
- Each Unicode value represents a single character.

Example :-
```java
char ch = '\u0061';
System.out.println(ch);
```
Output :-
```output
a
```
- Every valid escape character can be used as a char literal.

Example:-
```java
char ch1 = '\n';   // Valid (newline)
char ch2 = '\t';   // Valid (tab)
char ch3 = '\m';   // Compile-time error
```
Output :-
```output
Compile-Time Error illegal escape character
```
| Escape Character | Description     |
| ---------------- | --------------- |
| `\n`             | New line        |
| `\t`             | Horizontal tab  |
| `\r`             | Carriage return |
| `\b`             | Backspace       |
| `\f`             | Form feed       |
| `\'`             | Single quote    |
| `\"`             | Double quote    |
| `\\`             | Backslash       |

- Any sequence of characters enclosed within double quotes (" ") is treated as a string literal.

example :-
```java
String s = "durga";
```

#### 1.7 version enhancement to literals

##### Binary Literals

- For integral data types, up to Java 1.6, we could specify literal values in:
    - Decimal form
    - Octal form
    - Hexadecimal form
- From Java 1.7 onwards, we can also specify `binary literals`.
- Allowed digits in binary literals are `0` and `1`.
- A binary literal must be prefixed with `0b` or `0B`

Example :-
```java
int x = 0b1111;
System.out.println(x);
```
Output :-
```output
15
```

##### Uses of Underscore (_) in Numeric Literals

- From Java 1.7 onwards, we can use underscore (`_`) symbols between digits of numeric literals.
- Underscores can be used in integral and floating-point literals.

Examples :-
```java
double d1 = 123456.789;
double d2 = 1_23_456.7_8_9;
double d3 = 123_456.7_8_9;
```
- The main advantage of using underscores is that code readability is improved.

- We can use more than one underscore (`_`) between digits in numeric literals.

Example :-
```java
double d1 = 1____23____45__6.7_8_9;
double d2 = 1__2___3____45__6.7_8_9;
```
- Underscores can be placed only between digits.
- Underscores cannot be placed:
  - At the beginning or end of a literal
  - Next to a decimal point
  - Before or after a type suffix (`f`, `d`, `l`)
  - Before or after prefixes (`0x`, `0b`)

[Image](https://tinyurl.com/2s3dumts)

### Arrays

1. [Introduction](#introduction-array)
2. [Array Declartion](#array-declartion)
3. [Array Creation](#array-creation)
4. [Array Initialization](#array-initialization)
5. [Array Declaration, Creation & Initialization in a single line](#array-declaration-creation--initialization-in-a-single-line)
6. [length vs length()](#length-vs-length)
7. [Anonymous Arrays](#anonymous-arrays)
8. [Array element assignments](#array-element-assignments)
9. [Array variable assignments](#array-variable-assignments)

#### Introduction Array

- An array is an indexed collection of a fixed number of homogeneous data elements.
- The main advantage of arrays is that we can represent a large number of values using a single variable, which improves code readability.
- The main disadvantage of arrays is that they are fixed in size. Once an array is created, its size cannot be increased or decreased based on our requirement.
Therefore, to use arrays effectively, we must know the size in advance, which is not always possible.

#### Array Declartion

##### One dimension Array declartion

Syntax
```java
int[] x;
int []x;
int x[];
```
- int[] x is recommended because the array type is clearly separated from the variable name, which improves readability.
- At the time of array declaration, we cannot specify the size.
If we do, a compile-time error will occur.
```java
int[6] x;   // Invalid → compile-time error
int[] x;    // Valid
```
##### Two dimension Array declartion

Syntax
```java
int[][] x;
int [][]x;
int x[][];
int[] []x;
int[] x[];
int []x[];
```
- which of the following are valid
```java
int[] a, b;        // a → 1D, b → 1D   ✅ Valid

int[] a[], b;      // a → 2D, b → 1D   ✅ Valid

int[] a[], b[];    // a → 2D, b → 2D   ✅ Valid

int[][] a, b;      // a → 2D, b → 2D   ✅ Valid

int[][] a, b[];    // a → 2D, b → 3D   ✅ Valid

int[][] a, []b;    // ❌ Compile-time error
```
- If we want to specify the array dimension before the variable name, that facility is applicable only to the first variable in a declaration.
- If we try to apply this for the remaining variables, we will get a compile-time error.
```java
int[] []a,[]b,[]c; // ❌ Compile-time error
```
##### Three dimension Array declartion

Syntax
```java
int[][][] a;
int [][][]a;
int a[][][];
int[] [][]a;
int[] a[][];
int[] []a[];
int[][] []a;
int[][] a[];
int [][]a[];
int [][]a[];
```

#### Array Creation

- Every array in Java is an object, so we can create arrays using the `new` operator.
```java
int[] a = new int[3];
```
- For every array type, a corresponding class is available.
- These array classes are part of the Java language itself and are not accessible at the programmer level (we cannot explicitly create or extend them).
```java
int[] a = new int[3];
System.out.println(a.getClass().getName());
``` 
Output :-
```output
[I
```
Explanation of Output
- `[I` represents:
  - `[` → one-dimensional array
  - `I` → `int` type

| Array Type | corresponding Class name|
| ---------  | --------------------|
| `int[]`  | `[I` |
| `int[][]`  | `[[I` |
| `double[]`  | `[D` |
| `short[]`  | `[S` |
| `byte[]`  | `[B` | 
| `char[]`  | `[C` | 
| `boolean[]`  | `[Z `|

##### Conclusion

- At the time of array creation, it is mandatory to specify the size of the array.
```java
int[] a = new int[];    // ❌ Compile-time error
int[] a = new int[6];   // ✅ Valid
```
Output :-
```output
Compile-Time Error array dimension missing
```

- It is legal to create an array with size `0` in Java.
- A zero-length array does not store any elements, but it is a valid array object.
```java
int[] x = new int[0];
```
- If we try to specify a negative value as the array size, the program compiles successfully. But at runtime, the JVM throws a `NegativeArraySizeException`.
```java
int[] x = new int[-3];
```
Output :-
```output
Exception in thread "main" java.lang.NegativeArraySizeException
```
- To specify the array size, the allowed data types are: `byte`, `short`, `char`, and `int`. If we try to use any other data type, the compiler will throw a compile-time error.
```java
int[] x1 = new int[10];    // Valid
int[] x2 = new int['a'];   // Valid ('a' = 97)

byte b = 20;
int[] x3 = new int[b];     // Valid

short s = 30;
int[] x4 = new int[s];     // Valid

int[] x5 = new int[10L];   // ❌ Compile-time error
```
Output :-
```output
Compile-Time Error possible lossy conversion from long to int
```
> **NOTE :-** The maximum allowed array size in Java is `2147483647`, which is the maximum value of the `int` data type (`Integer.MAX_VALUE`).

#### Two dimension Creation

- In Java, two-dimensional arrays are not implemented using a matrix style.
- Instead, Java follows the array-of-arrays approach for creating multidimensional arrays.
- The main advantage of this approach is better memory utilization, because each row can have a different length.

Example 1:-
```java
int[][] x = new int[2][];
x[0] = new int[2];
x[1] = new int[3];
```
Example 2:-
```java
int[][][] x = new int[2][][];
x[0] = new int[3][];
x[0][0] = new int[1];
x[0][1] = new int[2];
x[0][2] = new int[3];
x[1] = new int[2][2];
```

#### Array Initialization

- Once we create an array, every element is automatically initialized with its default value.
- The default value depends on the data type of the array.
```java
int[] x = new int[3];

System.out.println(x);
System.out.println(x[0]);
```
Output :-
```output
[I@3e25a5
0
```
- `x[0]` prints `0` because the default value of `int` is `0`.
- When we try to print a reference variable (like an array object), Java internally calls the `toString()` method.
- The default implementation of `toString()` returns a string in the following format:
```code
<classname>@<hashcode_in_hexadecimal>
```
```java
int[][] x = new int[3][2];

System.out.println(x);
System.out.println(x[0]);
System.out.println(x[0][0]);
```
Output :-
```output
[[I@3e25a5
[[I@1e85d6
0
```
```java
int[][] x = new int[3][];

System.out.println(x);
System.out.println(x[0]);
System.out.println(x[0][0]);
```
Output :-
```output
[[I@3e25a5
null
Runtime Error NullPointerException
```
> **NOTE :-** If we try to perform any operation on a `null` reference, the JVM throws a runtime exception called `NullPointerException`.

- Once we create an array, every element is automatically initialized with its default value.
- If we are not satisfied with the default values, we can override them by assigning our own customized values.
```java
int[] x = new int[3];   // default values: 0, 0, 0

x[0] = 10;
x[1] = 20;
x[2] = 30;             // customized values
x[6] = 12; // Runtime Exception
x[-6] = 10; // Runtime Exception
x[2.6] = 189; // compile-time error
```
Output :-
  - `x[6] = 12;` and `x[-6] = 10;`
```output
Runtime Exception java.lang.ArrayIndexOutOfBoundsException
```
- `x[2.6] = 189;`
```output
compile-time error incompatible types: possible lossy conversion from double to int
```

#### Array Declaration, Creation & Initialization in a single line

- In Java, we can declare, create, and initialize an array in a single line using the shortcut (array literal) representation.
```java
int[] x;
x = new int[3];
x[0] = 10;
x[1] = 20;
x[2] = 30;

// in single line
int[] x = {10,20,30};
char[] ch = {'a','b','c','e','o'};
String[] s = {"A","AA","AAA"};
```

- we can declare, create, and initialize multi-dimensional arrays in a single line using array literals.
```java
int[][] x = {{10,20},{40,50,30}};
``` 

#### length vs length()

##### length
- `length` is a final variable applicable only for arrays.
- It represents the size (number of elements) of the array.
```java
int[] x = new int[6];
System.out.println(x.length); // 6
System.out.println(x.length()); // compile time error
```
Output :-
```output
6
compile time error caannot find symbol
symbol : method length()
location : class int[]
```
##### length()

- `length()` is a final method applicable for String objects.
- `length()` method returns the number of characters present in the String.
```java
String s = "durga";
System.out.println(s.length()); // 5
System.out.println(s.length); // compile time error
```
Output :-
```output
5
compile time error caannot find symbol
symbol : variable length
location : class java.lang.String
```

> **NOTE :-** `length` variable is applicable for arrays but not for String objects where as `length()` method is applicable for String objects but not for arrays

```java
String[] s = {"A","AA","AAA"};
System.out.println(s.length);
System.out.println(s.length());
System.out.println(s[0].length);
System.out.println(s[0].length());
```
Output :-
- `s.length`
```output
3
```
- `s.length()`
```output
Compile-time error cannot find symbol: method length()
```
- `s[0].length`
```output
Compile-time error cannot find symbol: variable length
```
- `s[0].length()`
```output
1
```
- In multidimensional arrays, the `length` variable represents only the size of the current dimension, not the total number of elements in the array.
```java 
int[][] x = new int[6][3];
System.out.println(x.length);
System.out.println(x[0].length);
```
```output
6
3
```

#### Anonymous Arrays

- Sometimes, we can create an array without a name. Such nameless arrays are called anonymous arrays.
- The main purpose of an anonymous array is instant (one-time) use.
- Anonymous arrays are commonly used while passing arrays as method arguments.

Syntax
```java
new int[]{10, 20, 30, 40};
```
Example :-

```java
class Test {
    public static void main(String[] args) {
        sum(new int[]{10, 20, 30, 40}); // anonymous array
    }

    public static void sum(int[] x) {
        int total = 0;
        for (int x1 : x) {
            total += x1;
        }
        System.out.println("The sum is " + total);
    }
}
```

- We can also create multidimensional anonymous arrays in Java.

Syntax
```java
new int[][]{{10,20},{30,40,50}}
```
- Based on our requirement, we can assign a name to an anonymous array.
- Once a name is given, it is no longer called an anonymous array.
```java
int[] x = new int[]{10, 20, 30, 40}; // named array
```
Example  :-
```java
class Test {
    public static void main(String[] args) {
        sum(new int[]{10, 20, 30, 40}); // anonymous array
    }

    public static void sum(int[] x) {
        int total = 0;
        for (int x1 : x) {
            total += x1;
        }
        System.out.println("The sum is " + total);
    }
}
```
- In the above example, an array is required only to invoke the `sum()` method.
- After the method execution is completed, the array is no longer used.
- Since the array is needed for one-time usage only, using an anonymous array is the best choice.

#### Array element assignments

##### Case

<details>
<summary>
Case -1
</summary>

- In the case of primitive arrays, array elements can be assigned values that can be implicitly promoted to the declared type of the array.
```java
int[] x = new int[5];

x[0] = 10;      // int → int ✔
x[1] = 'a';     // char → int ✔ (Unicode value 97)

byte b = 20;
x[2] = b;       // byte → int ✔

short s = 30;
x[3] = s;       // short → int ✔

x[4] = 10L;     // ❌ compile-time error
```
- In the case of float type arrays, the following data types are allowed because they can be implicitly promoted to float:
  - byte
  - short
  - char
  - int
  - long
  - float
</details>


<details>
<summary>
Case -2
</summary>

- In the case of object type arrays, array elements can store:
  - An object of the declared type, or
  - An object of any child (subclass) type of the declared type.

Example :- `Object` Array
```java
Object[] a = new Object[10];

a[0] = new Object();          // Object → Object ✔
a[1] = new String("Raj");     // String → Object ✔
a[2] = new Integer(10);       // Integer → Object ✔
```

Example :- `Number` Array
```java
Number[] a = new Number[10];

a[0] = new Integer(10);       // Integer → Number ✔
a[1] = new Double(10.5);      // Double → Number ✔
a[2] = new String("Raj");     // ❌ compile-time error
```
Output :-
```output
Compile-time error incompatible types: String cannot be converted to Number
```
</details>

<details>
<summary>
Case -3
</summary>

- In the case of interface type arrays, array elements can be: Objects of classes that implement the interface.
```java
Runnable[] r = new Runnable[10];

r[0] = new Thread();          // Thread implements Runnable ✔
r[1] = new String("Raj");     // ❌ compile-time error
```
Output
```output
Compile-time error incompatible types: String cannot be converted to Runnable
```
</details>

| **Array Type**   | **Allowed Element Types**   |
| ------- | -------------------- |
| **Primitive Arrays**           | Any value that can be **implicitly promoted** to the declared type    |
| **Object Type Arrays**         | Objects of the **declared class** or its **child (subclass) classes** |
| **Abstract Class Type Arrays** | Objects of its **concrete child classes**                             |
| **Interface Type Arrays**      | Objects of classes that **implement the interface**                   |

#### Array variable assignments

##### Case

<details>
<summary>
Case -1 
</summary> 

- Element-level promotion is allowed, but Array-level promotion is NOT allowed (except for reference types via inheritance).

Example :-
```java
int[] x = {10, 20, 30};
char[] ch = {'a', 'b', 'c'};

int[] b = x;      // ✔ valid
int[] c = ch;     // ❌ compile-time error
```
- Which of the following promotion will be performed automatically 
| Promotion               | Allowed |
| ----------------------- | ------- |
| `char` → `int`          | ✅       |
| `char[]` → `int[]`      | ❌       |
| `int` → `double`        | ✅       |
| `int[]` → `double[]`    | ❌       |
| `float` → `int`         | ❌       |
| `float[]` → `int[]`     | ❌       |
| `String` → `Object`     | ✅       |
| `String[]` → `Object[]` | ✅       |

- In the case of object type arrays, a child class array can be promoted to a parent class array.

Example :-
```java
String[] s = {"abc", "xyz", "pqr"};
Object[] o = s;   // ✔ valid
```
</details>



<details>
<summary>
Case -2 
</summary> 

- When one array is assigned to another:
  -  Elements are NOT copied
  -  Only the reference variable is reassigned

Example :-
```java
int[] a = {12, 23, 34, 45};
int[] b = {9, 87};

a = b;   // a now points to b's array
b = a;   // both reference the same array
```
[Image](https://tinyurl.com/36tddyma)
</details>



<details>
<summary>
Case -3 
</summary> 

- Whenever we assign one array to another array variable, the dimensions must match.
- If a variable is declared as a one-dimensional array reference, we can assign only a one-dimensional array to it.
- If we try to assign an array of a different dimension, we will get a compile-time error.

Example :-
```java
int[][] a = new int[3][];

a[0] = new int[4][3];   // ❌ compile-time error (2D array assigned to 1D reference)
a[0] = 10;              // ❌ compile-time error (int is not an array)

a[0] = new int[2];      // ✔ valid (1D array assigned to 1D reference)
```

> **NOTE :-** Whenever we assign one array to another array Both the data type and the dimension must match, The sizes of the arrays are NOT required to match.
</details>


Example-1 :-
```java
class Test{
    public static void main(String[] args){
        for(int i=0;i<=args.length;i++){
            System.out.println(args[i]);
        }
    }
}
```
Output :-
- `Java Test A B C`
```output
A
B
C
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 3  
```
- `Java Test A B `
```output
A
B
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 2  
```
- `Java Test`
```output
Nothing Run successfully
``` 

Example-2 :-

```java
class Test{
    public static void main(String[] args){
        String arg = {"X","Y","Z"};
        args = arg;
        for(String s : arg){
            System.out.println(s);
        }
    }
}
```
Output :-
- `Java Test A B C`
```output
X
Y
Z
```
- `Java Test A B`
```output
X
Y
Z
```
- `Java Test `
```output
X
Y
Z
```
[Image](https://tinyurl.com/yck8j7dn)

Example -3 :- [Image](https://tinyurl.com/44afrh8k)

### Types of variable 

Based on type of value represented by a variable all variable divided into two type

1. **Primitive variables** :- Can be used to represent Primitive values

Example :-
```java
int x = 10;
```

2. **Reference Variables** :- Can be used to refer Object

Example :-
```java
Student s = new Student();
```

#### Division 2
Based on position of declaration and behavior, variables in Java are divided into three types:
1. Instance variables
1. Static variables
1. Local variables

##### Instance Variables

- If the value of a variable varies from object to object, such variables are called **instance variables**.
- For every object, a separate copy of instance variables is created.
- Instance variables should be declared inside the class, but outside any method, block, or constructor.
- Instance variables are created at the time of object creation and destroyed at the time of object destruction. Hence, the scope of an instance variable is exactly the same as the scope of the object.
- Instance variables are stored in heap memory as a part of the object.

Example :-
```java
class Student {
    int id;   // instance variable
}

Student s1 = new Student();
Student s2 = new Student();

s1.id = 10;
s2.id = 20;
```
Here, id has different values for different objects, so it is an instance variable.
- We cannot access instance variables directly from a static area.
- We can access instance variables using an object reference from a static area.
- We can access instance variables directly from an instance area (non-static methods).

Example:-
```java
class Test {
    int x = 10;   // instance variable

    public static void main(String[] args) {
        System.out.println(x);      // ❌ compile-time error
        Test t = new Test();
        System.out.println(t.x);    // ✔ valid
    }

    public void m1() {
        System.out.println(x);      // ✔ direct access
    }
}
```
- For instance variables, the JVM always provides default values.
- Default values are assigned at the time of object creation.

Example :-
```java
class Test {
    // instance variables
    int x;
    double xx;
    boolean xxxx;
    String xxx;

    public static void main(String[] args) {
        Test t = new Test();
        System.out.println(t.x);     // 0
        System.out.println(t.xx);    // 0.0
        System.out.println(t.xxxx);  // false
        System.out.println(t.xxx);   // null
    }
}
``` 
- Instance variables are also known as Object-level variables or attributes.

##### Static Variables

- If the value of a variable does not vary from object to object, then it is not recommended to declare it as an instance variable. Such variables must be declared at class level using the `static` modifier.
- In the case of instance variables, a separate copy is created for every object. In the case of static variables, only one copy is created at class level and it is shared by all objects of the class.
- Static variables must be declared inside the class, but outside of any method, block, or constructor.
- Static variables are created at the time of class loading and destroyed at the time of class unloading.
Hence, the scope of a static variable is exactly the same as the scope of the `.class` file.
-When we run the command then `java Test` The JVM performs the following step :
    1. Start JVM
    2. Create and start the main thread
    3. Locate `Test.class` file
    4. Load `Test.class` → static variables are created
    5. Execute `main()` method
    6. Unload `Test.class` → static variables are destroyed
    7. Terminate main thread
    8. Shutdown JVM

- Static variables are stored in the Method Area (in modern JVMs, this is part of Metaspace).
- We can access a static variable in three ways:
  - By object reference ❌ (allowed, but not recommended)
  - By class name ✅ (recommended)
  - Directly within the same class ✅

Example :-
```java
class Test {
    static int x = 10;

    public static void main(String[] args) {
        Test t = new Test();

        System.out.println(t.x);      // allowed, but NOT recommended
        System.out.println(Test.x);   // recommended way
        System.out.println(x);        // direct access (same class)
    }
}
```
- Static variables can be accessed directly from `Static area`,`Instance area`. No object is required to access a static variable.

Example:-
```java
class Test {
    static int x = 10;

    public static void main(String[] args) {
        System.out.println(x);   // static area → direct access
    }

    public void m1() {
        System.out.println(x);   // instance area → direct access
    }
}
```
- For static variables, JVM automatically provides default values. Explicit initialization is not mandatory.

Example :-
```java
class Test {
    static int x;
    static double d;
    static String s;

    public static void main(String[] args) {
        System.out.println(x);  // 0
        System.out.println(d);  // 0.0
        System.out.println(s);  // null
    }
}
```
- Statoc avriable also known as Class-level variables or fields.

##### Local Variables

- Sometimes, to meet temporary requirements of the programmer, we declare variables inside a method, block, or constructor.
- Such variables are called:
  - Local variables
  - Temporary variables
  - Stack variables
  - Automatic variables
- Local variables are stored in Stack Memory
- Local variables are created when the block starts execution
- Once the block execution is completed, local variables are automatically destroyed. Hence, the scope of a local variable is limited to the block in which it is declared.

Example 1:-
```java
class Test{
    public static void main(String[] args){
        int i = 0;
        for(int j = 0; j < 2; j++){
            i = i + j;
        }
        System.out.println(i + " ..... " + j);
    }
}
```
Output :-
```output
cannot find symbol
symbol: variable j
```
Example 2:-
```java
class Test{
    public static void main(String[] args){
        try{
            int j = Integer.parseInt("ten");
        }
        catch(NumberFoundException e){
            j = 10;
        }
        System.out.println(j);
    }
}
```
Output :-
```output
cannot find symbol
symbol: variable j
```
- For local variables, the JVM will NOT provide default values. Initialization is compulsory before using a local variable.

Example 1:-
```java
class Test{
    public static void main(String[]args){
        int x;
        System.out.println("Hello");
    }
}
```
Output :-
```output
Hello
```
Example 2:-
```java
class Test{
    public static void main(String[]args){
        int x;
        System.out.println(x);
    }
}
```
Output :-
```output
variable x might not have been initialized
```
Example 3:-
```java
class Test{
    public static void main(String[] args){
        int x;
        if(args.length > 0){
            x = 10;
        }
        System.out.println(x);
    }
}
```
Output :-
```output
variable x might not have been initialized
```

Example 4:-
```java
class Test{
    public static void main(String[] args){
        int x;
        if(args.length > 0){
            x = 10;
        }
        else{
            x = 20;
        }
        System.out.println(x);
    }
}
```
Output :-
```output
10   (if arguments are passed)
20   (if no arguments are passed)
```

> **NOTE :-** 
> - It is not recommended to initialize local variables inside conditional or logical blocks, because there is no guarantee that those blocks will execute at runtime.
> - It is highly recommended to initialize local variables at the time of declaration, at least with default values.

- The only modifier applicable to a local variable is `final`.
- If we try to apply any other modifier, the compiler will throw a compile-time error.

Example :-
```java
class Test{
    public static void main(String[] args){

        public int x = 10;     // ❌ compile-time error
        private int x = 10;    // ❌ compile-time error
        protected int x = 10;  // ❌ compile-time error

        static int x = 10;     // ❌ compile-time error
        transient int x = 10;  // ❌ compile-time error
        volatile int x = 10;   // ❌ compile-time error

        final int x = 10;      // ✅ valid
    }
}
```
- If no modifier is specified, default access is applicable only for instance and static variables, not for local variables.


**Conclusion** :- For instance and static variables, JVM provides default values automatically, but for local variables JVM does not provide default values, so explicit initialization is mandatory before usage.

- Instance and static variables can be accessed simultaneously by multiple threads and hence are not thread-safe. In the case of local variables, for every thread a separate copy is created and hence local variables are thread-safe.

| **Type of Variable** | **Is Thread Safe?** |
| -------------------- | ------------------- |
| Instance Variable    | ❌ No                |
| Static Variable      | ❌ No                |
| Local Variable       | ✅ Yes               |

- Every variable in Java must be either
  - Instance variable, or
  - Static variable, or
  - Local variable
- Every variable in Java must also be either
  - Primitive type, or
  - Reference type
    - Hence, the valid combinations are:
      - Instance – Primitive
      - Instance – Reference
      - Static – Primitive
      - Static – Reference
      - Local – Primitive
      - Local – Reference

Example :-
```java
class Test {

    // Instance variables
    int a;          // instance - primitive
    String s;       // instance - reference

    // Static variables
    static int x;   // static - primitive
    static Test t;  // static - reference

    public static void main(String[] args) {

        // Local variables
        int y = 10;      // local - primitive
        String str = "Hi"; // local - reference
    }
}
```

#### Uninitialized Arrays

1. **Instance level**
```java
class Test {
    int[] x;
    int[] y = new int[3];

    public static void main(String[] args) {
        Test t = new Test();
        System.out.println(t.x);
        System.out.println(t.x[0]);
        System.out.println(t.y);
        System.out.println(t.y[0]);
    }
}
```
Output:-
- `t.x`
```output
null
```
- `t.x[0]`
```output
Exception in thread "main" java.lang.NullPointerException
```
- `t.y`
```output
[I@<hashcode>
```
- `t.y[0]`
```output
0
```
2. **Static level**
```java
class Test {
    static int[] x;
    static int[] y = new int[3];

    public static void main(String[] args) {
        Test t = new Test();
        System.out.println(t.x);
        System.out.println(t.x[0]);
        System.out.println(t.y);
        System.out.println(t.y[0]);
    }
}
```
Output:-
- `t.x`
```output
null
```
- `t.x[0]`
```output
Exception in thread "main" java.lang.NullPointerException
```
- `t.y`
```output
[I@<hashcode>
```
- `t.y[0]`
```output
0
```
3. **Local level**
```java
class Test {
    int[] x;              // instance reference variable (default = null)
    int[] y = new int[3]; // instance reference + object creation

    public static void main(String[] args) {
        Test t = new Test();
        System.out.println(t.x);
        System.out.println(t.x[0]);
        System.out.println(t.y);
        System.out.println(t.y[0]);
    }
}
```
Output:-
- `t.x`
```output
Compile time error variable x might not have been intialized
```
- `t.x[0]`
```output
Compile time error variable x might not have been intialized
```
- `t.y`
```output
[I@<hashcode>
```
- `t.y[0]`
```output
0
```


### Var-arg method (Variable-argument methods)

- Until the 1.4 version, we couldn’t declare a method with a variable number of arguments. If there was a change in the number of arguments, we had to create a new method, which increased code length and reduced readability. To overcome this problem, in 1.5 version, Java introduced var-arg methods. Using var-arg methods, we can declare a method that can take a variable number of arguments. Such methods are called var-arg methods.
- we can declare var-aeg method as follwos.

Synatx
```java
 m1(int... x)  
```
We can call this method by passing any number of int values, including zero.
> m1() ✅  
> m1(10) ✅  
> m1(10,5) ✅  
> m1(8,20,8,9,7,6) ✅  

```java
class Test{
    public static void m1(int... x){
        System.out.println("var-arg method");
    }
    public static void main(String []args){
        m1();
        m1(10);
        m1(1,8,3);
        m1(1,20,3,9);
    }
}
```
Output:-
```output
var-arg method
var-arg method
var-arg method
var-arg method
```
<details>
<summary>
Case 1
</summary>

Internally, a var-arg parameter is converted into a one-dimensional array. Hence, within the var-arg method, we can access individual values using their index.
```java
class Test{
    public static void sum(int... x){
        int total = 0;
        for(int x1 : x){
            total += x1;
        }
        System.out.println("The sum is "+total);
    }
    public static void main(String []args){
        sum();
        sum(10);
        sum(1,8,3);
        sum(1,20,3,9);
    }
}
```
Output:-
```output
The sum is 0
The sum is 10
The sum is 12
The sum is 33
```
</details>
<details>
<summary>
Case 2
</summary>

Which of the following are valid var-arg method declarations?

>m1(int... x) ✅  
>m1(int  ...x) ✅  
>m1(int...x) ✅  
>m1(int x...) ❎  
>m1(int. ..x) ❎  
>m1(int .x..) ❎  
</details>

<details>
<summary>
Case 3
</summary>

We can mix var-arg parameters with normal parameters in a method.
> m1(int x, int... y)  
> m1(String x, double... y) 
</details>
<details>
<summary>
Case 4
</summary>

If we mix normal parameters with a var-arg parameter, the var-arg parameter must be the last parameter.

>m1(double...d, String s)❎  
>m1(char c, String... s)✅ 
</details>
<details>
<summary>
Case 5
</summary>

Inside a var-arg method, we can have only one var-arg parameter; we cannot have more than one var-arg parameter.

>m1(int...x,double...d)❎
</details>

<details>
<summary>
Case 6
</summary>

“Inside a class, we cannot declare a var-arg method and the corresponding one-dimensional array method simultaneously; otherwise, we will get a compile-time error.
```java
class Test{
    public static void m1(int...x){
        System.out.println("int..");
    }
    public static void m1(int [] x){
        System.out.println("int[]");
    }
     public static void main(String [] args){
    }
}
```
Output:-
```output
CompileTime Error: can't declare both m1(int[]) and m1(int..) in Test
```
</details>

<details>
<summary>
Case 7
</summary>

In general, a var-arg method gets the least priority; that is, it is considered only if no other method matches. This is exactly like the default case in a switch statement.

```java
class Test{
    public static void m1(int...x){
        System.out.println("var-arg method");
    }
    public static void m1(int x){
        System.out.println("Genral Method");
    }
    public static void main(String [] args){
        m1();// var-arg method
        m1(10,20);// var-arg method
        m1(10); // Genral Method
    }
}
```
Output:-
```output
var-arg method
var-arg method
Genral Method
```
</details>

#### Equivalence b/w var-arg parameter and one-dimension Array

<details>
<summary>
Case 1
</summary>

Wherever a one-dimensional array is present, we can replace it with a var-arg parameter.
>m1(int[] x) replace with m1(int...x)  

example:- main(String args) replace with main(String... args)

| m1(int[] x) | m1(int... x) | Check |
| ------------ | ------------ | ---- |
| m1(new int[]{10}) | m1(10)| ✅ |
| m1(new int[]{10,20}) | m1(10,20) | ✅|

</details>

<details>
<summary>
Case 2
</summary>

Wherever a var-arg parameter is present, we cannot replace it with a one-dimensional array.
> m1(int...x) try to replace with m1(int[]x) invalid replacement

| m1(int..x) | m1(int[] x) |
| ------------ | ------------ |
| m1() | ❎ |
| m1(10) |❎  |
|  m1(10,20) | ❎ |
| m1(new int[]{10,20,30}) | ✅ |
</details>

```java
class Test{
    public static void m1(int[]... x){
        for(int[] x1:x){
            System.out.println(x1[0]);
        }
    }
    public static void main(String[] args){
        int [] a = new int[]{10,20,30};
        int [] b = new int[]{40,50,60};
        m1(a,b);
    }
}
```
Output:-
```output
10
40
```

> **NOTE :-**
> 1. In m1(int... x), we can call this method by passing a group of int values, and x will become a one-dimensional array.  
>2. m1(int[]... x) — we can call this method by passing a group of one-dimensional arrays, and x will become a two-dimensional int array.


### Main method 

- Whether a class contains a `main` method or not, and whether the `main` method is declared according to the requirement, is not checked by the compiler.
- These things are checked at runtime by the JVM.
- If the JVM is unable to find the `main()` method, it throws a runtime error saying:
`NoSuchMethodError: main`
```java
class Test{

}
```
Output :-
```output
Error: Main method not found in class Test, please define the main method as:
public static void main(String[] args)
```
- At runtime, the JVM always searches for the main() method with the following prototype:<br/>
`public static void main(String[] args)`
  - `public` → So that the JVM can call it from anywhere
  - `static` → So the JVM can call this method without creating an object
  - `void` → The main() method does not return anything to the JVM
  - `main` → This is the method name configured inside the JVM
  - `String[] args` → Used to accept command-line arguments
- The above syntax is very strict, and if we perform any change, we will get a runtime exception saying `NoSuchMethodError: main`.

- Even though the above syntax is very strict, the following changes are acceptable:
  - Instead of `public` `static`, we can write `static` `public` because the order of modifiers is not important.
  - We can declare the `String[]` parameter in any acceptable form:
    - `main(String[] args)` 
    - `main(String []args)` 
    - `main(String args[])` 
  - Instead of args, we can use any valid Java identifier.
Example: `main(String[] Raj)`
  - We can replace the String[] parameter with a var-args parameter.
Example: `main(String... args)`

- We can declare the main method with the following modifiers: `final`, `synchronized`, and `strictfp`.
Exmaple :-
```java
class Test {
    public static final synchronized strictfp void main(String... Raj) {
        System.out.println("Valid main");
    }
}
```

<details>
<summary>
Which of the following main method declarations are valid?
</summary>

| Main method declaration                                              | Status    | Reason    |
| ------ | --------- | ------------ |
| `public static void main(String args)`                               | ❌ Invalid | Must be `String[] args` or `String... args`   |
| `public static void Main(String[] args)`                             | ❌ Invalid | Method name is case-sensitive; must be `main` |
| `public void main(String[] args)`                                    | ❌ Invalid | `static` is mandatory                         |
|`public static int main(String[] args)`|❌ Invalid| The return type must be `void` |
| `final synchronized strictfp public void main(String[] args)`        | ❌ Invalid | `static` is missing                           |
| `final synchronized strictfp public static void main(String[] args)` | ✅ Valid   | All required conditions are satisfied         |
| `public static void main(String... args)`                            | ✅ Valid   | Var-args are allowed                          |

**Q.** In which of the above cases will we get a compile-time error?

**Ans** In the above cases, we will not get any compile-time error.
Except for the last two valid cases, in all the remaining cases we will get a runtime exception saying:
`NoSuchMethodError: main.`
</details>

#### Case

<details>
<summary>
Case 1
</summary>

Overloading of the `main` method is possible, but the JVM always calls only the `main()` method with the `String[]` argument.  
Any other overloaded main methods must be called explicitly, like a normal method call.

Example :-
```java
class Test {
    public static void main(String[] args) {
        System.out.println("String[]");
    }

    public static void main(int[] args) {
        System.out.println("int[]");
    }
}
```
Output :-
```output
String[]
```
</details>

<details>
<summary>
Case 2
</summary>

The inheritance concept is applicable to the `main()` method.  
When we execute a child class, if the child class does not contain a` main()` method, then the parent class’s `main()` method will be executed.

Example :-
```java
class Parent {
    public static void main(String[] args) {
        System.out.println("Parent main");
    }
}

class Child extends Parent {
}
```
Output :-
- Command: `java Parent`
```output
Parent main
```
- Command: `java Child`
```output
Parent main
```
📌 Reason:
The main() method is static, so it is inherited, and the JVM searches the class hierarchy to find a valid main() method.
</details>

<details>
<summary>
Case 3
</summary>

It may seem that the overriding concept is applicable to the main method, but it is not overriding.  
Instead, it is an example of method hiding.

Example :-
```java
class Parent {
    public static void main(String[] args) {
        System.out.println("Parent main");
    }
}

class Child extends Parent {
    public static void main(String[] args) {
        System.out.println("Child main");
    }
}
```
Output :-
- Command: `java Parent`
```output
Parent main
```
- Command: `java Child`
```output
Child main
```
</details>

> **NOTE :-** For the main() method, inheritance and overloading concepts are applicable, but the overriding concept is not applicable.Instead of overriding, method hiding is applicable.

#### 1.7 version Enhancements with respect to main method

- Up to Java 1.6, if a class does not contain a `main()` method, we get a runtime exception saying:
`NoSuchMethodError: main`
- From Java 1.7 onwards, instead of `NoSuchMethodError`, the JVM provides a more descriptive error message.

Example :-
```java
class Test{} 
```
Outptu :-
| Java Version | Result|
| ------------ | ----- |
| **1.6**      | `javac Test.java` ✅<br>`java Test` → Runtime Error: `NoSuchMethodError: main`                                                                                  |
| **1.7+**     | `javac Test.java` ✅<br>`java Test` → Error: Main method not found in class Test, please define the main method as:<br>`public static void main(String[] args)` |

- From Java 1.7 onwards, the `main()` method is mandatory to start program execution.  
Hence, even if a class contains a static block, it will not be executed if the class does not contain a `main()` method.

Example :-
```java
class Test {
    static {
        System.out.println("static block");
    }
}
```
Output:-
| Java Version | Result  |
| ------------ | ---- |
| **1.6**      | `javac Test.java` ✅<br>`java Test` → Output: `static block`<br>Runtime Error: `NoSuchMethodError: main`                                                        |
| **1.7+**     | `javac Test.java` ✅<br>`java Test` → Error: Main method not found in class Test, please define the main method as:<br>`public static void main(String[] args)` |

- 

Example :-
```java
class Test{
    static{
        System.out.println("static block");
        System.exit(0);
    }
}
```
Output:-
| Java Version | Result  |
| ------------ | ---- |
| **1.6**      | `javac Test.java` ✅<br>`java Test` → Output: `static block`  |
| **1.7+**     | `javac Test.java` ✅<br>`java Test` → Error: Main method not found in class Test, please define the main method as:<br>`public static void main(String[] args)` |

Example :-
```java
class Test{
    static{
        System.out.println("static block");
    }
    public static void main(String[] args){
        System.out.println("Main method");
    }
}
```
Output:-
| Java Version | Result  |
| ------------ | ---- |
| **1.6**      | `javac Test.java` ✅<br>`java Test` → Output: `static block`<br> Main method  |
| **1.7+**     | `javac Test.java` ✅<br>`java Test` → Output: `static block` <br> Main method  |

[Image 1.6v](https://tinyurl.com/yn3edeeb)  
[Image 1.7v](https://tinyurl.com/muxah8d7)

### Command line arguments

- The arguments passed from the command prompt are called `command-line arguments`.

- Using these command-line arguments, the JVM creates a String[] array and passes that array as an argument while calling the main() method.

Example :-
```
java Test A B C

args[0] -> A
args[1] -> B
args[2] -> C
```

- The main objective of command-line arguments is to customize the behavior of the `main()` method.

Example :-
```java
class Test {
    public static void main(String[] args) {
        for (int i = 0; i < args.length; i++) {
            System.out.println(args[i]);
        }
    }
}
```
Output :-
- Command: `java Test A B C`
```output
A
B
C
```

- Command: `java Test A B`
```output
A
B
```

- Command: `java Test`
```output
```

Example 2 :-
```java
class Test {
    public static void main(String[] args) {
        string[] argh = {"x","y"};
        args = argh;
        for (int i = 0; i < args.length; i++) {
            System.out.println(args[i]);
        }
    }
}
```
Output :-
- Command: `java Test A B C`
```output
x
y
```

- Command: `java Test A B`
```output
x
y
```

- Command: `java Test`
```output
x
y
```
- Within the main() method, command-line arguments are available as String values.
```java
class Test {
    public static void main(String[] args) {
    System.out.println(args[0]+args[1]);
    }
}
```
output :-
- Command: `java Test 10 20`
```output
1020
```
- Usually, a space is the separator between command-line arguments.  
If a command-line argument itself contains spaces, then we must enclose that argument within double quotes (`" "`).

Example :-
```java
class Test {
    public static void main(String[] args) {
    System.out.println(args[0]);
    }
}
```
output :-
- Command: `java Test Note Book`
```output
Note
```
- Command: `java Test "Note Book"`
```output
Note Book
```

### Java coding standards


