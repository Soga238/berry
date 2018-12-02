---
layout: default
---

# Iteration Statements

An iterative statement is also a loop statement that is used to repeat some operations until the condition is met.

## while statement

The general form of the **`while` statement** is

``` ruby
while (condition)
    block
end
```

The `while` statement will test the result of *condition*. If it is true, it will execute *block* again, otherwise it will leave the `while` statement. If *condition* initial value is `false`, *block* will not be executed.

## for statement

Berry's `for` statement is used to traverse the container, which is somewhat different from the C. The general form of the **`for` statement** is

``` ruby
for (varaible : expression)
    block
end
```

The value of *expression* must be an iterable container, such as the class `range`. The `for` statement will get an iterator from the container, which can return a element of the container each time by using an iterator.

The *varaible* defines a variable whose scope is only in the `for` statement. Each loop gets an element of the container from the iterator and assigns it to *varaible*.

Each iteration will check if there are any elements in the container that are not accessed by the iterator. When all the elements have been processed, the loop will be terminated.

Here is an example of using the `for` statement. This example uses the `for` statement to fetch all elements of a `range` instance and print them. In addition, we demonstrate the scope of the iteration variable `i`.

``` ruby
i = "Hi, I'm fine." # outer variable
for (i : 0 .. 2)
    print(i)        # iteration variable
end
print(i)
```

The iteration variable `i` in this example does not change the value of the outer variable `i`. The result of the above example is

```
0
1
2
Hi, I'm fine.
```

### Implementation of `for` statement

The implementation of the `for` statement is more complicated than the `while` statement, and there are often requirements to implement iterable containers, so understanding the implementation of the `for` statement is necessary.

The `for` statement in the above example can be approximated to the following statement:

``` ruby
do
    it = __iterator__(0..2)
    while (__hasnext__(it))
        i = __next__(it)
        print(i)
    end
end
```

The variable `i` is the iteration variable, and the intermediate variable `it` is the iterator. User code cannot explicitly access the variable `it`.

The function `__iterator__()` calls the method `iter()` of the argument, so using the `for` iteration requires implementing the method `iter()` for the container, which returns an iterator instance of the container.

The argument to the function `__hasnext__()` is an iterator that calls the iterator's method `hashnext()`, which returns a boolean value. The method `hashnext()` returns true to indicate that there are still elements in the container that can be used for iteration, otherwise it means that all elements have been accessed.

The argument to function `__next__()` is also an iterator that calls the iterator's method `next()`, which returns the next element to be accessed.

Therefore, implementing your own iterable container requires implementing the method `iter()`, and the iterator instance returned by the method needs to implement the method `hasnext()` and the method `next()`.
