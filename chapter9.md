# Advanced Class Design

- **Abstract Classes**
    1. ***cannot be instantiated***
    2. All top-level types, including abstract classes, cannot be marked `protected` or `private`.
    3. ***may*** include zero or more **abstract methods** and **nonabstract methods**
    4. **may** contain constructors: although abstarct classes can not be instantiated, they can be initialized trhough constructors by their subclasses
    5. The first concrete class that extends an abstract class must provide an implementation for all of the inherited abstract methods.
    6. can not be `final`

- **Abstract Methods**
    1. An **abstract method** is a method that does not define an implementation when it is declared
    2. can only be defined in abstract classes and interfaces
    3. can not be `private` or `final`
    4. Implementing an abstract method in a subclass follows the same rules for overriding a method

- An abstract class can extend a nonabstract class

- **Interface**
    1. ***cannot be instantiated***
    2. All top-level types, including interfaces, cannot be marked `protected` or `private`.
    3. cannot be `final`
    4. may include zero or more abstract methods.
    5. An interface can extend any number of interfaces.
    6. An interface reference may be cast to any reference that inherits the interface, although this may produce an exception at runtime if the classes aren’t related.
    7. The compiler will only report an unrelated type error for an `instanceof` operation with an interface on the right side if the reference on the left side is a `final` class that does not inherit the interface.
    8. An interface method with a body must be marked `default`, `private`, `static`, or `private static`
    - Interfaces simply define a set of rules/ a contract that a class implementing them must follow
    - Interfaces are implicitly `abstract`, thus they cannot be `static` or `final` or `private` ((***implicit modifiers***))

- **Interface Methods**
    - has the same 4 rules as in ***Abstract Methods***
    5. Interface methods without a body are assumed to be `abstract` and `public`. (***implicit modifiers***)

- **Interface Variables**
    1. Interface variables are assumed to be `public`, `static`, and `final`. (***implicit modifiers***)
    2. Because interface variables are marked `final`, they must be initialized with a value when they are declared.

- **Difference between abstract classes and interfaces**
    1. Interfaces include implicit modifiers
    2. Interfaces can not have constructors
    3. support multiple inheritance: A class can implement any number of interfaces, separeted by comma
    
- **Inheriting Interfaces**
    1. An interface can extend multiple interfaces using `extends` since interfaces can not be initialized and don't have constructors. If an abstract class or interface is implementing an interface, it is not required to implement all the interface methods
    2. A class can implement an interface
    3. A class can extend another class whose ancestor implements an interface.

- **Duplicate Interface Method Declarations**
    - Since java allows multiple inheritance via interfaces, what would happen if a class inherits the same method from 2 different interfaces?
        - As they have identical method declarations, they are also considered **compatible**: complier can resolve differences without conflicts
    - What happens if a class implements multiple interfaces with methods with different signatures? 
        - This actually ***method overloading***, thus the class must implement both methods
    - What happens if a class/interface/abstarct class implements multiple interfaces with a method that has different return types?
        - If methods' return types are ***covariant***, you have to implement the method with return type that is the subclass. Ex: interfaceA has a method that returns `String`, interfaceB has also a method that returns `CharSequence` with the same signature: classC implements interfaceA and interfaceB, must implement the method with `String`
        - you can not implement if return types are not covariant!!!

- **Casting interfaces**
    - complier doesn't allow casting to unrelated types
    - The compiler does not allow a cast from an interface reference to an object reference if the object type does not implement the interface. 
    ```java
    interface Canine {}
    class Dog implements Canine {}
    class Wolf implements Canine {}
    public class BadCasts {
    public static void main(String[] args) {
        Canine canine = new Wolf();
        Canine badDog = (Dog)canine;   // throws exception at runtime: because of polymorphism, java can't decide the class of canine instance. Thus it complies and throw exception at runtime
        Object badDog = (String)canine; //DNC: String doesnt implement Canine
        } 
    }
    ```

- **Inner Classes**
    - Nested classes: member inner classes, local classes, anonymous classes, and static nested classes

- **Member Inner Class**
    - defined at the member level of a class
    - Developers often define a member inner class inside another class if the relationship between the two classes is very close
    - A top-level class can be only `public` or default, but member inner classes can have any access modifiers they want
    - A member inner class can contain many of the same methods and variables as a top-level class. But `static` members are disallowed in member inner classes
    - you can use a member inner class by calling it from outer class. one advantage is that you completely control the inner member class 