# Prototypes and Inheritance in JavaScript

JavaScript uses **prototypal inheritance**, a powerful feature that allows objects to inherit properties and methods from other objects. This concept is fundamental for building scalable applications and understanding how JavaScript works under the hood.

## Table of Contents

- [Prototypes and Inheritance in JavaScript](#prototypes-and-inheritance-in-javascript)
  - [Table of Contents](#table-of-contents)
  - [What is a Prototype?](#what-is-a-prototype)
    - [Example:](#example)
  - [Prototype Chain](#prototype-chain)
    - [Example:](#example-1)
  - [Prototypal Inheritance](#prototypal-inheritance)
    - [Example:](#example-2)
  - [Creating Objects with Prototypes](#creating-objects-with-prototypes)
    - [1. Using `Object.create()`:](#1-using-objectcreate)
    - [2. Manual Prototype Assignment:](#2-manual-prototype-assignment)
  - [ES6 Classes and Inheritance](#es6-classes-and-inheritance)
    - [Example:](#example-3)
  - [`Object.create()` and Inheritance](#objectcreate-and-inheritance)
    - [Example:](#example-4)
  - [Best Practices and Common Pitfalls](#best-practices-and-common-pitfalls)
    - [✅ Best Practices](#-best-practices)
    - [❌ Common Pitfalls](#-common-pitfalls)
  - [Summary](#summary)

---

## What is a Prototype?

Every JavaScript object has an internal link to another object called its **prototype**. When you try to access a property that does not exist in the current object, JavaScript automatically looks for it in the prototype.

### Example:
```js
const person = {
    greet() {
        console.log(`Hello, my name is ${this.name}`);
    }
};

const user = Object.create(person);
user.name = "Alice";
user.greet(); // "Hello, my name is Alice"
```

**Key Points:**
- The `__proto__` property (or `[[Prototype]]`) points to the prototype object.
- If a property is not found in the object, JavaScript searches the prototype chain.

---

## Prototype Chain

The **prototype chain** is a series of linked objects. JavaScript uses this chain to find properties and methods.

### Example:
```js
console.log(user.__proto__ === person); // true
console.log(person.__proto__ === Object.prototype); // true
```

**Key Points:**
- The top of the chain is `Object.prototype`.
- Accessing a non-existent property returns `undefined` after reaching the end of the chain.

---

## Prototypal Inheritance

Prototypal inheritance allows an object to inherit properties and methods from another object.

### Example:
```js
function Animal(name) {
    this.name = name;
}

Animal.prototype.speak = function() {
    console.log(`${this.name} makes a sound.`);
};

const dog = new Animal("Buddy");
dog.speak(); // "Buddy makes a sound."
```

**Key Points:**
- Functions have a `prototype` property that determines inheritance.
- The `new` keyword sets the prototype of the instance to the constructor's `prototype`.

---

## Creating Objects with Prototypes

### 1. Using `Object.create()`:
```js
const animal = {
    speak() {
        console.log(`${this.name} makes a sound.`);
    }
};

const cat = Object.create(animal);
cat.name = "Whiskers";
cat.speak(); // "Whiskers makes a sound."
```

### 2. Manual Prototype Assignment:
```js
function Car(make) {
    this.make = make;
}

Car.prototype.drive = function() {
    console.log(`${this.make} is driving.`);
};

const tesla = new Car("Tesla");
tesla.drive(); // "Tesla is driving."
```

---

## ES6 Classes and Inheritance

ES6 introduced `class` syntax, providing a cleaner way to implement inheritance.

### Example:
```js
class Animal {
    constructor(name) {
        this.name = name;
    }
    speak() {
        console.log(`${this.name} makes a sound.`);
    }
}

class Dog extends Animal {
    speak() {
        console.log(`${this.name} barks.`);
    }
}

const dog = new Dog("Rex");
dog.speak(); // "Rex barks."
```

**Key Points:**
- The `extends` keyword sets up inheritance.
- The `super()` function calls the constructor of the parent class.

---

## `Object.create()` and Inheritance

`Object.create()` creates a new object with a specified prototype.

### Example:
```js
const vehicle = {
    start() {
        console.log("Vehicle starting...");
    }
};

const car = Object.create(vehicle);
car.start(); // "Vehicle starting..."
```

**Use Cases:**
- Creating objects without constructor functions.
- Lightweight inheritance for simple structures.

---

## Best Practices and Common Pitfalls

### ✅ Best Practices
- Use **ES6 classes** for clarity and maintainability.
- Prefer **Object.create()** for lightweight object creation.
- Always use `super()` in subclass constructors.

### ❌ Common Pitfalls
- Confusing `prototype` with `__proto__`.
- Overwriting prototype objects instead of extending them.
- Forgetting to bind `this` in methods when needed.

```js
class Example {
    constructor() {
        this.message = "Hello";
    }
    greet() {
        console.log(this.message);
    }
}

const ex = new Example();
const greetFn = ex.greet;
greetFn(); // ❌ Undefined (this is not bound)

// ✅ Fix:
const boundGreet = ex.greet.bind(ex);
boundGreet(); // "Hello"
```

---

## Summary

| Concept                | Description                                  |
|------------------------|----------------------------------------------|
| **Prototype**          | Object from which properties are inherited   |
| **Prototype Chain**    | Linked chain of objects for property lookup  |
| **Prototypal Inheritance** | Inheritance through object prototypes     |
| **ES6 Classes**        | Cleaner syntax for object-oriented patterns  |
| **Object.create()**    | Creates a new object with a given prototype  |

---

Next, explore **[The `this` Keyword (Dynamic vs. Lexical Context)](3-this-keyword.md)** to understand how context impacts method execution and variable binding in JavaScript.

