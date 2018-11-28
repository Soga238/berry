---
layout: default
---

# Functions and Closures

Berry中的函数是一个命名了的代码块，我们通过调用函数来执行函数中的代码。函数可以接受0到多个参数并总是返回一个结果。另外，Berry不允许函数调用出现在定义之前。

## Functions

### Functions definition

例如我们要编写一个函数来计算阶乘，n的阶乘为从1到n所有数字的乘积，这样我们可以编写下面的函数：

``` ruby
def fact(a)
    ret = 1
    while (a > 1)
        ret = ret * a
        a = a - 1
    end
    return ret
end
```

使用关键字`def`来定义函数，上面代码中的`fact`就是函数的名字。函数名实际上表示存储函数的变量。因此，如果作用域中有同名的变量，定义函数会覆盖原先变量的值，同理对存储函数的变量赋值也会造成相反的结果。

### Functions call

当函数定义之后就可以调用了，函数调用时需要为函数提供必要的参数，而函数返回值也可以在表达式中使用。例如我们使用`fact()`函数来求5的阶乘并打印：

``` ruby
v = fact(5) # assign 5! to v
print(v)    # 120
```

函数调用需要为函数提供正确的参数，无论是参数的数量还是参数类型。被调用函数的参数初始化完成后解释器将开始执行被调函数的代码。

函数执行到一条`return`语句时会将返回值复制到合适的位置，之后解释器会返回主调函数并继续执行，函数调用完成。

### Return statement

`return`语句用于终止正在执行的函数并将一个值返回给主调函数。`return`语句有两种写法：

``` ruby
return
return expression
```

注意，第一种写法中函数还是会返回一个`nil`值到主调函数中，效果与使用`return nil`相同（尽管生成的中间代码并不相同）。

如果函数的最后一条代码不是`return`语句，解释器将会在此处隐式地添加一个返回`nil`的`return`语句。这样做是为了保证函数一定能返回。

## Closures

闭包指能够读取其他函数内部变量的函数。Berry允许将一个函数定义在另一个函数内，因此也支持闭包。闭包的一个简单例子如下：

``` ruby
def func(a)
    def clos()
        return a
    end
    return clos;
end
```

这个例子中的`func`函数中定义了一个函数`clos`。`clos`的返回值是函数`func`的局部变量`a`，因此函数`clos`是一个闭包。最后`func`返回了函数`clos`，故可以通过调用`func`的返回值来间接地调用`clos`：

``` ruby
f = func(5)
v = f()     # 5
```

变量`v`的值最终等于`5`，这说明闭包`clos`正确地返回了`func`的局部变量`a`。为了保证闭包能够访问外层函数的局部变量，解释器需要在外层函数返回之前把闭包会访问的变量用单独的环境保存。这个环境仅对该外层函数中的闭包可见，就像该函数的局部变量一样。

利用闭包可以实现一个计数器：

``` ruby
def counter()
    cnt = -1
    def clos()
        cnt = cnt + 1
        return cnt
    end
    return clos
end
```

函数`counter`返回一个用于计数的闭包。每次调用这个闭包后得到的的返回值都会比上一次调用的返回值大1（第一次调用的返回值为0）：

``` ruby
c = counter()
print(c())      # 0
print(c())      # 1
print(c())      # 2
```

## Native Functions and Native Closures
