# Modern JavaScript: ES6+ Features

JavaScript has evolved significantly with the introduction of **ES6 (ECMAScript 2015)** and subsequent updates. These modern features enhance code readability, reduce complexity, and improve performance. This guide provides a comprehensive and unique explanation of essential ES6+ concepts that every JavaScript developer should know.

---

## Table of Contents

- [Modern JavaScript: ES6+ Features](#modern-javascript-es6-features)
  - [Table of Contents](#table-of-contents)
  - [Let and Const](#let-and-const)
    - [1. **`let`** - Block-scoped variable](#1-let---block-scoped-variable)
    - [2. **`const`** - Block-scoped, immutable reference](#2-const---block-scoped-immutable-reference)
  - [Arrow Functions](#arrow-functions)
    - [Multi-line Example:](#multi-line-example)
    - [Lexical `this` Example:](#lexical-this-example)
  - [Template Literals](#template-literals)
    - [Multi-line String:](#multi-line-string)
  - [Destructuring Assignment](#destructuring-assignment)
    - [1. **Array Destructuring**](#1-array-destructuring)
    - [2. **Object Destructuring**](#2-object-destructuring)
    - [Default Values:](#default-values)
  - [Spread and Rest Operators](#spread-and-rest-operators)
    - [1. **Spread Operator (`...`)** - Expands iterable elements.](#1-spread-operator----expands-iterable-elements)
    - [2. **Rest Operator (`...`)** - Condenses multiple elements into one.](#2-rest-operator----condenses-multiple-elements-into-one)
  - [Default Parameters](#default-parameters)
  - [Enhanced Object Literals](#enhanced-object-literals)
  - [Classes](#classes)
    - [Basic Class:](#basic-class)
    - [Inheritance:](#inheritance)
  - [Modules (ESM vs. CJS)](#modules-esm-vs-cjs)
    - [1. **ESM (ECMAScript Modules)** – Modern standard](#1-esm-ecmascript-modules--modern-standard)
    - [2. **CJS (CommonJS)** – Node.js standard](#2-cjs-commonjs--nodejs-standard)
  - [Promises and Async/Await](#promises-and-asyncawait)
    - [1. **Promise Example:**](#1-promise-example)
    - [2. **Async/Await Example:**](#2-asyncawait-example)
  - [Optional Chaining (`?.`)](#optional-chaining-)
  - [Nullish Coalescing Operator (`??`)](#nullish-coalescing-operator-)
  - [BigInt](#bigint)
  - [Dynamic Import](#dynamic-import)
  - [Other Notable ES6+ Features](#other-notable-es6-features)
  - [Summary](#summary)

---

## Let and Const

### 1. **`let`** - Block-scoped variable
```js
let count = 10;
if (true) {
    let count = 20; // Different scope
    console.log(count); // 20
}
console.log(count); // 10
```

### 2. **`const`** - Block-scoped, immutable reference
```js
const PI = 3.14159;
// PI = 3; ❌ TypeError: Assignment to constant variable
```

**Key Insight:** `const` variables can be **mutated** if they reference objects.
```js
const user = { name: "Alice" };
user.name = "Bob"; // ✅ Allowed
```

---

## Arrow Functions

Arrow functions offer a concise syntax and **lexical `this`** binding.
```js
const add = (a, b) => a + b;
console.log(add(5, 3)); // 8
```

### Multi-line Example:
```js
const greet = (name) => {
    console.log(`Hello, ${name}!`);
};
```

### Lexical `this` Example:
```js
function Timer() {
    this.seconds = 0;
    setInterval(() => this.seconds++, 1000);
}
const timer = new Timer();
```

---

## Template Literals

Template literals support **string interpolation** and **multi-line strings**:
```js
const name = "Alice";
const greeting = `Hello, ${name}!`;
console.log(greeting); // Hello, Alice!
```

### Multi-line String:
```js
const multiline = `This is
on multiple lines.`;
console.log(multiline);
```

---

## Destructuring Assignment

Destructuring extracts values from arrays or properties from objects.

### 1. **Array Destructuring**
```js
const [first, second] = [1, 2];
console.log(first); // 1
```

### 2. **Object Destructuring**
```js
const user = { name: "Alice", age: 30 };
const { name, age } = user;
console.log(name); // Alice
```

### Default Values:
```js
const { country = "Unknown" } = user;
console.log(country); // Unknown
```

---

## Spread and Rest Operators

### 1. **Spread Operator (`...`)** - Expands iterable elements.
```js
const arr1 = [1, 2];
const arr2 = [3, 4];
const combined = [...arr1, ...arr2];
console.log(combined); // [1, 2, 3, 4]
```

### 2. **Rest Operator (`...`)** - Condenses multiple elements into one.
```js
function sum(...numbers) {
    return numbers.reduce((acc, num) => acc + num, 0);
}
console.log(sum(1, 2, 3)); // 6
```

---

## Default Parameters

Default parameters provide fallback values:
```js
function greet(name = "Guest") {
    console.log(`Hello, ${name}!`);
}

greet(); // Hello, Guest!
```

---

## Enhanced Object Literals

ES6 introduced shorthand for defining object properties and methods:
```js
const name = "Alice";
const user = {
    name,
    greet() {
        console.log(`Hello, ${this.name}!`);
    }
};
user.greet();
```

---

## Classes

JavaScript classes provide a **cleaner syntax** for object-oriented programming.

### Basic Class:
```js
class Person {
    constructor(name) {
        this.name = name;
    }
    greet() {
        console.log(`Hello, ${this.name}!`);
    }
}

const alice = new Person("Alice");
alice.greet(); // Hello, Alice!
```

### Inheritance:
```js
class Developer extends Person {
    constructor(name, language) {
        super(name);
        this.language = language;
    }
    code() {
        console.log(`${this.name} codes in ${this.language}.`);
    }
}

const dev = new Developer("Bob", "JavaScript");
dev.code(); // Bob codes in JavaScript.
```

---

## Modules (ESM vs. CJS)

### 1. **ESM (ECMAScript Modules)** – Modern standard
- **Export:**
  ```js
  export const name = "Alice";
  export function greet() { console.log("Hello!"); }
  ```
- **Import:**
  ```js
  import { name, greet } from "./module.js";
  ```

### 2. **CJS (CommonJS)** – Node.js standard
- **Export:**
  ```js
  module.exports = { name: "Alice" };
  ```
- **Import:**
  ```js
  const { name } = require("./module.js");
  ```

---

## Promises and Async/Await

### 1. **Promise Example:**
```js
const fetchData = new Promise((resolve) => {
    setTimeout(() => resolve("Data loaded"), 1000);
});

fetchData.then(console.log); // Data loaded
```

### 2. **Async/Await Example:**
```js
async function loadData() {
    const data = await fetchData;
    console.log(data);
}
loadData();
```

---

## Optional Chaining (`?.`)

Safely access nested properties:
```js
const user = { profile: { name: "Alice" } };
console.log(user?.profile?.name); // Alice
console.log(user?.address?.city); // undefined (no error)
```

---

## Nullish Coalescing Operator (`??`)

Provides default values when `null` or `undefined`:
```js
const value = null ?? "Default";
console.log(value); // Default
```

---

## BigInt

`BigInt` allows representation of integers beyond `Number.MAX_SAFE_INTEGER`:
```js
const largeNumber = 9007199254740991n;
console.log(largeNumber + 1n); // 9007199254740992n
```

---

## Dynamic Import

Dynamic `import()` enables code splitting:
```js
async function loadModule() {
    const { greet } = await import("./module.js");
    greet();
}
loadModule();
```

---

## Other Notable ES6+ Features

- **Symbol:** Unique and immutable data type.
- **Map/Set:** Efficient key-value and unique value storage.
- **WeakMap/WeakSet:** Weakly referenced collections, useful for memory optimization.
- **Proxy:** Enables creation of custom behavior for fundamental operations.
- **Reflect API:** Provides methods for interceptable JavaScript operations.
- **GlobalThis:** A standard way to access the global object across environments.

---

## Summary

| Feature                  | Description                                       | Example                    |
|--------------------------|---------------------------------------------------|----------------------------|
| `let` & `const`          | Block-scoped variables                             | `let a = 1; const b = 2;`  |
| Arrow Functions          | Shorter syntax and lexical `this`                  | `(a, b) => a + b`          |
| Template Literals        | Multi-line strings and interpolation               | ``Hello, ${name}``         |
| Destructuring            | Unpack values from arrays/objects                  | `const { x } = obj;`       |
| Spread/Rest Operators    | Expand/condense iterable values                    | `[...arr]` or `(…args)`    |
| Classes                 | Object-oriented programming syntax                 | `class User {}`            |
| Modules (ESM/CJS)        | Code modularization                                | `import/export`            |
| Promises & Async/Await   | Handle asynchronous operations                     | `await fetch()`            |
| Optional Chaining        | Safe property access                               | `obj?.prop`                |
| Nullish Coalescing       | Default values for null/undefined                  | `value ?? 'default'`       |
| BigInt                   | Large integer support                              | `9007199254740991n`        |
| Dynamic Import           | Code splitting and lazy loading                    | `import('./module.js')`    |

---

Mastering these **ES6+ features** will significantly improve your JavaScript codebase, making it modern, clean, and performant. 🚀✨

