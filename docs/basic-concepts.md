---
layout: default
---

# Basic Concepts

Berry source files are usually plain text files with the extension ".be".

## Comments

Berry supports line comments and block comments. Line comments begin with the character '#' and end with a newline. block comments begin with the string '-#' and end with '-#'. E.g.

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

## Numerical Value

The numeric literals supported by Berry both integer and floating point numbers

``` ruby
40     # integer
3.14   # real
1.1e-6 # real
```

## Identifier

Identifiers are words that begin with a letter or underscore followed by a number of letters, numbers, or underscores. Like most languages, Berry is case sensitive.

```
a
TestVariable
Test_Var
_init
baseClass
```

## Keywords

Berry reserves the following tokens as keywords.

```
if elif else while for def end
class break continue return
true false nil var do
```

## Statements

Statements are divided into expression statements, ifstatements, whilestatements, forstatements, function definition statements, and class definition statements.

An expression statement may be an assignment operation or a function call.

```ruby
a = 1    # assignment statement
print(a) # call atatement
```

Expect single-line comments, the newline character ('`\r`', '`\n`') is only considered a blank character, so the statement can be written in a wrap.
实际上多个语句置于一行也不会有什么问题，但是当出现一些情况时，原本的两个语句会被错误的解析为一条语句。

```ruby
a = 1 +
	func()  # wrap line
b = 1 c = 2 # multiple statements in the same line
a = c
(b) = 1     # be regarded as a function call
```

The following methods can solve the ambiguity:

Do not use parentheses to the left of the assignment number, but simply use a simple expression.
Use the ' ;' symbol to explicitly separate statements.

## Block

A block is a collection of statements. A block appears in a control statement, function, or method body. E.g.

```ruby
if (isOpen)
    close()
end
```

## Operator

| PREC |          OPERATOR           | DESCRIPTION              | ASSOCIATES |
| :--: | :-------------------------: | ------------------------ | ---------- |
|  1   |            `()`             | Brackets                 | -          |
|  2   |        `()` `[]` `.`        | Call, Index, Field       | Left       |
|  3   |           `-` `!`           | Negate, Not              | Left      |
|  4   |         `*` `/` `%`         | Multiply, Divide, Modulo | Left       |
|  5   |           `+` `-`           | Add, Subtract            | Left       |
|  6   | `<` `<=` `==` `!=` `>` `>=` | Relational Operator      | Left       |
|  7   |            `&&`             | Logical and              | Left       |
|  8   |           `\|\|`            | Logical or               | Left       |
|  9   |             `=`             | Assignment               | Right      |

# Syntax

## Type and Values

Berry supports the following **types** : nil, integer, real, bool, string, closure, native function, class, instance, list, and map.

**Literal**, value that is fixed by its coding within the program using it. Literals may be integers, floats, booleans, strings and booleans. For example, a number `34` is an integer literal.

### nil

Nil indicates that the value of the object is a null value. A keyword nilcan be used to represent a nil value.

### Integer

An integer type is a signed integer whose specific length depends on the implementation. Usually in a 32-bit environment, the integer is a 32-bit signed number. The integer literal is a series of consecutive numbers such `123` as.

### Real

The implementation of floating-point types is also determined by implementation. Usually, the C language `double` type is used to implement floating point, but in some cases the `float` implementation is used to save memory.

### Boolean

Boolean takes the value `true` or `false`, which is usually used in logical operations.

### String

A string type is used to represent a string of characters. Berry can use a pair of single or double quotes to refer to a character to represent a string. There is no difference between the two strings.

### Closure

Berry's functions usually appear as a closure, and closures are objects that are generated at runtime. In simple terms, you can use closures like functions in C.

### Native Function

The native function is a function implemented in C language, and it is actually a closure in its implementation. For Berry code and users, Berry Closure is no different from Native Function.

### Class and Instance

Berry provides some object-oriented functionality through classes. Class can be created by C-API or defined using a Berry script. Berry's class consists of several methods and member variables.

#### Define a class

Uses keyword `class` definitions class.

``` ruby
class TestClass
end
```

Class is stored in the variable table of the scope in which it is defined, just like any other type.

#### Methods and Members

The methods in Class are similar to the general function `def` initions, which defare defined using keywords in the class block , and the member variables need to be defined using `var` keywords

<div class="highlight"><pre class="highlight"><code><span class="k">class</span> <span class="nc">TestClass</span>
    <span class="k">var</span> <span class="n">a</span> <span class="c1"># define member variable</span>
    <span class="k">def</span> <span class="nf">init</span><span class="p">()</span> <span class="c1"># 定义init方法</span>
        <span class="nb">self</span><span class="p">.</span><span class="nf">a</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="k">end</span>
    <span class="k">def</span> <span class="nf">method</span><span class="p">(</span><span class="n">a</span><span class="p">)</span> <span class="c1"># define method</span>
        <span class="k">return</span> <span class="n">a</span> <span class="o">*</span> <span class="mi">2</span>
    <span class="k">end</span>
<span class="k">end</span>
</code></pre></div>

#### Constructor and Instantiation

Berry gets an instance by calling the name of the class.

``` ruby
class TestClass
    ...
end
obj = TestClass() # instantiation a class
```

The number of parameters used for instantiation depends on the number of explicit constructor arguments of the class. The explicit constructor of Class is a `init` method, you can define the initialization behavior of the class in the class. When instantiated, the interpreter will generate an instance object based on the class information. Berry allows initmethods to have a return value but will not be used when instantiating.

### List

List is a variable-length array. The construction methods of List are as follows

``` ruby
l1 = []           # structure a empty list with '[]'
l2 = list()       # structure a empty list with list class
l3 = [0, 1, 2, 3] # structure and initialize list
```
Using empty square brackets for "`[]`" to construct an listempty list is exactly the same as constructing an empty list with a class. The former is just a syntactic sugar for the latter.

Appending an object to the end of the list can be done using `append()` method

``` ruby
l.append(value)
```

The method of reading or writing to an object stored in the list

``` ruby
value = l[index]        # read by index operation
value = l.item(index)   # read by item() method
l[index] = value        # write by index operation
l.setitem(index, value) # write by setitem() method
```

### Map

