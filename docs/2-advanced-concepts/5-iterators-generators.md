# Iterators and Generators in JavaScript

Iterators and generators are powerful tools in JavaScript that simplify the handling of **sequences**, **asynchronous flows**, and **custom data structures**. This guide provides a deep dive into these concepts, covering everything from basic definitions to advanced use cases.

---

## Table of Contents

1. [Introduction to Iterators](#introduction-to-iterators)  
2. [Creating Custom Iterators](#creating-custom-iterators)  
3. [Built-in Iterables in JavaScript](#built-in-iterables-in-javascript)  
4. [Generator Functions: Basics](#generator-functions-basics)  
5. [Advanced Generator Concepts](#advanced-generator-concepts)  
6. [Asynchronous Generators and `for await...of`](#asynchronous-generators-and-for-awaitof)  
7. [Use Cases and Practical Examples](#use-cases-and-practical-examples)  
8. [Common Pitfalls and Best Practices](#common-pitfalls-and-best-practices)  
9. [Summary](#summary)  

---

## Introduction to Iterators

An **iterator** is an object that provides a **`next()`** method, which returns:
- **value**: The next value in the sequence.
- **done**: A boolean indicating whether the sequence is finished.

### Basic Iterator Example:
```js
const iterable = [1, 2, 3];
const iterator = iterable[Symbol.iterator]();

console.log(iterator.next()); // { value: 1, done: false }
console.log(iterator.next()); // { value: 2, done: false }
console.log(iterator.next()); // { value: 3, done: false }
console.log(iterator.next()); // { value: undefined, done: true }
```

---

## Creating Custom Iterators

You can create custom iterators by implementing the `Symbol.iterator` method.

### Custom Iterator Example:
```js
const customIterable = {
    data: ["a", "b", "c"],
    [Symbol.iterator]() {
        let index = 0;
        const { data } = this;
        return {
            next() {
                if (index < data.length) {
                    return { value: data[index++], done: false };
                } else {
                    return { done: true };
                }
            }
        };
    }
};

for (const value of customIterable) {
    console.log(value); // "a", "b", "c"
}
```

---

## Built-in Iterables in JavaScript

JavaScript has several built-in iterable objects:

- **Arrays:** `[1, 2, 3]`
- **Strings:** "Hello"
- **Maps:** `new Map()`
- **Sets:** `new Set()`
- **Arguments Object** (within functions)
- **NodeList:** Returned by DOM queries

These objects work seamlessly with `for...of` loops and spread syntax.

### Example with `for...of`:
```js
for (const char of "Hello") {
    console.log(char); // H e l l o
}
```

---

## Generator Functions: Basics

**Generator functions** provide a simple way to implement iterators. They are declared using `function*` and use the `yield` keyword.

### Basic Generator Example:
```js
function* generateNumbers() {
    yield 1;
    yield 2;
    yield 3;
}

const generator = generateNumbers();
console.log(generator.next()); // { value: 1, done: false }
console.log(generator.next()); // { value: 2, done: false }
console.log(generator.next()); // { value: 3, done: false }
console.log(generator.next()); // { value: undefined, done: true }
```

### `for...of` with Generators:
```js
for (const num of generateNumbers()) {
    console.log(num); // 1 2 3
}
```

---

## Advanced Generator Concepts

### 1. Passing Arguments to Generators:
```js
function* greetGenerator() {
    const name = yield "What's your name?";
    yield `Hello, ${name}!`;
}

const greeter = greetGenerator();
console.log(greeter.next().value); // "What's your name?"
console.log(greeter.next("Alice").value); // "Hello, Alice!"
```

### 2. Infinite Generators:
```js
function* infiniteGenerator() {
    let i = 0;
    while (true) {
        yield i++;
    }
}

const infinite = infiniteGenerator();
console.log(infinite.next().value); // 0
console.log(infinite.next().value); // 1
```

### 3. Generator Delegation:
```js
function* numbers() {
    yield 1;
    yield 2;
}

function* combinedGenerator() {
    yield* numbers();
    yield 3;
}

for (const value of combinedGenerator()) {
    console.log(value); // 1, 2, 3
}
```

---

## Asynchronous Generators and `for await...of`

Asynchronous generators return an **AsyncIterator**, using `async function*`.

### Example:
```js
async function* asyncGenerator() {
    yield await Promise.resolve("Hello");
    yield await Promise.resolve("World");
}

(async () => {
    for await (const word of asyncGenerator()) {
        console.log(word); // Hello, World
    }
})();
```

---

## Use Cases and Practical Examples

### 1. **Data Streaming:** Efficiently processing large data sets.

### 2. **State Machines:** Simplify state management by pausing and resuming execution.

### 3. **Lazy Evaluation:** Generate values on demand, improving performance.

### 4. **Asynchronous Iteration:** Handling paginated API responses.

```js
async function* fetchPaginatedData(pages) {
    for (const page of pages) {
        yield await fetch(page).then(res => res.json());
    }
}
```

---

## Common Pitfalls and Best Practices

### ✅ Best Practices:
- Use `for...of` for synchronous iteration.
- Use `for await...of` for asynchronous data streams.
- Use generators for lazy computations and infinite sequences.

### ❌ Common Pitfalls:
- Forgetting `*` in `function*` for generators.
- Misusing `next()` without handling `done`.
- Overusing generators when simpler iteration would suffice.

---

## Summary

| Concept               | Description                                    | Example               |
|-----------------------|------------------------------------------------|-----------------------|
| **Iterator**          | Object with a `next()` method                  | `[Symbol.iterator]()` |
| **Generator**         | Function that yields values lazily             | `function* () {}`     |
| **Async Generator**   | Generator that yields promises                 | `async function* () {}`|
| **`for...of`**        | Iterates over iterable objects                 | `for (x of arr) {}`   |
| **`for await...of`**  | Iterates over async iterable objects           | `for await (x of arr) {}`|
| **Yield**             | Pauses execution, returns value                | `yield value;`        |
| **Yield***            | Delegates generator to another generator       | `yield* otherGen();`  |

---

Now that you’ve explored **Iterators and Generators**, proceed to **[Memory Management (GC, Memory Leaks)](6-memory-management.md)** to understand how JavaScript optimizes memory usage and prevents leaks.

