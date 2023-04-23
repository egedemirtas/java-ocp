# Operators

- **Increment and Decrement**
    - **Pre- :**If the operator is placed before the operand, then the operator is applied first and the value returned is the new value of the expression. 
    - **Post- :**If the operator is placed after the operand, then the original value of the expression is returned, with operator applied after the value is returned.
- **Numeric Promotions**
    1. If two values have different data types, Java will automatically promote one of the values to the larger of the two data types.
    2. If one of the values is integral and the other is floating-point, Java will automatically promote the integral value to the floating-point value’s data type.
    3. Smaller data types: `byte`, `short`, and `char` are first promoted to int any time they’re used with a Java binary arithmetic operator, even if neither of the operands is int.
        - Unary operators are excluded from this rule
    4. After all promotion has occurred and the operands have the same data type, the resulting value will have the same data type as its promoted operands.
- **Assignment Operator**
    - auto cast from small to larger data types, otherwise throws error 
    - assignment operator returns the assigned value
- **Compound Assignment:** automatically casts variables from large to small
- **Equality Operator:**
    - can compare: 2 objects(compares reference adress), 2 booleans or 2 numerics(auto promotion)
- **Relational Operator**: allows promotion