# JavaScript Basics

## Table of Contents

1. [Syntax and Structure](#syntax-and-structure)
2. [Variables and Scoping](#variables-and-scoping)
3. [Data Types Deep Dive](#data-types-deep-dive)
4. [Type Coercion](#type-coercion)
5. [Functions](#functions)

---

## Syntax and Structure

JavaScript syntax is the set of rules that define a correctly structured JavaScript program. 

### Statements vs. Expressions
- **Statements** perform actions (e.g., `if`, `for`, `while`).
- **Expressions** evaluate to a value (e.g., `2 + 2`, `x > 10`).

Example:
```js
let a = 10; // Statement
console.log(a * 2); // Expression
```

### Code Blocks and Indentation
JavaScript uses `{}` to define blocks of code:
```js
if (true) {
    console.log("Hello, World!");
}
```
It is recommended to use **consistent indentation** (2 or 4 spaces).

### Comments
- Single-line comments: `// This is a comment`
- Multi-line comments:
```js
/*
   This is a multi-line comment
*/
```

---

## Variables and Scoping

JavaScript provides three ways to declare variables: `var`, `let`, and `const`.

### `var` vs. `let` vs. `const`
| Feature       | `var`  | `let`  | `const`  |
|--------------|--------|--------|----------|
| Scope       | Function | Block  | Block    |
| Hoisting    | Yes (initialized as `undefined`) | Yes (in Temporal Dead Zone) | Yes (in Temporal Dead Zone) |
| Reassignment | Yes    | Yes    | No       |

Example:
```js
let name = "Alice";
const age = 25;
var city = "New York";
```

### Hoisting
Variables declared with `var` are hoisted and initialized with `undefined`, while `let` and `const` remain in the **Temporal Dead Zone (TDZ)**.

```js
console.log(a); // undefined
var a = 5;

console.log(b); // ReferenceError: Cannot access 'b' before initialization
let b = 10;
```

---

## Data Types Deep Dive

JavaScript has **primitive** and **reference** types:

### Primitive Types
- `string`
- `number`
- `boolean`
- `null`
- `undefined`
- `symbol`
- `bigint`

Example:
```js
let str = "Hello";
let num = 42;
let flag = true;
let uniqueId = Symbol("id");
let bigNum = 9007199254740991n;
```

### Reference Types
- `Object`
- `Array`
- `Function`

Example:
```js
let obj = { name: "Alice", age: 25 };
let arr = [1, 2, 3];
let func = function() { console.log("Hello"); };
```

---

## Type Coercion

JavaScript automatically converts types when needed.

### Implicit vs. Explicit Conversion
- **Implicit:** JavaScript converts types automatically.
- **Explicit:** Using `Number()`, `String()`, `Boolean()`.

Example:
```js
console.log("5" + 5); // "55" (string concatenation)
console.log("5" - 2); // 3 (numeric subtraction)
console.log(Number("123")); // 123
console.log(Boolean(0)); // false
```

### `==` vs. `===`
- `==` performs **type coercion**.
- `===` compares **both value and type**.

Example:
```js
console.log(5 == "5"); // true
console.log(5 === "5"); // false
```

---

## Functions

Functions are reusable blocks of code that perform specific tasks. JavaScript supports different types of functions, each serving different purposes.

### Function Declaration
A function declaration defines a function that can be called before its definition due to **hoisting**.
```js
function greet(name) {
    return `Hello, ${name}!`;
}
console.log(greet("Alice"));
```

### Function Expression
A function expression assigns a function to a variable. These are **not hoisted**.
```js
const greet = function(name) {
    return `Hello, ${name}!`;
};
console.log(greet("Bob"));
```

### Arrow Functions
Arrow functions provide a concise way to write functions and have a **lexical `this`**.
```js
const greet = (name) => `Hello, ${name}!`;
console.log(greet("Charlie"));
```

### Immediately Invoked Function Expressions (IIFE)
IIFEs execute **immediately** after they are defined. Useful for **module pattern** and avoiding global scope pollution.
```js
(function() {
    console.log("IIFE executed");
})();
```

### Default Parameters
Default parameters allow functions to have default values if no argument is provided.
```js
function greet(name = "Guest") {
    return `Hello, ${name}!`;
}
console.log(greet()); // "Hello, Guest!"
```

### Rest and Spread Operators
- **Rest (`...args`)**: Collects all remaining arguments into an array.
- **Spread (`...`)**: Expands an array into individual elements.

Example:
```js
function sum(...numbers) {
    return numbers.reduce((acc, num) => acc + num, 0);
}
console.log(sum(1, 2, 3, 4)); // 10
```

```js
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5];
console.log(arr2); // [1, 2, 3, 4, 5]
```

### Higher-Order Functions
A function that **takes another function as an argument** or **returns a function**.
```js
function operateOnNumbers(a, b, operation) {
    return operation(a, b);
}

const add = (x, y) => x + y;
console.log(operateOnNumbers(5, 10, add)); // 15
```

### Callback Functions
A function passed as an argument to another function.
```js
function fetchData(callback) {
    setTimeout(() => {
        callback("Data received");
    }, 1000);
}

fetchData(message => console.log(message));
```

---


