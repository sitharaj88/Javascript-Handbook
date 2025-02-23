# Decorators and Proxies in JavaScript

Modern JavaScript provides powerful meta-programming capabilities through **Decorators** and **Proxies**. These features allow developers to modify and extend the behavior of classes, objects, and functions dynamically and elegantly.

---

## Table of Contents

- [Decorators and Proxies in JavaScript](#decorators-and-proxies-in-javascript)
  - [Table of Contents](#table-of-contents)
  - [Introduction to Decorators](#introduction-to-decorators)
    - [Why Use Decorators?](#why-use-decorators)
  - [Using Decorators in JavaScript](#using-decorators-in-javascript)
    - [1. **Class Decorators**](#1-class-decorators)
    - [2. **Method Decorators**](#2-method-decorators)
    - [3. **Property Decorators**](#3-property-decorators)
    - [4. **Parameter Decorators**](#4-parameter-decorators)
  - [Advanced Decorator Patterns](#advanced-decorator-patterns)
    - [Example - Caching Decorator:](#example---caching-decorator)
  - [Introduction to Proxies](#introduction-to-proxies)
    - [Why Use Proxies?](#why-use-proxies)
  - [Creating Proxies](#creating-proxies)
    - [Basic Proxy Example:](#basic-proxy-example)
  - [Common Traps in Proxies](#common-traps-in-proxies)
    - [Example - Validation Proxy:](#example---validation-proxy)
  - [Reflect API with Proxies](#reflect-api-with-proxies)
    - [Example:](#example)
  - [Use Cases for Decorators and Proxies](#use-cases-for-decorators-and-proxies)
  - [Performance Considerations](#performance-considerations)
  - [Best Practices](#best-practices)
  - [Summary](#summary)

---

## Introduction to Decorators

**Decorators** provide a way to **annotate** and **modify classes** and their members. They are part of a proposed ECMAScript standard and widely used in frameworks like **Angular** and **NestJS**.

### Why Use Decorators?
- Enhance readability by separating concerns.
- Reuse logic across multiple components.
- Dynamically extend behavior without modifying source code.

---

## Using Decorators in JavaScript

### 1. **Class Decorators**
```js
function Logger(constructor) {
    console.log(`Class created: ${constructor.name}`);
}

@Logger
class User {
    constructor(name) {
        this.name = name;
    }
}
```

### 2. **Method Decorators**
```js
function Log(target, key, descriptor) {
    const original = descriptor.value;
    descriptor.value = function (...args) {
        console.log(`Calling ${key} with ${args}`);
        return original.apply(this, args);
    };
    return descriptor;
}

class Calculator {
    @Log
    add(a, b) {
        return a + b;
    }
}
```

### 3. **Property Decorators**
```js
function ReadOnly(target, key) {
    Object.defineProperty(target, key, { writable: false });
}

class Book {
    @ReadOnly
    title = "JavaScript Guide";
}
```

### 4. **Parameter Decorators**
```js
function LogParam(target, key, index) {
    console.log(`Parameter at index ${index} in method ${key}`);
}

class Printer {
    print(@LogParam message) {
        console.log(message);
    }
}
```

---

## Advanced Decorator Patterns

- **Validation Decorators** for form inputs.
- **Authorization Checks** for APIs.
- **Caching Results** for expensive operations.
- **Deprecation Warnings** for legacy methods.

### Example - Caching Decorator:
```js
function Cache(target, key, descriptor) {
    const cache = new Map();
    const original = descriptor.value;

    descriptor.value = function (...args) {
        const key = JSON.stringify(args);
        if (cache.has(key)) return cache.get(key);
        const result = original.apply(this, args);
        cache.set(key, result);
        return result;
    };
    return descriptor;
}

class MathOps {
    @Cache
    multiply(a, b) {
        console.log("Calculating...");
        return a * b;
    }
}
```

---

## Introduction to Proxies

**Proxies** allow you to define custom behavior for fundamental operations (e.g., property lookup, assignment, enumeration).

### Why Use Proxies?
- Intercept operations for validation, logging, or access control.
- Create reactive objects (e.g., Vue.js reactivity system).
- Implement dynamic behavior without modifying original objects.

---

## Creating Proxies

### Basic Proxy Example:
```js
const user = { name: "Alice" };

const proxy = new Proxy(user, {
    get(target, prop) {
        console.log(`Accessing ${prop}`);
        return target[prop];
    },
    set(target, prop, value) {
        console.log(`Setting ${prop} to ${value}`);
        target[prop] = value;
        return true;
    }
});

proxy.name;      // Accessing name -> "Alice"
proxy.age = 30;  // Setting age to 30
```

---

## Common Traps in Proxies

| Trap      | Description                          | Example                 |
|-----------|--------------------------------------|-------------------------|
| `get`     | Intercepts property reads            | `proxy.prop`            |
| `set`     | Intercepts property assignments      | `proxy.prop = value`    |
| `has`     | Intercepts `in` operator checks      | `'prop' in proxy`       |
| `deleteProperty` | Intercepts `delete` operations | `delete proxy.prop`     |
| `apply`   | Intercepts function calls            | `proxy()`               |
| `construct`| Intercepts `new` operator calls     | `new proxy()`           |

### Example - Validation Proxy:
```js
const validator = {
    set(obj, prop, value) {
        if (prop === "age" && typeof value !== "number") {
            throw new TypeError("Age must be a number");
        }
        obj[prop] = value;
        return true;
    }
};

const person = new Proxy({}, validator);
person.age = 25;   // ✅ Works
person.age = "old"; // ❌ Throws TypeError
```

---

## Reflect API with Proxies

The **Reflect** API complements Proxies by providing methods that correspond to proxy traps, ensuring consistent behavior.

### Example:
```js
const handler = {
    get(target, prop, receiver) {
        return Reflect.get(...arguments);
    },
    set(target, prop, value, receiver) {
        return Reflect.set(...arguments);
    }
};

const obj = new Proxy({}, handler);
obj.name = "Bob";
console.log(obj.name); // Bob
```

**Why Use Reflect?**
- Avoid recursion issues in proxy traps.
- Provides default behavior when traps don’t intercept.

---

## Use Cases for Decorators and Proxies

- **Access Control:** Using Proxies to create protected objects.
- **Data Binding:** Vue.js uses Proxies for reactive data.
- **Logging and Profiling:** Decorators to log function execution.
- **API Rate Limiting:** Proxies to throttle API calls.
- **Dependency Injection:** Decorators in frameworks like Angular.

---

## Performance Considerations

- Decorators can add overhead; use them judiciously.
- Proxies may impact performance if traps handle high-frequency operations.
- Benchmark critical code paths when using meta-programming.

---

## Best Practices

- **Use Decorators for Reusability:** Encapsulate common logic.
- **Minimize Proxy Layers:** Excessive nesting affects performance.
- **Combine Reflect with Proxies:** Ensures reliable default behavior.
- **Document Decorator Behavior:** Clarify impacts on function or class usage.
- **Avoid Overusing Proxies:** Use only where dynamic behavior is needed.

---

## Summary

| Concept   | Description                                   | Example                |
|-----------|-----------------------------------------------|------------------------|
| **Decorator** | Function to modify class/method behavior  | `@Logger class MyClass`|
| **Proxy**     | Object wrapper intercepting operations     | `new Proxy(obj, handler)`|
| **Reflect**   | Provides default methods for proxies       | `Reflect.get()`        |
| **Class Decorator** | Modifies entire class behavior      | `@MyDecorator`         |
| **Method Decorator**| Wraps/extends function logic        | `@Log` on methods       |
| **Proxy Traps**    | Methods intercepting object operations| `get`, `set`, `apply`  |

---

By mastering **Decorators** and **Proxies**, you unlock the power of **meta-programming** in JavaScript. These tools are essential for writing **scalable**, **maintainable**, and **dynamic** applications. 🚀✨

