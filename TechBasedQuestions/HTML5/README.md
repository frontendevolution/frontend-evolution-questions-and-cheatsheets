# 📘 HTML Document Structure — Interview Questions

A curated set of **deep, interview-level questions** on HTML Document Structure.  
Click on each question to reveal the answer 👇

---

## ❓ Questions & Answers

<details>
<summary><strong>1. What is the difference between the &lt;html&gt;, &lt;head&gt;, and &lt;body&gt; elements — and what happens if you omit them?</strong></summary>

These three elements form the skeleton of every HTML document:

- `<html>` → Root element  
- `<head>` → Metadata (not rendered)  
- `<body>` → Visible content  

Browsers are forgiving — if omitted, they are implicitly created by the HTML parser.

⚠️ But relying on this:
- Breaks best practices  
- Can confuse linters, validators, and screen readers  
- Risks future compatibility issues  

</details>

---

<details>
<summary><strong>2. Why does &lt;meta charset='UTF-8'&gt; need to appear within the first 1024 bytes of the document?</strong></summary>

Browsers start parsing before knowing encoding, so they guess based on the first ~1024 bytes.

If charset appears too late:
- Text may render incorrectly  
- Security risks (e.g., UTF-7 attacks)  

✅ Best practice:
Place it as the **first child of `<head>`**

</details>

---

<details>
<summary><strong>3. What does the &lt;!DOCTYPE html&gt; declaration actually do in a modern browser?</strong></summary>

It’s a **mode switch**, not a version declaration.

- ✅ With it → **Standards mode**  
- ❌ Without it → **Quirks mode** (old browser behavior)

Impacts:
- CSS box model  
- Layout rendering  
- Consistency across browsers  

</details>

---

<details>
<summary><strong>4. What is the &lt;base&gt; element and when would you actually use it?</strong></summary>

Sets a **default URL or target** for all relative paths.

📌 Useful in:
- Email templates  
- Static sites  
- Apps in subdirectories  

⚠️ Caveats:
- Only one `<base>` allowed  
- Affects ALL links, images, forms  
- Misuse = hard-to-debug issues  

</details>

---

<details>
<summary><strong>5. What is the difference between a 'render-blocking' and a 'parser-blocking' resource?</strong></summary>

- **Render-blocking** → Prevents page from painting  
  - Example: CSS in `<head>`

- **Parser-blocking** → Stops HTML parsing  
  - Example: `<script>` without `defer/async`

💡 Best practice:
```html
<script defer src="script.js"></script>
