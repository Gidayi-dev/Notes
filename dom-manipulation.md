# **DOM Manipulation: Detailed Notes with Full Explanations**

---

## 1. What is the DOM and why manipulate it?

The **DOM (Document Object Model)** is like a **tree of objects** that represents every part of your HTML page — every tag, attribute, and text.

* When a web page loads, the browser creates this model.
* JavaScript can **talk to this model** to change the content, structure, and style **while the page is loaded**.
* This lets you build interactive pages — for example:

  * Add new items to a list without refreshing.
  * Change colors or fonts based on user actions.
  * Respond to clicks, scrolls, or form inputs.

**Manipulating the DOM** means you get or create these objects and then change them using JavaScript.

---

## 2. Selecting Elements: `document.querySelector()` and `querySelectorAll()`

Before changing anything, you need to **select** the element you want to work on.

* `document.querySelector(selector)` will find the **first** element that matches a CSS selector you pass it.

  For example:

  ```js
  const button = document.querySelector(".submit-btn");
  ```

  This gets the first element with class `"submit-btn"`.

* `document.querySelectorAll(selector)` finds **all** matching elements and returns a list.

  Example:

  ```js
  const allButtons = document.querySelectorAll("button");
  ```

  This gets all `<button>` elements.

**Why CSS selectors?**
Because CSS selectors are a powerful, flexible way to specify elements: by tag, class, id, attributes, nested selectors, and more.

**What happens internally?**
`querySelector()` looks through the DOM tree and stops when it finds the first matching element, then returns it for you to use.

---

## 3. Changing Text and HTML Content: `.textContent` and `.innerHTML`

Once you have an element, you might want to:

* Change its text (without touching any HTML tags inside).
* Or change its entire HTML content (which may contain other tags).

### `.textContent`

* This property sets or gets the **text inside** an element.
* It treats everything as plain text, **ignoring any HTML tags**.

Example:

```js
const message = document.querySelector("#msg");
message.textContent = "Hello, world!";
```

If you set `.textContent` to `"<b>Hi</b>"`, it will literally show the text `<b>Hi</b>`, **not bold Hi**.

### `.innerHTML`

* This sets or gets the **HTML markup inside** an element.
* It parses the string as HTML and inserts it.

Example:

```js
message.innerHTML = "<b>Hi</b>";
```

This will make the content bold because it inserts a `<b>` tag.

**Why the difference matters:**
If you want users to see exactly the text they type, use `.textContent`.
If you want to add elements or formatting dynamically, use `.innerHTML`.

---

## 4. Creating New Elements: `document.createElement()`

Sometimes, you want to add something new — like a new list item or button.

You do this by:

* Calling `document.createElement(tagName)`.
* This **creates a brand-new element** in memory but doesn’t add it to the page yet.

Example:

```js
const newDiv = document.createElement("div");
```

Now `newDiv` is a `<div>` element — but it’s not visible on the page until you add it somewhere.

---

## 5. Adding Elements to the Page: `.appendChild()`

To make the new element appear in your page, you must insert it into an existing element.

* Every element is a **node** in the DOM tree.
* You can append a new child node with `.appendChild(childNode)`.

Example:

```js
const container = document.querySelector("#container");
container.appendChild(newDiv);
```

Now your `newDiv` becomes the last child inside the container and will show up on the page.

---

## 6. Removing Elements: `.removeChild()`

If you want to delete an element from the page, use `.removeChild(childNode)` on its parent.

Example:

```js
container.removeChild(newDiv);
```

This removes the `newDiv` from the container and the page.

---

## 7. Setting and Getting Attributes: `.setAttribute()` and `.getAttribute()`

HTML elements have attributes like `id`, `class`, `src`, `href`, and custom ones like `data-*`.

You can change or read these with:

* `.setAttribute(name, value)` to add or update an attribute.

Example:

```js
newDiv.setAttribute("class", "highlight");
```

* `.getAttribute(name)` to read an attribute’s value.

Example:

```js
const className = newDiv.getAttribute("class");
```

This is useful for adding classes, changing image sources, or toggling data attributes.

---

## 8. Styling Elements: `.style`

You can directly modify **inline CSS styles** of an element using the `.style` property.

Example:

```js
newDiv.style.backgroundColor = "yellow";
newDiv.style.fontSize = "20px";
```

This changes the style immediately, without modifying external CSS files.

---

## 9. Responding to User Events: `.addEventListener()`

To make your page interactive, you listen to user actions (clicks, typing, hovering).

* `.addEventListener(eventName, callback)` attaches a function that runs when the event happens.

Example:

```js
button.addEventListener("click", () => {
  alert("You clicked the button!");
});
```

You can listen to many events: `click`, `keydown`, `mouseover`, `submit`, and more.

---

## 10. Running Code After the Page Loads: `window.onload`

Sometimes, your script runs before the page is fully loaded, so your elements don’t exist yet.

`window.onload` lets you run code **only after the entire page (images, styles, etc.) has loaded**.

Example:

```js
window.onload = function() {
  const btn = document.querySelector("button");
  // safe to manipulate elements here
};
```

---

## 11. Scrolling the Page: `window.scrollTo(x, y)`

You can programmatically scroll the page to a specific position.

Example:

```js
window.scrollTo(0, 500); // scrolls down 500 pixels vertically
```

Useful for jumping to a section or focusing the user’s view.

---

# **Full Project with Step-by-Step Explanation**

---

Here is a **To-Do List** example with detailed explanations for every step.

---

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Detailed To-Do List Example</title>
<style>
  body { font-family: Arial, sans-serif; padding: 20px; }
  #todo-list { margin-top: 20px; }
  .todo-item { padding: 10px; border: 1px solid #ccc; margin-bottom: 5px; cursor: pointer; }
  .done { text-decoration: line-through; color: gray; }
  button { padding: 5px 10px; }
</style>
</head>
<body>

<h1>My To-Do List</h1>

<!-- Input field where user types a new task -->
<input type="text" id="task-input" placeholder="Enter a new task" />

<!-- Button to add the new task -->
<button id="add-task-btn">Add Task</button>

<!-- Container to hold the list of tasks -->
<div id="todo-list"></div>

<script>
// Wait for entire page to load before running code
window.onload = function () {

  // Select the input field where the user types a task
  const input = document.querySelector("#task-input");

  // Select the 'Add Task' button
  const addButton = document.querySelector("#add-task-btn");

  // Select the container that will hold all the to-do items
  const todoList = document.querySelector("#todo-list");

  /**
   * This function creates a new task element with the task text
   * It adds event listeners to toggle "done" state and remove the task
   */
  function createTodoItem(text) {
    // Create a new <div> to hold the task text and buttons
    const todoItem = document.createElement("div");

    // Add a CSS class for styling
    todoItem.classList.add("todo-item");

    // Set the visible text content to the task description
    todoItem.textContent = text;

    // When clicked, toggle the "done" style (line-through)
    todoItem.addEventListener("click", () => {
      todoItem.classList.toggle("done");
    });

    // Create a button element to remove the task
    const removeBtn = document.createElement("button");

    // Set the text on the remove button
    removeBtn.textContent = "Remove";

    // Add some inline CSS styles for the remove button
    removeBtn.style.marginLeft = "10px";
    removeBtn.style.padding = "2px 5px";

    // When clicked, this button will remove the task from the list
    removeBtn.addEventListener("click", (event) => {
      // Prevent the click from toggling done on the parent task
      event.stopPropagation();

      // Remove this task element from its parent container
      todoList.removeChild(todoItem);
    });

    // Add the remove button inside the task element div
    todoItem.appendChild(removeBtn);

    // Return the complete task element
    return todoItem;
  }

  // Listen for clicks on the "Add Task" button
  addButton.addEventListener("click", () => {
    // Get the text the user typed, and trim whitespace
    const taskText = input.value.trim();

    // If the input is empty, alert the user and do nothing
    if (taskText === "") {
      alert("Please enter a task!");
      return;
    }

    // Create a new task element with the text
    const newTask = createTodoItem(taskText);

    // Add the new task to the todo list container, so it shows on the page
    todoList.appendChild(newTask);

    // Clear the input field to prepare for the next task
    input
```


.value = "";

```
// Scroll the new task smoothly into view (user experience improvement)
newTask.scrollIntoView({ behavior: "smooth" });
```

});

// Bonus: Allow adding a task by pressing the Enter key in the input box
input.addEventListener("keydown", (event) => {
if (event.key === "Enter") {
addButton.click();
}
});

}; </script>

</body>
</html>
```

---

### **Step-by-step explanation of the code:**

1. **Wait for Page Load**
   We use `window.onload` to delay running the script until all HTML elements exist in the DOM, so that `querySelector` calls don’t return `null`.

2. **Selecting Elements**
   We select the input box, the add button, and the container where tasks will appear — using `querySelector("#id")` because these elements have unique IDs.

3. **Creating a New To-Do Item**

   * `document.createElement("div")` creates a new empty div.
   * `.classList.add("todo-item")` adds a CSS class for styling.
   * `.textContent = text` inserts the task text safely.
   * We add a click event listener to toggle the `.done` class, which applies strikethrough styles.
   * We create a remove button inside the task item:

     * Also created with `createElement`.
     * Styled inline using `.style`.
     * Added a click listener that stops event propagation and removes the task.
   * The remove button is appended as a child of the task div.

4. **Adding the Task to the Page**
   When the Add Task button is clicked:

   * We get the trimmed text from the input box.
   * If empty, we alert the user.
   * Otherwise, create the task div and append it to the todo list container.
   * Clear the input for the next task.
   * Scroll the new item smoothly into view for user feedback.

5. **Bonus: Adding Tasks via Enter Key**
   Listening to the `keydown` event on the input box allows pressing Enter to act like clicking Add Task.

---

# Why this is important for real projects:

* **Dynamic content:** The user can add or remove items without page reload.
* **Event-driven:** The interface responds to user clicks and key presses.
* **Clean code:** Functions separate logic for clarity and reuse.
* **Good UX:** Scrolls new items into view, clears input automatically.
