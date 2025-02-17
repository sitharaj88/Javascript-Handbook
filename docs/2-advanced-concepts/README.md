# Advanced JavaScript Concepts

## Table of Contents

1. [Closures and Lexical Scope](#closures-and-lexical-scope)
2. [Prototypes and Inheritance](#prototypes-and-inheritance)
3. [The `this` Keyword](#the-this-keyword)
4. [Promises and Async/Await](#promises-and-async-await)
5. [Iterators and Generators](#iterators-and-generators)
6. [Memory Management](#memory-management)

---

## Closures and Lexical Scope

### What is Lexical Scope?
Lexical scope means that a function can access variables from its **own scope**, **parent scope**, and the **global scope**, but not from child functions.

Example:
```js
function outer() {
    let outerVar = "I'm from outer";
    
    function inner() {
        console.log(outerVar); // Can access outerVar
    }
    
    inner();
}

outer();
```

### What is a Closure?
A closure is when an **inner function** remembers and can access variables from **its outer function**, even after the outer function has finished executing.

Example:
```js
function createCounter() {
    let count = 0;
    
    return function() {
        count++;
        console.log(count);
    };
}

const counter = createCounter();
counter(); // 1
counter(); // 2
```
Closures are often used in **data encapsulation** and **maintaining state** in JavaScript.

---

## Prototypes and Inheritance

### Understanding Prototypes
JavaScript uses **prototypal inheritance**, where objects inherit properties from their prototype.

Example:
```js
function Person(name) {
    this.name = name;
}

Person.prototype.greet = function() {
    console.log(`Hello, my name is ${this.name}`);
};

const person1 = new Person("Alice");
person1.greet(); // Hello, my name is Alice
```

### Class-Based Inheritance (ES6)
With ES6, JavaScript introduced `class` syntax for a more structured way to create objects.
```js
class Animal {
    constructor(name) {
        this.name = name;
    }
    speak() {
        console.log(`${this.name} makes a noise`);
    }
}

class Dog extends Animal {
    speak() {
        console.log(`${this.name} barks`);
    }
}

const dog = new Dog("Buddy");
dog.speak(); // Buddy barks
```

---

## The `this` Keyword

### Understanding `this`
`this` refers to the object that is executing the function.

Example:
```js
const user = {
    name: "Alice",
    greet() {
        console.log(`Hello, ${this.name}`);
    }
};
user.greet(); // Hello, Alice
```

### Arrow Functions and `this`
Arrow functions **do not have their own `this`**; they inherit it from their surrounding scope.
```js
const user = {
    name: "Alice",
    greet: () => {
        console.log(`Hello, ${this.name}`); // `this` is not bound correctly
    }
};
user.greet(); // Hello, undefined
```
**Fix:** Use a regular function inside an object.

---

## Promises and Async/Await

### What is a Promise?
A Promise is an object that represents **an asynchronous operation**.

Example:
```js
const fetchData = new Promise((resolve, reject) => {
    setTimeout(() => resolve("Data received"), 2000);
});

fetchData.then(data => console.log(data));
```

### Async/Await
Async/Await makes asynchronous code look synchronous.

Example:
```js
async function getData() {
    let data = await fetchData;
    console.log(data);
}

getData();
```

---

## Iterators and Generators

### What is an Iterator?
An **iterator** is an object that allows you to traverse a collection.

Example:
```js
const array = [1, 2, 3];
const iterator = array[Symbol.iterator]();

console.log(iterator.next()); // { value: 1, done: false }
console.log(iterator.next()); // { value: 2, done: false }
```

### What is a Generator?
A generator function can **pause and resume execution**.

Example:
```js
function* numberGenerator() {
    yield 1;
    yield 2;
    yield 3;
}

const gen = numberGenerator();
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
```

---

## Memory Management

### How JavaScript Handles Memory
JavaScript automatically allocates and frees memory using **Garbage Collection**.

### Avoiding Memory Leaks
1. **Unnecessary Global Variables**
   ```js
   var data = new Array(1000000); // Unused data can cause memory leaks
   ```
   
2. **Event Listeners Not Removed**
   ```js
   function attachListener() {
       let button = document.getElementById("btn");
       button.addEventListener("click", () => console.log("Clicked!"));
   }
   // Ensure to remove listeners when not needed
   button.removeEventListener("click", callback);
   ```

---

