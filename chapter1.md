# Components of Java
- **IDE:** makes writing and running code easier
- **JDK:** contains minimum software you need to do dev
    - **javac:** complier: turns source code to bytecode(**.class**)
    - **java:** launcher: launches JVM and then calls the code
    - **JVM:** knows how to run bytecode on the machine it is on
    - **jar:** archiver
    - **Javadoc:** document generator
    - **APIs:** reusable codes
    ```shell
    javac Ege.java     # The result is a file of bytecode by the same name, but with a .class filename extension
    java Ege "hello"   # Notice that we must omit the .class extension to run Ege.java.
    ```
- **JRE:** subset of **JDK**, can run code but cannot compile code (as of java 11 no longer available)
- **Benefits of Java:**
    - **OOP:** all code defined in classes, functional programming allowed in classes 
    - **Encapsulation:** access modifiers to protect data from unintended access and modification.
    - **Platform Independent:** ***“write once, run everywhere”*** compiled once into bytecode, then can be run everywhere
    - **Robust:** garbage collection prevents memory leak
    - **Simple:** no pointer, no operator overloading
    - **Secure:** runs in JVM
    - **Multithreaded**
    - **Backward Compatibility**
- **Java Class Structure**
    - Classes are basic building blocks
    - Classes consist of members called fields and methods. 
    - Variables hold the state of the program, methods operate on that state
    - An object is an runtime instance of a Java class in memory
    - **Method Signature:** name + parameter list
- **Classes vs Files**:
    - A public class name needs to match the file name
    - If you have nultiple classes in 1 file, then only 1 of them can be public
- **`main()`**
    - Execution begins with `main()`; lets the ***JVM*** call our code
    - Its is a gateway between the startup of a Java process (***JVM*** allocates memory/CPU etc), and the beginning of the code.
    - Must exists, must be `static`
- **Package Declarations and Imports**
    - **Packages:** logical groupings for classes
    - **`import`:** tell Java which packages to look in for classes
    - A **wildcard** ending an `import` statement means you want to import all classes in that package. (it does not import child packages)
    - Importing all the classes with wildcard doesn't slow down program execution. Complier figures out which classes are needed.
