# Data Types Deep Dive in JavaScript

Understanding JavaScript's data types is crucial for writing reliable and efficient code. JavaScript has **primitive** and **reference** types, each with unique characteristics. This guide covers:

- **Primitive Data Types**
  - `string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `bigint`
- **Reference Data Types**
  - `object`, `array`, `function`
- **Type Conversion & Type Coercion**
- **Mutability vs. Immutability**
- **Memory Management & Performance Considerations**

---

## Primitive Data Types

Primitive values are **immutable** (cannot be changed) and stored directly in memory.

### 1. String
Strings represent text and are enclosed in single, double, or backticks (````).
```js
let single = 'Hello';
let double = "World";
let template = `Hello, ${double}!`;
console.log(template); // "Hello, World!"
```

- Strings are **immutable** (cannot be changed after creation).
- **Common Methods:** `.length`, `.toUpperCase()`, `.slice()`, `.trim()`, `.includes()`.

---

### 2. Number
JavaScript has only **one** numeric type, `number`, which can be an **integer** or a **floating-point** value.
```js
let int = 100;
let float = 10.5;
console.log(typeof int, typeof float); // 'number' 'number'
```

- `NaN` (Not-a-Number) is a special numeric value indicating invalid operations.
- **Infinity & -Infinity** are special numeric values for large or small numbers.

Example:
```js
console.log(10 / 0); // Infinity
console.log('text' / 2); // NaN
```

---

### 3. Boolean
Booleans represent `true` or `false` values.
```js
let isActive = true;
let isCompleted = false;
console.log(typeof isActive); // 'boolean'
```

- Used in **logical operations** and **control flow**.
- **Truthy & Falsy values:**
  ```js
  console.log(Boolean(0)); // false
  console.log(Boolean("")); // false
  console.log(Boolean(1)); // true
  console.log(Boolean("text")); // true
  ```

---

### 4. Null
`null` is an intentional absence of a value.
```js
let emptyValue = null;
console.log(typeof emptyValue); // 'object' (JS quirk)
```
- Often used to **reset** variables or indicate an **empty state**.

---

### 5. Undefined
`undefined` means a variable is **declared but not assigned a value**.
```js
let notAssigned;
console.log(notAssigned); // undefined
```
- Functions return `undefined` when no return statement is specified.

---

### 6. Symbol (ES6+)
`Symbol` creates unique values useful for object properties.
```js
const id = Symbol("id");
console.log(id); // Symbol(id)
```
- Used for **object property keys** to avoid naming conflicts.

---

### 7. BigInt (ES11+)
`BigInt` is used for very large integers beyond `Number.MAX_SAFE_INTEGER`.
```js
let bigNum = 9007199254740991n;
console.log(bigNum + 1n); // 9007199254740992n
```
- Cannot mix `BigInt` with `number`.

---

## Reference Data Types

Reference types store **memory addresses** instead of actual values.

### 1. Object
Objects store **key-value pairs**.
```js
let person = { name: "Alice", age: 25 };
console.log(person.name); // Alice
```

- **Objects are mutable** (can be modified after creation).
- **Common Methods:** `Object.keys()`, `Object.values()`, `Object.assign()`.

---

### 2. Array
Arrays hold **ordered collections** of values.
```js
let numbers = [1, 2, 3];
console.log(numbers[0]); // 1
```

- Arrays are **mutable**.
- **Common Methods:** `.push()`, `.pop()`, `.map()`, `.filter()`.

---

### 3. Function
Functions are **first-class citizens** in JavaScript (can be assigned to variables, passed as arguments, or returned from functions).
```js
function greet(name) {
    return `Hello, ${name}!`;
}
console.log(greet("Bob"));
```

---

## Type Conversion & Type Coercion

### 1. Explicit Conversion
Using built-in methods:
```js
console.log(Number("123")); // 123
console.log(String(100)); // "100"
console.log(Boolean(0)); // false
```

### 2. Implicit Conversion (Type Coercion)
```js
console.log("5" + 5); // "55" (string concatenation)
console.log("5" - 1); // 4 (numeric conversion)
```
- JavaScript tries to **guess** the intended type, which can lead to unexpected behavior.

---

## Mutability vs. Immutability
- **Primitive types** are immutable:
  ```js
  let str = "hello";
  str[0] = "H"; // ❌ Doesn't change the string
  ```
- **Objects and arrays are mutable:**
  ```js
  let obj = { name: "Alice" };
  obj.name = "Bob"; // ✅ Modified successfully
  ```

To create **immutable** objects, use `Object.freeze()`:
```js
const obj = Object.freeze({ key: "value" });
obj.key = "newValue"; // ❌ Error in strict mode
```

---

## Memory Management & Performance Considerations

### 1. Garbage Collection (GC)
JavaScript uses **automatic garbage collection** to free unused memory.

### 2. Avoiding Memory Leaks
Common causes of memory leaks:
- **Unused global variables:**
  ```js
  var data = new Array(1000000); // ❌ Memory leak risk
  ```
- **Dangling references:**
  ```js
  let obj = { name: "Alice" };
  let ref = obj;
  obj = null; // `ref` still holds the object in memory
  ```
- **Unremoved event listeners:**
  ```js
  function attachListener() {
      let button = document.getElementById("btn");
      button.addEventListener("click", () => console.log("Clicked!"));
  }
  // Ensure to remove listeners
  button.removeEventListener("click", callback);
  ```

---

## Summary

| Type | Category | Mutable? |
|------|----------|----------|
| `string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `bigint` | Primitive | No |
| `object`, `array`, `function` | Reference | Yes |

Now that you've mastered JavaScript data types, continue with **[Type Coercion](4-type-coercion.md)** to understand implicit and explicit type conversions!

