---
layout: default
---

# Functions and Closures

The Berry function is a named code block that executes the code through a function call. A function can accept 0 to more arguments and always return a result. In addition, Berry does not allow functions to be called before they are defined.

## Functions

### Functions definition

The function is defined using the keyword `def`, which is defined as

``` ruby
def function_name(arguments)
    block
end
```

The *function_name* is the name of this function. The *arguments* is a list of formal parameters for this function. Functions can be used without parameters or multiple parameters. The *block* is a code block that implements this function. The function can be an empty function, ie there is no statement in *block*.

For example, we have to write a function to calculate the factorial, and the factorial of n means the product of all numbers from 1 to n, so we can write the following function:

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

The `fact` here is the name of the function. The function name is actually the variable name of the stored function.
Therefore, if there is a variable with the same name in the scope, the definition function will overwrite the old value of the variable. Similarly, assigning a value to the variable of the stored function will also have the opposite result.

### Functions call

When the function is defined, it can be called. The function call needs to provide the necessary parameters for the function, and the function return value can also be used in the expression. For example, we use the `fact()` function to find the factorial of 5 and print it

``` ruby
v = fact(5) # assign 5! to v
print(v)    # 120
```

Function calls need to provide the correct parameters for the function, both in number and type. After the parameters of the called function are initialized, the interpreter will start executing the code of the called function.

When the function executes a `return` statement, it will copy the return value to the appropriate location. After that, the interpreter will return the calling function and continue execution, and the function call is completed.

### Return statement

The `return` statement is used to terminate the function being executed and return a value to the calling function. The `return` statement has two ways of writing

``` ruby
return
return expression
```

Note that in the first way, the function will still return a `nil` value, the effect is the same as using `return nil` (although the generated intermediate code is somewhat different).

If the last code of the function is not a `return` statement, the interpreter will add an implicit `return` statement that returns `nil` here. This is done to ensure that the function will return.

## Closures

A closure is a function that can access local variables of outer functions. The local variables of the outer functions used by the closure is called the free variables of the closure.

Berry allows a function to be defined in another function, so it also supports closures. Strictly, all Berry functions are implemented as a closure, but closures without free variables are usually called functions.

A closures (including a function) an instance constructed by the prototype at runtime. This section mainly describes the closure features with free variables. A simple example of a closure is

``` ruby
def func(a)
    def clos()
        return a
    end
    return clos;
end
```

A function `clos` is defined in the function `func`. The return value of `clos` is the local variable `a` of the function `func`, so the function `clos` is a closure. Finally the `func` returns the function `clos`, so you can call the `clos` indirectly by calling the return value of the `func`:

``` ruby
f = func(5)
v = f()     # 5
```

The value of the variable `v` is finally `5`, which means that the closure `clos` correctly returns the local variable `a` of the `func`. In order to ensure that the closure can access the free variables, the interpreter needs to save the variables that the closure will access in a separate environment before the outer function returns. This environment is only visible to closures in the outer function, just like the local variables of the outer function.

A counter can be implemented with a closure:

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

The function `counter` returns a closure for counting. The return value of each call to this closure will be one greater than the return value of the previous call (the return value of the first call is 0):

``` ruby
c = counter()
print(c())      # 0
print(c())      # 1
print(c())      # 2
```

## Native Functions

A native function is a function implemented in C, which can be used like a Berry function. Native functions are different from closures, they have no free variables. Native functions are used to extend the functionality of the Berry VM (virtual machine). For example, the native function `print` implements the printing function for berry, and the IO operation cannot be directly implemented by Berry code.

The implementation of native functions requires the use of Berry's C-API. Please refer to the chapter [API Reference](./api-reference.html) for details.

## Native Closures

Native closures are different from native functions in that they support free variables. However, native closures must be constructed by a native function or a native closure at the time of the call, and the free variables of the native closure must be initialized by them. This means that the Berry code cannot be used to initialize the free variables of the native closure.

Native closures are also used to extend Berry. For Berry code, it is very similar to native functions because you can't initialize free variables for native closures in Berry code.

The implementation of native closures requires the use of Berry's C-API too. Please refer to the chapter [API Reference](./api-reference.html) for details.
