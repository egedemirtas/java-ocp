# Methods and Encapsulation

- **Method Signature:** method name and parameter list

- **Access Modifiers**:
    - **`private`**: method can be only called within the class
    - **`protected`**: same package or subclass
    - **default**: has no keyword, method can be called from classes that are in the same package
    - **`public`**: can be called from any class

- **Varargs**
    - must be the last in method's paramter list
    - allowed to have at most 1 vargars per method
    - You can pass to varargs parameters:
        - array
        - list the elementsas literals
        - omit the vararg parameter (empty array will be created)
        - null (array reference that refers to null)
    
- **static**
    - `static` member called class variable
    - `static` methods/variables don't require an instance of class
    - Applies to the class, not an instance of class
    - Methods that use any `static` variable must be static as well
    - A `static` member cannot call an instance member without referencing an instance of the class. However an instance member can call any instance or class variable

- **Constant Variable**
    - use `static final`: 
        - `static` is used for memory management
        - You can assign a value once, after you declare a constant variable
    - Asume you have a `static final` list, you can actually modify the list, but you can not refer to another list!

- Avoid using **static initializer blocks**

- `import` is for classes, `import static` is for static members of classes

- Java is a ***pass-by-value*** language: copy of the variable is made and the method receives that copy. Assignments made in the method do not affect the caller

- **Method Overloading**
    - Same name but different ***method signatures***. So only paramter list can change
    - On an overloaded method you can also have different access modifiers, specifiers, return types and exception list

- **Autoboxing in Method Parameters**: java will do only 1 conversion
```java
public static void play(Long l) {}

public static void main(String[] args) {
    play(4);    //DNC: int->long->Long
}
```

- **Generics**
    - ***Type Erasure***: generics are used at compile time, thus `List<String> strings` will be compiled as `List strings`
    - Because of type erasure you cannot overload with generic paramters:
    ```java
    public void walk(List<String> strings) {}
    public void walk(List<Integer> integers) {}    // DNC
    ```
    - You also can`t overload a generic method in a parent class
    ```java
    public class LongTailAnimal {
        protected void chew(List<Object> input) {}
    }
    public class Anteater extends LongTailAnimal {
        protected void chew(List<Double> input) {}  // DNC
    }
    ```

- **Encapsulation**
    - ***Encapsulation*** means only methods in the class can refer to the instance variables. Callers are required to use these methods.
    - As long as instance variables are `private`, the class is encapsulated. Only methods can read/update these variables.
    - Uses ***getter/accessor methods*** and ***setter/mutator methods***
    - Prevents unwanted changes/access to the variables


