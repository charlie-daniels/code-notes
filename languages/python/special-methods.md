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

# 
