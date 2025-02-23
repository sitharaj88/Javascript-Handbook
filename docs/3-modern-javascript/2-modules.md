# JavaScript Modules: ESM vs. CJS

JavaScript modules are essential for organizing and structuring code, especially in large applications. Modules allow developers to split code into reusable pieces and manage dependencies effectively. This guide covers everything you need to know about **ECMAScript Modules (ESM)** and **CommonJS (CJS)**, including differences, use cases, and best practices.

---

## Table of Contents

- [JavaScript Modules: ESM vs. CJS](#javascript-modules-esm-vs-cjs)
  - [Table of Contents](#table-of-contents)
  - [Introduction to JavaScript Modules](#introduction-to-javascript-modules)
    - [Key Benefits:](#key-benefits)
  - [Why Use Modules?](#why-use-modules)
  - [ECMAScript Modules (ESM)](#ecmascript-modules-esm)
    - [1. **Exporting from a Module**](#1-exporting-from-a-module)
      - [Named Exports:](#named-exports)
      - [Default Export:](#default-export)
    - [2. **Importing Modules**](#2-importing-modules)
      - [Named Imports:](#named-imports)
      - [Default Import:](#default-import)
    - [3. **Dynamic Imports**](#3-dynamic-imports)
    - [4. **ESM in Node.js**](#4-esm-in-nodejs)
  - [CommonJS (CJS)](#commonjs-cjs)
    - [1. **Exporting in CJS**](#1-exporting-in-cjs)
    - [2. **Importing in CJS**](#2-importing-in-cjs)
    - [3. **CJS Characteristics:**](#3-cjs-characteristics)
  - [Key Differences Between ESM and CJS](#key-differences-between-esm-and-cjs)
  - [When to Use ESM vs. CJS](#when-to-use-esm-vs-cjs)
  - [Advanced Module Patterns](#advanced-module-patterns)
    - [1. **Re-Exporting Modules**](#1-re-exporting-modules)
    - [2. **Import Meta**](#2-import-meta)
    - [3. **Mixing ESM and CJS**](#3-mixing-esm-and-cjs)
  - [Best Practices](#best-practices)
  - [Summary](#summary)

---

## Introduction to JavaScript Modules

Modules help in splitting large codebases into smaller, reusable files. Each module can export functionality and import it from other modules.

### Key Benefits:
- Reusability of code
- Improved maintainability
- Clear dependency management
- Enhanced performance via lazy loading

---

## Why Use Modules?

Without modules, JavaScript code would have:
- **Global namespace pollution**
- **Difficulty in managing dependencies**
- **Reduced code maintainability**

Modules solve these problems by providing **scope isolation** and **structured code sharing**.

---

## ECMAScript Modules (ESM)

ESM is the **standard module system** in modern JavaScript. Supported by all modern browsers and Node.js (from v12+), ESM uses `import` and `export` keywords.

### 1. **Exporting from a Module**

#### Named Exports:
```js
// utils.js
export const PI = 3.14159;
export function calculateArea(radius) {
    return PI * radius ** 2;
}
```

#### Default Export:
```js
// math.js
export default function add(a, b) {
    return a + b;
}
```

### 2. **Importing Modules**

#### Named Imports:
```js
import { PI, calculateArea } from './utils.js';
console.log(calculateArea(5));
```

#### Default Import:
```js
import add from './math.js';
console.log(add(3, 7)); // 10
```

### 3. **Dynamic Imports**

Dynamic imports enable **code splitting** and **lazy loading**:
```js
async function loadModule() {
    const { default: add } = await import('./math.js');
    console.log(add(5, 10));
}
loadModule();
```

### 4. **ESM in Node.js**
- Use `.mjs` extension or set `"type": "module"` in `package.json`.
- Example `package.json`:
  ```json
  {
    "type": "module"
  }
  ```

---

## CommonJS (CJS)

CJS is the **default module system** in Node.js before ES6.

### 1. **Exporting in CJS**
```js
// utils.js
const PI = 3.14159;
function calculateArea(radius) {
    return PI * radius ** 2;
}
module.exports = { PI, calculateArea };
```

### 2. **Importing in CJS**
```js
const { PI, calculateArea } = require('./utils.js');
console.log(calculateArea(5));
```

### 3. **CJS Characteristics:**
- Synchronous loading.
- Suitable for server-side code.
- Not natively supported in browsers without bundlers.

---

## Key Differences Between ESM and CJS

| Feature              | ESM                         | CJS                     |
|----------------------|------------------------------|-------------------------|
| Syntax               | `import` / `export`          | `require` / `module.exports`|
| Loading              | Asynchronous                 | Synchronous             |
| Scope                | Strict mode by default       | Non-strict mode default |
| Usage in Browsers    | Native support               | Requires bundlers       |
| Dynamic Imports      | `import()`                   | `require()`             |
| Top-Level `await`    | Supported                    | Not supported           |

---

## When to Use ESM vs. CJS

- **Use ESM** if:
  - Targeting modern browsers.
  - Writing code for newer Node.js versions.
  - Need asynchronous loading and top-level `await`.

- **Use CJS** if:
  - Maintaining legacy Node.js applications.
  - Working with packages that only support CJS.

---

## Advanced Module Patterns

### 1. **Re-Exporting Modules**
```js
// index.js
export * from './utils.js';
export * from './math.js';
```

### 2. **Import Meta**
Provides metadata about the current module.
```js
console.log(import.meta.url); // URL of the current module
```

### 3. **Mixing ESM and CJS**

- Use `createRequire` from `module` in Node.js:
```js
import { createRequire } from 'module';
const require = createRequire(import.meta.url);
const pkg = require('./package.json');
```

---

## Best Practices

- **Prefer ESM:** Modern, flexible, and future-proof.
- **Use Absolute Imports:** Avoid complex relative paths.
- **Leverage Dynamic Imports:** Load modules only when needed.
- **Avoid Circular Dependencies:** Structure modules to prevent infinite loops.
- **Document Public APIs:** Clarify what modules expose.
- **Bundle Efficiently:** Use tools like Webpack, Rollup, or Vite for production builds.

---

## Summary

| Concept          | ESM                         | CJS                     |
|------------------|------------------------------|-------------------------|
| Syntax           | `import` / `export`          | `require` / `module.exports`|
| Loading          | Asynchronous                 | Synchronous             |
| Usage Context    | Browsers, modern Node.js     | Node.js (legacy/compat) |
| Performance      | Better tree-shaking support  | Requires bundling       |
| Compatibility    | Modern standard              | Legacy applications     |

---

Understanding **JavaScript modules** is essential for scalable applications. By mastering both **ESM** and **CJS**, you can build modular, maintainable, and performant JavaScript codebases. 🚀✨

