# Type Coercion in JavaScript

Type coercion is JavaScript’s ability to **automatically convert data types** during operations. This behavior can lead to **unexpected results** if not properly understood. This guide covers:

- **Implicit Type Coercion** (Automatic conversion)
- **Explicit Type Conversion** (Manual conversion)
- **Truthy & Falsy Values**
- **`==` vs. `===` Comparisons**
- **Common Pitfalls and Best Practices**

---

## Implicit Type Coercion

JavaScript automatically converts one type to another when required in operations.

### 1. String Coercion (Concatenation)
```js
console.log("5" + 5); // "55" (Number converts to string)
console.log("Hello " + true); // "Hello true"
console.log("Value: " + null); // "Value: null"
```
**Rule:** If one operand is a `string`, JavaScript converts the other to a `string` and concatenates.

### 2. Numeric Coercion (Mathematical Operations)
```js
console.log("5" - 2); // 3 (String converted to Number)
console.log("10" * "2"); // 20 (Both converted to Numbers)
console.log("100" / "5"); // 20 (Both converted to Numbers)
```
**Rule:** For non-addition (`+`) operations, JavaScript converts strings to numbers.

### 3. Boolean Coercion
```js
console.log("hello" == true); // false ("hello" converts to true, but 1 != true)
console.log(1 == true); // true (1 converts to true)
console.log(0 == false); // true (0 converts to false)
```
**Rule:** `1`, `"non-empty strings"`, and objects convert to `true`. `0`, `""`, `null`, `undefined`, and `NaN` convert to `false`.

---

## Explicit Type Conversion

Manually converting values using built-in functions.

### 1. String Conversion
```js
console.log(String(123)); // "123"
console.log(String(true)); // "true"
console.log((123).toString()); // "123"
```

### 2. Number Conversion
```js
console.log(Number("456")); // 456
console.log(Number("text")); // NaN
console.log(parseInt("42px")); // 42
console.log(parseFloat("3.14cm")); // 3.14
```

### 3. Boolean Conversion
```js
console.log(Boolean(1)); // true
console.log(Boolean(0)); // false
console.log(Boolean("")); // false
console.log(Boolean("Hello")); // true
```

---

## Truthy & Falsy Values

### Falsy Values
These values convert to `false` when coerced into a Boolean:
```js
console.log(Boolean(0));      // false
console.log(Boolean(""));    // false
console.log(Boolean(null));  // false
console.log(Boolean(undefined)); // false
console.log(Boolean(NaN));   // false
```

### Truthy Values
All values **except** falsy ones are truthy:
```js
console.log(Boolean(1));      // true
console.log(Boolean("Hello")); // true
console.log(Boolean([]));     // true
console.log(Boolean({}));     // true
```

**Edge Case:**
```js
console.log(Boolean("false")); // true (Non-empty string is truthy!)
```

---

## `==` vs. `===` Comparisons

### 1. Loose Equality (`==`)
Allows **type coercion** before comparison.
```js
console.log(5 == "5"); // true (String converted to Number)
console.log(0 == false); // true (0 is falsy)
console.log(null == undefined); // true (special case)
```

### 2. Strict Equality (`===`)
Compares **values and types**, without conversion.
```js
console.log(5 === "5"); // false (Different types)
console.log(0 === false); // false (Different types)
console.log(null === undefined); // false (Different types)
```
**Best Practice:** Prefer `===` to avoid unexpected type coercion.

---

## Common Pitfalls

### 1. Unexpected `null` and `undefined` behavior
```js
console.log(null == 0); // false
console.log(null >= 0); // true (Confusing!)
```
**Explanation:** `null` and `undefined` behave inconsistently in comparisons.

### 2. Using `+` with non-string values
```js
console.log([] + []); // "" (Arrays convert to empty strings)
console.log([] + {}); // "[object Object]"
```

### 3. Misuse of Falsy Values in Conditions
```js
let value = "0";
if (value) {
    console.log("Truthy");
} else {
    console.log("Falsy");
} // "Truthy" ("0" is a non-empty string)
```

---

## Best Practices

- Use **explicit type conversion** when possible.
- Avoid `==`, prefer `===`.
- Be cautious with falsy values in conditions.
- **Check for `null` and `undefined` separately** to avoid surprises.

```js
if (value !== null && value !== undefined) {
    console.log("Value is defined");
}
```

---

## Summary

| Type Coercion | Example | Result |
|--------------|---------|--------|
| String Coercion | `"5" + 5` | "55" |
| Numeric Coercion | `"5" - 2` | 3 |
| Boolean Coercion | `Boolean("hello")` | true |
| Loose Equality (`==`) | `0 == false` | true |
| Strict Equality (`===`) | `0 === false` | false |

---

Next, continue to **[Functions in JavaScript](5-functions.md)** to explore how JavaScript handles function declarations, expressions, and IIFE!

