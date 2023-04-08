# My Summary and Notes of Java SE 11 Developer

# Chapter 1

<details>

  <summary>Components Of Java</summary>

## Components of Java

- Use integrated development environment (IDE) to make writing and running code easier.
- Java Development Kit (`JDK`):

  - Contains min software you need to do development.
  - Key pieces:
    - compiler: [`javac`](#javac-program-generates-bytecode-file-class-that-the-java-command-can-run)
    - launcher: [`java`](#java-launches-the-java-virtual-machine-jvm-before-running-the-code)
    - archiver command: `jar`
    - API(application programming interfaces) documentation command: `javadoc`
    - `JVM`

- Java Runtime Environment (`JRE`)

  - The `JRE` was a subset of the `JDK` that was used for running a program but could not compile one.
  - In Java 11, the `JRE` is no longer available as a stand-alone download or a subdirectory of the `JDK`.

- Flow:
  1. #### `javac`: program generates bytecode file (`.class`) that the `java` command can run.
  2. #### `java`: launches the `Java Virtual Machine (JVM)` before running the code.
  3. `JVM`: knows how to run bytecode (`.class`) on the actual machine it is on.

</details>

<details>

  <summary>Benefits of Java</summary>

## Benefits of Java

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

</details>

<details>

  <summary>Java Class Structure</summary>

## Java Class Structure

- <u>Classes</u>: basic building blocks.
- <u>Defining a class</u>: you describe all the parts and characteristics of building blocks.
- <u>Object</u>: is a runtime instance of a class in memory. An object is often referred to as an instance since it represents a single representation of the class.
- All the various objects of all the different classes represent the state of your program.
- <u>Reference</u>: is a variable that points to an object.

<details>

  <summary>Fields and Methods</summary>

### Fields and Methods

- methods/functions/procedures + fields/variables = members of class
- Variables hold the state of the program, methods operate on that state
- keyword: a word with special meaning
- The method name and parameter types are called the method signature.
- The method declaration consists of additional information such as the return type

</details>

<details>

<summary>Comments</summary>

### Comments

1. single line
2. multiple line
3. javadoc
</details>

<details>

<summary>Classes and Files</summary>

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

</details>

</details>


<details>

<summary>Writing a main() Method</summary>

## Writing a `main()` Method

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
java Ege           # Notice that we must omit the .class extension to run Ege.java.
```
- `java` accepts the name of the class!!!
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

</details>

## Package Declarations and Imports
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

### `javac` `java` `jar`
Option | `javac` | `java` | `jar`
--- | --- | --- | ---
`-cp` `-classpath` `--class-path` | X | X | X
`-d` | X | - | -
`-c` | - | - | X
`-C` | - | - | X
`-v` | - | - | X
`-f` | - | - | X

## Ordering Elements In Class

Element | Required? | Location
--- | --- | ---
Package declaration | No | First line of file
Import | No | immediately after package declaration
Class declaration | Yes | After import
Field declarations | No | inside class
Method declarations | No | inside class
Comments | No | Can go anywhere even in first line of file

## Code Formating In Exam

Don't need to check for imports if:
- Code that begins with a class name
- Code that begins with a method declaration
- Code that begins with a code snippet that would normally be inside a class or method,
- Code that has line numbers that don’t begin with 1

## Bonus:

```java
// INSERT PACKAGE NAME HERE
public class Bird { }
```
- Bird is in `/my/directory/named/A/Bird.java`
- The package name represents any folders underneath the current path
- Thus `package my.directory.named.A;` wont work
- Correct one is `package named.A;`


___
 

# Chapter 2: Java Building Blocks

## Creating Objects
```java
public class Chick {
  public Chick() {
    System.out.println("in constructor");
  }
}
```
Key points of constructor: 
  - the name of the constructor matches the name of the class
  - there’s no return type.

### Instance Initializer Blocks (IIB)

- Code block: the code between `{}`
- Instance initializer: when the code block is out of a method

### Order of Initialization

- Fields and instance initializer blocks run in the order they appear
- Constructor runs after fields and IIB
- Order matters for the fields and blocks of code. You can’t refer to a variable before it has been defined


## Understanding Data Types

### Primitive types: 8 built-in data types

Keyword | Type | Example
--- | --- | ---
`boolean` | true/false | true
`byte` | 8bit integral | 123
`short` | 16bit integral | 123
`int` | 32bit integral | 123
`long` | 64bit integral | 123L
`float` | 32bit floating-point | 123.45f
`double` | 64bit floating-point | 123.456
`char` | 16bit unicode | 'a'

- String is not primitive even though there is built-in support. It is an object.
- byte can hold between -128 to 127
- `short` and `char` are closely related: 
  - `short` is signed, `char` is unsigned; thus `char` has higher range for positive integer
  - you can use them interchangeably in some cases
  ```java
  short bird = 'd';
  char mammal = (short)83;

  System.out.println(bird); // Prints 100
  System.out.println(mammal); // Prints S

  short reptile = 65535; // DOES NOT COMPILE
  char fish = (short)-1; // DOES NOT COMPILE
  ```

### Literals
- When a number is present in the code, it is called a literal.

```java
long max = 3123456789; // DOES NOT COMPILE, because 3123456789 is seen as int, however this is bigger than Integer.MAX_VALUE
long max = 3123456789L; // now Java knows it is a long
```

- Underscore
  - You can not put `_` at the beginning/end of literal and right before/after decimal point
  ```java
  double notAtStart = _1000.00; // DOES NOT COMPILE
  double notAtEnd = 1000.00_; // DOES NOT COMPILE
  double notByDecimal = 1000_.00; // DOES NOT COMPILE
  double annoyingButLegal = 1_00_0.0_0; // compiles
  double reallyUgly = 1__________2; // Also compiles
  ```

### Reference Types
- Reference type is an instance of an object
- Primitive types hold their values in the memory where variable is allocated
- Reference types point to an object by storing the object's memory adress
- A reference can be assigned to another object of the same or compatible type.
- A reference can be assigned to a new object using the new keyword.

### Primitive VS Reference Types
- Primitive types can not be null
  ```java
  int value = null; // DOES NOT COMPILE
  String s = null;
  ```
- Reference types can be used to call methods (if reference is not null)
  ```java
  String reference = "hello";
  int len = reference.length();
  int bad = len.length(); // DOES NOT COMPILE
  ```
- all the primitive types have lowercase type names. bUt reference types are classes, by convention begin with uppercase.

## Declaring Variables

### Identifiers
- An identifier is the name of a variable, method, class, interface, or package
- 4 rules for legal identifiers:
  1. Must begin with a letter or `$` or `_`
  2. Can include numbers but cannot start with them
  3. `_` is not allowed as identifier
  4. Cannot use java's reserved words (`abstract`, `case`, `continue`, `const`, `goto`, `true`...)

### Declaring Multiple Variables
- You can declare many variables in the same declaration as long as they are all of the same type. You can also initialize any or all of those values inline.
```java
void sandFence() {
 String s1, s2;
 String s3 = "yes", s4 = "no";

 int num, String value; // DOES NOT COMPILE
}
```

## Initializing Variables

### Initiliazing Local Variables
- A local variable is a variable defined within a constructor, method, or initializer block
- Local variables do not have a default value and must be initialized before use. Complier will report error if you use an uninitialized variable.

### Passing Constructor and Method Paramters
- Variables passed to a constructor or method are called constructor parameters or method parameters
- They are like local variables that have been initialized before the method is called, by the caller.
```java
public void findAnswer(boolean check) {}

public void checkAnswer() {
 boolean value;
 findAnswer(value); // DOES NOT COMPILE: value is not initialized
}
```

### Defining Instance and Class Variables
- An instance variable, often called a field, is a value defined within a specific instance of an object
- On the other hand, a class variable is one that is defined on the class level and ***shared among all instances of the class***. It can even be publicly accessible to classes outside the class without requiring an instance to use.
- You can tell a variable is a class variable because it has the keyword `static` before it
- Instance and class variables do not require you to initialize them. As soon as you declare these variables, they are given a default value:
  Variable Type | Default Initialization Value
  --- | --- 
  `boolean` | `false`
  `byte`, `short`, `int`, `long` | 0
  `float`, `double` | 0.0
  `char` | '\u0000' (NUL)
  All object references | `null`

### Introducing `var`
- you just type `var` instead of the primitive or reference type
- `var is a specific type defined at compile time. It does not change type at runtime.
- The formal name of this feature is local variable type inference:
  1. Thus can be used only as local variable
    ```java
    public class VarKeyword {
      var tricky = "Hello"; // DOES NOT COMPILE: this is an instance variable
    }
    ```

  2. Instructing the compiler to determine the type for you
    ```java
    public void reassignment() {
      var number = 7;
      number = 4;
      number = "five"; // DOES NOT COMPILE
    }

    var apples = (short)10;
    apples = (byte)5;   // value stored in apples is still short but in here byte is automatically promoted to short
    apples = 1_000_000; // DOES NOT COMPILE: beyond the limits of short
    ```

- the compiler looks only at the line with the declaration. Initialization has to be done in the same line as declaration for `var`, otherwise code does not compile:
```java
public void reassignment() {
  var question; // does not compile
  question = 1;
}
```

- Java does not allow `var` in multiple variable declarations.

- While a `var` cannot be initialized with a null value without a type, it can be assigned a null value after it is declared (provided that the underlying data type of the `var` is an object)
- `var` can be initialized to a null value if the type is specified
```java
var n = null; // DOES NOT COMPILE: cannot be initialized to null

var n = "myData";
n = null;

var m = 4;
m = null; // DOES NOT COMPILE: int cannot be null

var o = (String)null; // var can be initialized to a null value if the type is specified
```

### Bonus
```java
public int addition(var a, var b) { // DOES NOT COMPILE: var can be used only for local variables, a and b are method parameters
 return a + b;
}
```
```java
package var;

public class Var { // because of case sensitivity this is allowed
  public void var() { // Naming a method var is legal: var is not a reserved word
    var var = "var"; // Naming a local variable var is legal: var is not a reserved word
  }
  public void Var() {
    Var var = new Var(); // Naming a local variable var is legal: var is not a reserved word 
  }
}
```

- While `var` is not a reserved word and allowed to be used as an identifier, it is considered a `reserved type name`.
- A `reserved type name` means it cannot be used to define a type, such as a class, interface, or enum
```java
public class var { // DOES NOT COMPILE
  public var() {
  }
}
}
```

## Managing Variable Scope
- **Local variables**: In scope from declaration to end of block
- **Instance variables**:  In scope from declaration until object eligible for garbage collection
- **Class variables**: In scope from declaration until program ends 

## Destroying Objects
- All Java objects are stored in your program memory’s heap.
- ***Garbage collection*** refers to the process of automatically freeing memory on the heap by deleting objects that are eligible for garbage collection
- ***eligible for garbage collection*** refers to an object’s state of no longer being accessible in a program.
- eligible for garbage collection does'nt mean the object will be immediately garbage collected.

### Calling `System.gc()`
- What is the System.gc() command guaranteed to do? Nothing, actually. It merely suggests that the JVM kick off garbage collection. Nothing is guaranteed.
- JVM can ignore this request. `System.gc()` is not guaranteed to run or do anything. 
- Program may still run out of memory even if `System.gc()` is called

### Tracing Eligibility
- An object is no longer reachable when one of two situations occurs:
  1. The object no longer has any references pointing to it.
  2. All references to the object have gone out of scope.

