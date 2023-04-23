# Core Java APIs

- **`String`**
    - doesn't need `new`to be instantiated
    - implements `CharSequence`
    - **Immutability**: once it is created it can not be changed
    - **Immutable classes are `final`:** prevents subclass creation. You wouldn’t want a subclass adding mutable behavior.
    - **`String intern()`:** 
        - returns the value from the string pool if it is there, otherwise add to string pool
        - `String` literals are automatically added to pool, thus you would need to use `intern()` only with `Strings` constructed with `new String()`

- **`StringBuilder`:** 
    - mutable
    - doesn't implement `equals()`

- If a class doesn’t have an equals method java uses `==`

- **String Pool**
    - location in JVM that collects strings
    - contains literals and constants
    - `myObject.toString()` doesn't go to string pool

- **Arrays**
    - fixed size
    - `myArray.toString()` -> `Ljava.lang .String;@160bc7c0`
    - Can print contents of an array with `Arrays.toString(myArray)`
    - `Arrays.sort(myArray)`
    - `Arrays.binarySearch(myArray, search)`: only works for ascending sorted arrays

- **Varargs**: 
    - `String... args`
    - Lets a method accept variable number of values

- **ArrayList**
    - implements `List` and `toString()`
    - `Collections.sort(myArrList);`

- **Wrapper Classes**
    - immutable
    - takes advantage of caching
    - Each one of them has its own constructor but it is not recommeded to create a wrapper object with constructors. Instead use `float.valueOf((float) 1.0)` (allows objetc caching)
    - Each wrapper can be converted back to primitive: `intValue()`

- **Autoboxing and Unboxing**
    - **Autoboxing**: type the primitive value, and Java will convert it to the relevant wrapper class for you
    - **Unboxing**: opposite of autoboxing

- **ArrayList to Array**
    - `Object[] objectArray = list.toArray();`: using `toArray()` without parameters will return `Object` array
    - `String[] stringArray = list.toArray(new String[0]);` 

- **Array to List**
    - `List<String> list = Arrays.asList(array);`: fixed size list, list and array are connected
    - `List<String> list = List.of(array);`: returns immutable list
    - Creating mutable and disconnected list from array:
    ```java
    List<String> fixedSizeList = Arrays.asList("a", "b", "c");
    List<String> expandableList = new ArrayList<>(fixedSizeList);
    ```

- **Sets**
    - can not contain duplicate values
    - `HashSet` and `TreeSet`(when ordering is important) implements `Set`

- **Maps**
    - has key and value
    - `HashMap` and `TreeMap`(when ordering is important) implements `Map`