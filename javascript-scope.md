### ✅ What is **Scope** in JavaScript?

> **Scope** is about **where** in your code you can **access** variables.

Imagine your code like a house:

* Each **room** in the house is like a **block of code**.
* Some things (variables) are **only available inside one room**, while others are available in **the whole house**.

There are a few **types of scope**:

---

### 1. **Global Scope**

* Variables declared **outside** of functions or blocks.
* They can be accessed **anywhere** in your code.

```js
let globalVar = "I'm global!";

function showVar() {
  console.log(globalVar); // You can access it here
}

showVar();
console.log(globalVar); // And here too
```

---

### 2. **Function Scope**

* Variables declared **inside a function**.
* You **can't** access them from **outside** the function.

```js
function myFunc() {
  let message = "Hello!";
  console.log(message); // ✅ This works
}

myFunc();
console.log(message); // ❌ Error! message is not defined
```

---

### 3. **Block Scope** (with `let` and `const`)

* Introduced in **ES6**.
* Variables declared inside `{}` using `let` or `const` are **not accessible outside** that block.

```js
if (true) {
  let blockVar = "I'm inside the block!";
  console.log(blockVar); // ✅
}

console.log(blockVar); // ❌ Error! blockVar is not defined
```

If you used `var` instead of `let`, `blockVar` **would leak out** (which is why `let` and `const` are preferred).

---

### Visual Summary

| Scope Type     | Keyword Used          | Accessible Outside? |
| -------------- | --------------------- | ------------------- |
| Global         | `var`, `let`, `const` | ✅ Yes               |
| Function Scope | `var`, `let`, `const` | ❌ No                |
| Block Scope    | `let`, `const`        | ❌ No                |

---

### Practice Tip

Try running this code in the browser console or on [JSFiddle](https://jsfiddle.net/) or [CodePen](https://codepen.io/):

```js
let name = "Alice"; // global

function greet() {
  let greeting = "Hello"; // function scope
  if (true) {
    let punctuation = "!"; // block scope
    console.log(greeting + ", " + name + punctuation); // ✅ Works
  }
  // console.log(punctuation); // ❌ Would throw error
}

greet();
```