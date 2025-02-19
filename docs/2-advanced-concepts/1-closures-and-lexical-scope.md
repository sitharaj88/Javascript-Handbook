# Closures and Lexical Scope in JavaScript

Understanding **closures** and **lexical scope** is essential for mastering JavaScript. These concepts allow developers to write more efficient, secure, and modular code. In this guide, we'll explore:

- **Lexical Scope**
- **What are Closures?**
- **How Closures Work**
- **Practical Use Cases of Closures**
- **Common Pitfalls with Closures**
- **Best Practices**

---

## Lexical Scope

### What is Lexical Scope?
**Lexical scope** (also called **static scope**) refers to how variable accessibility is determined by the **location** where variables are declared in the source code.

- Inner functions have access to variables defined in their **outer functions**.
- Variables are accessible based on **where** they are declared, **not** where they are called.

### Example:
```js
function outerFunction() {
    const outerVariable = "I am from outerFunction";

    function innerFunction() {
        console.log(outerVariable); // ✅ Accessible due to lexical scope
    }

    innerFunction();
}

outerFunction(); // Output: "I am from outerFunction"
```

### Key Points:
- Variables in the **outer scope** are accessible inside the **inner scope**.
- The **reverse is not true**; outer functions **cannot** access variables from inner functions.

```js
function outerFunction() {
    function innerFunction() {
        const innerVariable = "Inner Value";
    }
    console.log(innerVariable); // ❌ ReferenceError
}

outerFunction();
```

---

## What are Closures?

A **closure** is created when a function **remembers** its **lexical scope** even when the function is executed **outside** that scope.

### Key Characteristics:
- A closure gives **access to an outer function's scope** from an inner function.
- Closures are **created automatically** in JavaScript when functions are defined.

### Basic Example:
```js
function outer() {
    let count = 0;
    
    return function inner() {
        count++;
        console.log(`Count: ${count}`);
    };
}

const counter = outer();
counter(); // Count: 1
counter(); // Count: 2
```

**Why this works:** The `inner` function **remembers** the `count` variable from the `outer` function, even after `outer` has finished executing.

---

## How Closures Work

Closures **capture variables** from their outer lexical scope **by reference** (not by value). This allows variables to **persist** between multiple invocations.

### Example with Persistent State:
```js
function createCounter() {
    let count = 0;

    return {
        increment: function() {
            count++;
            console.log(`Count: ${count}`);
        },
        decrement: function() {
            count--;
            console.log(`Count: ${count}`);
        }
    };
}

const counter = createCounter();
counter.increment(); // Count: 1
counter.increment(); // Count: 2
counter.decrement(); // Count: 1
```

Here, `count` remains **private** to `createCounter`, demonstrating **data encapsulation** using closures.

---

## Practical Use Cases of Closures

### 1. **Data Encapsulation (Private Variables)**
Closures can create **private variables** that **cannot** be accessed from outside.

```js
function createBankAccount(initialBalance) {
    let balance = initialBalance;

    return {
        getBalance: () => balance,
        deposit: amount => balance += amount,
        withdraw: amount => balance -= amount
    };
}

const account = createBankAccount(100);
console.log(account.getBalance()); // 100
account.deposit(50);
console.log(account.getBalance()); // 150
```

### 2. **Function Factories**
Closures allow you to **generate customized functions**.

```js
function greet(greeting) {
    return function(name) {
        console.log(`${greeting}, ${name}!`);
    };
}

const sayHello = greet("Hello");
sayHello("Alice"); // Hello, Alice!
sayHello("Bob");   // Hello, Bob!
```

### 3. **Partial Application**
Fixing some arguments of a function using closures.

```js
function multiply(a) {
    return function(b) {
        return a * b;
    };
}

const double = multiply(2);
console.log(double(5)); // 10

const triple = multiply(3);
console.log(triple(5)); // 15
```

### 4. **Memoization**
Closures help cache results for **performance optimization**.

```js
function memoize(fn) {
    const cache = {};
    return function(n) {
        if (n in cache) {
            console.log("Fetching from cache");
            return cache[n];
        }
        console.log("Calculating result");
        cache[n] = fn(n);
        return cache[n];
    };
}

function factorial(x) {
    if (x === 0) return 1;
    return x * factorial(x - 1);
}

const memoizedFactorial = memoize(factorial);
console.log(memoizedFactorial(5)); // Calculates and returns 120
console.log(memoizedFactorial(5)); // Fetches from cache: 120
```

---

## Common Pitfalls with Closures

### 1. **Memory Leaks**
Closures can cause memory leaks if large objects remain referenced unnecessarily.

**Example:**
```js
function createLargeClosure() {
    let largeArray = new Array(1000000).fill("data");
    return function() {
        console.log(largeArray[0]);
    };
}

const closure = createLargeClosure();
closure(); // Memory may not be freed due to closure holding reference
```

**Solution:** Ensure variables are dereferenced when no longer needed.

---

### 2. **Unexpected Behavior in Loops**
Closures can capture loop variables in unexpected ways.

**Problematic Example:**
```js
for (var i = 0; i < 3; i++) {
    setTimeout(function() {
        console.log(i); // Outputs 3, 3, 3
    }, 1000);
}
```

**Solution:** Use `let` for block scoping:
```js
for (let i = 0; i < 3; i++) {
    setTimeout(function() {
        console.log(i); // Outputs 0, 1, 2
    }, 1000);
}
```

---

## Best Practices

- **Minimize closure scope:** Only capture necessary variables.
- **Avoid referencing large objects:** Helps prevent memory leaks.
- **Understand `this` context:** Arrow functions don’t have their own `this`, which can be beneficial inside closures.
- **Use closures for privacy:** Protect variables from external access.
- **Be cautious with closures in loops:** Always use `let` for block scope.

---

## Summary

| Concept               | Description                                      |
|----------------------|--------------------------------------------------|
| **Lexical Scope**    | Determines variable access based on code location |
| **Closure**          | Function that remembers outer scope variables     |
| **Use Cases**        | Data privacy, function factories, memoization     |
| **Common Pitfalls**  | Memory leaks, loop variable capture issues        |
| **Best Practices**   | Limit closure scope, avoid large object references|

---

Now that you understand **closures and lexical scope**, move on to **[Prototypes and Inheritance](2-prototypes-and-inheritance.md)** to explore how JavaScript handles object inheritance and prototype chains!

