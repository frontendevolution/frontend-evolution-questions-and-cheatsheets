# 🧠 HTML Master Cheat Sheet (Structure → Forms → SEO)

> 🚀 Everything you need for **interviews + real-world frontend development**

---

# 📌 1. HTML DOCUMENT STRUCTURE

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Document</title>
</head>
<body>
  <!-- Content -->
</body>
</html>
```

### 🔹 Breakdown

* `<!DOCTYPE html>` → HTML5 declaration
* `<html lang="en">` → Root + language (SEO + accessibility)
* `<head>` → Metadata (not visible)
* `<body>` → UI content

### ⚡ Important

* Browser auto-corrects missing tags (error recovery)
* DOM is built from this structure

---

# 📌 2. SEMANTIC HTML ELEMENTS

### 🔹 Why Semantic?

* SEO improvement
* Accessibility (screen readers)
* Clean structure

### 🔹 Core Layout Tags

```html
<header></header>
<nav></nav>
<main></main>
<section></section>
<article></article>
<aside></aside>
<footer></footer>
```

### 🔹 Meaning

| Tag         | Purpose                 |
| ----------- | ----------------------- |
| `<header>`  | Top content / intro     |
| `<nav>`     | Navigation links        |
| `<main>`    | Main content (only one) |
| `<section>` | Thematic grouping       |
| `<article>` | Independent content     |
| `<aside>`   | Sidebar / ads           |
| `<footer>`  | Bottom content          |

### ⚡ Rules

* Use `<main>` only once
* Don’t overuse `<section>`
* `<article>` should make sense standalone

---

# 📌 3. HEAD TAG (ADVANCED)

### 🔹 Purpose

Controls:

* SEO
* Performance
* Rendering
* Metadata

### 🔹 Example

```html
<head>
  <title>My Website</title>

  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <meta name="description" content="Learn HTML" />
  <meta name="author" content="John Doe" />

  <link rel="stylesheet" href="style.css" />

  <script defer src="script.js"></script>
</head>
```

### 🔹 Script Loading

| Attribute | Behavior                               |
| --------- | -------------------------------------- |
| `defer`   | Loads in parallel, executes after HTML |
| `async`   | Loads + executes immediately           |

---

# 📌 4. META TAGS (FULL)

### 🔹 Core Meta

```html
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<meta name="description" content="Best HTML guide" />
<meta name="keywords" content="HTML, CSS, JS" />
<meta name="author" content="Your Name" />
```

### 🔹 SEO / Crawling

```html
<meta name="robots" content="index, follow" />
```

### 🔹 Open Graph (Facebook, LinkedIn)

```html
<meta property="og:title" content="Title" />
<meta property="og:description" content="Description" />
<meta property="og:image" content="image.jpg" />
<meta property="og:url" content="https://example.com" />
```

### 🔹 Twitter Cards

```html
<meta name="twitter:card" content="summary_large_image" />
```

---

# 📌 5. SEO BASICS (HTML LEVEL)

### 🔹 Must Do

* Use **semantic tags**
* Proper heading hierarchy
* Add `alt` to images
* Clean URLs
* Fast loading

### 🔹 Example

```html
<h1>Main Title</h1>
<h2>Subheading</h2>
<img src="img.jpg" alt="A description" />
```

### 🔹 Bad Practice

```html
<div class="title"></div> ❌ (Use h1 instead)
```

---

# 📌 6. HTML FORMS (COMPLETE)

### 🔹 Basic Structure

```html
<form action="/submit" method="POST">
  <label for="name">Name:</label>
  <input id="name" name="name" type="text" />
  
  <button type="submit">Submit</button>
</form>
```

### 🔹 Attributes

| Attribute      | Purpose            |
| -------------- | ------------------ |
| `action`       | API endpoint       |
| `method`       | GET / POST         |
| `autocomplete` | Autofill           |
| `novalidate`   | Disable validation |

---

# 📌 7. INPUT TYPES (FULL LIST)

```html
<input type="text" />
<input type="email" />
<input type="password" />
<input type="number" />
<input type="tel" />
<input type="url" />
<input type="search" />

<input type="date" />
<input type="time" />
<input type="datetime-local" />
<input type="month" />
<input type="week" />

<input type="file" />
<input type="checkbox" />
<input type="radio" />

<input type="range" />
<input type="color" />

<input type="hidden" />
<input type="submit" />
<input type="reset" />
<button type="button"></button>
```

---

# 📌 8. FORM ELEMENTS (BEYOND INPUT)

### 🔹 `<textarea>`

```html
<textarea rows="4" cols="50"></textarea>
```

### 🔹 `<select>` (Dropdown)

```html
<select name="country">
  <option value="">Select</option>
  <option value="india">India</option>
</select>
```

### 🔹 Multiple Select

```html
<select multiple>
  <option>HTML</option>
  <option>CSS</option>
</select>
```

### 🔹 `<optgroup>`

```html
<optgroup label="Frontend">
  <option>HTML</option>
</optgroup>
```

### 🔹 `<fieldset>` + `<legend>`

```html
<fieldset>
  <legend>Personal Info</legend>
  <input type="text" />
</fieldset>
```

---

# 📌 9. FORM VALIDATION (NATIVE)

### 🔹 Attributes

```html
<input required />
<input minlength="3" maxlength="10" />
<input type="number" min="1" max="100" />
<input pattern="[A-Za-z]+" />
<input type="email" />
```

### 🔹 Example

```html
<form>
  <input type="email" required />
  <button>Submit</button>
</form>
```

### 🔹 Disable Validation

```html
<form novalidate>
```

---

# 📌 10. ACCESSIBILITY (A11Y)

### 🔹 Best Practices

* Always use `<label>`

```html
<label for="email">Email</label>
<input id="email" type="email" />
```

* Use `aria-*` when needed

```html
<button aria-label="Close"></button>
```

---

# 📌 11. FORM DATA FLOW

### 🔹 GET Method

* Data visible in URL
* Used for search/filter

### 🔹 POST Method

* Data in request body
* Used for secure submission

---

# 📌 12. INTERVIEW GOLD POINTS

* HTML is parsed → DOM tree created
* Browser auto-fixes broken HTML
* Semantic HTML improves SEO + accessibility
* Use native validation before JS
* `<select>` ensures controlled input
* `<meta viewport>` is mandatory for responsive design

---

# 🚀 FINAL SUMMARY

> HTML is not just markup — it's **structure + meaning + accessibility + SEO + data handling**.
