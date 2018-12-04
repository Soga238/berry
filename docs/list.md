---
layout: default
---

# List

## Basis

List is a variable-length array. The construction methods of List are as follows

``` ruby
l1 = []           # structure a empty list with '[]'
l2 = list()       # structure a empty list with class list
l3 = [0, 1, 2, 3] # structure and initialize list
```

Using empty square brackets for "`[]`" to construct an empty list is exactly the same as constructing an empty list with a class. The former is just a syntactic sugar for the latter.

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

## Method and operation

* `append(value)`
    * Append an element `value` to the end of the list.
* `item(index)`
    * Get the element whose index is `index`, the `index` must be an integer.
* `setitem(index, value)`
    * Assign `value` to an element with index `index`, the `index` must be an integer.
* `size()`
    * Get the number of list elements.
* `resize(count)`
    * Set the capacity of the list to `count`, and the `count` must be an integer. If the new capacity is larger than the old one, the extension will be filled with `nil`, otherwise the tail elements will be discarded.
* `iter()`
    * Return a list iterator.
* `tostring()`
    * Convert list content to a string.
