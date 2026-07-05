# File I/O

1. [File](#file)
2. [FileWriter](#filewriter)
3. [FileReader](#filereader)
4. [BufferedWriter](#bufferedwriter)
5. [BufferedReader](#bufferedreader)
6. [PrintWriter](#printwriter)

## File

```java
File f = new File("abc.txt");
```
This line will not create any physical file. First, it checks whether a physical file named `abc.txt` is available or not.  
If it is available, then `f` simply references that file.

If it is not available, then we are just creating a Java `File` object to represent the name `abc.txt`. 
```java
File f = new File("abc.txt");
System.out.println(f.exists()); // checks whether the file exists or not
f.createNewFile(); // creates a file
System.out.println(f.exists());
```
Output
- 1st run
```outptu
false
true
```
- 2nd run
```outptu
true
true
```
- We can also use a Java `File` object to represent a directory directly.
```java
File f = new File("durg123");
System.out.println(f.exists()); // checks whether the directory exists or not
f.mkdir(); // it creates a directory
System.out.println(f.exists());
```
Output
- 1st run
```outptu
false
true
```
- 2nd run
```outptu
true
true
```
> **NOTE:** In Unix, everything is treated as a file. The Java File I/O concept is implemented based on the Unix operating system. Hence, a Java `File` object can be used to represent both files and directories.

### File class Constructors

```java
File f = new File(String name);
```
It creates a Java `File` object to represent the name of a file or directory in the current working directory.

Example: Write code to create a file `abc.txt` in the current working directory.
```java
File f = new File("abc.txt");
f.createNewFile();
```

```java
File f = new File(String subDirectoryName, String name);
// Or
File f = new File(File subDirectory, String name);
```
It creates a Java `File` object to represent the name of a file or directory present in the specified subdirectory.

**Example**: Write code to create a directory named `durga123` in the current working directory and create a file named `demo.txt` inside that directory.

```java
File f = new File("durga123");
f.mkdir();

File f1 = new File("durga123", "demo.txt");
// or
File f1 = new File(f, "demo.txt");

f1.createNewFile();
```

Example: Write code to create a file named `abc.txt` in the `E://xyz` folder.
```java
File f = new File("E://xyz", "abc.txt");
f.createNewFile();
```
Assume that the `E://xyz` folder is already available in our system.

### Important Method present in FILE class

| Methods  | Definition |
| ------------------------- | --------------- |
| `boolean exists()`        | Returns `true` if the specified file or directory is available.  |
| `boolean createNewFile()` | First, this method checks whether the specified file is already available or not. If it is already available, then this method returns `false` without creating any physical file. If the file is not available, then this method creates a new file and returns `true`.                     |
| `boolean mkdir()`         | First, this method checks whether the specified directory is already available or not. If it is already available, then this method returns `false` without creating any physical directory. If the directory is not available, then this method creates a new directory and returns `true`. |
| `boolean isFile()`        | Returns `true` if the specified `File` object is pointing to a physical file. |
| `boolean isDirectory()`   | Returns `true` if the specified `File` object is pointing to a physical directory. |
| `String[] list()`         | This method returns the names of all files and subdirectories present in the specified directory. |
| `boolean delete()`        | Deletes the specified file or directory.  |

**Example**: Write a program to display the names of all files and subdirectories present in `C://durga-classes`.
```java
File f = new File("C://durga-classes");
String[] fileList = f.list();

int count = 0;

for (String s : fileList) {
    count++;
    System.out.println(s);
}

System.out.println("The total number of files and directories: " + count);
```

**Example**: To display only file names

```java
File f = new File("C://durga-classes");
String[] fileList = f.list();

int count = 0;

for (String s : fileList) {
    File f1 = new File(f, s);
    if (f1.isFile()) {
        count++;
        System.out.println(s);
    }
}

System.out.println("The total number of files: " + count);
```
**Example**: To display only directory names

```java
File f = new File("C://durga-classes");
String[] fileList = f.list();

int count = 0;

for (String s : fileList) {
    File f1 = new File(f, s);
    if (f1.isDirectory()) {
        count++;
        System.out.println(s);
    }
}

System.out.println("The total number of directories: " + count);
```

## FileWriter

 we can use filewriter to write charecter data to file.

### FileWriter Constructor 

```java
FileWriter fw = new FileWriter(String fname);
```
```java
FileWriter fw = new FileWriter(File f);
```
The above FileWriter constructors are meant for overwriting existing data. Instead of overwriting, if we want to perform an append operation, then we have to create a FileWriter by using the following constructors:
```java
FileWriter fw = new FileWriter(String fname, boolean append);
```
```java
FileWriter fw = new FileWriter(File f, boolean append);
```
> **NOTE**: If the specified file is not already available, then all the above constructors will create that file.

### Method

| Method             | Definition        |
| ------------------ | ----------------- |
| `write(int ch)`    | Writes a single character.                                                                 |
| `write(char[] ch)` | Writes an array of characters.                                                             |
| `write(String s)`  | Writes a string to the file.                                                               |
| `flush()`          | Guarantees that the total data, including the last character, will be written to the file. |
| `close()`          | Closes the file.                                                                           |


Example :
```java
import java.io.*;

class FileWriterDemo2 {
    public static void main(String[] args) throws IOException {

        FileWriter fw = new FileWriter("abc.txt");

        fw.write(100); // adding a single character
        fw.write("\nMy name is Ashutosh Raj");
        fw.write('\n'); // new line

        char[] ch1 = {'a', 'b', 'c'};
        fw.write(ch1);
        fw.write('\n'); // new line

        fw.flush();
        fw.close();
    }
}
```
Output  
The abc.txt file will contain the following output:
```output
D
My name is Ashutosh Raj
abc
```
In the above program, FileWriter performs overwriting of existing data.  
Instead of overwriting, if we want to perform an append operation, then we have to create the FileWriter object as follows:
`FileWriter fw = new FileWriter("abc.txt", true);`

> **NOTE:** The main problem with `FileWriter` is that we have to insert the line separator (`\n`) manually, which varies from system to system. This creates difficulty for the programmer. We can solve this problem by using `BufferedWriter` and `PrintWriter` classes.

## FileReader

We can use `FileReader` to read character data from a file.

### FileReader Constructors

```java
FileReader fr = new FileReader(String fname);
```
```java
FileReader fr = new FileReader(File f);
```
### Methods

1. **int read()**  
It attempts to read the next character from the file and returns its Unicode value. If the next character is not available, then this method returns `-1`. Since this method returns a Unicode value (an `int` value), at the time of printing we have to perform typecasting.

Example:
```java
FileReader fr = new FileReader("abc.txt");
int i = fr.read();

while (i != -1) {
    System.out.println((char) i);
    i = fr.read();
}
```
2. **int read(char[] ch)**  
It attempts to read characters from the file into a character array and returns the number of characters copied from the file.

Example :
```java
File f = new File("abc.txt");
char[] ch = new char[(int) f.length()];
FileReader fr = new FileReader(f);

fr.read(ch);

for (char ch1 : ch) {
    System.out.print(ch1);
}
```
3. **void close()**  
This method is used after reading or writing operations to close the file.

> **NOTE:** By using FileReader, we can read data character by character, which is not convenient for the programmer. 

The use of `FileWriter` and `FileReader` is not recommended because:
- While writing data using `FileWriter`, we have to insert the line separator (`\n`) manually, which varies from system to system. This is difficult for the programmer.
- By using `FileReader`, we can read data character by character, which is not convenient for the programmer.
- To overcome these problems, we should use BufferedWr`iter and `BufferedReader`.

## BufferedWriter

We can use `BufferedWriter` to write character data to a file.

### BufferedWriter Constructors

```java
BufferedWriter bw = new BufferedWriter(Writer w);
```
```java
BufferedWriter bw = new BufferedWriter(Writer w, int bufferSize);
```
> **NOTE:** `BufferedWriter` cannot communicate directly with the file. It communicates through another `Writer` object.


**Q** Which of the following are valid?
 
- `BufferedWriter bw = new BufferedWriter("abc.txt"); ` ❌ Invalid
- `BufferedWriter bw = new BufferedWriter(new File("abc.txt"));` ❌ Invalid
- `BufferedWriter bw = new BufferedWriter(new FileWriter("abc.txt"));` ✅ Valid
- `BufferedWriter bw =new BufferedWriter(new BufferedWriter(new FileWriter("abc.txt")));` ✅ Valid

### Methods

1. `write(int ch)`
1. `write(char[] ch)`
1. `write(String s)`
1. `flush()`
1. `close()`
1. `newLine()` – Inserts a line separator.

**Q:** When compared with FileWriter, which additional capability is available in BufferedWriter in the form of a method?  

**Ans:** Inserting a new line character (using the newLine() method).

Example :
```java
import java.io.*;

class BufferedWriterDemo {
    public static void main(String[] args) throws IOException {

        FileWriter fw = new FileWriter("abc.txt");
        BufferedWriter bw = new BufferedWriter(fw);

        bw.write(97);
        bw.newLine();

        char[] ch1 = {'a', 'b', 'c', 'd'};
        bw.write(ch1);
        bw.newLine();

        bw.write("Ashutosh");
        bw.newLine();

        bw.write("Raj");

        bw.flush();
        bw.close();
    }
}
```
Output 
```output
a
abcd
Ashutosh
Raj
```

> **NOTE:** Whenever we close a BufferedWriter, the internally associated FileWriter is closed automatically, and we are not required to close it explicitly.


## BufferedReader

we can use BufferedReader to read character data from the file
the mainaddvantage of BufferedReader when compared with file reader is we caan read data line by line in addition to character by character 

### BufferedReader Constructors

```java
BufferedReader br = new BufferedReader(Reader r);
```
```java
BufferedReader br = new BufferedReader(Reader r,int bufferSize);
```
>**NOTE:** BufferedReader can't communicate directly with the file and it can communicate via some reader object

### Methods

```java
int read();
int read(char[] ch);
void close();
String readLine();
```
Explanation:
- `int read()` – Reads a single character from the file and returns its ASCII/Unicode value. If the end of the file is reached, it returns -1.
- `int read(char[] ch)` – Reads multiple characters from the file and stores them into the character array. It returns the number of characters read.
- `void close()` – Closes the stream and releases the associated resources.
- `String readLine()` – It attempts to read the next line from the file and returns it. If the next line is not available, this method returns null.

## PrintWriter

It is the most enhanced writer used to write character data to a file.  
The main advantage of **PrintWriter** over **FileWriter** and **BufferedWriter** is that we can write any type of primitive data directly to the file.

### PrintWriter Constructors:

```java
PrintWriter pw = new PrintWriter(String filename);
PrintWriter pw = new PrintWriter(File f);
PrintWriter pw = new PrintWriter(Writer w);
```
PrintWriter can communicate directly with a file or it can communicate through another Writer object.

### Methods of PrintWriter

```java
write(char ch);
write(char[] ch);
write(String s);

flush();
close();

print(char ch);
print(double d);
print(int i);
print(boolean b);
print(String s);

println(char ch);
println(double d);
println(int i);
println(boolean b);
println(String s);
```
Explanation:

- `write()` → Used to write character data to the file.
- `print()` → Used to print different types of data without moving to the next line.
- `println()` → Used to print data and move the cursor to the next line.
- `flush()` → Forces the data to be written immediately to the file.
- `close()` → Closes the stream and releases the resources.
```java
import java.io.*;

class PrintWriterDemo1 {
    public static void main(String[] args) throws IOException {
        FileWriter fw = new FileWriter("abc.txt");
        PrintWriter out = new PrintWriter(fw);

        out.write(100);
        out.println(100);
        out.println(true);
        out.println('c');
        out.println("Ashutoh");

        out.flush();
        out.close();
    }
}
```
Output
```output
d100
true
c
Ashutoh
```

**Q.** What is the difference between `write(100)` and `print(100)`?

In the case of `write(100)`, the corresponding character '**d**' will be added to the file because 100 represents the character '**d**' in ASCII/Unicode.  
But in the case of `print(100)`, the integer value 100 will be written directly to the file as text.


> **NOTE:** The most enhanced writer to write character data to a file is `PrintWriter`, whereas the most enhanced reader to read character data from a file is `BufferedReader`.  
- In general, we use Readers and Writers to handle character data (text data), whereas we use Streams to handle binary data such as images, videos, and audio files.
- We use an OutputStream to write binary data to a file and an InputStream to read binary data from a file.

```diagram
Object
  |
  |-- Writer
  |     |
  |     |-- OutputStreamWriter
  |     |        |
  |     |        |-- FileWriter
  |     |
  |     |-- BufferedWriter
  |     |
  |     |-- PrintWriter
  |
  |-- Reader
        |
        |-- InputStreamReader
        |        |
        |        |-- FileReader
        |
        |-- BufferedReader
```

**Q.** Write a program to merge data from two files into a third file?
```java
import java.io.*;

class FileMergeDemo {
    public static void main(String[] args) throws IOException {

        BufferedReader br1 = new BufferedReader(new FileReader("file1.txt"));
        BufferedReader br2 = new BufferedReader(new FileReader("file2.txt"));

        PrintWriter pw = new PrintWriter(new FileWriter("file3.txt"));

        String line = br1.readLine();

        while (line != null) {
            pw.println(line);
            line = br1.readLine();
        }

        line = br2.readLine();

        while (line != null) {
            pw.println(line);
            line = br2.readLine();
        }

        br1.close();
        br2.close();
        pw.close();

        System.out.println("Data merged successfully into file3.txt");
    }
}
```
Output

- file1.txt
```output
Hello
Java
```
- file2.txt
```output
Welcome
Programming
```
- file3.txt
```output
Hello
Java
Welcome
Programming
```


**Q.** Write a program to perform a file merge operation where the merging should be done line by line alternately?
```java
import java.io.*;

class FileMergeAlternate {
    public static void main(String[] args) throws IOException {

        BufferedReader br1 = new BufferedReader(new FileReader("file1.txt"));
        BufferedReader br2 = new BufferedReader(new FileReader("file2.txt"));

        PrintWriter pw = new PrintWriter(new FileWriter("file3.txt"));

        String line1 = br1.readLine();
        String line2 = br2.readLine();

        while (line1 != null || line2 != null) {

            if (line1 != null) {
                pw.println(line1);
                line1 = br1.readLine();
            }

            if (line2 != null) {
                pw.println(line2);
                line2 = br2.readLine();
            }
        }

        br1.close();
        br2.close();
        pw.close();

        System.out.println("Files merged alternately into file3.txt");
    }
}
```
Output

- file1.txt
```output
A
B
C
```
- file2.txt
```output
1
2
3
```
- file3.txt
```output
A
1
B
2
C
3
```

**Q.** Write a program to perform a file extension operation?
```java
import java.io.*;

class FileExtensionDemo {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new FileReader("input.txt"));
        PrintWriter pw1 = new PrintWriter(new FileWriter("output.txt"));
        PrintWriter pw2 = new PrintWriter(new FileWriter("delete.txt"));

        String line = br.readLine();

        while (line != null) {

            boolean available = false;

            BufferedReader br1 = new BufferedReader(new FileReader("delete.txt"));
            String target = br1.readLine();

            while (target != null) {
                if (line.equals(target)) {
                    available = true;
                    break;
                }
                target = br1.readLine();
            }

            if (available == false) {
                pw1.println(line);
            }

            line = br.readLine();
            br1.close();
        }

        br.close();
        pw1.close();
        pw2.close();
    }
}
```
**Q.** Write a program to remove duplicates from the given input file?

```java
import java.io.*;
import java.util.HashSet;

class RemoveDuplicates {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new FileReader("input.txt"));
        PrintWriter pw = new PrintWriter(new FileWriter("output.txt"));

        HashSet<String> set = new HashSet<>();

        String line = br.readLine();

        while (line != null) {

            if (!set.contains(line)) {
                pw.println(line);
                set.add(line);
            }

            line = br.readLine();
        }

        br.close();
        pw.close();

        System.out.println("Duplicates removed successfully.");
    }
}
```
Output
- input.txt
```output
Java
Python
Java
C++
Python
```
- output.txt
```output
Java
Python
C++
```
