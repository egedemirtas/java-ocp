# My Summary and Notes of Java SE 11 Developer

## Chapter 1

### Components of Java

- Use integrated development environment (IDE) to make writing and running code easier.
- Java Development Kit (`JDK`):

  - Contains min software you need to do development.
  - Key pieces:
    - compiler: [`javac`](#javac-program-generates-bytecode-file-class-that-the-java-command-can-run)
    - launcher: [`java`](#java-launches-the-java-virtual-machine-jvm-before-running-the-code)
    - archiver command: `jar`
    - API(application programming interfaces) documentation command: `javadoc`

- Java Runtime Environment (`JRE`)

  - The `JRE` was a subset of the `JDK` that was used for running a program but could not compile one.
  - In Java 11, the `JRE` is no longer available as a stand-alone download or a subdirectory of the `JDK`.

- Flow:
  1. #### `javac`: program generates bytecode file (`.class`) that the `java` command can run.
  2. #### `java`: launches the `Java Virtual Machine (JVM)` before running the code.
  3. `JVM`: knows how to run bytecode (`.class`) on the actual machine it is on.

### Benefits of Java

- `Object Oriented`:
  - All code is defined in classes, and most of those classes can be instantiated into objects. (static classes are an exception)
  - Java allows for functional programming within a class
- `Encapsulation`: Java supports access modifiers to protect data from unintended access and modification.
- `Platform Independent`: Java is an interpreted language that gets compiled to bytecode.
  - `“write once, run everywhere.”`: Java code gets compiled once rather than needing to be recompiled for different operating systems.
  - It is possible to write code that throws an exception in some environments
- `Robust`: prevents memory leaks by managing garbage collection automatically.
- `Simple`: no pointers, no operator overloading.
- `Secure`: Java code runs inside the `JVM`. This creates a sandbox that makes it hard for Java code to do evil things to the computer it is running on.
- `Multithreaded`
- `Backward Compatibility`: Most of the time, old programs will work with later versions of Java. Sometimes, changes that will break backward compatibility occur. Deprecation is a flag to indicate it shouldn’t be used.

### Java Class Structure

- <u>Classes</u>: basic building blocks.
- <u>Defining a class</u>: you describe all the parts and characteristics of building blocks.
- <u>Object</u>: is a runtime instance of a class in memory. An object is often referred to as an instance since it represents a single representation of the class.
- All the various objects of all the different classes represent the state of your program.
- <u>Reference</u>: is a variable that points to an object.

### Fields and Methods

- methods/functions/procedures + fields/variables = members of class
- Variables hold the state of the program, methods operate on that state
- keyword: a word with special meaning
- The method name and parameter types are called the method signature.
- The method declaration consists of additional information such as the return type

### Comments

1. single line
2. multiple line
3. javadoc

### Classes vs Files

- Most of the time, each Java class is defined in its own .java file
- If you do have a public class, it needs to match the filename.
- Access modifiers: default, private, protected, public
- You can declare a class without writing a access modifer for the class. In this case the class will be default.
- You can even put two classes in the same file. When you do so, at most one of the classes in the file is allowed to be public:

```java
public class Animal {
}
class Animal2 { // default
}
```

### Writing a `main()` Method

- A Java program begins execution with its `main()` method.
- `main()` method is the gateway between the startup of a Java process (managed by the `JVM`), and the beginning of the code. `JVM` calls on the underlying system to allocate memory and CPU time, access files, and so on
- The `main()` method lets the JVM call our code.
- To compile Java code, the file must have the extension `.java`
```java
public class Ege {
  public static void main(String[] args) {
    System.out.println(args[0]);
    System.out.println(args[1]);
  }
}
```
```shell
javac Ege.java     # The result is a file of bytecode by the same name, but with a .class filename extension
java Ege           # Notice that we must omit the .class extension to run Ege.java
```
- To compile Java code: the file must have the extension .java and class name must match file name.
- `static` binds a method to its class so it can be called by just the class name. Java doesn’t need to create an object to call the `main()`
- If `main()` is not present, the process will throw an error and terminate.
- If `main()` is not static it will throw exception. Non-static `main()` is invisble for JVM.
- `main()` method’s parameter list:
  - an array of java.lang.String objects
  ```java
  String[] args   //  The variable name args hints that this list contains values that were read in when the JVM started.
  String args[]   //  The characters [] are brackets and represent an array. An array is a fixed-size list of items that are all of the same type.
  String... args  //  The characters ... are called varargs (variable argument lists).
  ```

### Passing Parameters to Java Program

```java
public class Ege {
  public static void main(String[] args) {
    System.out.println(args[0]);
    System.out.println(args[1]);
  }
}
```
```shell
javac Ege.java
java Ege Pipet "cok seviyorum" # use double quotes if you want to use a sentence

# output:
# Pipet
# cok seviyorum
```

- All command-line arguments are treated as String objects. Thus if you type 123 as an argument, it will compile and `args[0]` returns 123 since `args` is String array
- If you try `System.out.println(args[2]);` for this example, it will throw exception: `java.lang.ArrayIndexOutOfBoundsException`

### Running Code In One Line

```shell
java Ege.java Pipet "cok seviyorum"
```
- You can run a program without compiling it. 
- Java is still a compiled language, which means the code is being compiled in memory (Even if the code compiles properly, no `.class` file is created) and the java command can give you a compiler error.

Full | single-file source-code
--- | ---
Produces a `.class` file | Fully in memory 
For any program | For programs with one file
Can import code in any available Java library | Can only import code that came with the JDK


### Package Declarations and Imports
- Packages: logical groupings for classes
- `import`: tell Java which packages to look in for classes
- If a package begins with `java` or `javax`, this means it came with the JDK

### Wildcards
```java
import java.util.*; // imports all the classes in java.util.
```
- Every class in the java.util package is available to this program when Java compiles it. 
- It doesn’t import child packages, fields, or methods; it imports only classes. 
- Importing all the classes with wildcard doesn't slow down program execution. Complier figures out which classes are needed.

### Redundant Imports
- `java.lang` automatically imported thus can use `System` without import statement.

### Naming Conflicts
- class names don’t have to be unique across all of Java: `java.util.Date` `java.sql.Date`

```java
// When the class is found in multiple packages, Java gives you a compiler error
import java.util.*;
import java.sql.*; 

// it works. If you explicitly import a class name, it takes precedence over any wildcards present
import java.util.Date;
import java.sql.*;

// both have precendence: Java gives you a compiler error
import java.util.Date;
import java.sql.Date;

// if you really need to use both classes:
import java.util.Date;
public class Conflicts {
  Date date; // or java.util.Date date;
  java.sql.Date sqlDate;
}
```

### Compiling and Running Code With Package
```java
package packagea;
public class ClassA {
}
//--------------------------------
package packageb;
import packagea.ClassA;
public class ClassB {
  public static void main(String[] args) {
    ClassA a;
    System.out.println("Got it");
  }
}
```
1. Go to C:\temp
2. Compile `javac packagea/ClassA.java packageb/ClassB.java` or `javac packagea/*.java packageb/*.java` (if you want all the classes to be compiled under packagea and packageb)
3. 2 files created: `packagea/ClassA.class` and `packageb/ClassB.class`
4. Run `java packageb.ClassB`

- `javac` places the compiled classes in the same directory as the source code
- The `-d` option specifies this target directory:
```shell
javac -d classes packagea/ClassA.java packageb/ClassB.java
```
- Packages created in these directories: `classes/packagea/ClassA.class` and `classes/packageb/ClassB.class`
- To run the program, you specify the classpath:
```shell
java -cp classes packageb.ClassB
java -classpath classes packageb.ClassB
java --class-path classes packageb.ClassB
```
- You can't use `-d` for `java` command
- You can use classpath commands for both `java` and `javac`

### Compling With JAR File
```shell
java -cp ".;C:\temp\someOtherLocation;c:\temp\myJar.jar" myPackage.MyClass     # semi colon used to seperate: look for packages in current directory
                                                                               # and someOtherLocation and within myJar.jar

java -cp "C:\temp\directoryWithJars\*" myPackage.MyClass                       # match all the JARs in directory, excluding subdirectories
```

### Creating JAR File
```shell
jar -cvf myNewFile.jar                        # -c = --create, -v = --verbose, -f = --file, 
jar --create --verbose --file myNewFile.jar

jar -cvf myNewFile.jar -C dir                 # specify directory
```

### Ordering Elements In Class

Element | Required? | Location
--- | --- | ---
Package declaration | No | First line of file
Import | No | immediately after package declaration
Class declaration | Yes | After import
Field declarations | No | inside class
Method declarations | No | inside class
Comments | No | Can go anywhere even in first line of file

### Code Formating In Exam

Don't need to check for imports if:
- Code that begins with a class name
- Code that begins with a method declaration
- Code that begins with a code snippet that would normally be inside a class or method,
- Code that has line numbers that don’t begin with 1