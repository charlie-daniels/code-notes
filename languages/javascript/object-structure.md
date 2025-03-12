# Object Structure

## The problem with constructors

They can easily cause bugs in your code. They *look* like regular functions, but don't *behave* like regular functions. Using constructor functions without the `new` keyword will not work.

### The solution: Factory Functions

These will return the object after instantiation, allowing constructors to look and behave in a more managable way.

```js
const myObj = (str) => {
    const func = () => console.log(str);
    return { str };
}
```

The constructor can then be called in a more classical way:

```js
const myInstance = myObj("I'm an object")

// myInstance is an object with property str: "I'm an object"
```

> [!NOTE]
> 
> Object shorthand can be used like above, where the variable passed has the same name as the property being created. This shortens `{ str: str }` to `{ str }`.

## A quick summary of object scope terminology

### Global

Outermost scope, the same as a browser window.

### Local

Any scope defined past the global scope.

### Function

Within a first-layer function.

### Lexical

For nested functions, where the inner function has access to the outer function.

### Block scope

Within any curly braces.

> ![NOTE]
> 
> When defining variables, `var` uses function scope, however `let` and `const` use block scope.

## Closures

This object structure is a function that allows an inner function access to its outer scope. These are useful to associate data with a function that operates on that data.

Here is an example that actually puts this in to practice as I didn't fully understand the first time:

```js
function makeAdder(x) {
  return function(y) {
    return x + y;
  };
}

const add5 = makeAdder(5);
const add10 = makeAdder(10);

console.log(add5(2)); // 7
console.log(add10(2)); // 12
```

Another example would be a button that needed to be made several times with different values. All could be made with a closure (basically, a function factory).

## Modules

These are functions that return groups of functions as an object. They are called IIFEs (Immediately Invoked Function Expressions), and can only be used once. The return value can be assigned to a variable, which can then be referenced to interact with the internal methods.

This mimics many other object oriented languages. The functions are also as a bonus private or public, creating segmentation.

```js
const calculator = (() => {
    const add = (a, b) => a + b;
    const sub = (a, b) => a - b;
    // et cetera...
    return { add, sub };
})(); // IIFE is called immediately and assigned to a variable

calculator.add(4, 6); // 10
```

> [!IMPORTANT]
> 
> IIFEs, including modules should **ALWAYS** enable `use strict` as not doing so could cause catastrophic data leakage, nullifying the point of modular code in the first place.

### Object privacy

Public and private methods can only be *emulated* by JavaScript. Functions inside a module are either returned if public, or not if private.

```js
const Module = (function() {
    const privateMethod = () => console.log('private');
    return {
        publicMethod: () => console.log('public');
    }
})();
```
