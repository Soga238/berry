---
layout: default
---

# Expressions

## Basis

Berry provides some unary operators and binary operators. For example, the logical AND operator `&&` is a binary operator and the logical NOT operator `!` is a unary operator. Some operators can be used as either a unary operator or a binary operator. For example, the `-` operator represents a subtraction in the expression `1-2`, and the negative operator is represented in the expression `-1`.

It is important to note whether the type of the operand supports the current operation. For example, the operation `"10"+10` is illegal because Berry does not allow a string to be added to an integer. Usually Berry does not perform implicit type conversion. , but when an integer is added to a floating point number, Berry will automatically convert the integer operand to a floating point number. For example, executing `1.1+1` will result in a result of `2.1`.

In expressions, the precedence and associativity of operators determine the order of calculations. The precedence and associativity of operators are given in the [Basic Concepts](./basic-concepts.html) chapter.

The precedence specifies the order of calculation between different operators. The expression with higher precedence will be evaluated first. For example, when evaluating the expression `1+2*3`, the result of `2*3` will be calculated first. And then calculate the addition expression.

The associativity specifies the order of calculation of the operands on both sides of the operator. For example, the addition expression `expr1 + expr2` will first calculate the value of `expr1` and then the value of `expr2`, so the addition operator is left-associative.

### Arithmetic Operator

| OPERATOR |    FUNCTION    |   EXAMPLES    |
| :------: | :------------: | :-----------: |
|   `+`    | Unary positive |   `+ expr`    |
|   `-`    | Unary negative |   `- expr`    |
|   `+`    |      Add       | `expr + expr` |
|   `-`    |    Subtract    | `expr - expr` |
|   `*`    |    Multiply    | `expr * expr` |
|   `/`    |     Divide     | `expr / expr` |
|   `%`    |     Modulo     | `expr % expr` |

#### Description

For the add operator `+`, when the operand is two strings, the string concatenation is performed. All arithmetic operators except the `%` can support integer and real operands, and the operator `%` only supports integer types.

All arithmetic operators can be overloaded in classes.

The positive operator `+` doesn't actually generate any code, it's completely useless. It's not recommended to use.

#### Type Promotions

When the operand of an arithmetic operation (except for the `%`) is an integer and a real, the integer operand is converted to a real. In addition, Berry does not perform other implicit type conversions.

### Relational Operators

| OPERATOR |      FUNCTION      |    EXAMPLES    |
| :------: | :----------------: | :------------: |
|   `<`    |     Less than      | `expr < expr`  |
|   `<=`   | Less than or equal | `expr <= expr` |
|   `==`   |       Equal        | `expr == expr` |
|   `!=`   |     Not equal      | `expr != expr` |
|   `>=`   |  Greater or equal  | `expr >= expr` |
|   `>`    |    Greater than    | `expr > expr`  |

#### Description

Relational expressions are evaluated by comparing the size relationship of the operands. When the relationship is satisfied, the value of the expression is `true`, otherwise it is `false`. 

Relational operators allow the use of a combination of the following operands (the left and right order can be reversed):

* **integer** *relop* **integer**
* **integer** *relop* **real**
* **string** *relop* **string**

All relational operators can be overloaded in classes.

### Logical Operators

| OPERATOR |  FUNCTION   |    EXAMPLES    |
| :------: | :---------: | :------------: |
|   `&&`   | Logical AND | `expr && expr` |
|   `||`   | Logical OR  | `expr || expr` |
|   `!`    | Logical NOT |    `!expr`     |

#### Description

For logical AND operators, the result of a logical expression is `true` when both operand values are `true`, otherwise it's `false`.

For logical OR operators, the result of a logical expression is `false` when both operand values are `false`, otherwise it's `true`.

Logical operators require that the operands be a boolean type, otherwise the following conversion rules will be tried:

* Nil: Convert to `false`.
* Integer: Convert to `false` when the value is `0`, otherwise it's `true`.
* Real: Convert to `false` when the value is `0.0`, otherwise it's `true`.
* Instance: If the method `tobool()` is supplied, the return value of the method will be used, otherwise it's `true`.
* Other: Convert to `true`.

### Assignment operator

The assignment operator `=` only appears in an assignment expression, and its left operand must be a writable object. Assignment expressions do not return a value. You can't use an assignment operator in the middle of an expression like C, so you can only have at most one assignment in an expression.

### Field Operator and Index Operator

The field operator `.` is used to access the member field of the class object. E.g:

``` ruby
l = list()
l.append("item 0")
s = l.item(0)
```

The index operator `[]` is used to access an element of an object, for example

``` ruby
n = l[2]
```

This statement will return the element corresponding to index `2` in object `l`.