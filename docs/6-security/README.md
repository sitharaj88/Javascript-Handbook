# Security in JavaScript Applications

Ensuring robust **security** in web applications is critical for protecting user data, preventing vulnerabilities, and maintaining trust. This section explores essential web security topics, including XSS, CSRF, Content Security Policy (CSP), and sandboxing techniques.

---

## 📚 Table of Contents

1. [XSS & CSRF: Understanding and Prevention](1-xss-csrf.md)  
2. [Content Security Policy (CSP)](2-csp.md)  
3. [Sandboxing Techniques (iframes, postMessage)](3-sandboxing.md)  

---

## 🔒 1. XSS & CSRF: Understanding and Prevention

Explore **Cross-Site Scripting (XSS)** and **Cross-Site Request Forgery (CSRF)**—two of the most common web vulnerabilities—and how to prevent them.

### ⚡ **Key Concepts:**
- **XSS:** Malicious scripts injected into trusted websites.
- **CSRF:** Unauthorized actions performed by authenticated users.
- **Prevention Techniques:**
  - Input validation and output encoding.
  - Using `SameSite` cookies for CSRF protection.

🔗 **[Explore XSS & CSRF »](1-xss-csrf.md)**

---

## 🛡️ 2. Content Security Policy (CSP)

**CSP** is a powerful tool that prevents XSS attacks by controlling resources the browser is allowed to load.

### 🛠️ **Key Topics:**
- Defining CSP headers.
- Restricting inline scripts and dynamic code execution.
- Mitigating XSS risks by controlling third-party scripts.

🔗 **[Learn More About CSP »](2-csp.md)**

---

## 🏗️ 3. Sandboxing Techniques (iframes, postMessage)

Sandboxing isolates untrusted code, ensuring it cannot affect the host application.

### ✨ **Key Concepts:**
- **iframes with sandbox attributes:** Restrict access to certain APIs.
- **postMessage:** Secure cross-origin communication.
- **Web Workers:** Execute code in background threads securely.

🔗 **[Explore Sandboxing Techniques »](3-sandboxing.md)**

---

## 🚀 What's Next?

After mastering **security fundamentals**, continue exploring:

- ⚡ **[Tooling Ecosystem](../7-tooling-ecosystem/README.md)** – Learn about development tools that enhance application performance and security.
- 🏃 **[Performance Optimization](../5-performance-optimization/README.md)** – Explore techniques to build high-performance web applications.

By implementing these **security measures**, developers can protect web applications from common vulnerabilities, ensuring **user safety** and **data integrity**. 🛡️✨

