---
layout: default
---

# Basic Concepts

Berry源文件通常是扩展名为".be"的纯文本文件。

## Comments

Berry支持单行注释和块注释。单行注释以字符'`#`'开头，到换行符结束；多行注释以串'`#-`'开头，到'`-#`'结束。例如：

```
# this is a line comment
#- this is a
   block comment
-#
```

像C语言一样，多行注释不支持嵌套，例如下面的情况：

```
#- some comments -# ... -#
```

解析器将在第一个'`-#`'处终止注释的解析。

## Numerical Value

Berry支持的数值字面量有整数和浮点数两种：

``` ruby
40 # integer
3.14 # real
1.1e-6 # real
```

## Identifier

标识符是指那些以字母或下划线开头，然后跟随若干字母、数字或者下划线的单词。和大部分语言一样，Berry是大小写敏感的。

```
a
TestVariable
Test_Var
_init
baseClass
```

## Keywords

Berry保留以下token用作关键字：

```
if elif else while for def end
class break continue return
true false nil var do
```

## Statements

语句分为表达式语句，`if`语句，`while`语句，`for`语句，函数定义语句和类定义语句几种。

一条表达式语句可能是一次赋值运算或者函数调用。

```ruby
a = 1 # assignment statement
print(a) # call atatement
```

除了单行注释以外，换行符（`\r`, `\n`）只是被认为是一个空白字符，所以语句可以折行书写。

实际上多个语句置于一行也不会有什么问题，但是当出现一些情况时，原本的两个语句会被错误的解析为一条语句。

```ruby
a = 1 +
	func()   # wrap line
b = 1 c = 2 # multiple statements in the same line
a = c
(b) = 1 # be regarded as a function call
```

以下方法可以解决歧义：

* 赋值号左边不要使用括号，而是只是用简单表达式。
* 使用''`;`'符号显式地分隔语句。

## Block

块是若干语句的集合。块出现在控制语句、函数或方法体中。例如：

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
|  3   |           `-` `!`           | Negate, Not              | Right      |
|  4   |         `*` `/` `%`         | Multiply, Divide, Modulo | Left       |
|  5   |           `+` `-`           | Add, Subtract            | Left       |
|  6   | `<` `<=` `==` `!=` `>` `>=` | Relational Operator      | Left       |
|  7   |            `&&`             | Logical and              | Left       |
|  8   |           `\|\|`            | Logical or               | Left       |
|  9   |             `=`             | Assignment               | Right      |

# Syntax

## Type and Values

Berry支持的**类型**有：nil, integer, real, bool, string, closure, native function, class, instance, list和map几种。

**字面量**（literal）用于表达源代码中的固定值。字面量可能为整数、浮点数、boolean、string和boolean等类型。例如数字`3`就是一个整型字面量。

### nil

nil表示该对象的值为一个空值。使用关键字`nil`就可以表示一个nil值。

### Integer

整数类型是一个有符号整形量，其具体长度依赖实现。通常在32位环境下，整型为32位的有符号数。整型字面量为一串连续的数字如`123`等。

### Real

浮点类型的实现也根据实现来决定，通常会使用C语言的`double`类型来实现浮点，但是在某些时候为了省内存会使用`float`实现。

### Boolean

Boolean取值为`true`或`false`，它通常在逻辑运算时使用。

### String

字符串类型用于表示一串字符。Berry中可以使用一对单引号或者双引号引用一段字符来表示字符串，这两种字符串没有任何区别。

### Closure

Berry的函数通常表现为一个闭包，闭包是在运行时生成的对象。简单而言，你可以像在C语言中使用函数那样使用闭包。

### Native Function

原生函数即使用C语言实现的函数，实际上在实现上它依然是一种闭包。对于Berry代码和用户而言，Berry Closure和Native Function并无区别。

### Class and Instance
Berry通过class提供一些面向对象功能。Class可以由C-API创建或使用Berry脚本定义。Berry的class由若干方法和成员变量组成

#### Define a class

Class使用关键字`class`定义：

``` ruby
class TestClass
end
```

Class会存储在定义所在的作用域的变量表中，就像其他的类型一样。

#### Methods and Members

Class中的方法和一般的函数定义相似，在class block中使用关键字`def`来定义，而成员变量需要使用`var`关键字定义：
<div class="highlight"><pre class="highlight"><code><span class="k">class</span> <span class="nc">TestClass</span>
    <span class="k">var</span> <span class="n">a</span> <span class="c1"># 定义成员变量</span>
    <span class="k">def</span> <span class="nf">init</span><span class="p">()</span> <span class="c1"># 定义init方法</span>
        <span class="nb">self</span><span class="p">.</span><span class="nf">a</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="k">end</span>
    <span class="k">def</span> <span class="nf">method</span><span class="p">(</span><span class="n">a</span><span class="p">)</span> <span class="c1"># 定义method方法</span>
        <span class="k">return</span> <span class="n">a</span> <span class="o">*</span> <span class="mi">2</span>
    <span class="k">end</span>
<span class="k">end</span>
</code></pre></div>

#### Constructor and Instantiation

Berry通过调用类的名字来得到一个实例：

``` ruby
class TestClass
    ...
end
obj = TestClass() # 实例化一个类
```

实例化使用的参数数量取决于类的显式构造函数参数数量。Class的显式构造函数为`init`方法，你可以在class中定义该方法来自定义类的初始化行为。实例化时解释器会根据class的信息来生成一个instance对象。Berry虽然允许`init`方法具有返回值但不会在实例化时使用。

### List

List是一种可变长度的数组，List的构造方法有以下几种:

``` ruby
l1 = []           # 构造一个空list
l2 = list()       # 构造一个空list
l3 = [0, 1, 2, 3] # 构造并初始化list
```

使用空方括号对"`[]`"来构造一个空list和使用`list`类构造空list完全一样，前者不过是后者的一个语法糖。

在list末尾追加一个对象可使用`append()`方法来实现：

``` ruby
l.append(value)
```

读取或者写入list存储的某个对象的方法：

``` ruby
value = l[index]        # 通过下标运算读取
value = l.item(index)   # 通过item()方法读取
l[index] = value        # 通过下标运算写入
l.setitem(index, value) # 通过setitem()方法写入
```

### Map

