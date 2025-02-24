# Node.js Core Concepts (Event Loop, Streams)

**Node.js** is a powerful runtime environment that allows developers to build scalable, high-performance server-side applications using JavaScript. At its core, Node.js leverages the **event loop**, **non-blocking I/O**, and **stream processing** to handle large numbers of simultaneous connections with high throughput.

---

## 📚 Table of Contents

- [Node.js Core Concepts (Event Loop, Streams)](#nodejs-core-concepts-event-loop-streams)
  - [📚 Table of Contents](#-table-of-contents)
  - [🌟 1. Introduction to Node.js](#-1-introduction-to-nodejs)
  - [🔄 2. Event Loop and Asynchronous Programming](#-2-event-loop-and-asynchronous-programming)
    - [🔥 **Phases of the Event Loop:**](#-phases-of-the-event-loop)
    - [⚡ **Timers, Microtasks, and Macrotasks:**](#-timers-microtasks-and-macrotasks)
    - [💡 **Practical Example of the Event Loop:**](#-practical-example-of-the-event-loop)
  - [🏗️ 3. Streams and Buffering](#️-3-streams-and-buffering)
    - [✨ **Types of Streams:**](#-types-of-streams)
    - [⚙️ **Working with Streams:**](#️-working-with-streams)
    - [🔗 **Piping Streams:**](#-piping-streams)
  - [📂 4. File System Operations](#-4-file-system-operations)
    - [📝 **Reading and Writing Files:**](#-reading-and-writing-files)
    - [🔄 **Stream-Based File Processing:**](#-stream-based-file-processing)
  - [💡 5. Best Practices for Node.js Development](#-5-best-practices-for-nodejs-development)
  - [⚠️ 6. Common Pitfalls](#️-6-common-pitfalls)
  - [📌 7. Summary](#-7-summary)

---

## 🌟 1. Introduction to Node.js

Node.js allows developers to use JavaScript for server-side programming. It uses the **V8 JavaScript engine** and offers:

- **Single-threaded architecture** with **event-driven** capabilities.
- **Non-blocking I/O operations** for high performance.
- A robust ecosystem through **npm**.

---

## 🔄 2. Event Loop and Asynchronous Programming

The **event loop** is the heart of Node.js, allowing asynchronous, non-blocking execution.

### 🔥 **Phases of the Event Loop:**
1. **Timers:** Executes callbacks scheduled by `setTimeout` and `setInterval`.
2. **Pending Callbacks:** Executes I/O callbacks.
3. **Idle, Prepare:** Internal operations.
4. **Poll:** Retrieves new I/O events.
5. **Check:** Executes `setImmediate()` callbacks.
6. **Close Callbacks:** Executes `close` events.

### ⚡ **Timers, Microtasks, and Macrotasks:**
```js
setTimeout(() => console.log("Timeout"), 0);
setImmediate(() => console.log("Immediate"));
Promise.resolve().then(() => console.log("Promise"));

// Output:
// Promise
// Timeout
// Immediate
```

### 💡 **Practical Example of the Event Loop:**
```js
const fs = require("fs");

fs.readFile("file.txt", () => console.log("File read"));
setTimeout(() => console.log("Timer 1"), 0);
Promise.resolve().then(() => console.log("Promise resolved"));
```

---

## 🏗️ 3. Streams and Buffering

Streams handle large data efficiently by processing data in **chunks** instead of loading entire data sets into memory.

### ✨ **Types of Streams:**
- **Readable:** Reading data (e.g., `fs.createReadStream`).
- **Writable:** Writing data (e.g., `fs.createWriteStream`).
- **Duplex:** Both read and write (e.g., TCP sockets).
- **Transform:** Modify data while reading/writing (e.g., compression).

### ⚙️ **Working with Streams:**
```js
const fs = require("fs");

const readable = fs.createReadStream("input.txt");
readable.on("data", (chunk) => console.log(`Received ${chunk.length} bytes`));
```

### 🔗 **Piping Streams:**
```js
const readable = fs.createReadStream("input.txt");
const writable = fs.createWriteStream("output.txt");
readable.pipe(writable);
```

---

## 📂 4. File System Operations

Node.js provides the **fs** module to handle file operations efficiently.

### 📝 **Reading and Writing Files:**
```js
const fs = require("fs");

// Reading a file
fs.readFile("input.txt", "utf8", (err, data) => {
  if (err) throw err;
  console.log(data);
});

// Writing to a file
fs.writeFile("output.txt", "Hello, Node.js!", (err) => {
  if (err) throw err;
  console.log("File written successfully!");
});
```

### 🔄 **Stream-Based File Processing:**
```js
const readable = fs.createReadStream("largefile.txt");
const writable = fs.createWriteStream("copy.txt");
readable.pipe(writable);
```

---

## 💡 5. Best Practices for Node.js Development

- ✅ **Avoid blocking the event loop** with synchronous operations.
- ✅ **Use streams** for handling large files.
- ✅ **Handle errors gracefully** with try-catch blocks and `.catch()`.
- ✅ **Utilize async/await** for cleaner asynchronous code.
- ✅ **Leverage environment variables** for configuration.

---

## ⚠️ 6. Common Pitfalls

- ❌ **Blocking operations:** Avoid `fs.readFileSync` in production.
- ❌ **Unhandled promise rejections:** Always handle `.catch()`.
- ❌ **Memory leaks:** Ensure streams and connections are closed.
- ❌ **Ignoring the event loop:** Misunderstanding async execution can cause bottlenecks.

---

## 📌 7. Summary

| Concept              | Description                      | Key APIs/Modules          |
|----------------------|----------------------------------|---------------------------|
| **Event Loop**       | Handles async execution           | `setTimeout`, `setImmediate`, Promises |
| **Streams**          | Efficient data processing         | `fs.createReadStream`, `pipe()` |
| **File Operations**  | Reading and writing files         | `fs.readFile`, `fs.writeFile` |
| **Async Patterns**   | Manage asynchronous logic         | `async/await`, Promises   |

---

By mastering these **Node.js core concepts**, developers can build **scalable**, **efficient**, and **robust** backend applications that handle high loads without sacrificing performance. 🚀✨

