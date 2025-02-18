# Variables and Scoping in JavaScript

Understanding variables and scoping in JavaScript is crucial for writing bug-free, maintainable code. This section covers:

- Variable declarations (`var`, `let`, `const`)
- Scope types (Global, Function, Block)
- Hoisting behavior
- Temporal Dead Zone (TDZ)
- Common pitfalls and best practices

---

## Variable Declarations (`var`, `let`, `const`)

JavaScript provides three ways to declare variables: `var`, `let`, and `const`.

### `var` (Function-scoped, Hoisted, Can be Redeclared)
```js
var name = "Alice";
console.log(name); // Alice

var name = "Bob"; // Allowed
console.log(name); // Bob
```
**Issues with `var`:**
- It is **function-scoped**, meaning it ignores block `{}` boundaries.
- It allows **redeclaration**, which can lead to accidental overwrites.
- It is **hoisted**, but initialized as `undefined`.

Example of scope issue with `var`:
```js
if (true) {
    var message = "Hello";
}
console.log(message); // Accessible outside the block (Bad Practice)
```

---

### `let` (Block-scoped, Hoisted but in TDZ, Cannot be Redeclared)
```js
let age = 25;
age = 26; // Allowed

let age = 30; // ❌ SyntaxError: Identifier 'age' has already been declared
```
- `let` is **block-scoped**, meaning it respects `{}`.
- It is **hoisted**, but cannot be accessed before declaration (Temporal Dead Zone - TDZ).

Example:
```js
if (true) {
    let status = "Active";
    console.log(status); // Active
}
console.log(status); // ❌ ReferenceError: status is not defined
```

---

### `const` (Block-scoped, Hoisted but in TDZ, Cannot be Reassigned)
```js
const PI = 3.14159;
PI = 3.14; // ❌ TypeError: Assignment to constant variable.
```
- **Must be initialized** at the time of declaration.
- **Cannot be reassigned**, but **objects declared with `const` can be mutated**.

Example:
```js
const person = { name: "Alice" };
person.name = "Bob"; // Allowed ✅
console.log(person); // { name: "Bob" }

person = { name: "Charlie" }; // ❌ TypeError: Assignment to constant variable.
```

---

## Scope in JavaScript

### 1. Global Scope
A variable declared **outside** any function is in the **global scope** and accessible everywhere.

```js
var globalVar = "I'm global";

function showGlobal() {
    console.log(globalVar);
}
showGlobal(); // I'm global
```
**Pitfall:** Too many global variables can lead to naming conflicts.

---

### 2. Function Scope
A variable declared inside a **function** is **not accessible** outside it.
```js
function myFunction() {
    var localVar = "I'm local";
    console.log(localVar); // Accessible ✅
}

console.log(localVar); // ❌ ReferenceError: localVar is not defined
```

---

### 3. Block Scope
- **`let` and `const` are block-scoped**.
- **`var` is NOT block-scoped** (can lead to unintended behavior).

Example:
```js
if (true) {
    let blockVar = "Inside block";
}
console.log(blockVar); // ❌ ReferenceError: blockVar is not defined
```

**Pitfall:** Avoid using `var` inside blocks since it will still be accessible globally.

```js
if (true) {
    var testVar = "Oops";
}
console.log(testVar); // Accessible! (Unintended behavior)
```

---

## Hoisting in JavaScript

Hoisting is JavaScript’s behavior of moving variable and function **declarations** to the top of their scope before execution.

**Example with `var` (Hoisted but Undefined):**
```js
console.log(myVar); // undefined
var myVar = 10;
```

**Example with `let` and `const` (Hoisted but in TDZ):**
```js
console.log(myLet); // ❌ ReferenceError: Cannot access 'myLet' before initialization
let myLet = 20;
```

---

## Temporal Dead Zone (TDZ)

Variables declared with `let` and `const` exist in a **Temporal Dead Zone** from the start of the block until the declaration is encountered.

Example:
```js
console.log(a); // ❌ ReferenceError
let a = 5;
```

This prevents accidental use of variables **before** they are declared.

---

## Best Practices and Pitfalls

### ✅ Best Practices
- **Prefer `const`** unless you need to reassign a value.
- Use `let` for variables that change.
- Avoid using `var` due to its **scope issues**.
- Use **meaningful variable names** for better readability.
- Avoid **global variables** to prevent conflicts.

### ❌ Common Pitfalls
- **Redeclaring variables** using `var` can cause bugs.
- **Accessing variables before declaration** (TDZ issue with `let`/`const`).
- **Mutating `const` objects** (allowed but should be used carefully).
- **Global pollution** (too many global variables).

---

## Summary

| Feature       | `var` | `let` | `const` |
|--------------|-------|-------|--------|
| Scope       | Function | Block  | Block  |
| Hoisting    | Yes (undefined) | Yes (TDZ) | Yes (TDZ) |
| Reassignment | Yes   | Yes   | No  |
| Redeclaration | Yes  | No  | No  |

- **Use `const`** by default, only use `let` when reassignment is required.
- **Avoid `var`** due to its lack of block-scoping and redeclaration issues.
- **Understand hoisting** and avoid accessing variables before they are declared.

---

Now that you've mastered variables and scoping, proceed to **[Data Types Deep Dive](3-data-types-deep-dive.md)** for a deeper look into JavaScript's data types!

