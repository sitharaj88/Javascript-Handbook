# Functions in JavaScript

Functions are fundamental in JavaScript, enabling code reuse, modularity, and abstraction. This guide covers:

- **Function Declarations vs. Expressions**
- **Arrow Functions**
- **Immediately Invoked Function Expressions (IIFE)**
- **Higher-Order Functions**
- **Closures**
- **Default Parameters & Rest/Spread Operators**
- **Function Hoisting**
- **Best Practices & Common Pitfalls**

---

## Function Declarations vs. Function Expressions

### 1. Function Declaration
A function declaration is defined using the `function` keyword and is **hoisted**, meaning it can be called before its definition.

```js
function greet(name) {
    return `Hello, ${name}!`;
}

console.log(greet("Alice")); // "Hello, Alice!"
```

### 2. Function Expression
A function expression is assigned to a variable and **not hoisted**.

```js
const greet = function(name) {
    return `Hello, ${name}!`;
};

console.log(greet("Bob")); // "Hello, Bob!"
```

**Key Difference:** Function expressions **cannot** be called before they are defined.

```js
console.log(sum(5, 3)); // ❌ ReferenceError
const sum = function(a, b) {
    return a + b;
};
```

---

## Arrow Functions (ES6+)

Arrow functions provide a **concise** syntax for writing functions and **do not bind `this`**.

```js
const add = (a, b) => a + b;
console.log(add(2, 3)); // 5
```

### 1. Single Parameter (No Parentheses Needed)
```js
const square = num => num * num;
console.log(square(4)); // 16
```

### 2. Multi-Line Function Body
```js
const multiply = (a, b) => {
    console.log("Multiplying...");
    return a * b;
};
console.log(multiply(3, 4)); // 12
```

### 3. Arrow Functions and `this`
Arrow functions do **not** have their own `this`. Instead, they inherit `this` from their enclosing scope.

```js
const obj = {
    name: "Alice",
    greet: function() {
        setTimeout(() => {
            console.log(`Hello, ${this.name}`); // Works ✅
        }, 1000);
    }
};
obj.greet();
```

---

## Immediately Invoked Function Expressions (IIFE)

IIFEs execute **immediately** after declaration, useful for **isolating scope**.

```js
(function() {
    console.log("IIFE executed");
})();
```

---

## Higher-Order Functions

A higher-order function **takes another function as an argument** or **returns a function**.

```js
function operate(a, b, operation) {
    return operation(a, b);
}

const sum = (x, y) => x + y;
console.log(operate(5, 3, sum)); // 8
```

**Common Examples:**
- `.map()`, `.filter()`, `.reduce()`

```js
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8, 10]
```

---

## Closures

A closure is when an **inner function remembers** variables from its **outer function**.

```js
function counter() {
    let count = 0;
    return function() {
        count++;
        console.log(count);
    };
}

const increment = counter();
increment(); // 1
increment(); // 2
```

Closures are useful for **data encapsulation** and maintaining **private variables**.

---

## Default Parameters & Rest/Spread Operators

### 1. Default Parameters
Set default values for function parameters.

```js
function greet(name = "Guest") {
    return `Hello, ${name}!`;
}
console.log(greet()); // "Hello, Guest!"
```

### 2. Rest Parameters (`...`)
Collects arguments into an array.

```js
function sum(...numbers) {
    return numbers.reduce((acc, num) => acc + num, 0);
}
console.log(sum(1, 2, 3, 4)); // 10
```

### 3. Spread Operator (`...`)
Expands arrays into separate arguments.

```js
const nums = [1, 2, 3];
console.log(Math.max(...nums)); // 3
```

---

## Function Hoisting

### 1. Hoisting with Function Declarations
```js
console.log(sayHello()); // ✅ Works

function sayHello() {
    return "Hello!";
}
```

### 2. No Hoisting with Function Expressions
```js
console.log(sayHi()); // ❌ ReferenceError
const sayHi = function() {
    return "Hi!";
};
```

---

## Best Practices & Common Pitfalls

### ✅ Best Practices
- Use **function declarations** for readability.
- Use **arrow functions** when `this` binding is not needed.
- Use **default parameters** to prevent `undefined` values.
- Use **IIFE** to **avoid polluting the global scope**.
- **Encapsulate logic** inside functions for reusability.

### ❌ Common Pitfalls
- **Confusing function expressions with function declarations.**
- **Using `var` instead of `let` or `const`** (avoids scoping issues).
- **Forgetting `return` in arrow functions.**
- **Overusing nested functions** (keep them modular).

```js
const multiply = (a, b) => {
    a * b; // ❌ No return statement
};
console.log(multiply(2, 3)); // undefined
```

**Fix:**
```js
const multiply = (a, b) => a * b;
console.log(multiply(2, 3)); // 6
```

---

## Summary

| Feature | Function Declaration | Function Expression | Arrow Function |
|---------|----------------------|----------------------|---------------|
| Hoisting | ✅ Yes | ❌ No | ❌ No |
| `this` Binding | ✅ Yes | ✅ Yes | ❌ No |
| Syntax | `function func(){}` | `const func = function(){}` | `const func = () => {}` |

---

Now that you've mastered JavaScript functions, move on to **[Advanced Concepts](../2-advanced-concepts/README.md)** to explore closures, async functions, and more!

