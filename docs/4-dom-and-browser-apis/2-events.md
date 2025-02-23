# JavaScript Events (Bubbling, Custom Events)

JavaScript **events** are essential for creating interactive web applications. Understanding how events work, propagate, and can be customized is critical for developing dynamic user experiences.

---

## 📚 Table of Contents

1. [Introduction to Events](#introduction-to-events)  
2. [Adding and Removing Event Listeners](#adding-and-removing-event-listeners)  
3. [Event Propagation: Bubbling and Capturing](#event-propagation-bubbling-and-capturing)  
4. [Event Delegation](#event-delegation)  
5. [Creating and Dispatching Custom Events](#creating-and-dispatching-custom-events)  
6. [Debouncing and Throttling Events](#debouncing-and-throttling-events)  
7. [Best Practices for Event Handling](#best-practices-for-event-handling)  
8. [Common Pitfalls](#common-pitfalls)  
9. [Summary](#summary)  

---

## 🌟 1. Introduction to Events

Events represent actions or occurrences (e.g., clicks, key presses, form submissions) that happen in the browser. JavaScript responds to these events by executing code.

### 🔥 **Common Event Types:**
- **Mouse events:** `click`, `dblclick`, `mouseenter`, `mouseleave`
- **Keyboard events:** `keydown`, `keyup`, `keypress`
- **Form events:** `submit`, `change`, `input`
- **Window events:** `load`, `resize`, `scroll`

---

## 🛠️ 2. Adding and Removing Event Listeners

### 1. **Adding Event Listeners**
```js
const button = document.querySelector("button");
button.addEventListener("click", () => {
  console.log("Button clicked!");
});
```

### 2. **Removing Event Listeners**
```js
function handleClick() {
  console.log("Clicked!");
}

button.addEventListener("click", handleClick);

// Later, remove the listener
button.removeEventListener("click", handleClick);
```

---

## 🔄 3. Event Propagation: Bubbling and Capturing

### **Event Propagation Phases:**
1. **Capturing Phase:** Event travels from the root to the target element.
2. **Target Phase:** Event reaches the target element.
3. **Bubbling Phase:** Event bubbles up from the target to the root.

### Example:
```js
const outer = document.getElementById("outer");
const inner = document.getElementById("inner");

outer.addEventListener("click", () => console.log("Outer clicked (bubbling)"));
inner.addEventListener("click", () => console.log("Inner clicked"));
```

### Capturing Mode Example:
```js
outer.addEventListener("click", () => console.log("Captured at outer"), true);
```

---

## 🎯 4. Event Delegation

**Event delegation** leverages **bubbling** to handle events efficiently.

### Example:
```js
const list = document.getElementById("list");

list.addEventListener("click", (event) => {
  if (event.target.tagName === "LI") {
    console.log(`Item clicked: ${event.target.textContent}`);
  }
});
```

**✨ Why Use Event Delegation?**
- Fewer event listeners.
- Handles dynamically added elements.

---

## 🧩 5. Creating and Dispatching Custom Events

Custom events enable communication between components.

### Creating a Custom Event:
```js
const customEvent = new CustomEvent("userLogin", {
  detail: { username: "Alice" }
});

document.dispatchEvent(customEvent);
```

### Listening for Custom Events:
```js
document.addEventListener("userLogin", (event) => {
  console.log(`Welcome, ${event.detail.username}!`);
});
```

---

## ⏳ 6. Debouncing and Throttling Events

### 1. **Debouncing:** Delays execution until after a specified time since the last event.
```js
function debounce(func, delay) {
  let timer;
  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => func.apply(this, args), delay);
  };
}

window.addEventListener("resize", debounce(() => {
  console.log("Window resized!");
}, 300));
```

### 2. **Throttling:** Ensures the function executes at most once in a specified period.
```js
function throttle(func, limit) {
  let inThrottle;
  return function (...args) {
    if (!inThrottle) {
      func.apply(this, args);
      inThrottle = true;
      setTimeout(() => (inThrottle = false), limit);
    }
  };
}

window.addEventListener("scroll", throttle(() => {
  console.log("Scrolling...");
}, 500));
```

---

## 💡 7. Best Practices for Event Handling

- ✅ **Use event delegation** for dynamic lists.
- ✅ **Detach unused event listeners** to prevent memory leaks.
- ✅ **Debounce high-frequency events** (e.g., `resize`, `input`).
- ✅ **Pass `{ passive: true }`** for scroll listeners to improve performance.
- ✅ **Stop event propagation cautiously** (`event.stopPropagation()`).

---

## ⚠️ 8. Common Pitfalls

- ❌ **Memory leaks** from unremoved listeners.
- ❌ **Overusing `stopPropagation()`**, which can break event chains.
- ❌ **Performance bottlenecks** from heavy operations inside event handlers.
- ❌ **Ignoring passive event listeners**, impacting scroll performance.

### 🔒 **Example (Avoid Memory Leaks):**
```js
const button = document.querySelector("button");

function handleClick() {
  console.log("Clicked!");
}

button.addEventListener("click", handleClick);

// Proper removal
button.removeEventListener("click", handleClick);
```

---

## 📌 9. Summary

| Concept                  | Method/Property              | Example Usage                  |
|--------------------------|------------------------------|--------------------------------|
| **Add Event Listener**   | `addEventListener()`         | `element.addEventListener("click", handler)`|
| **Remove Event Listener**| `removeEventListener()`      | `element.removeEventListener("click", handler)`|
| **Event Propagation**    | Bubbling/Capturing Phases    | `addEventListener("click", handler, true)`|
| **Event Delegation**     | Parent listener for children | `parent.addEventListener("click", handler)`|
| **Custom Events**        | `CustomEvent` & `dispatchEvent()`| `new CustomEvent("type", { detail: {} })`|
| **Debounce Function**    | Controlled event firing      | `debounce(handler, delay)`     |
| **Throttle Function**    | Limited event execution rate | `throttle(handler, limit)`     |

---

Understanding and mastering **JavaScript events**, from basic listeners to advanced propagation and custom events, empowers you to create **dynamic**, **responsive**, and **high-performance** web applications. 🚀✨

