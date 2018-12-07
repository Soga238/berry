---
layout: default
---

# Base Library

## Functions

### `print()`

**Description**

Print out the input arguments.

The `print()` function accepts any type, any number of arguments. All types of data can be printed out. However, the instance type is special. If the instance provides the `tostring()` method, the return value of the method will be printed.

**Usage**

``` ruby
print(...)
```

**Examples**

``` ruby
print('Hello World!') # Hello World!
print([1, 2, '3'])    # [1, 2, '3']
print(print)          # <function: 0x561092293780>
```

---

### `type()`

**Description**

Get the type of the argument. The return value is a string describing the type of the argument.

**Usage**

``` ruby
type(value)
```

* *value*: The value of the type to be tested.
* *return value*: A string describing the type.

**Examples**

``` ruby
type(0)         # int
type(0.5)       # real
type('hello')   # string
type(print)     # function
```

---


