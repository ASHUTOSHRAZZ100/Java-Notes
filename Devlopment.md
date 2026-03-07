# Devlopment

## Javac

We can use the javac command to compile a single Java source file or a group of Java source files.

```bash
javac [option] Test.java
javac [option] A.java B.java C.java
javac [option] *.java
```
Options are:
- `-version` : Shows Java compiler version
- `-d` : Specifies destination directory for `.class` files
- `-source` : Specifies Java source version
- `-verbose` : Shows detailed compilation process
- `-cp`/`-classpath` : Specifies path to find classes and libraries

## Java

We use the `java` command to run a compiled `.class` file.

```bash
java [options] Test A B C
```
- `A`, `B`, `C` are command-line arguments passed to the main() method.  

Options are:
  - `-version` : Displays Java runtime version
  - `-D` : Sets a system property
  - `-ea`/`-esa` : Enable assertions
  - `-dsa`/`-da` : Disable assertions

> **NOTE:** We can compile any number of Java source files at a time, but we can run only one `.class` file at a time using the `java`

## Classpath

- Classpath describes the location where the required .class files are available.

- The Java compiler (`javac`) and JVM use the classpath to locate the required `.class` files.

- By default, the JVM always searches the current working directory for required `.class` files.

- If we set the classpath explicitly, then the JVM searches only in the specified classpath location and does not search in the current working directory.

We can set the classpath in three ways:

1. Environment variable `CLASSPATH`
2. Command prompt level
3. Command level using `-cp` or `-classpath` option

### Environment Variable CLASSPATH

- This way of setting the classpath is permanent and remains preserved even after system restart.
- Whenever we install permanent software in our system, this approach is recommended.

### Command prompt level

At the command prompt level, we can set the classpath using the set command:
```bash
set classpath=c:\durgaclass
```
- This classpath setting is valid only for that particular command prompt session.
- Once the command prompt is closed, the classpath will be lost.

### Command Level

At the command level, we can set the classpath using the -cp option:
```java
java -cp c:\durgaclass Test
```
- This classpath setting is valid only for that particular command execution.
- Once the command execution is completed, the classpath will be lost.

> **NOTE:** Among the three ways of setting the classpath, setting the classpath at the command level is recommended, because dependent classes may vary from command to command.

- Once we set the classpath, we can run our program from any location.
- Once we set the classpath explicitly, the JVM will not search the current working directory unless it is included in the classpath. It will search only in the specified classpath locations.

Example 1:
```java
class Test {
    public static void main(String[] args) {
        System.out.println("Classpath Demo");
    }
}
```
Output
- Compile the Program `C:\raj> javac Test.java`
- Run from Same Directory `C:\raj> java Test`
```output
Classpath Demo
```
- Run from Another Directory Without Classpath `C:\> java Test`
```output
Runtime Error: NoClassDefFoundError: Test
```
- Run with Classpath `C:\> java -cp C:\raj Test`
```output
Classpath Demo
```
- Run from Another Drive `D:\> java -cp C:\raj Test`
```output
Classpath Demo
```
- Run from Another Drive `E:\> java -cp C:\raj Test`
```output
Classpath Demo
```
- Incorrect Classpath `C:\> java -cp E:\ Test`
```output
Runtime Error: NoClassDefFoundError: Test
```
- Including Current Directory in Classpath `C:\> java -cp .;E:\ Test`
```output
Classpath Demo
```

Example 2:
- File in Directory C:
```java
public class AStudent {
    public void m1() {
        System.out.println("I want a job");
    }
}
```
- File in Directory D:
```java
public class ItIndustry {
    public static void main(String[] args) {
        AStudent a1 = new AStudent();
        a1.m1();
        System.out.println("You will get it");
    }
}
```
Compilation and Execution
- Step 1: Compile AStudent `C:\> javac AStudent.java`
- Step 2: Compile `ItIndustry` without Classpath `D:\> javac ItIndustry.java`
```
Compile-time error: cannot find symbol
symbol: class AStudent
location: class ItIndustry
```
- Step 3: Compile with Classpath `D:\> javac -cp C:\ ItIndustry.java` ✅ Valid compilation
- Step 4: Run without Classpath `D:\> java ItIndustry`
```output
Runtime Error: NoClassDefFoundError: AStudent
```
- Step 5: Run with Only C:\ in Classpath `D:\> java -cp C:\ ItIndustry` ❌ Still Error
- Step 6: Include Current Directory and C: `D:\> java -cp .;C:\ ItIndustry`
```Output
I want a job
You will get it
```
- Run from Another Directory `E:\> java -cp D:\;C:\ ItIndustry`
```Output
I want a job
You will get it
```

Example 3:
- File in Directory C:\
```digram
C:
└── pack1
    └── pack2
        └── Kareena.class
```
```java
package pack1.pack2;

public class Kareena {
    public void m1() {
        System.out.println("Hello Saif, can you please set the hello tune?");
    }
}
```
- File in Directory D:\
```digram
D:
└── pack3
    └── pack4
        └── Saif.class
```
```java
package pack3.pack4;

import pack1.pack2.Kareena;

public class Saif {
    public void m2() {
        Kareena k = new Kareena();
        k.m1();
        System.out.println("Not possible because I am in SCJP class");
    }
}
```
- File in Directory E:\
```digram
E:
└── Durga.class
```
```java
import pack3.pack4.Saif;

public class Durga {
    public static void main(String[] args) {
        Saif s = new Saif();
        s.m2();
        System.out.println("Hello Kareena, can I help you?");
    }
}
```
Compilation Commands
- Compile Kareena `C:\> javac -d . Kareena.java`
- Compile Saif (without classpath) `D:\> javac -d . Saif.java`
```output
Compile-time error: cannot find symbol
symbol: class Kareena
location: class pack3.pack4.Saif
```
- Compile Saif with Classpath `D:\> javac -d . -cp C:\ Saif.java`
- Compile Durga (without classpath) `E:\> javac Durga.java`
```output
Compile-time error: cannot find symbol
symbol: class Saif
location: class Durga
```
- Compile Durga with Classpath `E:\> javac -cp D:\ Durga.java`

Runtime Execution
- Run without classpath `E:\> java Durga`
```output
Runtime Error: NoClassDefFoundError: pack3.pack4.Saif
```
- Include D:\ in Classpath `E:\> java -cp .;D:\ Durga`
```output
Runtime Error: NoClassDefFoundError: pack1.pack2.Kareena
```
- Include All Required Locations `E:\> java -cp .;D:\;C:\ Durga`
```output
Hello Saif, can you please set the hello tune?
Not possible because I am in SCJP class
Hello Kareena, can I help you?
```
- Run from Another Drive `F:\> java -cp E:\;D:\;C:\ Durga`

#### Conclusion

- If any location is created because of a package statement, that location should be resolved by using an import statement, and the base package location must be included in the classpath.
- The compiler checks only one-level dependency, whereas the JVM checks all levels of dependencies during runtime.
- In the classpath, the order of locations is important, and the JVM always searches from left to right until the required match is found.