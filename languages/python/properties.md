# Properties

Hold information in an safe encapsulated data structure with properties, which also come along with getters setters, etc, just like in other languages.

## Practical Example

If a class variable is set as a combination of two other variables passed at instantiation, but the user needs to change this variable later on. This simplifies the process, and they do not need to create a method and change every class variable call to a method call.

## Declaration

### Getters

```python
@property
def foo(self):
    return foo + bar
```

### Setter

```python
@foo.setter
def foo(self, foobar):
    self.foo = foobar
```

### Deleter

```python
@foo.deleter
def foo(self)
    def foobar = None
```
