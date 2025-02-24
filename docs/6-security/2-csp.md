# Content Security Policy (CSP)

A **Content Security Policy (CSP)** is a critical layer of security that helps prevent cross-site scripting (XSS), clickjacking, and other code injection attacks. By defining a CSP, developers control which resources the browser can load, adding a robust defense against malicious exploits.

---

## 📚 Table of Contents

1. [Introduction to CSP](#introduction-to-csp)  
2. [Why CSP Matters](#why-csp-matters)  
3. [CSP Directives Explained](#csp-directives-explained)  
4. [Implementing CSP](#implementing-csp)  
5. [CSP Reporting and Monitoring](#csp-reporting-and-monitoring)  
6. [Best Practices for CSP](#best-practices-for-csp)  
7. [Common Pitfalls and How to Avoid Them](#common-pitfalls-and-how-to-avoid-them)  
8. [Summary](#summary)  

---

## 🌟 1. Introduction to CSP

**Content Security Policy (CSP)** defines approved sources of content that browsers can load, drastically reducing the risk of XSS attacks.

### 💡 **Key Benefits:**
- Blocks malicious scripts and inline code execution.
- Mitigates risks from third-party scripts.
- Enforces secure content delivery.

---

## 🔒 2. Why CSP Matters

- **Prevents XSS:** By disallowing unauthorized scripts, CSP eliminates many XSS vectors.
- **Secures Dynamic Content:** Restricts content injection vulnerabilities.
- **Improves Site Integrity:** Protects users from malicious redirects and code injections.

---

## 🧩 3. CSP Directives Explained

### 🛠️ **Essential CSP Directives:**

| Directive            | Description                           | Example Usage                    |
|----------------------|---------------------------------------|-----------------------------------|
| `default-src`        | Fallback for other directives          | `default-src 'self';`             |
| `script-src`         | Allowed script sources                 | `script-src 'self' https://cdn.com;` |
| `style-src`          | Allowed stylesheets                   | `style-src 'self' 'unsafe-inline';` |
| `img-src`            | Allowed image sources                 | `img-src *;`                      |
| `connect-src`        | Allowed AJAX, WebSocket connections   | `connect-src 'self' api.example.com;` |
| `font-src`           | Allowed font sources                  | `font-src 'self' fonts.example.com;` |
| `frame-src`          | Allowed iframes and frames            | `frame-src 'none';`               |
| `object-src`         | Allowed plugins and embedded objects  | `object-src 'none';`              |

---

## 🚀 4. Implementing CSP

### ✨ **1. Using Meta Tags:**
```html
<meta http-equiv="Content-Security-Policy" content="default-src 'self'; script-src 'self' https://cdn.com;">
```

### 🏃 **2. Using HTTP Headers:**
Setting CSP headers via the server:
```http
Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.com;
```

### ⚡ **3. Dynamic CSP Generation (Express.js Example):**
```js
app.use((req, res, next) => {
  res.setHeader("Content-Security-Policy", "default-src 'self'; script-src 'self' https://cdn.com;");
  next();
});
```

---

## 📡 5. CSP Reporting and Monitoring

CSP can report policy violations, aiding in proactive security management.

### 🔎 **Enable Reporting:**
```http
Content-Security-Policy-Report-Only: default-src 'self'; report-uri /csp-report-endpoint;
```

### 💬 **CSP Report Handler (Node.js Example):**
```js
app.post('/csp-report-endpoint', (req, res) => {
  console.log('CSP Violation:', req.body);
  res.status(204).end();
});
```

---

## 💡 6. Best Practices for CSP

- ✅ **Adopt a strict `default-src` policy**.
- ✅ **Avoid `unsafe-inline`** in `script-src`.
- ✅ **Use nonces or hashes** for inline scripts.
- ✅ **Serve all scripts over HTTPS**.
- ✅ **Test policies in `Report-Only` mode** before enforcement.

### 🔐 **Nonce Example:**
```html
<meta http-equiv="Content-Security-Policy" content="script-src 'nonce-abc123';">
<script nonce="abc123">console.log('Secure script');</script>
```

---

## ⚠️ 7. Common Pitfalls and How to Avoid Them

- ❌ **Overly permissive policies** (`*` wildcard usage).
- ❌ **Using `unsafe-inline`** without proper controls.
- ❌ **Ignoring third-party content risks**.
- ❌ **Not testing CSP with different browsers**.

### 🏃 **Debugging CSP Issues:**
- Use **browser dev tools** to inspect CSP violations.
- Monitor reports using **report-uri** endpoints.

---

## 📌 8. Summary

| Aspect               | Recommendation                  | Example                      |
|----------------------|----------------------------------|------------------------------|
| **Default Policy**   | `default-src 'self';`            | Restrict all external content|
| **Script Handling**  | Use `script-src 'self' https://cdn.com;` | Avoid inline scripts       |
| **Styles Handling**  | `style-src 'self';`              | Load styles from trusted sources|
| **Reporting**        | `report-uri /csp-report-endpoint;` | Monitor CSP violations       |
| **Advanced Security**| Use **nonces** or **hashes**     | Inline scripts with dynamic nonces|

---

Implementing a strong **Content Security Policy (CSP)** is essential for creating **secure**, **resilient**, and **trusted** web applications. By following these best practices, developers can significantly reduce vulnerabilities like **XSS** and protect applications from malicious exploits. 🛡️✨

