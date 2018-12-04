---
layout: default
---

# Map

## Basis

Map is a container for storing key-value pairs. Maps can be constructed using a pair of curly braces or by calling the class `map`.

``` ruby
m1 = {}             # structure a empty map with '{}'
m2 = map()          # structure a empty list with class map
m3 = {0: 1, "v": 4} # structure and initialize map
```

Map uses the method `insert` to insert a new key-value pair, and the method `remove` to delete an existing key-value pair.

``` ruby
m = {}
m.insert{0, 1}  # map: {0: 1}. insert a new key-value pair.
m.remove{0}     # map: {}. remove a key-value pair.
```

Map uses the `item` method to read an existing key-value pair, and sets the value of an existing key-value pair via `setitem`. These operations can also use index operator `[]`.

``` ruby
m = {'key': 0, 1: 'value'}
m.item('key')               # read by item() method
m[1]                        # read by index operation
m.setitem(1, 0)             # write by setitem() method
m['key'] = 'test'           # write by index operation
```

## Method and operation

* `insert(key, value)`
    * Insert a key-value pair into the map. Update the old value if the key already exists.
* `remove(key)`
    * Delete an existing key-value pair with a key of `key`.
* `item(key)`
    * Returns the value corresponding to the key `key`.
* `setitem(key, value)`
    * Set the value of the key `key` to `value`, the key must exist.
* `size()`
    * Get the number of map key-value pairs.
* `iter()`
    * Return a map iterator.
* `tostring()`
    * Convert map content to a string.
