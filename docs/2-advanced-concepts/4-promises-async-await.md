# Promises and Async/Await in JavaScript (Microtask Queue)

Asynchronous programming is vital for modern JavaScript applications, especially when dealing with network requests, file operations, or any time-consuming tasks. **Promises** and **`async/await`** simplify handling asynchronous operations. In this guide, we'll explore:

## Table of Contents

1. [Introduction to Asynchronous JavaScript](#introduction-to-asynchronous-javascript)  
2. [Understanding Promises](#understanding-promises)  
3. [Promise Instance Methods (`then`, `catch`, `finally`)](#promise-instance-methods)  
4. [Promise Static Methods (All Available Functions)](#promise-static-methods)  
5. [Chaining Promises](#chaining-promises)  
6. [Error Handling in Promises](#error-handling-in-promises)  
7. [Async/Await](#asyncawait)  
8. [Understanding the Microtask Queue](#understanding-the-microtask-queue)  
9. [Best Practices and Common Pitfalls](#best-practices-and-common-pitfalls)  

---

## Introduction to Asynchronous JavaScript

JavaScript is **single-threaded**, meaning it can execute one operation at a time. Asynchronous programming allows tasks like network requests or timers to run **without blocking** the main thread.

### Traditional Callbacks:
```js
setTimeout(() => {
    console.log("Task completed!");
}, 2000);
```

**Problem:** Callback hell when dealing with multiple asynchronous operations.

---

## Understanding Promises

A **Promise** represents the **eventual completion** or **failure** of an asynchronous operation.

### States of a Promise:
- **Pending:** Initial state, neither fulfilled nor rejected.
- **Fulfilled:** Operation completed successfully.
- **Rejected:** Operation failed.

### Creating a Promise:
```js
const fetchData = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve("Data fetched successfully!");
    }, 2000);
});

fetchData.then(data => console.log(data));
```

---

## Promise Instance Methods

### 1. `then()` - Handles successful resolution.
```js
fetchData.then(data => console.log(data));
```

### 2. `catch()` - Handles errors.
```js
fetchData
    .then(data => console.log(data))
    .catch(error => console.error("Error:", error));
```

### 3. `finally()` - Runs after promise settles (fulfilled or rejected).
```js
fetchData
    .then(data => console.log(data))
    .catch(error => console.error("Error:", error))
    .finally(() => console.log("Operation completed."));
```

---

## Promise Static Methods (All Available Functions)

JavaScript provides several **static methods** on the `Promise` constructor for handling multiple asynchronous operations:

### 1. `Promise.resolve(value)`
Returns a promise resolved with the given value.
```js
Promise.resolve("Resolved!").then(console.log); // "Resolved!"
```

### 2. `Promise.reject(reason)`
Returns a promise rejected with the given reason.
```js
Promise.reject("Error occurred").catch(console.error); // "Error occurred"
```

### 3. `Promise.all(iterable)`
Waits for all promises to resolve or any to reject.
```js
Promise.all([
    Promise.resolve("One"),
    Promise.resolve("Two")
]).then(console.log); // ["One", "Two"]
```

### 4. `Promise.allSettled(iterable)`
Waits for all promises to settle (fulfilled or rejected) and returns their results.
```js
Promise.allSettled([
    Promise.resolve("Success"),
    Promise.reject("Failure")
]).then(console.log);
```

### 5. `Promise.race(iterable)`
Resolves or rejects as soon as one of the promises settles.
```js
Promise.race([
    new Promise(resolve => setTimeout(resolve, 100, "First")),
    new Promise(resolve => setTimeout(resolve, 200, "Second"))
]).then(console.log); // "First"
```

### 6. `Promise.any(iterable)`
Resolves as soon as **any** promise is fulfilled; rejects if **all** promises are rejected.
```js
Promise.any([
    Promise.reject("Fail 1"),
    Promise.resolve("Success"),
    Promise.reject("Fail 2")
]).then(console.log); // "Success"
```

### 7. `Promise.withResolvers()` *(Stage 3 Proposal)*
Creates a promise with explicit `resolve` and `reject` functions.
```js
const { promise, resolve, reject } = Promise.withResolvers();
resolve("Manually resolved!");
promise.then(console.log); // "Manually resolved!"
```

---

## Chaining Promises

Promises can be **chained** to execute multiple asynchronous operations in sequence.

```js
fetchData
    .then(data => {
        console.log(data);
        return "Processing data...";
    })
    .then(processed => console.log(processed))
    .catch(error => console.error(error));
```

---

## Error Handling in Promises

### Catching Errors in Chains:
```js
fetchData
    .then(data => {
        throw new Error("Something went wrong!");
    })
    .catch(error => console.error("Caught Error:", error));
```

### Handling Multiple Promises:
```js
Promise.all([
    Promise.resolve("Result 1"),
    Promise.resolve("Result 2")
]).then(results => console.log(results));
```

---

## Async/Await

**`async`** and **`await`** provide a more readable way to work with Promises.

### Example:
```js
async function fetchDataAsync() {
    try {
        const data = await fetchData;
        console.log(data);
    } catch (error) {
        console.error("Error:", error);
    } finally {
        console.log("Fetch attempt finished.");
    }
}

fetchDataAsync();
```

**Key Points:**
- `await` can only be used inside `async` functions.
- `async` functions **always return a promise**.

---

## Understanding the Microtask Queue

The **Microtask Queue** handles tasks that should execute **immediately after** the current operation but **before** the next event loop cycle.

### Example:
```js
console.log("Start");

Promise.resolve().then(() => console.log("Microtask"));

console.log("End");

// Output:
// Start
// End
// Microtask
```

**Key Insight:** Microtasks have **higher priority** than macrotasks (`setTimeout`, `setInterval`).

---

## Best Practices and Common Pitfalls

### ✅ Best Practices
- Always handle promise rejections using `catch` or `try-catch` with `async/await`.
- Use `Promise.all` for running multiple promises in parallel.
- Prefer `async/await` for better readability and error handling.
- Use `finally()` for cleanup tasks.
- Choose the appropriate static method (`all`, `allSettled`, `race`, `any`) based on the scenario.

### ❌ Common Pitfalls
- **Uncaught promise rejections:** Always use `catch` or `try-catch`.
- **Mixing callbacks and promises:** Stick to one pattern.
- **Ignoring microtask queue behavior:** Be mindful of execution order.
- **Using `Promise.race` without understanding behavior:** It resolves/rejects after the first settled promise, not necessarily the fastest.

---

## Summary

| Concept               | Description                                  | Example                |
|-----------------------|----------------------------------------------|------------------------|
| `Promise.resolve()`   | Creates a resolved promise                   | `Promise.resolve(value)`|
| `Promise.reject()`    | Creates a rejected promise                   | `Promise.reject(error)`|
| `Promise.all()`       | Waits for all to resolve or any to reject    | `Promise.all([...])`   |
| `Promise.allSettled()`| Waits for all to settle (fulfilled/rejected) | `Promise.allSettled([...])`|
| `Promise.race()`      | Resolves/rejects after first settled promise | `Promise.race([...])`  |
| `Promise.any()`       | Resolves after first fulfilled promise       | `Promise.any([...])`   |
| `Promise.withResolvers()` | Provides explicit resolve/reject functions| `Promise.withResolvers()`|
| `then()`              | Handles resolved promise                     | `promise.then(fn)`     |
| `catch()`             | Handles rejected promise                     | `promise.catch(fn)`    |
| `finally()`           | Runs after promise settles                   | `promise.finally(fn)`  |
| `async/await`         | Syntactic sugar for promises                 | `await promise`        |
| **Microtask Queue**   | Executes before next event loop              | `Promise.resolve()`    |

---

Now that you've mastered **Promises and Async/Await**, proceed to **[Iterators and Generators](5-iterators-generators.md)** to learn how JavaScript handles complex data flows and iteration patterns!