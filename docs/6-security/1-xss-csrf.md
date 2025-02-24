# XSS & CSRF: Understanding and Prevention

Securing web applications from attacks like **Cross-Site Scripting (XSS)** and **Cross-Site Request Forgery (CSRF)** is fundamental for protecting user data and maintaining trust. This guide provides a **deep dive** into these vulnerabilities, how they work, and best practices for prevention.

---

## 📚 Table of Contents

1. [Introduction to XSS](#introduction-to-xss)  
2. [Types of XSS Attacks](#types-of-xss-attacks)  
3. [Preventing XSS Attacks](#preventing-xss-attacks)  
4. [Introduction to CSRF](#introduction-to-csrf)  
5. [How CSRF Attacks Work](#how-csrf-attacks-work)  
6. [Preventing CSRF Attacks](#preventing-csrf-attacks)  
7. [Best Practices for Securing Web Applications](#best-practices-for-securing-web-applications)  
8. [Common Pitfalls](#common-pitfalls)  
9. [Summary](#summary)  

---

## 🔒 1. Introduction to XSS

**Cross-Site Scripting (XSS)** occurs when malicious scripts are injected into trusted web pages. These scripts run in the context of the victim's browser, potentially stealing sensitive data, hijacking sessions, or redirecting users.

### 💡 **Why XSS is Dangerous:**
- Can steal cookies, session tokens, and credentials.
- Allows attackers to impersonate users.
- Can perform actions on behalf of users without their consent.

---

## ⚡ 2. Types of XSS Attacks

### 1. **Stored XSS (Persistent):**
Malicious scripts are permanently stored on the target server (e.g., in a database).

```html
<!-- Malicious script saved in comments section -->
<script>alert('Hacked!');</script>
```

### 2. **Reflected XSS:**
The malicious script is reflected off a web server (e.g., via a URL).

```html
https://example.com/search?q=<script>alert('XSS')</script>
```

### 3. **DOM-Based XSS:**
Occurs when client-side JavaScript manipulates the DOM without proper sanitization.

```js
const userInput = location.hash.substring(1);
document.getElementById("output").innerHTML = userInput; // Vulnerable
```

---

## 🛡️ 3. Preventing XSS Attacks

### ✅ **1. Input Validation**
Validate all user inputs using **whitelisting** where possible:
```js
if (!/^[a-zA-Z0-9]*$/.test(userInput)) {
  throw new Error("Invalid input");
}
```

### 🏃 **2. Output Encoding**
Escape data before rendering it on the page:
```js
function escapeHTML(str) {
  return str.replace(/&/g, "&amp;")
            .replace(/</g, "&lt;")
            .replace(/>/g, "&gt;")
            .replace(/"/g, "&quot;")
            .replace(/'/g, "&#039;");
}
```

### 🧩 **3. Use HTTP-Only Cookies**
Prevent JavaScript from accessing sensitive cookies:
```http
Set-Cookie: sessionId=abc123; HttpOnly; Secure; SameSite=Strict;
```

### 🎯 **4. Content Security Policy (CSP)**
Define a strict CSP to prevent the execution of unauthorized scripts:
```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self';">
```

---

## 🌐 4. Introduction to CSRF

**Cross-Site Request Forgery (CSRF)** tricks authenticated users into submitting requests unknowingly. This can result in unauthorized actions like fund transfers or profile changes.

### 💡 **Why CSRF is Dangerous:**
- Exploits user sessions to perform unauthorized actions.
- Does not require user credentials.
- Common in applications lacking proper request validation.

---

## ⚡ 5. How CSRF Attacks Work

### 🏴 **Example Attack:**
```html
<img src="https://bank.com/transfer?amount=1000&to=attacker" />
```
When a user is logged into `bank.com`, this image request triggers a fund transfer without the user's consent.

---

## 🛡️ 6. Preventing CSRF Attacks

### ✅ **1. CSRF Tokens**
Generate a unique CSRF token for each user session and validate it on the server:

**Server-Side:**
```js
app.post('/transfer', (req, res) => {
  if (req.body.csrfToken !== req.session.csrfToken) {
    return res.status(403).send("Forbidden");
  }
  // Process request
});
```

**Client-Side:**
```html
<input type="hidden" name="csrfToken" value="{{csrfToken}}" />
```

### 🏃 **2. SameSite Cookies**
Prevent cookies from being sent on cross-site requests:
```http
Set-Cookie: sessionId=abc123; SameSite=Strict;
```

### 🧩 **3. Double Submit Cookies**
Send the CSRF token both as a cookie and a request parameter, verifying that both match.

### 🔒 **4. Verify Referer Header**
Ensure that requests originate from the expected domain:
```js
if (req.headers.referer !== 'https://trusted.com/') {
  return res.status(403).send("Forbidden");
}
```

---

## 💡 7. Best Practices for Securing Web Applications

- ✅ **Sanitize all user inputs** to prevent injection attacks.
- ✅ **Apply strict CSP policies** to block unauthorized scripts.
- ✅ **Use HTTPS** to prevent man-in-the-middle (MITM) attacks.
- ✅ **Set secure cookie flags** (`HttpOnly`, `Secure`, `SameSite`).
- ✅ **Limit cross-origin requests** to trusted domains.

---

## ⚠️ 8. Common Pitfalls

- ❌ Trusting client-side validation alone.
- ❌ Storing sensitive data in localStorage (vulnerable to XSS).
- ❌ Allowing third-party scripts without proper validation.
- ❌ Ignoring proper session management.

---

## 📌 9. Summary

| Vulnerability        | Description                           | Prevention Techniques                 |
|----------------------|---------------------------------------|----------------------------------------|
| **XSS (Cross-Site Scripting)** | Injects malicious scripts into web pages | Input validation, CSP, output encoding |
| **CSRF (Cross-Site Request Forgery)** | Performs unauthorized actions via authenticated sessions | CSRF tokens, SameSite cookies, referer checks |

---

By understanding and implementing these **security best practices**, developers can significantly reduce the risk of **XSS** and **CSRF** attacks, ensuring **safe**, **reliable**, and **trustworthy** web applications. 🛡️✨

