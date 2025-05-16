
# Tailwind CSS Setup for React Project

Quick guide to set up Tailwind CSS with the CLI in a React project using Vite and React Router.  
For full documentation, visit the [Tailwind CLI Docs](https://tailwindcss.com/docs/installation/cli).

**Last Updated:** May 16, 2025

---

## 🚀 Prerequisites

- Node.js **v18.20.0+**
- A React project using `src/main.jsx` as entry point (adjust if using `index.js`)

---

## ⚙️ Setup Steps

### 1. Install Tailwind CSS and CLI

```bash
npm install tailwindcss @tailwindcss/cli
````

> Installs Tailwind and its CLI for processing CSS.

---

### 2. Add Tailwind to your CSS

In `src/index.css`, add:

```css
@import "tailwindcss";
```

> This serves as the input file for the CLI.

---

### 3. Run Tailwind CLI (Development)

```bash
npx @tailwindcss/cli -i ./src/index.css -o ./src/output.css --watch
```

> Generates `output.css` from `index.css` and watches for changes.

---

### 4. Import `output.css` in `main.jsx`

In `src/main.jsx`, add:

```javascript
import './output.css';
```

> Loads Tailwind styles into your app. (Use `index.js` if using Create React App)

---

### 5. Test Tailwind Styling

In a component (e.g., `App.jsx`):

```jsx
<div className="bg-blue-500 text-white p-4">
  Test
</div>
```

Then run your app:

```bash
npm run dev   # for Vite
# or
npm start     # for Create React App
```

> Open in browser to verify styles are working.

---

### 6. Build for Production

```bash
npx @tailwindcss/cli -i ./src/index.css -o ./src/output.css
npm run build
```

> Creates a minified `output.css` and builds your production bundle.

---

## 🛠️ Troubleshooting

* **No styles appearing?**
  Make sure you’re importing `output.css`, not `index.css`.

* **CLI errors?**
  Double-check file paths:
  `./src/index.css`, `./src/output.css`

* **Missing classes?**
  Create a `tailwind.config.js` file with:

  ```javascript
  module.exports = {
    content: ["./src/**/*.{js,jsx,ts,tsx}"],
  };
  ```

* **Vite slow to refresh?**
  Try refreshing the browser or restarting `npm run dev`.

---

## 📝 Notes

* Keep the CLI running with `--watch` during development.
* Use `output.css` in your final production build (inside `dist/` or `build/`).

---
