# Class Design

- **Inheritance** is the process by which a subclass automatically includes any `public` or `protected` or **default** members of the class, defined in the parent class.

- **Inheritance** is transitive: X->Y->Z. X can access inherited members of Z. This is also **multiple level inheritance**

- **Single inheritance**: a class may inherit from only 1 direct parent class

- **Multiple Inheritance is not supported**: which parent to inherit values from in case of a conflict?

- A class may implement multiple interfaces

- All classes inherit from a single class: `Object`

- `toString()` and `equals()` methods are available in `Object`; therefore, they are accessible in all classes.

- ***Top-level class***: a class that is not defined inside another class. They can only have `public`or package-private(default) class.
- ***Inner class***: a class defined in another class. Can have `public`, default, protected, private access.
- Java file can have many top level classes but can have **at most** only 1 top-level `public` class

- **`this`**
    - refers to the current instance of the class
    - Can be used to access any member of the class, including inherited members.
    - cannot be used in static method or static initializer block (object creation is need for `this`)

- **`super`**
    - `super` reference excludes any memebers found the current class, and can refer only to the members available via inheritance.

- **Constructor**
    - same name as the class + no return type, not even `void`
    - Doesn't accept `var` as parameter
    - **Constructor overloading**: Declaring constructors with different signatures
    - **Instantiation**: Constructors used when creating new objects
    - **Default constructor**: If you don't have a constructor java will create one wtihot any parameters. Generated during compile time.
    - You can have `private` constructor:
        - Prevent ***default constructor***
        - Prevent instantiation of the class
        - Useful when class has only `static` members

- **`this()`**
    - refers to a constructor call within the class. Thus you can use it with parameters if such constructor exists: `this(weight, "brown");`

- **`super()`**
    - always refers to the most direct parent`s constructor

- the first statement of every constructor is either `this()` or `super()`

- Java compiler automatically inserts a call to the no-argument constructor `super()` if you do not explicitly call `this()` or `super()` as the first line of a constructor. These are all the same:
```java
public class Donkey {}

public class Donkey {
  public Donkey() {}
}

public class Donkey {
  public Donkey() {
    super(); 
  }
}
```

- You can extend a class which only have `private` constructor. However, only an inner class can extend it and able to call `super()`

- **Constructor and `final` fields**
    - `final` instance/class variables do not have default values
    - `final` instance/class variables can be assigned only once in: the line they are declared or intance initializer or constructor
    - By the time the constructor completes, all `final` instance variables must be assigned a value. 
    - (local `final` variables don't need to be initialized unless they are used)

## **Order Of Initialization**
1. **Class Initialization**
    - **Loading the class**: starting from highest super class, invoke all `static`members in the class hierarchy
    - A class may never be loaded if it is not used.
    - Happens at most once for each class
    - JVM controls when the class is initialized: 
        - when the program starts
        - when a static member of the class is referenced
        - just before an instance of the class is created

2. **Instance Initialization**
    - when `new` is used
    - starting from the highest super class; process all the instance variables, process all the instance initializers, initialize the constructor

1. The first statement of every constructor is a call to an overloaded constructor via this(), or a direct parent constructor via super().
2. If the first statement of a constructor is not a call to this() or super(), then the compiler will insert a no-argument super() as the first statement of the constructor.
3. Calling this() and super() after the first statement of a constructor results in a compiler error.
4. If the parent class doesn’t have a no-argument constructor, then every constructor in the child class must start with an explicit this() or super() constructor call.
5. If the parent class doesn’t have a no-argument constructor and the child doesn’t define any constructors, then the child class will not compile.
6. If a class only defines private constructors, then it cannot be extended by a top-level class.
7. All final instance variables must be assigned a value exactly once by the end of the constructor. Any final instance variables not assigned a value will be reported as a compiler error on the line the constructor is declared.

- **Method Overriding**
    - When a subclass declares a new implementation for an inherited method with the same signature and compatible return type.
    1. same signature
    2. The method in the child class must be at least as accessible as the method in the parent class.
    3. The method in the child class may not declare a **checked** exception that is broader than the parent class method, nor child method can not introduce new **checked** exception
    4. If the method returns a value, it must be the same or a subtype of the method in the parent class, known as ***covariant return types.***

- **Generics and Overriding**
    - You cannot overload methods wtih generic paramters but you can override them
    - When overriding a method with generic type, you must match the signature exactly (including the generic)
    - If an overridden method's return type is generic, then the return values must be covariant. And the generic must match exactly

- **Hiding `static` Methods**
    - same 4 rules of ***method overriding*** applied with 1 more: overridden method must be `static` both in child and parent
    - ***Hidden methods*** are not considered ***overriddden*** 

- **`final` Methods**
    - cannot be overriden nor hidden
    - you may want this if you want to guarantee a behaviour in the parent regardless of which child is invoking the method

- **Hidden Variables**: varaibles can not be overridden but can be hidden when chil and parent both define a variable with the same name

- **Polymorphism**
    - ***polymorphism***: the property of an object to take on many different forms
    - A Java object may be accessed 
        - using a reference with the same type as the object, 
        - a reference that is a superclass of the object, 
        - or a reference that defines an interface the object implements, either directly or through a superclass.
    - a cast is not required if the object is being reassigned to a super type or interface of the object

-**`instanceof` With Polymorphism**
    - can be used to check whether an object belongs to a particular class or interface and to prevent ClassCastExceptions at runtime
    - you can not use it with unrelated types

- **Polymorphism And Method Overriding**
    - ***polymorphism*** states that when you override a method, you replace all calls to it, even those defined in the parent class.
    - This way, subclasses have their own custom implementation of overridden methods. It also means the parent class does not need to be updated to use the custom or overridden method