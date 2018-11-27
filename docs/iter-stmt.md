---
layout: default
---

# Iteration Statements

迭代语句即循环语句，用于执行某些操作直到满足条件才停下来。

## while statement

**`while`语句**的一般形式为

``` ruby
while (condition)
    block
end
```

`while`语句会检测*condition*的结果，如果为`true`就会反复执行*block*，否则会离开该`while`语句。如果*condition*一开始值就是`false`将不会执行*block*。

## for statement

Berry的`for`语句用于遍历容器，这与C语言中的`for`语句有些不同。`for`语句的一般写法为

``` ruby
for (varaible : expression)
    block
end
```

*expression*表达式的值必须是一个可迭代的容器，例如`range`类。`for`语句将会从该容器中得到一个迭代器，通过使用迭代器可以每次返回容器的一个成员。

*varaible*定义了一个变量，该变量的作用域只在`for`语句内。每一次循环都会从迭代器中取出容器的一个值，然后把这个值赋值给*varaible*。

每次循环都会检查迭代器是否还有可以返回的元素，以便在所有元素处理完毕后终止循环。

下面给出一个使用`for`循环的例子。这个例子使用`for`循环来取出`range`类的所有成员并打印。然后，我们还示范了迭代变量`i`的作用域，

``` ruby
i = "Hi, I'm fine." # 外层变量
for (i : 0 .. 2)
    print(i) # 循环控制变量
end
print(i)
```
这个例子中迭代变量`i`不会改变外层变量`i`的值。上例的运行结果为

```
0
1
2
Hi, I'm fine.
```

### `for`语句的实现原理

`for`语句的实现比`while`语句要复杂，而用户很可能会有实现可迭代容器的需求，因此了解`for`语句的实现会很有必要。

前面例子中的`for`语句可以近似地等效为下面的语句：

``` ruby
do
    it = __iterator__(0..2)
    while (__hasnext__(it))
        i = __next__(it)
        print(i)
    end
end
```

上述代码中的变量`i`就是迭代变量，而`it`是一个用于保存迭代器的中间变量。用户代码无法显式地访问变量`it`。

`__iterator__()`函数会调用输入参数的`iter()`方法，因此，要对容器使用`for`迭代首先要提供`iter()`方法，该方法返回容器的一个迭代器实例。

`__hasnext__()`函数的参数为迭代器，它会调用迭代器的`hashnext()`方法，该方法的返回为一个`bool`值。`hashnext()`方法返回`true`表示容器中还有元素可用于迭代，否则表示所有容器都已经访问。

`__next__()`函数调用迭代器的`next()`方法，该方法返回待访问的下一个元素。

因此，实现自己的可迭代容器需要实现`iter()`方法，并且该方法返回的迭代器实例需要实现`hasnext()`方法和`next()`方法。
