# Java Building Blocks
- **Instance Initializer:** Code block(`{}`) that is outside of method
- **Primitive Types:**
    - Cannot be null
    - Primitive types hold their values in the memory where variable is allocated
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
- `short` is signed, `char` is unsigned; thus `char` has higher range for positive integer. You can use them interchangeably, as long as they do not exceed their limits.
- **Literal:** a number that is present in the code
- **Reference Types:** 
    - Reference types point to an object by storing the object's memory adress
    - Can be used to call methods
    - All reference types are the same size
- **Identifiers:** 
    - name of variable/method/class/interface/package
    - You cannot use ***reserved words***
- **Declaring Multiple Varaibles:**
    ```java
    void sandFence() {
        String s1, s2;
        String s3 = "yes", s4 = "no", s5;

        int num, String value; // DNC: must be the same type
    }
    ```
- **Local Variable:** variable defined in method/constructor/initializer block
- **Instance Variable vs Class Variable:**
    - **Instance variable** or **field**, is a value defined within a specific instance of an object
    - **Class variable** is one that is defined on the class level and shared among all instances of the class. Uses `static`
    - You don't need to initialize instance or class varables, they have default values:
      Variable Type | Default Initialization Value
        --- | --- 
        `boolean` | `false`
        `byte`, `short`, `int`, `long` | 0
        `float`, `double` | 0.0
        `char` | '\u0000' (NUL)
        All object references | `null`
- **`var`:**
    - can be used for primitive or reference type
    - defined at compile time and cannot be change during runtime
    - can only be used as **local variable**
    - declaration and initialization must be done in the same line
    - cannot be used multiple variable declarations
    - `var` can not be initialized to null, but can be assgined to it later
- **Managing Variable Scope**
    - **Local variables**: In scope from declaration to end of block
    - **Instance variables**:  In scope from declaration until object eligible for garbage collection
    - **Class variables**: In scope from declaration until program ends 
- **Destroying Objects**
    - objects stored in memory
    - **eligible for garbage collection:** object’s state of no longer being accessible in a program.
    - **`System.gc()`:** suggest JVM to start gabage collection
    - Eligible for garbage collection or `System.gc()` doesn't gurantee anything
    - Object is garbage collected but reference is not

