# 🧮 Colorful Calculator

A colorful, responsive calculator built with plain **HTML, CSS, and JavaScript**. No frameworks, no libraries, and no `eval()`. It follows the correct order of operations, works with both mouse and keyboard, and runs in any modern browser.

**🔗 Live demo:** https://YOUR-USERNAME.github.io/calculator/

> Replace `YOUR-USERNAME` with your GitHub username after you enable GitHub Pages (see [Deploy on GitHub Pages](#-deploy-on-github-pages)).

---

## 📸 Preview

Add a screenshot of your calculator here:

```
![Calculator screenshot](screenshot.png)
```

Save a screenshot as `screenshot.png` in the project folder, then remove the code fence above so the image shows on GitHub.

---

## 📑 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [How to Use](#-how-to-use)
- [Keyboard Shortcuts](#-keyboard-shortcuts)
- [How It Works](#-how-it-works)
- [Test Cases](#-test-cases)
- [Customization](#-customization)
- [Deploy on GitHub Pages](#-deploy-on-github-pages)
- [Future Improvements](#-future-improvements)
- [Contributing](#-contributing)
- [License](#-license)
- [Author](#-author)

---

## ✨ Features

- **Basic operations:** addition, subtraction, multiplication, and division
- **Correct order of operations:** `2 + 3 × 4` gives `14`, not `20`
- **Percent button:** converts the current number to a percentage (`50` → `0.5`)
- **Decimal support:** only one decimal point per number
- **Delete and clear:** `⌫` removes the last character, `AC` resets everything
- **Live expression display:** see the full expression as you type, with the previous calculation shown above the result
- **Keyboard support:** type with your keyboard instead of clicking
- **Error handling:** dividing by zero or entering an invalid expression shows `Error`, and the calculator recovers on the next key press
- **Floating-point fix:** `0.1 + 0.2` shows `0.3`, not `0.30000000000000004`
- **No leading zeros:** typing `0` then `7` gives `7`, not `07`
- **Negative numbers:** start an expression with `-` to enter a negative value
- **Colorful design:** animated gradient background, glowing display, and gradient buttons with hover and press effects

---

## 🛠 Tech Stack

| Technology | Purpose |
|---|---|
| **HTML5** | Structure of the calculator and buttons |
| **CSS3** | Layout (CSS Grid), gradients, animation, and button effects |
| **JavaScript (ES6)** | Calculator logic, expression parser, and input handling |

---

## 📁 Project Structure

```
calculator/
├── index.html    # Page structure: display and buttons
├── style.css     # All styling and animations
├── script.js     # Calculator logic
└── README.md     # Project documentation
```

---

## 🚀 Getting Started

### Prerequisites

- A modern web browser (Chrome, Edge, Firefox, Safari)
- Optional: [Git](https://git-scm.com/) to clone the project
- Optional: [VS Code](https://code.visualstudio.com/) to edit the code

### Option 1: Clone with Git

```bash
git clone https://github.com/YOUR-USERNAME/calculator.git
cd calculator
```

Then open `index.html` in your browser:

```bash
start index.html       # Windows
open index.html        # macOS
xdg-open index.html    # Linux
```

### Option 2: Download as ZIP

1. On the GitHub repository page, click **Code → Download ZIP**.
2. Extract the folder.
3. Double-click `index.html`.

### Option 3: Run a local server

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000`. Stop the server with `Ctrl + C`.

If you use VS Code, the **Live Server** extension refreshes the page automatically every time you save.

---

## 🖱 How to Use

1. Click the number buttons (or use your keyboard) to enter a number.
2. Click an operator (`+`, `−`, `×`, `÷`).
3. Enter the next number.
4. Press `=` to see the result.

You can chain several operations in one expression, for example `12 + 8 × 3 =`, and the calculator solves it in the correct order.

| Button | Action |
|---|---|
| `0`–`9` | Enter digits |
| `.` | Add a decimal point |
| `+` `−` `×` `÷` | Choose an operation |
| `%` | Divide the current number by 100 |
| `⌫` | Delete the last character |
| `AC` | Clear everything |
| `=` | Calculate the result |

---

## ⌨ Keyboard Shortcuts

| Key | Action |
|---|---|
| `0`–`9` | Enter digits |
| `.` | Decimal point |
| `+` `-` `*` `/` | Operators |
| `%` | Percent |
| `Enter` or `=` | Calculate |
| `Backspace` | Delete last character |
| `Esc` | Clear all |

---

## ⚙ How It Works

### Structure (`index.html`)

The calculator is a single card containing a display and a grid of buttons. Every button carries two data attributes:

- `data-action` says what the button does (`number`, `operator`, `equals`, `clear`, and so on)
- `data-value` holds the digit or operator it represents

This lets a single event listener handle every button, instead of one listener per button.

### Styling (`style.css`)

- The keypad uses **CSS Grid** with 4 equal columns. The `0` button uses `grid-column: span 2` to be double width.
- The background is a four-color gradient that slowly shifts using a `@keyframes` animation.
- Buttons use gradients and a lower shadow, which gives them a raised look that "presses" down when clicked.

### Logic (`script.js`)

The script keeps the typed expression as a string (for example `"12+3*4"`) and only calculates it when you press `=`.

To calculate, it does **not** use `eval()`, which can be unsafe. Instead it uses a small **recursive descent parser**:

1. **Tokenize:** split the string into numbers and operators using a regular expression.
2. **`parseExpression`:** handles `+` and `-` (lowest priority).
3. **`parseTerm`:** handles `*` and `/` (higher priority).
4. **`parseFactor`:** reads a number or a leading minus sign.

Because `parseExpression` calls `parseTerm` first, multiplication and division are always resolved before addition and subtraction.

Other important functions:

| Function | Purpose |
|---|---|
| `render()` | Updates the display |
| `inputNumber()` | Adds a digit and prevents leading zeros |
| `inputDecimal()` | Adds a decimal point, only one per number |
| `inputOperator()` | Adds an operator, replacing the previous one if two are pressed in a row |
| `percent()` | Converts the last number to a percentage |
| `equals()` | Evaluates the expression and handles errors |
| `formatNumber()` | Rounds floating-point noise (`0.1 + 0.2` → `0.3`) |
| `handleAction()` | Central handler for both clicks and keyboard input |

---

## ✅ Test Cases

Use these to confirm everything works:

| Input | Expected result |
|---|---|
| `5` `+` `3` `=` | `8` |
| `9` `÷` `3` `=` | `3` |
| `2` `+` `3` `×` `4` `=` | `14` |
| `0` `.` `1` `+` `0` `.` `2` `=` | `0.3` |
| `1` `0` `÷` `0` `=` | `Error` |
| `5` `0` `%` | `0.5` |
| `5` `+` `=` | `5` |
| `0` `7` | `7` |
| `-` `5` `+` `2` `=` | `-3` |

---

## 🎨 Customization

### Change the colors

Open `style.css` and edit the gradient values.

**Page background:**

```css
body {
  background: linear-gradient(135deg, #ff6ec4, #7873f5, #4ade80, #facc15);
}
```

**Operator buttons (`+ − × ÷`):**

```css
.op {
  background: linear-gradient(135deg, #fb923c, #f43f5e);
}
```

**Result text color:**

```css
#current {
  color: #fef08a;
}
```

### Change the size

```css
.calculator {
  width: 320px;   /* make it wider or narrower */
}
```

### Stop the animated background

Remove the `animation` line from the `body` rule in `style.css`.

---

## 🌐 Deploy on GitHub Pages

Host the calculator online for free:

1. Push your project to GitHub.
2. Open your repository and go to **Settings → Pages**.
3. Under **Branch**, select `main` and `/ (root)`, then click **Save**.
4. Wait a minute or two. Your site will be live at:

```
https://YOUR-USERNAME.github.io/calculator/
```

---

## 🔮 Future Improvements

- [ ] Light and dark theme toggle
- [ ] Calculation history panel
- [ ] Scientific functions (square root, powers, sin, cos, tan)
- [ ] Parentheses support
- [ ] Copy result to clipboard
- [ ] Theme color picker
- [ ] Sound effects on button press
- [ ] Installable as a Progressive Web App (PWA)

---

## 🤝 Contributing

Contributions, ideas, and bug reports are welcome.

1. Fork the repository
2. Create a branch: `git checkout -b feature/my-feature`
3. Commit your changes: `git commit -m "Add my feature"`
4. Push the branch: `git push origin feature/my-feature`
5. Open a Pull Request

---

## 📄 License

This project is licensed under the **MIT License**. You are free to use, modify, and share it.

To add the license, create a file named `LICENSE` in the project folder, or choose **Add file → Create new file → LICENSE** on GitHub and pick the MIT template.

---

## 👤 Author

**Melissa**

- GitHub: [@YOUR-USERNAME](https://github.com/YOUR-USERNAME)

If you like this project, give it a ⭐ on GitHub!
