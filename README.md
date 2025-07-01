# Omikuji (おみくじ) – Simple Fortune-Telling Web App

## Overview
This repository contains a minimal, self-contained web application that displays a traditional Japanese fortune (おみくじ) to the visitor.  
When the page loads, the user is asked for their name via a browser prompt, after which a random fortune is selected and rendered on screen alongside an image.

The project is intentionally lightweight—no build step, frameworks, or external dependencies are required—making it ideal for practicing **HTML**, **CSS**, and **JavaScript** basics or serving as a starting point for further customization.

---

## Project Structure
```
├── index.html   # Main HTML document
├── style.css    # Page styling (pure CSS)
├── omikuji.js   # Core application logic (vanilla JS)
├── omikuji.png  # Decorative fortune-stick image
└── README.md    # 📖 You are here
```

---

## Quick Start
1. **Clone** or **download** this repository.
2. Open `index.html` in any modern web browser (double-click or drag-and-drop the file into the browser window).
3. Enter your name in the prompt dialog. A random fortune will be displayed.

> ℹ️ No additional setup, web server, or package installation is necessary.

---

## Public API & Component Reference
Although the project is small, the following public-facing elements can be reused or extended.

### 1. HTML Elements
| ID | Purpose | Example Markup |
|---|---|---|
| `name` | Placeholder where the user's name will be injected. | `<span id="name"></span>` |
| `result` | Placeholder where the fortune result text will be injected. | `<span id="result"></span>` |

These two elements are referenced from JavaScript via `document.getElementById(...)`.

### 2. JavaScript Logic (`omikuji.js`)
```js
// omikuji.js (full file is only ~25 LOC)
var username;
var userresult;

username = prompt("お名前を教えてください");
if (username === "") {
  username = "名無し"; // default name when none is provided
}
document.getElementById("name").innerHTML = username;

var rand = Math.floor(Math.random() * 5);
if (rand === 0) userresult = "大吉"; // Great blessing
if (rand === 1) userresult = "中吉"; // Middle blessing
if (rand === 2) userresult = "小吉"; // Small blessing
if (rand === 3) userresult = "吉";   // Blessing
if (rand === 4) userresult = "凶";   // Curse
document.getElementById("result").innerHTML = userresult;
```

#### Public Variables
* `username` — String containing the visitor's name (defaults to `"名無し"`).
* `userresult` — String containing the selected fortune after the random draw.

> While these variables are declared in the global scope (making them accessible from `window.username` and `window.userresult`), no dedicated functions are currently exported. Feel free to refactor into functions or modules as needed.

#### Customization Guide  
Below are a few common ways to adapt the logic to your needs.

1. **Change the available fortunes**
```js
var fortunes = ["超大吉", "大吉", "吉", "半吉", "凶", "大凶"];
var rand = Math.floor(Math.random() * fortunes.length);
var userresult = fortunes[rand];
```

2. **Encapsulate logic inside a function**
```js
function drawFortune(name, container) {
  const fortunes = ["大吉", "中吉", "小吉", "吉", "凶"];
  const idx = Math.floor(Math.random() * fortunes.length);
  const result = fortunes[idx];

  container.querySelector("#name").textContent = name || "名無し";
  container.querySelector("#result").textContent = result;
  return result;
}

// Usage example
const wrapper = document;
const userFortune = drawFortune(prompt("Name?"), wrapper);
console.log(`Today's fortune for you is: ${userFortune}`);
```

3. **Use modules (ES Modules)**
```js
// fortune.js
export function drawFortune(fortunes = ["大吉", "中吉", "小吉", "吉", "凶"]) {
  const idx = Math.floor(Math.random() * fortunes.length);
  return fortunes[idx];
}

// main.js
import { drawFortune } from "./fortune.js";

const name = prompt("Name?") || "名無し";
const fortune = drawFortune();

document.getElementById("name").textContent = name;
document.getElementById("result").textContent = fortune;
```

---

## Styling (`style.css`)
The stylesheet is intentionally brief, targeting only the fortune text color and image sizing. Adjust as desired.
```css
img { height: 100px; }
#name   { color: blue;  }
#result { color: green; }
```

---

## Extending the Project
* **Add more fortunes or weighted probabilities** (e.g., make `凶` rarer).
* **Display fortunes graphically** with emojis or icons.
* **Persist fortunes** in localStorage so the result remains constant for a day.
* **Internationalize** prompts and fortunes for other languages.

---

## License
This project is released under the MIT License. Feel free to reuse or modify it for personal or commercial projects.