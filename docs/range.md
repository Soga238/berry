---
layout: default
---

# Range

## Basis

The range class represents an integer interval. Range instances can be constructed using the operator`..` or the range class.

``` ruby
r1 = 0..3
r2 = range(0, 3)
```

## Method and operation

* `lower()`
    * Return interval lower limit.
* `upper()`
    * Return interval upper limit.
* `setrange(lower, upper)`
    * Set a new range.
* `iter()`
    * Return a range iterator.
* `tostring()`
    * Convert range to a string.
