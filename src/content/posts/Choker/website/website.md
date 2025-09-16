---
title: How Websites Work
published: 2025-09-07
author: 'Choker'
description: Introduction to how websites are created and a walkthrough of basic web technologies and security concepts.
image: 'https://tryhackme-images.s3.amazonaws.com/room-icons/66704dd0e54a1f39bff7b1a1-1735573671043'
tags: ["Web", "HTML", "JavaScript", "Security"]
category: 'Choker'
draft: false
---

## 1. How Websites Work

- When a user visits a website, their browser (client) sends an HTTP/HTTPS request to a web server.
- The server processes the request and returns responses (HTML, CSS, JS, images, etc.) that the browser renders.
- Websites consist of:
  - **Front End (Client-Side)**: HTML, CSS, JavaScript displayed in the browser.
  - **Back End (Server-Side)**: Server logic, databases, authentication, APIs.

---

## 2. HTML

- HTML defines the structure of web pages.
- Basic elements:
  - `<!DOCTYPE html>`, `<html>`, `<head>`, `<body>`
  - `<h1> - <h6>`, `<p>`, `<a>`, `<img>`, `<form>`
- Attributes: `id`, `class`, `src`, `href`, `alt`

**Hands-on HTML Tasks:**
1. Fix a broken cat image → **Flag**: `HTMLHERO`
2. Add a dog image → **Flag**: `DOGHTML`

---

## 3. CSS

- Controls page layout and style.
- Can be included:
  - External: `<link rel="stylesheet" href="styles.css">`
  - Embedded: `<style> ... </style>`
  - Inline: `<div style="color:red;">`

---

## 4. JavaScript

- Adds interactivity and dynamic behavior.
- Modify DOM:
  document.getElementById('demo').innerText = 'Hack the Planet';

- Event handling:
  <button id="btn">Click</button>
  <script>
  document.getElementById('btn').addEventListener('click', () => {
    alert('Button clicked');
  });
  </script>

**Tasks:**
1. Change text of element with `id="demo"` → **Flag**: `JSISFUN`
2. Add a clickable button (practice)

---

## 5. Sensitive Data Exposure

- Developers sometimes leave secrets in front-end code (comments, JS variables).
- Inspect page source to find hidden password → **Flag**: `testpasswd`

---

## 6. HTML Injection

- Occurs when user input is rendered as HTML without sanitization.
- Example injection:
  <a href="http://hacker.com">malicious</a>
- **Flag**: `HTML_INJ3CTI0N`

---

## 7. Forms, Authentication, Sessions

- Forms submit data via GET/POST.
- Servers use cookies (`Set-Cookie`) to maintain sessions.
  <form action="/login" method="POST">
    <input name="username" />
    <input name="password" type="password" />
    <button type="submit">Login</button>
  </form>

---

## 8. Developer Tools

- Inspect DOM and CSS.
- Monitor network requests/responses.
- Test JavaScript interactions.
- View source to locate hidden flags or comments.

---

## 9. Example Flags / Lab Tasks

- Hidden values in page source → `testpasswd`
- Fix broken HTML/CSS → `HTMLHERO`, `DOGHTML`
- Manipulate elements via JS → `JSISFUN`
- Inject HTML → `HTML_INJ3CTI0N`
- Identify front-end/back-end components → `Front End`

---

## 10. Summary Table

| Section                | Key Takeaway                                          | Example Flag/Task      |
|------------------------|-------------------------------------------------------|------------------------|
| How Websites Work      | Client-server flow, DNS, TCP/TLS, HTTP(S)           | `Front End`            |
| HTML                   | Structure of pages                                    | `HTMLHERO`, `DOGHTML`  |
| CSS                    | Presentation and layout                               | (practice)             |
| JavaScript             | Interactivity and DOM manipulation                    | `JSISFUN`              |
| Sensitive Data         | Hidden secrets may exist in front-end code           | `testpasswd`           |
| HTML Injection         | Risk of unsanitized input                             | `HTML_INJ3CTI0N`       |
| Developer Tools        | Inspect and debug DOM, network, JS                    | (practice)             |

---

## 11. Practice / Finishing

- Inspect page source using "View Page Source".
- Use DevTools → Network tab for requests and responses.
- Modify HTML/JS in console to test interactions.
