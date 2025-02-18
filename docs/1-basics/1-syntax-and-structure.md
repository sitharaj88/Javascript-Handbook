# Syntax and Structure in JavaScript

Understanding JavaScript's syntax and structure is fundamental to writing clean, efficient, and maintainable code. This section covers:

- JavaScript statements and expressions
- Code blocks and indentation
- Comments
- Case sensitivity
- Semicolons and automatic semicolon insertion (ASI)
- Naming conventions and best practices

---

## Statements vs. Expressions

JavaScript programs consist of **statements** and **expressions**.

### Statements
A statement performs an action and usually ends with a semicolon (`;`). Examples of statements include:

```js
let x = 10; // Variable declaration statement
if (x > 5) { console.log("x is greater than 5"); } // Conditional statement
```

### Expressions
An expression produces a value and can be assigned to a variable.

```js
let sum = 5 + 10; // Arithmetic expression
let message = "Hello" + " World"; // String concatenation expression
console.log(sum); // 15
```

An **expression statement** is an expression that acts as a statement, such as:

```js
console.log("Hello, World!"); // Function call as a statement
```

---

## Code Blocks and Indentation

JavaScript uses **curly braces `{}`** to define blocks of code.

```js
if (true) {
    console.log("This is inside a block");
}
```

### Best Practices:
- Use **consistent indentation** (2 or 4 spaces) to improve readability.
- Always **use curly braces**, even for single-line conditions or loops.

```js
// Good Practice
if (condition) {
    console.log("Condition met");
}

// Avoid this (less readable)
if (condition) console.log("Condition met");
```

---

## Comments in JavaScript

Comments improve code readability and are ignored by the JavaScript engine.

### Single-line Comment:
```js
// This is a single-line comment
let name = "Alice"; // Inline comment
```

### Multi-line Comment:
```js
/*
 This is a multi-line comment.
 Useful for documentation.
*/
```

---

## Case Sensitivity in JavaScript

JavaScript is **case-sensitive**. This means:
```js
let myVariable = 10;
let MyVariable = 20;
console.log(myVariable); // 10
console.log(MyVariable); // 20 (different variable)
```

Always use **consistent casing conventions** for better readability.

---

## Semicolons and Automatic Semicolon Insertion (ASI)

JavaScript **automatically inserts semicolons** at the end of statements in some cases, but it's best to use them explicitly to avoid errors.

Example where ASI can cause unintended behavior:
```js
return
{
    message: "Hello";
};
// ASI causes 'return' to be interpreted as a standalone statement
```

Correct way:
```js
return {
    message: "Hello"
};
```

---

## Naming Conventions and Best Practices

### Variables and Function Names:
- Use **camelCase** for variables and functions:
  ```js
  let firstName = "John";
  function calculateTotal() {}
  ```

- Use **UPPER_CASE** for constants:
  ```js
  const PI = 3.14159;
  ```

- Use meaningful names:
  ```js
  let x = 10; // ❌ Bad Practice
  let userAge = 10; // ✅ Good Practice
  ```

### File and Folder Naming:
- Use **kebab-case** for filenames: `syntax-and-structure.js`
- Use **PascalCase** for class names:
  ```js
  class UserAccount {}
  ```

---

## Summary

- **Statements** perform actions, **expressions** produce values.
- **Use curly braces `{}`** for code blocks.
- **Indent consistently** (2 or 4 spaces).
- **Use comments** to improve readability.
- **JavaScript is case-sensitive**.
- **Avoid ASI pitfalls** by using semicolons.
- **Follow naming conventions** for better code organization.

Now that you've learned JavaScript's syntax and structure, move on to **[Variables and Scoping](2-variables-and-scoping.md)** to understand how JavaScript handles variable declarations and scope!

