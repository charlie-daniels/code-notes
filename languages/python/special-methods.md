# Special Methods

## What are they?

It is more easily explained with practical examples, but the idea is that they are methods  in which their behaviour varies depending on the argument. An example of this is the `print` function.

```python
print('a'+'b') # Prints 'ab'
print(1+2)     # Prints '3'
```

What Python is really reading behind the scenes explains this behaviour better:

```python
print(str.__add__('a', 'b'))
print(str.__add__(1, 2))
```

These methods with double underscores either side of them are referred to as 'dunder' methods. `__init__` is another example.

## Examples

### Unambiguous representation of the object

This is used for such things as debugging. `repr` *represents* the object.

```python
def __repr__(self):
    return f"MyClass({self.foo}, {self.bar})"
```

### Readable representation of the object

This is used for such things as displaying to an end user. `str` *stringifies* variables clearly for the user.

```python
def __str__(self):
    return f"{self.foo} - {self.bar}"
```

### Addition of objects

If you need a class that has the ability to sum objects, the `__add__` dunder method can be used.

```python
def __add__(self, other):
    return self.foo + other.bar
```

### Further use

There are many other dunder methods that can be found in the [Python docs](https://docs.python.org/3/reference/datamodel.html#special-method-names).

## Calling special methods

```python
repr(MyClass)
str(MyClass)
```

If the object itself is passed to the `print` function, it will return a call of `__str__`, unless it is not defined in which case it will return a call of `__repr__`. If both are omitted, it will print the location of the object in memory.

## 
