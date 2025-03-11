# Object Basics

## Prototypes

All objects have a *prototype*, another object that the original inherits from.

The base object is always the default JS `object`.

### Functions

Declaring fuctions on the prototype of an object saves memory as a single instance of each function is **shared** between all objects instantiated. (instead of a new function instance for each object instance).

```js
// Instantiate for each new object
function obj() {
    this.func = function() {
        console.log('foo');
    }
}

// Instantiate once for all objects created
function obj(bar) {
    this.foo = bar;
}

obj.prototype.foobar = (foo) => { console.log(foo) }
```

### Properties

All objects have properties, and can be created like so:

```js
// Assign prototype property

obj.prototype.newFunction = function() { ... }
```

Inherited properties come from the **prototype chain**. When an object property is referenced, JS searches the referenced prototype for that property. If it is not found, the next inherited class is searched. This continues until the JS base class is reached, `Object`.

Any object's prototype chain can be accessed with `obj.prototype`.

### Instantiation

Use `Object.create(prototype)` to set the prototype of an object, as opposed to the new keyword. This function has a return value of a new object with the specified superclass.

> [!IMPORTANT]
> 
> The use of the `new` keyword can result in any alterations to the created object may reference the global object instead of the new instance, altering any future objects created from the same prototype. However, ES6 strict mode  does not allow the `this` keyword to equal `globalThis` in a function call. Additionally, classes cannot be used without `new` at all. This is covered more in later notes.

## The **this** keyword

The `this` keyword is very complex and can mean any number of things given the context. 

### Outside of any function scope

`this` is set to the global object. *(the window in a browser, for example)*

```js
console.log(this); // browser window
```

### Inside a function invocation, outside of an object

`this` is set as the global object.

```js
function f() { console.log (this) } // browser window
```

### Inside an embedded function

`this` is set as the global object, unless strict mode is on, in which case it becomes `undefined`.

```js
function f() { function() { console.log(this) } } // browser window || undefined
```

### Inside a function property

`this` is set as the parent object. **However**, an embedded function does not set `this` as the parent object as it is not a method invocation.

```js
const obj = {
    sum: function() {
        console.log(this === obj); // true
        function calculate() {
            return this === obj; // false
        }
    }
    return calculate();
}
```

If an arrow function is used, the embedded function is a method invocation, so `this` is the parent object.

```js
const obj = {
    sum: function() {
        console.log(this === obj); // true
        function calculate() this === obj; // true
    }
    return calculate();
}
```

> [!NOTE]
> 
> `'use strict'` affects all inner scopes, so if the file is under these rules, the embedded function would return `undefined` as above due to the reference being out of scope.

### Bind a function to prevent undefined behaviour

To avoid the above where references are undefined, use the `bind` object method to associate the function with the object.

```js
const boundFunction = myObj.functionToBind.bind(myObj);
```

Or, more simply, use an arrow function inside the object for the same effect.

```js
// Inside the object
this.functionToBind = () => console.log(this === myObj); // true 
```

> [!WARNING]
> 
> Arrow functions bind content lexically, and permanently. If the `bind` method was used on an arrow function after it had been defined, there would be no effect and the `this` keyword would reference whatever the original context was after the arrow function was declared.
> 
> If this is not desired, the `function` keyword can be used instead.
