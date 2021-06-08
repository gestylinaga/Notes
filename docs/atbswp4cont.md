# Lists (cont.)

[see Chapter 4: Lists - part 1](atbswp4.md)

## Sequence Data Types

Lists aren't the only data type that represent an ordered **sequence of values**.
Strings can be considered a "list" too, in that it's a *list* of single characters.

Python Sequence Data Types include:
* lists
* strings
* range objects returned by `range()`
* tuples

This means that things you can do to lists can be done to other values of sequence types:
* indexing
* slicing
* with `for` loops
* with `len()` 
* with `in` and `not in`

```python
name = 'Zophie'
```
* `name[0]` returns `'Z'`
* `name[0:4]` returns `'Zoph'`
* `'Zo' in name` returns `True`
* `'z' in name` returns `False`

and:
```python
for i in name:
    print('***' + i + '***')
```
will return:
```
* * * Z * * *
* * * o * * *
* * * p * * *
* * * h * * *
* * * i * * *
* * * e * * *
```

### Mutable and Immutable Data Types

### The Tuple Data Type

### Converting Types with the list() and tuple() Functions


## References


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
