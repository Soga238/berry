---
layout: default
---

# List

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
