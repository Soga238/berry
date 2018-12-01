---
layout: default
---

# Basic Concepts

## Syntax

Berry source files are usually plain text files with the extension ".be".

### Comments

Berry supports line comments and block comments. Line comments begin with the character '`#`' and end with a newline. block comments begin with the string '`-#`' and end with '`-#`'. E.g.

```
# this is a line comment
#- this is a
   block comment
-#
```

Like the C language, block comments do not support nesting, such as the following

```
#- some comments -# ... -#
```

The parser will terminate the parsing of the block comment at the first '-#'.

### Literal

**Literal**, value that is fixed by its coding within the program using it. Literals may be integers, floats, booleans, strings and nil. For example, a number `34` is an integer literal.

#### Numerical Literal

The numeric literals supported by Berry both **integer** and **real** (floating point number).

``` ruby
40     # integer
0x80   # hexadecimal literal
3.14   # real
1.1e-6 # real
```
#### Boolean

Use keywords `true` or `false` to represent Boolean literals.

#### String

String literals are a paragraph of text enclosed in a pair of `"` or `'`.

``` ruby
'this is a string'
"this is a string"
```

#### Nil

A keyword `nil` can be used to represent a nil literals.

### Identifier

Identifiers are words that begin with a letter or underline followed by a number of letters, numbers or underline. Like most languages, Berry is case sensitive.

```
a
TestVariable
Test_Var
_init
baseClass
```

### Keywords

Berry reserves the following tokens as keywords.

```
if elif else while for def end
class break continue return
true false nil var do
```

### Operator

| PREC |          OPERATOR           | DESCRIPTION              | ASSOCIATES |
| :--: | :-------------------------: | ------------------------ | :--------: |
|  1   |            `()`             | Group                    |     -      |
|  2   |        `()` `[]` `.`        | Call, Index, Field       |    Left    |
|  3   |         `+` `-` `!`         | Positive, Negative, NOT  |    Left    |
|  4   |         `*` `/` `%`         | Multiply, Divide, Modulo |    Left    |
|  5   |           `+` `-`           | Add, Subtract            |    Left    |
|  6   |            `..`             | Range                    |    Left    |
|  7   | `<` `<=` `==` `!=` `>` `>=` | Relational Operator      |    Left    |
|  8   |            `&&`             | Logical AND              |    Left    |
|  9   |            `||`             | Logical OR               |    Left    |
|  10  |             `=`             | Assignment               |   Right    |

### Expression

An **expression** is a combination of one or more operands and operators that evaluates to produce a result. The operand can be a literal, variable, function-call or subexpression.

Similar to the four arithmetic operations, the precedence of operators affects the order in which expressions are evaluated.

This is an example of some expressions:

``` ruby
a = 1 + 5       # 6
print(a * 2)    # 12
b = type(a)     # 'int'
```

### Statements

Statements are divided into expression statements, `if` statements, `while` statements, `for` statements, function definition statements and class definition statements.

An expression statement may be an assignment operation or a function call.

``` ruby
a = 1    # assignment statement
print(a) # call atatement
```

Except line comments, the newline character ('`\r`', '`\n`') is only considered a blank character, so the statement can be written in a wrap. Berry allows multiple statements to be written on the same line. Sometimes, however, code that should have been two statements misinterprets into one statement.

``` ruby
a = 1 +
    func()  # wrap line
b = 1 c = 2 # multiple statements in the same line
a = c
(b) = 1     # be regarded as a function call
```

The following methods can solve the ambiguity:

* Do not use parentheses to the left of the assignment number, but simply use a simple 
expression.

* Use the '`;`' symbol to explicitly separate statements.

### Block

A block is a collection of statements. A block appears in a control statement, function, or method body. E.g.

``` ruby
if (isOpen)
    close()
end
```

## Type and Values

Data **type** is an attribute of data which tells Berry how to use the data. Data type defines the operations that can be done on the data and the meaning of the data. A type of value from which an expression may take its value.

### Built in type

The basic types supported by berry are:

* **Nil**. Nil indicates that the value of the object is a null value.
* **Integer**. Signed integer. It's length depends on the implementation. Usually in a 32bit platform, the integer is a 32bit signed number.
* **Real**. The implementation of floating-point types is also determined by implementation. Usually, the C language `double` type is used to implement floating point, but in some cases the `float` implementation is used to save memory.
* **Boolean**. Can be `true` or `false`, which is usually used in logical operations.
* **String**. Store a string of characters.
* **Function**. A named piece of code, used to implement some functions. The type *function* contains these subtypes: Berry-Closure, Native-Function and Native Closure.
* **Class**. Encapsulation of methods and membership sets. Used to support Object-Oriented Programming.
* **Instance**. Specific objects generated by class instantiation.
* **List**. Variable array. Any type can be stored.
* **Map**. Storage key value pairs. Values can make any type.
* **Range**. Represents an integer range, mainly used for range iteration.
