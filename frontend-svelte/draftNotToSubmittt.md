Note : Even though npm list @sveltejs/kit showed nothing, the fact that your svelte.config.js file imports @sveltejs/adapter-auto and references @sveltejs/kit suggests that this is a SvelteKit project.Hence, the file suggests that our project is sveltekit project and not only svelte app.

# Introduction to Frontend Development

## What is Frontend Development?

Frontend development is the process of building the user interface (UI) of a website or web application. It includes everything users see and interact with, such as:

Buttons, text, images, and layouts.

Animations and transitions.

Data displayed from a backend (like API responses).

Frontend developers use three core technologies:

HTML – Defines the structure of web pages.

CSS – Styles and arranges elements for better design.

JavaScript – Adds interactivity and logic.

Modern frontend development also uses frameworks (like SvelteKit) to build complex applications efficiently.

## Other Frontend Development Frameworks
While we are using SvelteKit, there are other popular frontend frameworks and libraries:

React.js – Developed by Facebook, React is widely used for building reusable UI components.

Vue.js – A progressive framework known for its simplicity and flexibility.

Angular – Developed by Google, Angular is a full-featured framework for large-scale applications.

Solid.js – Similar to React but optimized for performance.

Qwik – A newer framework focused on instant loading and fast interactivity.

## Is it necessary to master all frameworks?
we don’t need to master all frameworks. Most companies use one or two, so it's better to specialize in one (like SvelteKit) and understand the core concepts of others. If we know JavaScript well, switching between frameworks becomes easier.


## Does Every Framework Use JavaScript?

Almost all frontend frameworks are built on JavaScript or TypeScript (a superset of JavaScript) because:

Browsers run JavaScript natively.

It allows dynamic, interactive web applications.

However, some alternatives exist (like Blazor using C# or Elm), but JavaScript remains the industry standard.


## Essential JavaScript Concepts for Frontend Development
key topics that are essential for mastering frontend development are given below and then described in details.

DOM Manipulation – How JavaScript interacts with the webpage.

ES6+ Features – Modern JavaScript features like arrow functions, spread/rest operators, and destructuring.

Asynchronous JavaScript – Understanding Promises, async/await, and how APIs work.

JavaScript Modules & Import/Export – Organizing code efficiently.

Event Handling – How user interactions (like clicks) are managed.

Higher-Order Functions – Functions like .map(), .filter(), .reduce() for working with lists.


### DOM Manipulation in Javascript

What is the DOM?
The Document Object Model (DOM) represents a webpage as a structured tree of elements. JavaScript can modify this tree to update content dynamically.

#### Selecting Elements in the DOM
To manipulate an element, we first need to select it. JavaScript provides several ways to do this:

1. getElementById (Select by ID)
Use when selecting a single element by its unique id.

````js
const title = document.getElementById("main-tile");
console.log(title);     // log the element with ID "main-title"
````

2. querySelector (Select by CSS Selector)
More flexible—allows selecting by class, tag, or ID.

````js
const heading = document.querySelector(".header");
console.log(heading);  // Selects the first element with class "header"
````

3. querySelectorAll (Select Multiple Elements)
Use this to select multiple elements at once.

````js
const buttons = document.querySelectorAll(".btn");
console.log(buttons);  // logs a node list with all elements with class 'btn'
````

#### Modifying Elements
Once an element is selected, we can change its content, style, or attributes. The code below updates the text inside an element.

1.  Changing Text Content
````js
const title = document.getElementById("main-title");
title.textContent = "New title Updated!";
````

2. Changing HTML content
Directly sets new HTML inside an element.

````js
const container = document.querySelector(".contianer");
container.innerHTML = "<h2>New Content</h2>";
````

3. Changing Styles
Modifies the CSS of an element dynamically.

````js
const button = document.querySelector(".btn");
button.style.backgroundColor = "blue";
button.style.color = "white";
````

#### Adding and Removing the Elements
We can also create, add, and remove elements dynamically.

1. Creating and Appending Elements
Creates a new <div> and adds it to the page.

````js
const newDiv = document.createElemet("div");
newDiv.textContent = "I am a new div!"
document.body.appendChild(newDiv);

````

2. Removing Elements
This codes removes an element from page
````js
const elementToRemove = document.querySelector(".old-item");
elementToRemove.remove()
````

#### Handling Classes
We can manipulate CSS classes to change appearance dynamically.

````js
const box = document.querySelector(".box");

//Add a class
box.classList.add("highlight");

//Remove a class
box.classList.remove("highlight");

//Toggle a class (adds if missing, removes if present)
box.classList.toggle("active");
````

Useful for animations, dark mode, or changing styles dynamically.



### Modern JavaScript (ES6+) Features
ES6 (ECMAScript 2015) introduced many powerful features that make JavaScript code cleaner and more efficient. Here are the most important ones:

#### Let & Const (Block-Scoped Variables)
Before ES6, we used var, but now we use let and const for better variable control.
Use const by default unless you need to reassign the variable.

````js
let name = "Alice";  //can be reassigned
const age = 25; //cannot be changed
````
#### Let & Const (Block-Scoped Variables)
Arrow Functions (Shorter Function Syntax)

1. regular function
````js
function add(a, b){
    return a + b;
}
````

2. Arrow function
If there is only one statement {} and return are optional.
````js
const add = (a , b) => a + b;
````

3. Template Literals(String Interpolation)
Instead of using + for string concatenation, we use backticks (`) and ${} to insert variables.This is more readable and supports multi-line strings.

````js
const name = "John";
const message = `Hello, my name is ${name}!`;
````

4. Destructuring (Extract Values Easily)
Extract values from arrays and objects quickly.

Array Destructing
````js
const numbers = [1, 2, 3];
const [first , second] = numbers; //first=1 and second=2
````

Object Desctructing

````js
const person = {name: "Alice", age: 20};
const {name, age } = person; //name= "Alice" , age=20
````
Useful when working with API data.

5. Spread and Rest Operators(....)
Spread Operator (Expands an Array or Object)

````js
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5]; //[1, 2, 3, 4, 5]


const person = {name: "Bob"};
const updatedPerson = {...person, age:30} //{name: "Bob" , age:30}
````

Rest operators (collects remaining items)
The spread operators expands while the rest operators gathers

````js
const sum = (a,b, ...rest) => {
    console.log(rest); // Logs the remaining arguments
};
sum(1,2,3,4,5);  // rest = [3, 4, 5]
````

6. Default Parameters
Set default values in function parameters.It helps to  avoid undefined errors.

````js
const greet = (name = "Guest") => `hello , ${name}!`;
console.log(greet());  // "hello, Guest!"
console.log(greet("Alice")); // "hello, Alice!"
````

7. Promises & Async/Await (We’ll cover in depth later)
Promises handle asynchronous operations.

````js
const fetchData = () => new Promise((resolve) => setTimeout(() => resolve("Data loaded"),2000));

fetchData().then((data) => console.log(data));  // "Data loaded" after 2 sec
````

### Asynchronous JavaScript

JavaScript runs code synchronously (line by line), but some tasks (like fetching data from an API) take time. Asynchronous JavaScript allows these tasks to happen in the background without stopping the whole program.

1. Callbacks (Old Way of Handling Async Code)
A callback is a function passed as an argument to another function, which runs after a task is complete.

````js
function fetchData(callback){
    setTimeout(()=>{
        callback("Data loaded")
    }, 2000);
}

fetchData((data) => console.log(data)); // "Data Loaded" after 2 seconds
````
Problem: Callbacks can get messy when nested, leading to callback hell.

2. Promises (Better Way to Handle Async Code)
A Promise represents a future value—either resolved (success) or rejected (error).
Creating a Promise
````js
const fetchdata = () => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve("Data loaded");
        }, 2000);
    })
};
````
Instead of callbacks, we use .then() and .catch().

Using a Promise

````js
fetchData()
    .then((data) => console.log(data)) //Runs when resolved
    .catch((error) => console.error(error)) //Runs if rejected
````

3. Async/Await (Modern & Clean Way)
async/await makes async code look synchronous, improving readability.

Example: Fetching Data

````js
const fetchData = async () => {
    try {
        const data = await new Promise((resolve) => 
            setTimeout(() => resolve("Data Loaded"), 2000)
        );
        console.log(data); //"Data loaded" after 2 sec
    } catch (error) {
        console.error(error);
    }
};
fetchData();

````

Benefits of async/await>
1. Makes code easier to read.
2. Avoids the "callback hell" problem.
3. Uses try/catch for error handling.

4.  Real-World Example: Fetching API Data

Here’s how we fetch data from an API using fetch() and async/await:

````js
const getUsers = async () => {
    try {
        const response = await fetch("https://jsonplaceholder.typicode.com/users");
        const user = await response.json();
        console.log(users);  //Logs the user data
    } catch (error){
        console.error("Error fetching data:", error);
    }
};
getUser();
````
In the code given above, fetch() makes a network request.await response,json() converts the response to JavaScript and try/catch handles errors (e.g., no internet).

### JavaScript Modules & Import/Export
As projects grow, keeping all JavaScript in one file becomes messy. Modules help by splitting code into separate files, making it easier to manage and reuse.
We use modules to keeps code organized (separate concerns), avoids variable conflicts (no global scope pollution), imporves reusability (import functions only when needed)

1. Exporting and Importing Modules
Exporting (Making Functions/Variables Available in Other Files)
Use export to allow other files to access your code.

Named Export (Multiple Exports Allowed)
````js
//utils.js

export const greet = (name) => `Hello, ${name}!`;
export const add = (a , b) => a + b;

````

Default Export(Only One per file)
````js
//math.js
export default function multiply(a, b){
    return a * b;
}
````

2. Importing (Using code from other files)
Importing Named Exports
````js
//main.js
import {greet, add} from "./utils.js";

console.log(greet("Alice"));  // "Hello, Alice!"
console.log(add(2,3)); //5

````

Importing a Default Export
````js
// main.js
import multiply from "./math.js";

console.log(multiply(2,3));  // 6

````
Named exports need {} while default exports do not.

3. Importing Everything (*)
If a file has many exports, you can import them all as an object.
````js
//main.js
import * as Utils from "./utils.js";

console.log(Utils.greet("Bob"));  // "Hello, Bob!"
console.log(Utils.add(4,5)); //9
````

Utils.greet and Utils.add work like object properties


### Event Handling in Javascript

Event handling allows you to capture user interactions with the page, such as clicks, keypresses, and form submissions, and respond to them. This is crucial for building interactive websites.
1. What is an Event?
An event is any action or occurrence that the browser can detect, such as:Mouse clicks,Keyboard input,Scrolling,Page load

When an event occurs, the browser can trigger a specific function to handle the event (called an event handler)

2. Attaching Event Handlers
There are two main ways to attach event handlers in JavaScript:

Using addEventListener() :

This is the preferred way to attach events as it offers more flexibility (e.g., multiple event listeners on the same element)
addEventListener takes two arguments:
Event type (like "click", "keydown", etc.)
Callback function to run when the event occurs

````js
const button = document.querySelector(".btn");
button.addEventListener("click", () => {
    alert("Button Clicked!");
});
````

It is also possible to listen to multiple events on the same element:

````js
button.addEventListener("click", () => alert("Clicked!"));
button.addEventListener("mouseover", () => alert("Mouse Over!"));

````
Using Inline Event Handlers (Not Recommended):

This is the old way of handling events in HTML by putting the JavaScript code directly inside HTML tags. It’s not recommended because it mixes HTML and JavaScript.It is better to use addEventListener for cleaner, modular code.


````js
<button onclick="alert('Buttton clicked!')">Click Me </button>
````


3. Common Events:

Here are some common events you'll work with:

Mouse Events:

click – Triggered when the user clicks on an element.

mouseover – Triggered when the user hovers over an element.

mouseout – Triggered when the user moves the mouse away from an element.

Keyboard Events:

keydown – Triggered when a key is pressed down.

keyup – Triggered when the key is released.

keypress – Triggered when a character key is pressed.

Form Events:

submit – Triggered when a form is submitted.

input – Triggered when the value of an `<input>` element changes.

change – Triggered when a form element’s value changes (typically used with `<select>` and `<input>` elements).

4. Event Object
The event handler receives an event object that contains details about the event, such as the target element, mouse position, and key pressed.

````js
const button = document.querySelector(".btn");
button.addEventListener("click", (event) =>{
    console.log(event); //Logs the event object
    console.log(event.target);
})
````

`event.target` gives us the element that triggered the event (eg: the button). The event object also contains other useful properties like:
`evet.type` - The type of event (e.g., "click", "keypress").
`event.clientX` and `event.clientY` – The mouse position when the event occurred.

5. Event Propagation (Bubbling & Capturing)
Events in JavaScript can bubble up or capture down the DOM tree. Understanding this helps manage how events propagate.

Bubbling: Events first trigger on the target element, then propagate up to the parent elements.

Capturing: Events first trigger on the root of the DOM tree and then propagate down to the target element.

We can control this with the capture flag in addEventListener():

````js
document.querySelector(".parent").addEventListener("click", () => {
    alert("Parent Clicked!");
}, true); //true means capture phase
````

6. Removing Event Listeners
We can remove an event listener if you no longer need it:

````js
const button = document.querySelector(".btn");
const handleClick = () => alert("Button Clicked!");


button.addEventListener("click", handleclick);

//Later, remove the event listener
button.removeEventListener("click", handleClick);

````




### Higher-Order Functions in JavaScript
Higher-Order Functions (HOFs) are functions that take other functions as arguments or return functions. They make code more readable, reusable, and functional.

In JavaScript, .map(), .filter(), and .reduce() are the most commonly used HOFs when working with arrays.

1. `.map() `– Transform Each Element in an Array

Used for transforming an array by applying a function to each element. It returns a new array with modified values.

Key points about .map():

Does not modify the original array.

Returns a new array.

The callback function runs once for each element.

````js
const numbers = [1, 2, 3, 4, 5];

//Multiply each number by 2
const doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8, 10]
````

2. `.filter()` -  Select Elements That Meet a Condition

Used for filtering elements from an array based on a condition. Returns a new array with only the matching elements.
Key points about .filter():

Returns only elements that pass the test.

Does not modify the original array.

The callback function should return true to keep an element.


````js
const numbers = [1, 2, 3, 4, 5];

// Get even numbers 
const evens = numbers.filter(num => num % 2 == 0);

console.log(evens);
````

3. `.reduce` - Reduce an Array to a single Value
This function is used for reducing an array to a single value (sum, product, etc.).
How .reduce() works:

acc (accumulator) stores the result.

num is the current element.

0 is the initial value of acc.

````js
const numbers = [1, 2, 3, 4, 5];

// sum of all numbers
const sum = numbers.reduce((acc, num) => acc + num, 0);

console.log(sum); //15
````

Another Example:

 Find the maximum number in an array:

 ````js
 const max = numbers.reduce((acc, num) => (num > acc ?  num : acc), numbers[0]);
 console.log(max); //5
 ````

 4. Combining .map(), .filter(), and .reduce()
 We can chain these functions for powerful data transformations.

  Example: Given an array of people, find the total age of all people over 18.

  ````js
  const people = [
    {name : "Alice", age: 25},
    {name : "Bob", age:17},
    {name : "Charlie", age: 30},
    {name : "David", age: 15}
  ];

  // Get the total age of adults (age > 18)
  const totalAdultAge = people
    .filter(person => person.age > 18) //keep only adults
    .map(person => person.age) //extracts age
    .reduce((sum, age) => sum + age, 0); // sum ages


console.log(totalAdultAge); // 55
  ````

  First, we filter out people under 18, then extract their ages using map(), and finally sum them using reduce().

Why Use Higher-Order Functions?

Code is more readable and concise.

No need for loops like for or while.

Immutable approach – Does not modify the original array.

More declarative – Focuses on "what" rather than "how."




## Introduction to Svelte
Svelte is a frontend framework like React or Vue, but with a twist i.e. It compiles your code to efficient, minimal JavaScript at build time.
That means:No virtual DOM,Faster performance,Cleaner syntax and smaller bundle sizes.

Following things make Svelte Special
1. No runtime library - Compiled at build time = faster apps
2. Less boilerplate - 	Easy to write, easier to read
3. Reactivity built-in - No need for special APIs like setState()
4. Scoped CSS - Styles are local to components

### Svelte Project Structure with Vite
When you create a SvelteKit project (or even plain Svelte), it often uses Vite as the bundler.
Here’s a basic overview of the project structure you might see in your project:
````bash
my-app/
├── src/
│   ├── lib/           # Reusable components (e.g., Button.svelte)
│   ├── routes/        # Pages and routing (only for SvelteKit)
│   ├── app.html       # HTML template
│   └── main.js        # Entry point (plain Svelte)
├── static/            # Public assets like images (SvelteKit)
├── svelte.config.js   # Svelte-specific configuration
├── vite.config.js     # Vite build + dev config
├── package.json       # Project dependencies and scripts


````
Vite is a "Next-gen frontend tooling" which Starts a super-fast dev server, Bundles your code for production, Supports hot module reload (HMR).
it’s better than older tools (like Webpack) because Lightning-fast startup (no bundling during dev), Native support for ES modules, Built-in TypeScript, JSX, and framework support (like Svelte, Vue, etc.)

A sample vite.config.js for Svelte:
````js
import { sveltekit } from '@sveltejs/kit/vite';

const config = {
  plugins: [sveltekit()],
};

export default config;

````

### Svelte Basics: Components, Props, and Reactivity
What is a Svelte Component? - A component is just a .svelte file that contains three parts:
````svelte
<script>
  // JavaScript
</script>

<style>
  /* CSS (scoped to this component) */
</style>

<!-- HTML (template) -->
<h1>Hello Svelte!</h1>

````
Every .svelte file is a reusable piece of UI — like a button, a header, or a form.

#### Declaring Variables (Reactivity)
In Svelte, any top-level variable declared with let is reactive. When it changes, the DOM automatically updates.

````svelte
<script>
  let name = "Alice";
</script>

<h1>Hello {name}!</h1>
<input bind:value={name} />

````
 When the input value changes, name updates automatically
 The {} syntax injects the variable into the HTML

 #### Event Handling
 Svelte uses on:eventname for handling events.
 ````svelte
 <script>
  let count = 0;
  const increment = () => count += 1;
</script>

<button on:click={increment}>
  Clicked {count} times
</button>

 ````
 No need for .addEventListener()
 Events are easy to read and bind to functions


 #### Props – Passing Data to Components
 We can pass variables to a component from its parent using props.

ChildComponent.svelte
````svelte
<script>
  export let message;
</script>

<p>{message}</p>

````

ParentComponent.svelte
````svelte
<script>
  import ChildComponent from './ChildComponent.svelte';
</script>

<ChildComponent message="Hello from parent!" />


````

Props are marked with export let ...

####  Reactive Statements ($:)
Sometimes we want to automatically re-run code when a variable changes.
````svelte
<script>
  let count = 0;
  $: doubled = count * 2;
</script>

<p>{count} doubled is {doubled}</p>
<button on:click={() => count++}>Add</button>
````

`$:` makes the code reactive, like a live formula.

### Svelte Control Flow

#### if / else if / else Blocks
```` svelte
<script>
  let loggedIn = true;
</script>

{#if loggedIn}
  <p>Welcome back!</p>
{:else}
  <p>Please log in.</p>
{/if}

````
We can add {:else if condition} too, just like JavaScript.

#### each Block – Looping Through Lists
Render a list of items dynamically.
````svelte
<script>
  let users = ["Alice", "Bob", "Charlie"];
</script>

<ul>
  {#each users as user}
    <li>{user}</li>
  {/each}
</ul>

````

with an index:
````svelte
{#each users as user, i}
  <li>{i + 1}. {user}</li>
{/each}

````

Just like .map() in JavaScript, but much simpler in the template.

#### await Block – Waiting for Promises
Show different content based on the state of a Promise.

````svelte
<script>
  let userPromise = fetch('/api/user').then(res => res.json());
</script>

{#await userPromise}
  <p>Loading...</p>
{:then user}
  <p>Hello, {user.name}!</p>
{:catch error}
  <p>Error: {error.message}</p>
{/await}

````
{#await}: shows while waiting
{:then}: shows result when resolved
{:catch}: shows if there’s an error

### Styling in Svelte

Svelte gives us powerful styling options right inside your component.

1. Scoped Styles (Default Behavior)
When you add a `<style>` tag inside a Svelte component, it’s automatically scoped — meaning it applies only to that component.
````svelte
<style>
  h1 {
    color: teal;
  }
</style>

<h1>Hello</h1>

````
No class conflicts,  Clean separation per component,  No special setup needed

2. Global Styles
If you want a style to apply globally (to all components), use the :global selector.
````svelte
<style>
  :global(body) {
    margin: 0;
    font-family: sans-serif;
  }

  :global(.btn) {
    background: black;
    color: white;
    padding: 0.5rem;
  }
</style>

````
You’ll often use this for:body, html, Utility classes (e.g. .btn, .container), Reset styles

3.  CSS Variables & Component Props
You can use props to change styles dynamically via style attributes or classes.
````svelte
<script>
  export let color = "blue";
</script>

<div style="color: {color}">
  Styled Text
</div>

````
You can also pass class names in:
````svelte

<!-- Parent -->
<MyComponent class="my-style" />

<!-- Inside MyComponent -->
<div class={$$props.class}>Hello</div>

````
Best practices:
to do : Use scoped styles per component, Use meaningful class names	, Use utility-first CSS (like Tailwind, if preferred)
avoid : Hardcoding pixel values everywhere


### External CSS Frameworks in Frontend Development
These are pre-built collections of styles and utility classes that help you design your app faster without writing all the CSS from scratch.

Why to use a CSS Framework?
Faster development - Use ready-made classes/components
Consistent design - Keep UI uniform across pages/components
Utility helpers - Quick layout/styling (e.g. margin, padding)
 Reusability - Use common patterns like cards, buttons, etc.

 ####  Tailwind CSS (most modern Svelte projects use this)
 “Utility-first CSS framework” – style directly in your HTML.

 ````html
 <button class="bg-blue-500 hover:bg-blue-700 text-white px-4 py-2 rounded">
  Click me
</button>

 ````
 Highly customizable, Minimal CSS files, Works great with Svelte
 You can install it in your SvelteKit project with plugins like:
 ````bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p

 ````

####  Bootstrap
A component-based framework with pre-built styles.
````html
<button class="btn btn-primary">Click me</button>

````
Classic & widely used, Includes grid system and JS components, Might feel heavy/restrictive for custom design

####  Bulma
A lightweight framework that’s easy to learn.

````html
<button class="button is-primary">Click me</button>

````
Clean syntax, No JavaScript, just CSS, Less customizable than Tailwind

When to use css framework:
You want to move fast on UI, Your team already uses one, You like utility-based styling (Tailwind)

when to skip:
You want full design control, You’re learning pure CSS first, You prefer semantic HTML + separate CSS

### Reusable Components in Svelte
Components let you break your app into smaller, manageable, and reusable pieces of UI — like buttons, cards, modals, forms, etc.

benefits: Reuse logic/layout(Use the same UI pattern in multiple places), Simplify structure(Break big pages into small components), Maintain easily(Fix or update one place, affects all)

#### Basic Component Example
simple Button.svelte component:

````svelte
<!-- Button.svelte -->
<script>
  export let text = "Click Me";
  export let onClick = () => {};
</script>

<button on:click={onClick} class="btn">
  {text}
</button>

<style>
  .btn {
    padding: 0.5rem 1rem;
    background-color: teal;
    color: white;
    border-radius: 0.5rem;
    border: none;
  }
</style>

````
Now we can use it everywhere
````svelte
<script>
  import Button from './Button.svelte';

  const handleClick = () => {
    alert('Button clicked!');
  };
</script>

<Button text="Submit" onClick={handleClick} />

````

#### Slots – Custom Content Inside a Component
Slots let you pass HTML/content inside the component.
````svelte
<!-- Card.svelte -->
<div class="card">
  <slot />
</div>

<style>
  .card {
    padding: 1rem;
    border: 1px solid #ddd;
    border-radius: 1rem;
  }
</style>

````

then we can use it like shown here:
````svelte
<Card>
  <h2>Hello</h2>
  <p>This is inside the card!</p>
</Card>

````
Super flexible,Reusable layout structure with different content

#### Combining Components
````svelte
<!-- UserCard.svelte -->
<script>
  export let name;
</script>

<Card>
  <h3>{name}</h3>
  <Button text="Follow" onClick={() => alert(`Followed ${name}`)} />
</Card>

````

### Component Composition Patterns
Component composition is the practice of combining simple, smaller components to create more complex UI elements. The goal is to create components that can be reused and maintained independently.
Why Use Component Composition :
Reusability - Build once, use anywhere in the app
Clarity - Clear separation of concerns (UI, logic)
Maintainability - Easier to update and fix bugs


1.  Parent and Child Components

In Svelte, one component can pass data down to child components via props.

Parent Component
````svelte
<script>
  import Card from './Card.svelte';

  let user = { name: "Alice", age: 30 };
</script>

<Card user={user} />

````

child component
````svelte
<script>
  export let user;
</script>

<div class="card">
  <h2>{user.name}</h2>
  <p>Age: {user.age}</p>
</div>

````

This allows parent components to provide data to their children, while children are dumb components that render UI based on the data passed to them.


2. Conditional Rendering Inside Components
Sometimes you might want to show different content or layouts inside a component depending on some conditions. This can be achieved using Svelte's if, else, and {#each} blocks.

````svelte
<script>
  export let user = { name: 'Alice', age: 30, isOnline: true };
</script>

<div class="user-card">
  <h2>{user.name}</h2>
  <p>Age: {user.age}</p>

  {#if user.isOnline}
    <p>Status: Online</p>
  {:else}
    <p>Status: Offline</p>
  {/if}
</div>

````
Here, the user-card component will conditionally render the online/offline status based on the isOnline property.

3. Slots for Reusability and Flexibility
slots allow you to pass content to a component without modifying its internal structure.

For example, a Modal.svelte component might use a slot for the content:
````svelte
<!-- Modal.svelte -->
<div class="modal">
  <div class="modal-content">
    <slot /> <!-- Custom content passed here -->
  </div>
</div>

````
Now we can use it like this:

````svelte
<Modal>
  <h2>Warning</h2>
  <p>This is a warning message.</p>
</Modal>

````

This keeps the modal component flexible and reusable with different content.

4. Composing Larger Components with Smaller Ones
Often, you will create larger UI components by combining smaller ones. For example, an entire user profile page could be built using smaller components like ProfileHeader, UserPosts, UserBio, etc.
````svelte
<!-- ProfilePage.svelte -->
<script>
  import ProfileHeader from './ProfileHeader.svelte';
  import UserPosts from './UserPosts.svelte';
  import UserBio from './UserBio.svelte';
</script>

<ProfileHeader />
<UserBio />
<UserPosts />

````

Here, ProfilePage.svelte is a composition of 3 child components: ProfileHeader, UserBio, and UserPosts. Each of these components handles its own part of the UI.

5. State Lifting
State lifting is the practice of moving the state to the parent component so that it can be shared by multiple child components. This helps in syncing data between components.

````svelte
<!-- ParentComponent.svelte -->
<script>
  let count = 0;
  const increment = () => count++;
</script>

<ChildCounter count={count} increment={increment} />
<ChildCounter count={count} increment={increment} />

````

````svelte
<!-- ChildCounter.svelte -->
<script>
  export let count;
  export let increment;
</script>

<div>
  <p>Count: {count}</p>
  <button on:click={increment}>Increment</button>
</div>

````
The parent component lifts the state (count) and the increment function to control the state and pass them to the child components.

6.  Reusable Forms and Validation
You can create complex forms by composing smaller form elements (e.g., Input, Checkbox, RadioButton) and manage form submission and validation in a parent component.

````svelte
<!-- Form.svelte -->
<script>
  import Input from './Input.svelte';
  let name = '';
  const submitForm = () => {
    alert(`Submitted: ${name}`);
  };
</script>

<form on:submit|preventDefault={submitForm}>
  <Input bind:value={name} placeholder="Enter your name" />
  <button type="submit">Submit</button>
</form>

````

Here, the Input component is reusable for any form field, and the parent component handles the form logic.

Takeaways for Component Composition
best practice:
Keep components small, focused, and reusable, Use props and slots to pass data and content, Compose multiple components to form a complex UI
things to avoid:
Making one monolithic component for everything, Overcomplicating component APIs with too many options, Trying to do everything in one component

### Fetching API Data in Svelte
In Svelte, fetching data from APIs typically involves using the fetch API (or any other HTTP client like Axios) to get data and then display it in your components.

1. Basic Fetch Example
Let’s say we want to display a list of users from a simple API like `https://jsonplaceholder.typicode.com/users\ . Here’s how you can fetch the data and display it in Svelte.

fetching data:
````svelte
<script>
  let users = [];
  let loading = true;
  let error = null;

  // Fetch data when the component is created
  fetch('https://jsonplaceholder.typicode.com/users')
    .then(response => response.json())
    .then(data => {
      users = data;
      loading = false;
    })
    .catch(err => {
      error = err.message;
      loading = false;
    });
</script>

{#if loading}
  <p>Loading...</p>
{:else if error}
  <p>Error: {error}</p>
{:else}
  <ul>
    {#each users as user}
      <li>{user.name}</li>
    {/each}
  </ul>
{/if}

````

Key Points:
fetch() retrieves data from an API.

then() is used to handle the response when the data is ready.

catch() catches errors (like network issues).

Svelte's {#if} block manages the loading state and error handling.

2. Using Async/Await for Fetching
For better readability, you can use async and await to fetch data instead of using .then() and .catch().

Async/Await Example:
````svelte
<script>
  let users = [];
  let loading = true;
  let error = null;

  const fetchData = async () => {
    try {
      const response = await fetch('https://jsonplaceholder.typicode.com/users');
      users = await response.json();
      loading = false;
    } catch (err) {
      error = err.message;
      loading = false;
    }
  };

  fetchData();
</script>

{#if loading}
  <p>Loading...</p>
{:else if error}
  <p>Error: {error}</p>
{:else}
  <ul>
    {#each users as user}
      <li>{user.name}</li>
    {/each}
  </ul>
{/if}

````

Here, async/await makes the code easier to read and maintain compared to chaining .then() and .catch().

3. Displaying Data Dynamically with Lists
Now that you’ve fetched data, let’s make the UI more dynamic. If you have a list of data (like users), you can dynamically display it using Svelte's {#each} block.

Dynamic List Example:
````svelte

<script>
  let users = [];

  const fetchData = async () => {
    const response = await fetch('https://jsonplaceholder.typicode.com/users');
    users = await response.json();
  };

  fetchData();
</script>

<ul>
  {#each users as user}
    <li>
      <h3>{user.name}</h3>
      <p>{user.email}</p>
    </li>
  {/each}
</ul>

````

4. Handling Loading & Error States
You can manage the loading state and error state as shown in the earlier examples. However, you can also create a global error handler or a more reusable loading spinner if needed.

For example, using a custom loading spinner:
````svelte
{#if loading}
  <div class="spinner">Loading...</div>
{:else if error}
  <p>Error: {error}</p>
{:else}
  <ul>
    {#each users as user}
      <li>{user.name}</li>
    {/each}
  </ul>
{/if}

````

You can create a simple spinner component, like this:

````svelte
<!-- Spinner.svelte -->
<div class="spinner">Loading...</div>

<style>
  .spinner {
    animation: spin 1s infinite linear;
  }

  @keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
  }
</style>

````

And use it like:

````svelte
{#if loading}
  <Spinner />
{:else if error}
  <p>Error: {error}</p>
{:else}
  <ul>
    {#each users as user}
      <li>{user.name}</li>
    {/each}
  </ul>
{/if}

````

5. handling Pagination
When working with APIs that provide large datasets (e.g., users, posts), you’ll likely need to handle pagination (loading data in chunks).

For example, fetching data with pagination could look like this:

````svelte
<script>
  let users = [];
  let page = 1;
  let loading = false;
  let error = null;

  const fetchData = async () => {
    loading = true;
    try {
      const response = await fetch(`https://jsonplaceholder.typicode.com/users?_page=${page}&_limit=10`);
      users = await response.json();
      loading = false;
    } catch (err) {
      error = err.message;
      loading = false;
    }
  };

  fetchData();
</script>

<button on:click={() => { page--; fetchData(); }} disabled={page === 1}>
  Previous
</button>
<button on:click={() => { page++; fetchData(); }} disabled={loading}>
  Next
</button>

{#if loading}
  <p>Loading...</p>
{:else if error}
  <p>Error: {error}</p>
{:else}
  <ul>
    {#each users as user}
      <li>{user.name}</li>
    {/each}
  </ul>
{/if}
````

6. Fetching Data Inside Lifecycle Methods in Svelte
In Svelte, lifecycle methods (also called lifecycle hooks) allow you to run code at different stages of a component’s life. These hooks are particularly useful when you need to perform actions like fetching data, setting up subscriptions, or cleaning up resources.

One of the most common lifecycle hooks you'll use for data fetching is the onMount function.

The onMount Lifecycle Hook:
The onMount function is called after the component has been rendered in the DOM. This makes it an ideal place to put any asynchronous operations like fetching data from an API.

Basic Example of Using onMount:

````svelte
<script>
  import { onMount } from 'svelte';

  let users = [];
  let loading = true;
  let error = null;

  onMount(async () => {
    try {
      const response = await fetch('https://jsonplaceholder.typicode.com/users');
      users = await response.json();
      loading = false;
    } catch (err) {
      error = err.message;
      loading = false;
    }
  });
</script>

{#if loading}
  <p>Loading...</p>
{:else if error}
  <p>Error: {error}</p>
{:else}
  <ul>
    {#each users as user}
      <li>{user.name}</li>
    {/each}
  </ul>
{/if}

````

Key Points:
onMount() is imported from svelte and used to run code once the component is mounted in the DOM.
We define our fetching logic inside onMount(), ensuring that the data is loaded once the component is ready.

Why Use onMount for Fetching Data?
By using onMount, you ensure that data fetching only occurs once when the component is rendered. This is important for avoiding unnecessary network requests on every render or re-render.

Initial Fetch: The first time the component is loaded, it will trigger the data fetch.

No Re-fetching on Re-renders: If the component re-renders due to reactive state changes, it won’t re-fetch the data unless explicitly re-triggered.
Alternative: Using onDestroy for Cleanup

If you're subscribing to an external data stream (e.g., WebSocket, or event listeners), you might want to clean up after your component unmounts. This can be done with the onDestroy hook.

````svelte
<script>
  import { onMount, onDestroy } from 'svelte';

  let users = [];
  let loading = true;

  onMount(async () => {
    try {
      const response = await fetch('https://jsonplaceholder.typicode.com/users');
      users = await response.json();
      loading = false;
    } catch (err) {
      loading = false;
    }
  });

  onDestroy(() => {
    console.log('Component is being destroyed');
  });
</script>

````
Here, onDestroy() allows you to handle any cleanup (e.g., cancel network requests or unsubscribe from event listeners) when the component is no longer in use.

### State Management in Svelte
State management refers to how we handle and update the data that determines the state of our application. In Svelte, state management is straightforward, and you don't need external libraries like Redux or Vuex because Svelte has built-in reactivity.In Svelte, reactive state is what makes the UI update automatically when the underlying data changes. This is one of Svelte's strongest features.


1. Reactive Variables
A reactive variable in Svelte automatically updates the DOM whenever its value changes. You can make a variable reactive by using the $: syntax

Example:
````svelte
<script>
  let count = 0;

  // This is a reactive statement
  $: doubled = count * 2;
</script>

<p>Count: {count}</p>
<p>Doubled: {doubled}</p>

<button on:click={() => count++}>Increment</button>

````

Key Points:
Reactive statements (e.g., $: doubled = count * 2;) automatically re-run whenever the value of count changes.

In the example, whenever the button is clicked, the count is incremented, and the doubled value automatically updates.

2. Updating State
To update state, you simply change the value of a variable. Svelte takes care of updating the DOM for you.

````Example
<script>
  let name = "Alice";
  
  // A function to change the name
  function changeName() {
    name = "Bob";
  }
</script>

<p>Name: {name}</p>
<button on:click={changeName}>Change Name</button>

````

3. Two-Way Binding

Svelte makes it very easy to bind form elements (like inputs, checkboxes, and selects) to a variable using two-way binding. This means that the input field will automatically update the variable, and the variable will automatically update the input field when its value changes.

Example:
````svelte
<script>
  let name = "Alice";
</script>

<input bind:value={name} />
<p>Name: {name}</p>

````

Key Points:
The bind:value directive automatically creates a two-way binding between the input and the name variable.

When the user types in the input field, the name variable updates and vice versa.

4. Store for Global State Management
In more complex applications, managing state across multiple components can become challenging. This is where Svelte stores come into play. A store is an object that holds a value and allows multiple components to subscribe to changes to that value.
Basic Store Example:
Svelte has built-in store utilities like writable, readable, and derived for managing state.

Writable Store:

A writable store allows both reading and updating its value.

````svelte
<script>
  import { writable } from 'svelte/store';

  // Creating a writable store
  const count = writable(0);

  // Function to update the store value
  function increment() {
    count.update(n => n + 1);
  }
</script>

<p>Count: {$count}</p>
<button on:click={increment}>Increment</button>

````

key points:
writable creates a store that can be updated and read.

$count is the store subscription syntax in Svelte. It makes sure the component re-renders whenever the store value changes.

count.update() is used to update the store value. You can also use count.set() to directly set the value


Readable Store:
A readable store allows you to only read its value, but not update it directly.
````svelte
<script>
  import { readable } from 'svelte/store';

  // Creating a readable store
  const time = readable(new Date(), set => {
    const interval = setInterval(() => set(new Date()), 1000);

    // Cleanup when the component is destroyed
    return () => clearInterval(interval);
  });
</script>

<p>Current Time: {$time}</p>

````

Key Points:
readable creates a store that only allows reading.

The store's value is updated every second using a setInterval, and the store cleans up the interval when the component is destroyed.


Derived Store
A derived store is used to calculate new values based on the values of other stores.

````svelte
<script>
  import { writable, derived } from 'svelte/store';

  // Writable store
  const count = writable(0);

  // Derived store that computes doubled value
  const doubledCount = derived(count, $count => $count * 2);
</script>

<p>Count: {$count}</p>
<p>Doubled Count: {$doubledCount}</p>

<button on:click={() => count.update(n => n + 1)}>Increment</button>

````

derived is used to create a store whose value depends on one or more other stores.

The derived store will automatically update whenever the source stores (count in this case) change.

5.  Multiple Stores and Composition
In larger applications, you might have multiple stores for different parts of the app. You can combine them in a component by importing and subscribing to them.

````svelte
<script>
  import { writable } from 'svelte/store';

  const user = writable({ name: 'Alice', age: 25 });
  const theme = writable('light');
</script>

<p>User: {$user.name}, Age: {$user.age}</p>
<p>Theme: {$theme}</p>

````


Key Points:
You can combine multiple stores into your component and use them independently.

Svelte ensures that the UI will automatically update when any store’s value changes.

Takeaways for State Management in Svelte
best practice:
1. Use reactive variables for simple state management
2. Use writable stores for shared state across components
3. Use bind for two-way binding in forms
4. Use derived stores to calculate values based on other stores

to avoid:
Over-complicating simple state with unnecessary libraries
Storing too much data in a single store without clear separation of concerns
Forgetting to unsubscribe from stores, which can lead to memory leaks
Avoiding stores altogether when your app grows in complexity
