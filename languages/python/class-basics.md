# Class Basics

## Declaration

Classes, like most other OOP languages, simply requires the `class` keyword, followed by the name of the class. 

```python
class MyClass:
```

> [!NOTE]
> 
> The [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html#316-naming) dictates that classes should be in CamelCase, unlike most other naming conventions in Python which use snake_case.

## Constructors

In Python, constructors take the form of an `init` statement, and are declared inside the class. The first parameter is always `self`, as it passes a reference for the instance it creates.

```python
def __init__(self):
```

Parameters for the constructor are declared after the reference to the instance created. Instance variables created must be associated with the instance by setting each one to a reference to `self`:

```python
def __init__(self, foo, bar):
    self.foo = foo
    self.bar = bar
```

## Methods

These are declared in the same way as outside of a class, but must always pass `self` as the first parameter to give context.

```python
def foo(self):
```

These can be called either via the class, or in reference to an instance.

```python
MyClass.foo(my_instance) # Via the class

my_instance.foo() # Via the instance
```

## Class Variables

These should be the same for every instance that is created, and are declared at the top of a class.

```python
class MyClass:
    foo = 1
```

This can be changed dynamically, but can have unexpected effects if used incorrectly. If setting the class variable with a reference to the class instead of the instance, it will change for all instances.

```python
MyClass.foo = 2 # All previously created and future instance are now 2
```

However, if the class variable is set with a reference to a specific instance, only that instance is affected, **even if the class variable is then changed again** by referencing the class itself.

```python
a = MyClass()
b = MyClass()

a.foo = 2
MyClass.foo = 5

print(a.foo) # 2
print(b.foo) # 5
```

Python handles this by taking the class variable, assigning it to an instance variable, and then referring to that if the class variable is called. This is why the value remains the same even if the class variable is altered afterward.

> [!NOTE]
> 
> This can be avoided if needed by defining properties with setters and getters, but that is out of scope here.

> [!NOTE]
> 
> When referencing class variables from an instance, Python will also check any inherited classes up to the base class for a matching variable name. 

## Inheritance

### Method Resolution Order

Declare a class to inherit another by using the base class as a parameter for the new one.

```python
class Subclass(MyClass):
```

Python searches a subclass for attributes and methods, then proceeds to its superclass.

### Constructor

To extend the `__init__` method in the subclass, the predefined parameters do not need to be written out again inside the method. Instead, any arguments passed as a reference to the parameters of the superclass can be handled with `super()`.

```python
def __init__(self, foo, bar, new_var):
    super().__init__(foo, bar)
    self.new_var = new_var
```

### Useful Inheritance Methods

Call `isinstance` to check if an object is an instance of a class.

Call `issubclass` to check for a subclass of a superclass.


