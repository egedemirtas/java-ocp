# Making Decisions

- **`switch`**
    - `case`, `defult`, `break` are optional
    - `default`: it is branched to only if there is no matching case value for the switch statement, regardless of its position within the switch statement
    - allows `int`,`byte`,`short`,`char`(and their wrappers), `String`, `enum`, `var`(if matches any type in here)
    ```java
    var dayOfWeek = 5;
    switch(dayOfWeek) {
        case 0:
            System.out.println("Sunday");
        default:
            System.out.println("Weekday");
        case 6:
            System.out.println("Saturday");
            break;
    }

    //output:
    Weekday
    Saturday

    // if dayOfWeek = 6, Output:
    Saturday // default is branched only if there is no match

    // if dayOf Week =0, Output:
    Sunday
    Weekday   //  default statement is executed since there was no break statement in first case
    Saturday
    ```
    - the values in each `case` statement must be ***compile time constant values*** of the same data type as the `switch` value
    - ***Compile time constants***: `enum` variable, `final` variable, literals
    - support numeric promotion that does not require an explicit cast

- **`foreach`**
    - Right-side has to be: built in java array **or** object implementing `Iterable`
    - Left-side must be compatible with right side (`var` is also allowed)

- **`break`:** will terminate the nearest inner loop it is currently in the process of executing
- **`continue`:** finishes the ***current iteration*** of loop
- If there is **unreachable code** because of `break`,`continue`,`return` then code will not compile