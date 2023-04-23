# Lambdas

- **Functional Programming**:
    - you specify what to do rather than dealing with object state
    - uses **lambda**

- **Lambda**:
    - has paramters and body but no name
    - block of code that can be passed around
    - Lambdas work with interfaces that have only one abstract method (**functional interface**)
    - Lambda can always access instance variables and class variables
    - Lambda can access local variables and method parameter only if they are ***effectively final***

- **Functional Interfaces**
    1. **Predicate**: return boolean
    2. **Consumer**: receive a value but not return it
    3. **Supplier**: when generating values
    4. **Comparator**: for custom ordering
    5. **Bicosumer**: consumer with 2 parameters

- **Calling APIs With Lambdas**
    - `List` and `Set`declare `removeIf()` that takes `Predicate`
    ```java
    bunnyList.removeIf(s -> s.charAt(0) != 'h');
    ```
    - The `sort()` method takes `Comparator` that provides the sort order. works for `List`
    ```java
    bunnyList.sort((b1, b2) -> b1.compareTo(b2));
    ```
    - `foreach()` takes a `Consumer` and calls that lambda for each element. Works for `List`, `Set`, `Map`(you have to choose whether you want to go through the keys or values)
    ```java
    bunnies.forEach(b -> System.out.println(b));
    ```