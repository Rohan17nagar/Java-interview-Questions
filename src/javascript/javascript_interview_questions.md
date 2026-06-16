# 100 JavaScript Interview Questions & Answers Master Guide

This comprehensive document contains in-depth definitions, concrete code examples, and practical real-world analogies for the top 100 JavaScript interview questions.

---

## Table of Contents

1. [Core Fundamentals & Syntax (1-15)](#core-fundamentals--syntax-1-15)
2. [Functions & Scope (16-30)](#functions--scope-16-30)
3. [Objects & Arrays (31-50)](#objects--arrays-31-50)
4. [Object-Oriented Programming & Prototypes (51-63)](#object-oriented-programming--prototypes-51-63)
5. [Asynchronous JavaScript (64-75)](#asynchronous-javascript-64-75)
6. [DOM & Browser Web APIs (76-85)](#dom--browser-web-apis-76-85)
7. [Modern ES6+ Features & Tooling (86-93)](#modern-es6-features--tooling-86-93)
8. [Error Handling, Memory, & Performance (94-100)](#error-handling-memory--performance-94-100)

---

## Core Fundamentals & Syntax (1-15)

### 1. What are the different data types available in JavaScript?

- **Definition:** JavaScript has 8 built-in data types. 7 are primitive (immutable, stored by value): `Number`, `String`, `Boolean`, `Undefined`, `Null`, `Symbol`, and `BigInt`. 1 is structural/non-primitive: `Object` (which includes Arrays, Functions, and Dates).
- **Code Example:**

```javascript
const num = 42; // Number
const str = "Hello"; // String
const bool = true; // Boolean
let undef; // Undefined
const empty = null; // Null
const sym = Symbol("id"); // Symbol
const big = 900719925474n; // BigInt
const obj = { key: "val" }; // Object
```

- **Real-World Analogy:** A primitive data type is like a single stamped gold coin; its value is stamped directly on it. An object is like a shipping storage locker—it contains labeled shelves (properties) holding various items inside it.

### 2. What is the difference between primitive data types and non-primitive (reference) data types?

- **Definition:** Primitives store the actual value directly in the location that the variable accesses (Stack memory). Assigning a primitive copies the value. Non-primitives (Objects) store a reference (a memory address pointer) pointing to where the actual data sits (Heap memory). Assigning an object copies the reference pointer, not the actual object data.
- **Code Example:**

```javascript
// Primitive
let a = 10;
let b = a; // copies value
b = 20;
console.log(a); // 10 (unchanged)

// Reference
let obj1 = { name: "Alice" };
let obj2 = obj1; // copies reference pointer
obj2.name = "Bob";
console.log(obj1.name); // "Bob" (mutated!)
```

- **Real-World Analogy:** A primitive is like handing someone a photocopy of a document; if they scribble on their copy, your original sheet remains clean. A reference type is like giving someone the Google Docs shareable URL to your live project file; if they modify the text, everyone sees the edits.

### 3. Explain the differences between `var`, `let`, and `const`.

- **Definition:**
  - `var`: Function-scoped or globally-scoped, hoisted to the top of its scope, initializes as `undefined`, and allows re-declaration.
  - `let`: Block-scoped, hoisted but sits in a "Temporal Dead Zone" (TDZ) until evaluation, and cannot be re-declared in the same block.
  - `const`: Block-scoped like `let`, cannot be re-declared or re-assigned, and requires an immediate initial value.
- **Code Example:**

```javascript
if (true) {
  var x = "var";
  let y = "let";
  const z = "const";
}
console.log(x); // "var" (Escaped block scope!)
// console.log(y); // ReferenceError
// console.log(z); // ReferenceError
```

- **Real-World Analogy:** `var` is like a bulletin board across the entire company floor—anyone can pin things over it or look at it from down the hall. `let` is like an individual team whiteboard inside a locked conference room. `const` is that same team whiteboard, but the text is permanently engraved in granite.

### 4. What is the difference between `null` and `undefined`?

- **Definition:** `undefined` means a variable has been declared but has not yet been assigned a specific value. `null` is an assignment value that explicitly represents the intentional total absence of any object value.
- **Code Example:**

```javascript
let user;
console.log(user); // undefined

let cart = null; // System intentionally knows the cart is currently empty
console.log(cart); // null
```

- **Real-World Analogy:** `undefined` is an unboxed, unlabeled cardboard box sitting in your garage—you haven't even decided what goes there yet. `null` is a box you intentionally emptied and wrapped in a label that explicitly states "Empty Box".

### 5. What is the purpose of the `typeof` operator? What does `typeof null` return and why?

- **Definition:** The `typeof` operator returns a string indicating the data type of the unevaluated operand. Executing `typeof null` returns `"object"`. This is a historic, unfixable bug from the very first version of JavaScript where values were stored in 32-bit units, and the type tag for objects was `000`. Since `null` was represented as a pointer to nothing (all zeros), it mistakenly mapped to `"object"`.
- **Code Example:**

```javascript
console.log(typeof "Hello"); // "string"
console.log(typeof 42); // "number"
console.log(typeof null); // "object" (Legacy JS bug)
```

- **Real-World Analogy:** `typeof` is like a barcode scanner at a store checkout that tells you what type of item you have. Scanning a generic unbranded gift card (`null`) returns a reading of `"Physical Merchandise Item"` (`object`) due to an unpatched firmware glitch in the store's oldest scanners.

### 6. Explain the difference between the `==` (loose equality) and `===` (strict equality) operators.

- **Definition:** `==` compares two values for equality after performing implicit type coercion (converting both values to a common type first). `===` checks both the equality of the value and the equality of the underlying data type without performing coercion.
- **Code Example:**

```javascript
console.log(5 == "5"); // true  (string "5" is coerced to number 5)
console.log(5 === "5"); // false (types 'number' and 'string' do not match)
```

- **Real-World Analogy:** Loose equality (`==`) is like a relaxed bouncer at a nightclub who lets someone inside if their passport name loosely matches their ticket nickname. Strict equality (`===`) is like a customs border control officer who will reject entry if the official passport and visa paperwork do not perfectly match across data systems.

### 7. What is type coercion in JavaScript, and can you provide an example of implicit vs. explicit coercion?

- **Definition:** Type coercion is the automatic or deliberate conversion of a value from one data type to another. Implicit coercion occurs automatically behind the scenes when JavaScript encounters mismatched types in operations. Explicit coercion happens when a developer manually invokes a built-in function to change a type.
- **Code Example:**

```javascript
// Implicit Coercion
let result1 = "5" + 2; // "52" (number coerced to string for concatenation)
let result2 = "5" - 2; // 3    (string coerced to number for subtraction)

// Explicit Coercion
let result3 = Number("5") + 2; // 7
```

- **Real-World Analogy:** Implicit coercion is traveling to a foreign country where a local merchant silently converts your foreign currency paper bill to local coins to give you change. Explicit coercion is walking directly into an international airport currency exchange kiosk to deliberately swap your cash.

### 8. What are "falsy" values in JavaScript? List all of them.

- **Definition:** A falsy value is a value that evaluates to `false` when encountered in a Boolean context (such as an `if` condition statement).
- **Code Example:**

```javascript
// The 8 falsy values:
if (false) {
}
if (0) {
}
if (-0) {
}
if (0n) {
} // BigInt zero
if ("") {
} // Empty string
if (null) {
}
if (undefined) {
}
if (NaN) {
}
```

- **Real-World Analogy:** Think of a security gate that only lets valid tokens through. If you present a blank ticket, a zero-dollar gift card, or an empty wallet, the gate interprets these items as a lack of assets and denies entry.

### 9. What is the purpose of the double exclamation mark (`!!`) operator?

- **Definition:** The `!!` operator explicitly forces any JavaScript value to convert into its corresponding boolean equivalent (`true` or `false`). The first `!` inverts the value's truthiness to a strict boolean, and the second `!` inverts it back to its accurate boolean state.
- **Code Example:**

```javascript
const username = "JohnDoe";
const hasUser = !!username;
console.log(hasUser); // true

const score = 0;
console.log(!!score); // false
```

- **Real-World Analogy:** It is like turning a light switch on and off rapidly to test if electricity is actively running to a room, or asking a friend: "Is it _not true_ that you _don't_ have a spare car key?" to force a straight "Yes" or "No" response.

### 10. What is the nullish coalescing operator (`??`) and how does it differ from the logical OR (`||`) operator?

- **Definition:** The `??` operator returns its right-hand side operand only when its left-hand side operand is strictly `null` or `undefined`. The `||` operator returns its right-hand side operand if the left-hand side evaluates to _any_ falsy value (such as `0` or an empty string `""`).
- **Code Example:**

```javascript
const score = 0;

const finalScore1 = score || 10; // 10 (because 0 is falsy)
const finalScore2 = score ?? 10; // 0  (because 0 is not null/undefined)
```

- **Real-World Analogy:** `||` is an aggressive backup driver who takes over the wheel if you show _any_ sign of weakness (including if you are just resting your arms at `0` mph). `??` is a cautious backup driver who only takes over the steering wheel if you completely pass out or disappear from the vehicle (`null`/`undefined`).

### 11. What is the basic use of the `isNaN()` function, and how does it differ from `Number.isNaN()`?

- **Definition:** `isNaN()` attempts to coerce its argument to a Number first, then checks if it is `NaN`. This leads to false positives for non-numeric strings. `Number.isNaN()` does _not_ perform any implicit type coercion; it returns true _only_ if the current value is explicitly of type `Number` and evaluates to `NaN`.
- **Code Example:**

```javascript
console.log(isNaN("hello")); // true  ("hello" is coerced to NaN)
console.log(Number.isNaN("hello")); // false (type is string, not a NaN number)
console.log(Number.isNaN(NaN)); // true
```

- **Real-World Analogy:** `isNaN()` is an over-eager customs agent who tries to treat everything like a box of food, checking if it is spoiled. If you hand them a steel wrench, they try to taste it, spit it out, and declare it "spoiled food". `Number.isNaN()` checks if the item is explicitly a food crate first, and only declares it bad if it is an actual food container holding spoiled items.

### 12. What is the purpose of the conditional (ternary) operator?

- **Definition:** The ternary operator is a compact inline substitute for a standard `if...else` statement block. It accepts three operational blocks: a condition, an expression to execute if the condition evaluates to truthy, and an expression to execute if it is falsy.
- **Code Example:**

```javascript
const age = 20;
const access = age >= 18 ? "Allowed" : "Denied";
console.log(access); // "Allowed"
```

- **Real-World Analogy:** It is a fork in the road with a single regulatory road sign: "If you have a VIP pass, drive left; otherwise, drive right."

### 13. How do you create multiline strings and embed expressions using template literals?

- **Definition:** Template literals use backticks (`` ` ``) instead of standard quotes. They allow you to span strings across multiple text lines naturally without `\n` characters and let you directly embed code variables or expressions using `${expression}` syntax blocks.
- **Code Example:**

```javascript
const item = "laptop";
const cost = 999;

const message = `You bought a ${item}.
The total bill with tax is $${cost * 1.1}.`;
```

- **Real-World Analogy:** It is like a pre-printed form letter template where blank cut-out fields are automatically filled in with specific words or math operations as the letter feeds through the printer.

### 14. What are the different loops available in JavaScript (e.g., `for`, `while`, `do...while`)?

- **Definition:**
- `for`: Loops through a block of code a set number of times using an explicit counter.
- `while`: Loops through a block of code as long as a specified condition remains `true`.
- `do...while`: Loops through a block of code exactly once _before_ evaluating the truth statement condition, then repeats as long as the condition remains true.
- **Code Example:**

```javascript
// For loop
for (let i = 0; i < 3; i++) console.log(i);

// While loop
let count = 0;
while (count < 3) {
  console.log(count);
  count++;
}

// Do...While loop
let x = 5;
do {
  console.log(x); // prints 5 once even though condition is false
} while (x < 3);
```

- **Real-World Analogy:** A `for` loop is doing 10 jumping jacks by counting aloud from 1 to 10. A `while` loop is continuously sweeping your kitchen floor until it looks clean. A `do...while` loop is taking a bite of a mysterious food dish first, and _then_ deciding if you want to keep eating based on how it tasted.

### 15. What is the purpose of `break` and `continue` statements inside loops?

- **Definition:** `break` immediately terminates the loop entirely, shifting code execution down past the loop's closing brackets. `continue` immediately halts the current loop block iteration and skips to evaluating the next cycle step of the loop.
- **Code Example:**

```javascript
for (let i = 1; i <= 5; i++) {
  if (i === 2) continue; // skips printing 2
  if (i === 4) break; // stops the loop completely at 4
  console.log(i); // Output: 1, 3
}
```

- **Real-World Analogy:** Think of an assembly line inspecting 5 boxes. `continue` is finding a minor box wrinkle, throwing that single box in the recycling bin, and immediately pulling the next box forward. `break` is spotting a dangerous hazard on the assembly line, pressing the bright red emergency shutdown button, and walking out of the building.

---

## Functions & Scope (16-30)

### 16. What is the difference between a Function Declaration and a Function Expression?

- **Definition:** Function Declarations are standalone statements that are hoisted into memory at compile time, meaning they can be safely invoked before they appear in the source code file. Function Expressions are functions assigned to variables; they follow the variable's hoisting rules and cannot be invoked before they are evaluated in the script runtime.
- **Code Example:**

```javascript
// Declaration - Hoisted safely
greet();
function greet() {
  console.log("Hello!");
}

// Expression - Not hoisted before assignment
// expGreet(); // TypeError: expGreet is not a function
const expGreet = function () {
  console.log("Hi!");
};
```

- **Real-World Analogy:** A function declaration is like a permanent emergency fire exit built directly into a concrete wall structure when the building was raised. A function expression is like rolling out a temporary, movable safety ladder that is only available after a staff member fetches it from storage.

### 17. What are Arrow Functions, and how do they differ from regular functions?

- **Definition:** Arrow functions offer a compact syntax introduced in ES6. They differ from regular functions because they do not have their own context for the `this` keyword, do not have access to the `arguments` array object, cannot be used as prototype Object constructors, and cannot use the `yield` statement.
- **Code Example:**

```javascript
const regular = function (a, b) {
  return a + b;
};
const arrow = (a, b) => a + b; // Implicit return if braces omitted
```

- **Real-World Analogy:** A regular function is a traditional business office suite with its own independent address, local staff directory (`arguments`), and a customized manager (`this`). An arrow function is a temporary, collaborative desk inside an open co-working space that inherits its atmosphere, internet connection, and manager directly from the surrounding floor team.

### 18. What is the `arguments` object in JavaScript functions, and why does it not work inside arrow functions?

- **Definition:** The `arguments` object is a local, array-like object available inside non-arrow functions containing the values of the arguments passed to that function. Arrow functions do not possess an internal `arguments` binding; instead, they lexically look up and reference the arguments of their closest surrounding non-arrow parent function wrapper.
- **Code Example:**

```javascript
function regularFunc() {
  console.log(arguments[0]); // "apple"
}
regularFunc("apple");

const arrowFunc = () => {
  // console.log(arguments); // ReferenceError in strict global context
};
```

- **Real-World Analogy:** In a traditional restaurant, every table has a physical waiter notepad (`arguments`) detailing exactly what that specific table ordered. An arrow function is like a customer sitting at an open buffet counter who doesn't get an individual paper order slip, but can look up at the main menu board shared by the room.

### 19. Explain Global scope, Function scope, and Block scope.

- **Definition:**
  - Global scope: Accessible anywhere in the entire file application context.
  - Function scope: Variables declared with `var` inside a function are accessible only within that function block.
  - Block scope: Variables declared with `let` or `const` inside curly braces `{}` are accessible only within that specific code block.
- **Code Example:**

```javascript
const globalVar = "Global";

function testScope() {
  var funcVar = "Function";
  if (true) {
    let blockVar = "Block";
  }
  // console.log(blockVar); // ReferenceError
  console.log(funcVar); // Accessible
}
```

- **Real-World Analogy:** Global scope is public air outside that everyone can breathe. Function scope is like talking inside a private corporate office building. Block scope is like whispering to a colleague while hiding inside a single locked storage closet within that office building.

### 20. What is Lexical Scoping?

- **Definition:** Lexical scoping (or static scoping) means that the scope of a variable is determined entirely by its structural placement within the physical source code text file during compilation. Nested inner functions have structural access to variables declared in their outer parent scopes.
- **Code Example:**

```javascript
function outer() {
  const outerValue = "I am outside!";
  function inner() {
    console.log(outerValue); // Accesses parent variable naturally
  }
  inner();
}
outer();
```

- **Real-World Analogy:** Think of a set of translucent Russian nesting dolls. The small doll sitting nested deep inside can look outward through its clear plastic layers to see what the larger outer doll has written on its shell, but the large outer doll cannot look inward to read what is written on the small doll's hidden paper note.

### 21. What is Hoisting? How does hoisting behave differently for `var`, `let`, `const`, and function declarations?

- **Definition:** Hoisting is the behavior where the engine allocates memory declarations for variables and functions before executing the step-by-step code. Function declarations are hoisted with their complete bodies. Variables declared with `var` are hoisted and initialized with a value of `undefined`. Variables declared with `let` and `const` are hoisted into memory but remain uninitialized in a "Temporal Dead Zone" (TDZ) until their actual line of code is evaluated.
- **Code Example:**

```javascript
console.log(a); // undefined (due to var hoisting)
var a = 5;

// console.log(b); // ReferenceError: Cannot access 'b' before initialization
let b = 10;
```

- **Real-World Analogy:** Hoisting is like a theater staff walking through an empty auditorium setting up empty chairs with name placards on them before the doors open. A `var` placard is set out immediately but wrapped in an unreadable sheet (`undefined`). A `let` or `const` placard is placed on the seat, but a security guard stands over it (TDZ) and refuses to let you look at or touch it until the event officially starts.

### 22. What is a Closure? Provide a practical use case for closures.

- **Definition:** A closure is a function that retains access to its lexical scope (outer variables) even when that function is executed outside of its original originating block scope context. This is highly useful for managing private state data without exposing variables globally.
- **Code Example:**

```javascript
function createCounter() {
  let count = 0; // Private variable
  return function () {
    count++;
    return count;
  };
}
const counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2
```

- **Real-World Analogy:** A closure is like a hotel room key card. Even after the check-in desk clerk finishes their daily shift and goes home, your physical key card remembers its unique structural access permissions and lets you back into your private room.

### 23. What is an IIFE (Immediately Invoked Function Expression) and what is its traditional syntax?

- **Definition:** An IIFE is a function expression that runs immediately as soon as the JavaScript engine compiles and encounters it. It is commonly wrapped in parentheses to treat the statement explicitly as an expression, followed by an execution invocation set `()`. It prevents polluting the global scope namespace.
- **Code Example:**

```javascript
(function () {
  const privateSecret = "IIFE Init";
  console.log(privateSecret);
})();
```

- **Real-World Analogy:** An IIFE is like a self-destructing message envelope that opens up, reads its text content aloud, and immediately dissolves into ash, ensuring no traces of its internal data spill onto the desk space.

### 24. What are Higher-Order Functions? Give an example.

- **Definition:** A Higher-Order Function is any function that performs at least one of the following tasks: it accepts one or more functions as input parameters, or it returns an executable function as its final operational output.
- **Code Example:**

```javascript
const repeatTwice = (callback) => {
  callback();
  callback();
};
repeatTwice(() => console.log("Hello HoF"));
```

- **Real-World Analogy:** A Higher-Order function is like a manager hiring an independent contractor. The manager doesn't personally carry out the manual task; instead, they take a specialist worker (a callback function) and tell them exactly when and how many times to execute their work trade.

### 25. What is a Callback Function?

- **Definition:** A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some routine action or respond to an event.
- **Code Example:**

```javascript
function processUser(name, callback) {
  console.log(`Processing ${name}`);
  callback();
}
processUser("Alice", () => console.log("Callback Done!"));
```

- **Real-World Analogy:** A callback is like giving a service auto-shop your phone number when you drop off your car. You don't stand around waiting for hours; you go about your day, and they use your number to call you back when the car is ready.

### 26. What are Default Parameters in JavaScript functions?

- **Definition:** Default parameters allow named function parameters to be initialized with default backup values if no value or an explicit value of `undefined` is passed into the function call.
- **Code Example:**

```javascript
function welcomeUser(user = "Guest") {
  return `Welcome, ${user}!`;
}
console.log(welcomeUser()); // "Welcome, Guest!"
console.log(welcomeUser("Alice")); // "Welcome, Alice!"
```

- **Real-World Analogy:** It is like a smart electronic form field that automatically fills in your home state as "California" unless you explicitly click the dropdown box and select a different location.

### 27. Explain the concept of Rest Parameters (`...args`) and how they work in a function's arguments list.

- **Definition:** The rest parameter syntax allows a function to accept an indefinite number of arguments as a clean, native JavaScript Array. It must always be the last named parameter in the function declaration signature.
- **Code Example:**

```javascript
function sumAll(...numbers) {
  return numbers.reduce((acc, curr) => acc + curr, 0);
}
console.log(sumAll(1, 2, 3, 4)); // 10
```

- **Real-World Analogy:** It is like a flexible hitchhiker backpack that expands to hold whatever loose items you toss into it, gathering them into a single organized container.

### 28. What is Function Currying?

- **Definition:** Currying is a functional programming technique that transforms a function that takes multiple arguments simultaneously into a series of nested functions that take those arguments one at a time.
- **Code Example:**

```javascript
const uncurriedSum = (a, b) => a + b;

// Curried version
const curriedSum = (a) => (b) => a + b;
console.log(curriedSum(2)(3)); // 5
```

- **Real-World Analogy:** Currying is like buying a modular furniture set. Instead of delivery workers dragging a massive, pre-assembled multi-room sofa through your narrow front door all at once, they carry in one modular piece at a time and clip them together sequentially.

### 29. What is a Pure Function, and what are its characteristics?

- **Definition:** A pure function is a deterministic function that always returns the exact same output given the exact same input parameters, and causes zero observable side effects (such as modifying external global variables, mutating input objects, or hitting network endpoints).
- **Code Example:**

```javascript
// Pure Function
const add = (a, b) => a + b;

// Impure Function (mutates external state)
let total = 0;
const addImpure = (a) => (total += a);
```

- **Real-World Analogy:** A pure function is like an ordinary calculator. Every single time you type `2 + 2`, it will output `4`. It doesn't secretly change the brightness of the room's lights or modify files on your computer while calculating.

### 30. What is recursion, and what are the mandatory components of a recursive function to prevent a stack overflow?

- **Definition:** Recursion is a programming technique where a function calls itself to solve smaller sub-problems. To prevent infinite loops that cause a stack overflow error, a recursive function must have: a **Base Case** (the termination condition that stops execution) and a **Recursive Step** (which moves the operational data state closer to the base case).
- **Code Example:**

```javascript
function factorial(n) {
  if (n <= 1) return 1; // Base case
  return n * factorial(n - 1); // Recursive step
}
console.log(factorial(5)); // 120
```

- **Real-World Analogy:** Recursion is like peeling a large onion down layer by layer. The recursive step is peeling off one outer skin layer to reveal a slightly smaller onion underneath. The base case is reaching the core center point where there are no more layers left to peel, ending the task.

---

## Objects & Arrays (31-50)

### 31. What are the different ways to create an object in JavaScript?

- **Definition:** Objects can be created using Object Literals, the `new Object()` constructor pattern, factory functions, constructor functions with the `new` keyword, `Object.create()`, or modern ES6 Class templates.
- **Code Example:**

```javascript
const lit = { name: "Literal" }; // Object Literal
const constObj = new Object(); // Constructor pattern
const protoObj = Object.create({ protoKey: 1 }); // From prototype
```

- **Real-World Analogy:** Creating an object literal is like crafting a birdhouse from scratch using raw loose lumber on your workbench. Using a Class constructor is like running an automated assembly line factory floor that stamps out identical prefabricated birdhouses using a master blueprinted mold layout.

### 32. Explain the difference between Dot notation and Bracket notation for accessing object properties.

- **Definition:** Dot notation (`obj.prop`) requires property names to be valid identifiers that are hardcoded directly into the script. Bracket notation (`obj["prop"]`) is highly flexible because it accepts dynamic variable evaluations, string evaluation statements, and names containing spaces, numbers, or special characters.
- **Code Example:**

```javascript
const user = { name: "Alex", "user age": 30 };
console.log(user.name); // Dot notation

const key = "name";
console.log(user[key]); // Bracket notation with dynamic variable
console.log(user["user age"]); // Bracket notation for invalid identifier strings
```

- **Real-World Analogy:** Dot notation is like pushing a dedicated physical button on an elevator marked `[Lobby]`. Bracket notation is like speaking into a smart intercom system, saying the variable phrase: "Take me to the floor listed on this piece of paper I am holding."

### 33. What is the difference between a Shallow Copy and a Deep Copy? How can you achieve each?

- **Definition:** A shallow copy duplicates only the top-level values of an object; any nested objects within it retain their original reference addresses. A deep copy copies absolutely all nesting levels recursively, ensuring zero shared references. Shallow copies use `{...obj}` or `Object.assign()`. Deep copies traditionally use `structuredClone(obj)` or `JSON.parse(JSON.stringify(obj))`.
- **Code Example:**

```javascript
const original = { a: 1, nested: { b: 2 } };

// Shallow Copy
const shallow = { ...original };
shallow.nested.b = 99; // Alters the original object's nested data!

// Deep Copy
const deep = structuredClone(original);
```

- **Real-World Analogy:** A shallow copy of a physical house blueprint duplicates the main outer structural walls but keeps a single shared key pointer to a shared electrical fuse box down the street. A deep copy creates an entirely new independent house on a new lot with its own dedicated electrical fuse infrastructure.

### 34. What is Object and Array Destructuring? Provide a brief code syntax snippet for both.

- **Definition:** Destructuring is an ES6 expression syntax pattern that allows you to cleanly unpack values from arrays or properties from objects into distinct, independent variables.
- **Code Example:**

```javascript
// Object Destructuring
const person = { title: "Dev", exp: 5 };
const { title, exp } = person;

// Array Destructuring
const coords = [10, 20];
const [x, y] = coords;
```

- **Real-World Analogy:** Instead of unboxing an entire delivered tech kit box tool by tool, destructuring is like holding out both hands and shouting: "Give me just the camera lens and the charger battery directly out of that shipment bag!"

### 35. What is the Spread Operator (`...`) and how is it used with objects and arrays?

- **Definition:** The spread operator expands an iterable collection (like an array or an object) into individual discrete elements or key-value pairs.
- **Code Example:**

```javascript
const arr1 = [1, 2];
const arr2 = [...arr1, 3, 4]; // [1, 2, 3, 4]

const baseObj = { x: 1 };
const fullObj = { ...baseObj, y: 2 }; // { x: 1, y: 2 }
```

- **Real-World Analogy:** It is like dumping out a bag of marbles onto a table so that every single marble sits separate, spread out, and exposed, rather than keeping them contained inside the pouch container.

### 36. How do you check if a specific property exists inside an object?

- **Definition:** Property presence can be validated using the `in` operator (which checks local properties and inherited prototype properties) or the `Object.hasOwn()` method (which explicitly checks _only_ the object's direct, non-inherited properties).
- **Code Example:**

```javascript
const car = { make: "Tesla" };
console.log("make" in car); // true
console.log("toString" in car); // true (inherited)
console.log(Object.hasOwn(car, "make")); // true
console.log(Object.hasOwn(car, "toString")); // false (inherited)
```

- **Real-World Analogy:** The `in` operator asks if a tool is available anywhere in your workshop (including tools borrowed from your neighbor). `Object.hasOwn()` asks if that tool is explicitly owned by you and stored inside your personal toolbox.

### 37. What is the difference between `Object.freeze()` and `Object.seal()`?

- **Definition:** `Object.freeze()` makes an object completely immutable: you cannot add, delete, or modify properties. `Object.seal()` prevents adding or deleting properties, but allows modifying the values of existing properties.
- **Code Example:**

```javascript
const frozen = Object.freeze({ x: 1 });
frozen.x = 2; // Fails silently or throws error in strict mode

const sealed = Object.seal({ y: 1 });
sealed.y = 2; // Allowed!
// delete sealed.y; // Forbidden
```

- **Real-World Analogy:** `Object.freeze()` is like encasing an object inside a solid block of ice; you cannot change anything inside. `Object.seal()` is like putting a glass display box over an item with pre-installed dials; you can't add or remove pieces from the case, but you can turn the existing dials to change their values.

### 38. What is the purpose of `Object.preventExtensions()`?

- **Definition:** `Object.preventExtensions()` prevents new properties from ever being appended to an object. However, unlike sealing or freezing, existing properties _can_ be modified and deleted freely.
- **Code Example:**

```javascript
const item = { name: "Book" };
Object.preventExtensions(item);
// item.price = 10; // Fails silently or errors out
delete item.name; // Works perfectly!
```

- **Real-World Analogy:** It is like closing the passenger doors of a train car. No new passengers are allowed onto the train, but the existing passengers inside can move around or exit the train freely at the next stop.

### 39. How can you reliably determine if a JavaScript object is completely empty?

- **Definition:** An object is empty if it has no direct properties or Symbol properties. You can check this by passing the object to `Object.keys()`, `Object.getOwnPropertyNames()`, and `Object.getOwnPropertySymbols()`, and ensuring their lengths are all 0.
- **Code Example:**

```javascript
function isEmpty(obj) {
  return Object.keys(obj).length === 0 && obj.constructor === Object;
}
console.log(isEmpty({})); // true
console.log(isEmpty({ a: 1 })); // false
```

- **Real-World Analogy:** It is like walking up to a rental locker and opening the door wide to visually verify that there are no physical items on the shelves or dynamic keycards left inside.

### 40. What are accessor properties (Getters and Setters) in objects?

- **Definition:** Accessor properties are specialized object methods that mimic standard object data properties. They use the `get` and `set` keywords to intercept code attempts to read or write to those properties.
- **Code Example:**

```javascript
const account = {
  _bal: 100,
  get balance() {
    return `$${this._bal}`;
  },
  set balance(val) {
    if (val >= 0) this._bal = val;
  },
};
account.balance = 200; // invokes set
console.log(account.balance); // invokes get -> "$200"
```

- **Real-World Analogy:** A getter/setter is like a security guard standing in front of a warehouse vault door. Instead of letting anyone grab or toss items inside, you tell the guard what you want, and they validate your request before handling the items for you.

### 41. What is the difference between the `for...in` and `for...of` loops?

- **Definition:** `for...in` iterates over all enumerable **string keys/properties** of an object (including inherited properties on the prototype chain). `for...of` iterates over the **values** of an iterable collection (such as Arrays, Strings, Maps, or Sets).
- **Code Example:**

```javascript
const list = ["a", "b"];

for (let key in list) console.log(key); // "0", "1" (indexes/keys)
for (let val of list) console.log(val); // "a", "b" (values)
```

- **Real-World Analogy:** Imagine reading a textbook. `for...in` loops through the index page numbers and chapter listings at the back of the book. `for...of` loops through the actual text story content written on the physical pages.

### 42. Explain the purpose of the following Array prototype methods: `map()`, `filter()`, and `reduce()`.

- **Definition:**
  - `map()`: Transforms an array by running a callback function on each element and returns a new array of the exact same length.
  - `filter()`: Evaluates each element against a boolean condition and returns a new array containing only the elements that match.
  - `reduce()`: Iterates through an array to accumulate its elements into a single final value (such as a number, string, object, or array).
- **Code Example:**

```javascript
const nums = [1, 2, 3, 4];
const doubled = nums.map((x) => x * 2); // [2, 4, 6, 8]
const evens = nums.filter((x) => x % 2 === 0); // [2, 4]
const sum = nums.reduce((acc, c) => acc + c, 0); // 10
```

- **Real-World Analogy:** Imagine processing apples. `map()` is peeling every apple individually. `filter()` is discarding the rotten apples. `reduce()` is tossing all the remaining apples into a blender to squeeze them into a single cup of apple juice.

### 43. What is the difference between `Array.prototype.forEach()` and `Array.prototype.map()`?

- **Definition:** `forEach()` executes a callback function on each element of an array for its side effects (like saving to a database or updating the UI) and returns `undefined`. `map()` allocates memory to construct and return a brand-new array containing the transformed results without modifying the original array.
- **Code Example:**

```javascript
const items = [1, 2];
const resForEach = items.forEach((x) => {
  /* side effects here */
}); // undefined
const resMap = items.map((x) => x * 10); // [10, 20]
```

- **Real-World Analogy:** `forEach()` is like a mail carrier visiting every house on a street to drop off individual flyers; nothing changes about the street layout itself. `map()` is like a construction crew looking at every house on the street and building an entirely new replica neighborhood on the next block where every house has an added solar panel.

### 44. How do the `slice()` and `splice()` array methods differ in functionality?

- **Definition:** `slice()` returns a shallow copy of a portion of an array based on start/end indexes and does _not_ modify the original array. `splice()` directly mutates the original array by removing, replacing, or adding elements at a specified index position.
- **Code Example:**

```javascript
let arr = ["a", "b", "c", "d"];

let sliced = arr.slice(1, 3);
console.log(arr); // ["a", "b", "c", "d"] (unchanged)

let spliced = arr.splice(1, 2);
console.log(arr); // ["a", "d"] (mutated!)
```

- **Real-World Analogy:** `slice()` is taking a digital photograph of a section of a cake; your cake stays perfectly intact on the kitchen counter. `splice()` is taking a physical knife, cutting out a large slice of the cake, and eating it; the original cake is now physically missing that chunk.

### 45. What do the `some()` and `every()` array methods check for?

- **Definition:** `some()` returns `true` if at least one element in the array passes the callback function's condition. `every()` returns `true` only if absolutely all elements in the array pass the condition. Both methods stop iterating early as soon as the final outcome is certain (short-circuiting).
- **Code Example:**

```javascript
const ages = [12, 15, 21, 14];
console.log(ages.some((age) => age >= 18)); // true  (one adult)
console.log(ages.every((age) => age >= 18)); // false (not all are adults)
```

- **Real-World Analogy:** `some()` is checking if anyone in a tour group brought an umbrella; if the first person has one, you stop checking. `every()` is a theme park ride operator checking if every single passenger has locked their safety harness; if even one harness is open, the ride cannot start.

### 46. How do you find the index of an element in an array using modern array methods?

- **Definition:** For primitive values, you can use `indexOf()`. For complex reference types (like objects) that require evaluating a condition, you can use `findIndex()`.
- **Code Example:**

```javascript
const fruits = ["apple", "banana"];
console.log(fruits.indexOf("banana")); // 1

const users = [{ id: 1 }, { id: 2 }];
console.log(users.findIndex((u) => u.id === 2)); // 1
```

- **Real-World Analogy:** `indexOf()` is looking at a line of people and asking: "What position is John standing in?". `findIndex()` is walking down that same line asking: "What position is the first person standing in who is wearing a red hat?"

### 47. How do you flatten a multi-dimensional array in JavaScript without writing a manual loop?

- **Definition:** You can use the `Array.prototype.flat()` method. It accepts an optional depth number argument specifying how many levels of nesting to flatten (default is `1`). You can pass `Infinity` to completely flatten arrays of any nesting depth.
- **Code Example:**

```javascript
const deepArr = [1, [2, [3, 4]]];
console.log(deepArr.flat(1)); // [1, 2, [3, 4]]
console.log(deepArr.flat(Infinity)); // [1, 2, 3, 4]
```

- **Real-World Analogy:** It is like flattening a stack of folded cardboard boxes. Flattening by depth 1 unzips the main shipping boxes. Flattening by `Infinity` steps on every single sub-box until everything lies completely flat on the floor together.

### 48. What are the `Map` and `Set` objects introduced in ES6, and how do they differ from standard objects and arrays?

- **Definition:** `Map` is a collection of keyed data pairs where keys can be _any_ data type (including objects or functions), and keys retain their insertion order. `Set` is a collection of completely unique values, meaning duplicates are automatically discarded.
- **Code Example:**

```javascript
// Map
const myMap = new Map();
myMap.set({ id: 1 }, "User Object Key!");

// Set
const mySet = new Set([1, 1, 2, 3]);
console.log([...mySet]); // [1, 2, 3] (duplicates removed)
```

- **Real-World Analogy:** A standard object restricts keys to strings or symbols. A `Map` is a high-end filing cabinet where you can use anything—even a physical tool or an asset object—as the security key tag to open a locker. A `Set` is a guest list for an exclusive club that automatically blocks anyone whose name is already checked in on the sheet.

### 49. What is a `WeakMap` and how does it differ from a regular `Map`?

- **Definition:** In a `WeakMap`, keys _must_ be objects, and those object keys are held weakly. If an object key has no other active references left in the application, the garbage collector can reclaim it and remove the key-value pair from the `WeakMap` automatically. `WeakMap` keys are not enumerable (cannot be looped over).
- **Code Example:**

```javascript
let user = { name: "Bob" };
const wMap = new WeakMap();
wMap.set(user, "metadata");

user = null; // The object is now eligible for garbage collection!
```

- **Real-World Analogy:** A standard `Map` is like a library book catalog that keeps tracking a book forever until you manually delete its entry card. A `WeakMap` is like sticking a post-it note onto a temporary rented moving box. If the owner throws that box into a trash compactor (`null`), your post-it note vanishes into the garbage along with it.

### 50. What is a `WeakSet` and when would you use it?

- **Definition:** A `WeakSet` is a collection of unique objects held weakly. Just like `WeakMap`, objects inside a `WeakSet` can be garbage collected if no other references point to them. They are primarily used to tag objects or track metadata state without creating memory leaks.
- **Code Example:**

```javascript
const activeConnections = new WeakSet();
let domesticSocket = { port: 8080 };

activeConnections.add(domesticSocket);
console.log(activeConnections.has(domesticSocket)); // true
```

- **Real-World Analogy:** It is like handing out paper entry stamps at a convention floor. The stamp lets you check if an item belongs to the event (`has()`), but if a guest throws away their stamped cup or gear, the system stops tracking it entirely.

---

## Object-Oriented Programming & Prototypes (51-63)

### 51. Explain the execution context of the `this` keyword in different environments (Global, Method, Function, Strict mode).

- **Definition:** The value of `this` is determined by _how_ a function is invoked:
  - Global Context: Refers to the global object (`window` in browsers).
  - Object Method: Refers to the object owning the called method.
  - Regular Function: Refers to the global object, but evaluates to `undefined` in Strict Mode.
  - Arrow Function: Inherits `this` lexically from its surrounding outer block parent scope.
- **Code Example:**

```javascript
"use strict";
console.log(this); // window (in global browser context)

const obj = {
  name: "Dev",
  print() {
    console.log(this.name);
  }, // 'this' is obj
};
obj.print();

function regular() {
  console.log(this);
}
regular(); // undefined (due to strict mode)
```

- **Real-World Analogy:** `this` is an index pronoun word like "Me". If a speaker stands alone on an empty public square, "Me" means that speaker (Global). If a team member speaks inside a private corporate board meeting room, "Me" means that specific corporate body. If you scream "Me" inside a strict clean laboratory room without context, nobody responds (`undefined`).

### 52. What is the purpose of the `call()`, `apply()`, and `bind()` methods? How do they differ?

- **Definition:** All three methods change the execution context of the `this` keyword for a function:
  - `call()`: Invokes the function immediately, accepting arguments separated by commas.
  - `apply()`: Invokes the function immediately, accepting arguments inside a single combined array.
  - `bind()`: Returns a brand-new function with `this` permanently bound, allowing it to be executed later.
- **Code Example:**

```javascript
const user = { name: "Alice" };
function greet(city, country) {
  console.log(`${this.name} from ${city}, ${country}`);
}

greet.call(user, "Paris", "FR"); // Comma separated arguments
greet.apply(user, ["Paris", "FR"]); // Array argument
const bound = greet.bind(user, "Paris", "FR");
bound(); // Executes later
```

- **Real-World Analogy:** Imagine an actor delivering a speech. `call()` is handing the actor a costume and a list of lines separated by commas, telling them to go on stage right now. `apply()` is handing them all those same items packed neatly inside a single luggage suitcase. `bind()` is pre-recording the actor's performance with that costume so you can play the video tape whenever you want in the future.

### 53. What is Prototypal Inheritance?

- **Definition:** Prototypal inheritance is a built-in feature where JavaScript objects inherit properties and methods directly from other objects via an internal link called a prototype.
- **Code Example:**

```javascript
const animal = { eats: true };
const rabbit = Object.create(animal); // rabbit inherits from animal
console.log(rabbit.eats); // true
```

- **Real-World Analogy:** It is like inheriting an old family recipe book. If you don't personally know how to make a dish, you don't give up; you look up the instructions in the inherited family recipe book passed down by your parents.

### 54. What is the Prototype Chain, and how does JavaScript look up properties on an object?

- **Definition:** The prototype chain is a linked series of object references. When you look up a property on an object, JavaScript first looks at the object's direct properties. If it can't find it there, it travels up the chain via the internal `[[Prototype]]` link, searching parent prototypes until it finds the property or reaches `null`.
- **Code Example:**

```javascript
const grandParent = { hair: "curly" };
const parent = Object.create(grandParent);
const child = Object.create(parent);
console.log(child.hair); // "curly" (traverses up child -> parent -> grandParent)
```

- **Real-World Analogy:** It is like trying to borrow a tool. You first look inside your own garage box. If it's not there, you walk over to ask your parent. If they don't have it either, they call your grandparent to see if it's in their workshop.

### 55. What is the difference between `__proto__` and `prototype`?

- **Definition:** `__proto__` is an accessor property exposed on every object instance that points to that specific object's actual prototype link. `prototype` is a property found exclusively on constructor functions (and classes) that defines the blueprint prototype link that will be assigned to all new instances created using the `new` keyword.
- **Code Example:**

```javascript
function Person() {}
const alice = new Person();

console.log(alice.__proto__ === Person.prototype); // true
```

- **Real-World Analogy:** `Person.prototype` is the master blueprint design kept safe at a manufacturing factory floor. `alice.__proto__` is the tracking label stuck onto the physical toy product in your hand, pointing back to the factory blueprint it was made from.

### 56. What is the purpose of `Object.create()`?

- **Definition:** `Object.create()` constructs a brand-new object and sets its internal `[[Prototype]]` link directly to the object passed in as the first argument.
- **Code Example:**

```javascript
const proto = {
  greet() {
    return "Hi";
  },
};
const obj = Object.create(proto);
console.log(obj.greet()); // "Hi"
```

- **Real-World Analogy:** It is like using a 3D scanner to scan an item and using it as the foundational mold pattern for creating a new product.

### 57. How do you check if an object is an instance of a specific class or constructor function?

- **Definition:** You can use the `instanceof` operator. It checks if the `prototype` property of a constructor or class exists anywhere along the targeted object’s prototype chain.
- **Code Example:**

```javascript
class Car {}
const myCar = new Car();
console.log(myCar instanceof Car); // true
console.log(myCar instanceof Object); // true
```

- **Real-World Analogy:** It is like checking a dog's pedigree certification papers to see if its lineage traces back to a specific ancestral breed registry line.

### 58. How do JavaScript Classes (introduced in ES6) work under the hood?

- **Definition:** JavaScript classes are primarily "syntactic sugar" over the existing prototypal inheritance system. Under the hood, a class declaration compiles down into standard prototype objects and constructor functions.
- **Code Example:**

```javascript
class User {
  constructor(name) {
    this.name = name;
  }
  sayHi() {
    return this.name;
  }
}
// Compiles down to a traditional constructor function and:
// User.prototype.sayHi = function() { return this.name; };
```

- **Real-World Analogy:** It is like modern automatic transmission in a car. The dashboard controls look completely new, clean, and futuristic, but underneath the metal hood, the car is still running on traditional mechanical combustion pistons and gears.

### 59. What is the purpose of the `super` keyword in class inheritance?

- **Definition:** The `super` keyword is used to call functions or constructors on an object's parent class. In a derived child class constructor, you must call `super()` before accessing the `this` keyword.
- **Code Example:**

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }
}
class Dog extends Animal {
  constructor(name, breed) {
    super(name); // Invokes the parent constructor
    this.breed = breed;
  }
}
```

- **Real-World Analogy:** It is like a franchise business store opening a new branch. Before the local manager can buy custom furniture (`this`), they must first call corporate headquarters (`super()`) to lay down the foundational structural framework of the business brand.

### 60. What are Static Methods and Properties in JavaScript classes?

- **Definition:** Static methods and properties are called directly on the class itself, rather than on instances of the class. They are defined using the `static` keyword and are often used for utility or factory functions.
- **Code Example:**

```javascript
class MathUtil {
  static pi = 3.14159;
  static triple(x) {
    return x * 3;
  }
}
console.log(MathUtil.pi); // 3.14159
console.log(MathUtil.triple(3)); // 9
// const instance = new MathUtil(); instance.triple(3); // TypeError
```

- **Real-World Analogy:** Imagine a blueprint for an airplane. A static property is a global specification note written in the top margin of the blueprint blueprint itself (like "Designed in 2026"). It belongs to the blueprint document, not to the individual physical airplanes built and flying in the sky.

### 61. What are Private Class Fields (e.g., `#property`) and how do they enforce encapsulation?

- **Definition:** Private class fields are declared with a hash `#` prefix. They are completely inaccessible outside the class body, enforcing encapsulation at the language level rather than by convention.
- **Code Example:**

```javascript
class BankVault {
  #secretCode = "12345";
  checkCode(code) {
    return this.#secretCode === code;
  }
}
const vault = new BankVault();
// console.log(vault.#secretCode); // SyntaxError: Private field
```

- **Real-World Analogy:** It is like a bank vault with a hidden internal mechanism. Customers can only interact with it through the front keypad window (`checkCode`); they cannot reach through the steel wall to touch or modify the internal locking mechanism directly.

### 62. Can JavaScript achieve multiple inheritance? If not, what are Mixins and how do they work around this?

- **Definition:** JavaScript does not support multiple inheritance; an object can have only one prototype link. Mixins work around this limitation by copying properties and methods from multiple source objects into a target class prototype, combining functionalities.
- **Code Example:**

```javascript
const canFly = {
  fly() {
    console.log("Flying!");
  },
};
const canSwim = {
  swim() {
    console.log("Swimming!");
  },
};

class Superhero {}
Object.assign(Superhero.prototype, canFly, canSwim); // Mixin pattern

const hero = new Superhero();
hero.fly(); // "Flying!"
hero.swim(); // "Swimming!"
```

- **Real-World Analogy:** You can only have one legal biological birth parent listed on an official document (single prototype inheritance link). However, a Mixin is like taking guitar lessons from one teacher and karate classes from another, adding individual skill sets to your personal repertoire.

### 63. Explain the difference between composition and classical inheritance.

- **Definition:** Classical inheritance design models what objects **are** using deep, rigid class hierarchies (`class Dog extends Animal`). Composition models what objects **do** by combining small, independent, reusable behaviors together into a flexible whole.
- **Code Example:**

```javascript
// Composition Pattern
const speaker = (state) => ({ speak: () => console.log(state.name) });
const driver = (state) => ({ drive: () => console.log("Driving") });

const createRobotDriver = (name) => {
  let state = { name };
  return Object.assign({}, speaker(state), driver(state));
};
```

- **Real-World Analogy:** Classical inheritance is like a rigid military chain of command where every rank is strictly derived from the rank above it. Composition is like a Swiss Army knife: instead of inheriting from a "Master Blade Class", you build a tool by clipping together an independent knife blade, a corkscrew tool, and a small pair of scissors.

---

## Asynchronous JavaScript (64-75)

### 64. What is the Event Loop? Explain its components (Call Stack, Web APIs, Task Queue).

- **Definition:** The Event Loop is the mechanism that allows JavaScript to perform non-blocking I/O operations despite being single-threaded.
  - **Call Stack:** Tracks the line of code currently executing.
  - **Web APIs:** Browser threads that handle asynchronous tasks like timers or network requests.
  - **Task Queue (Callback Queue):** Holds callbacks from completed async tasks, waiting to be pushed onto the Call Stack once it is completely empty.
- **Code Example:**

```javascript
console.log("Start");
setTimeout(() => console.log("Timeout"), 0);
console.log("End");
// Output Order: "Start" -> "End" -> "Timeout"
```

- **Real-World Analogy:** Imagine a busy restaurant kitchen. The head chef (Call Stack) can only cook one dish at a time. When a customer orders a slow-baked pie, the chef hands it off to an automated oven timer (Web APIs) and continues cooking other dishes. When the timer dings, the pie sits on the pickup counter (Task Queue) until the chef finishes their current dish and clears space on the workstation counter to wrap it up.

### 65. What is the difference between Synchronous and Asynchronous code execution?

- **Definition:** Synchronous code runs line by line in sequence; each line must finish executing before the next line can start, blocking further execution. Asynchronous code schedules a task to run in the background, allowing subsequent lines of code to run immediately without waiting for the task to finish.
- **Code Example:**

```javascript
// Synchronous blocking
const data = fetchSync("api/url"); // blocks everything until downloaded
console.log("Done");

// Asynchronous non-blocking
fetch("api/url").then(() => console.log("Fetched"));
console.log("Done First"); // runs immediately
```

- **Real-World Analogy:** Synchronous is standing in a long line at a coffee shop waiting for the barista to make the drink for the person ahead of you before you can even order. Asynchronous is ordering online, sitting down at a table to read a book, and picking up your drink when your name is called.

### 66. What is "Callback Hell" (Pyramid of Doom), and what are the modern ways to mitigate it?

- **Definition:** Callback Hell refers to heavily nested, unreadable code caused by chaining multiple asynchronous callback functions inside one another. It can be mitigated by splitting code into named modular functions, using Promises, or writing clean `async/await` syntax.
- **Code Example:**

```javascript
// Callback Hell
getData(function (a) {
  getMoreData(a, function (b) {
    getEvenMoreData(b, function (c) {
      console.log(c);
    });
  });
});

// Mitigated with Async/Await
const c = await getEvenMoreData(await getMoreData(await getData()));
```

- **Real-World Analogy:** Callback hell is like a bureaucratic permit process: you must open a box to find a key, to unlock a filing cabinet, to get a folder, to read a paper that tells you where the next office is located, resulting in a confusing, nested mess.

### 67. What is a Promise? What are its three mutually exclusive states?

- **Definition:** A Promise is a proxy object representing the eventual completion or failure of an asynchronous operation. Its three states are:
  - `pending`: Initial operational state, neither fulfilled nor rejected.
  - `fulfilled`: The asynchronous operation completed successfully.
  - `rejected`: The asynchronous operation failed with an error.
- **Code Example:**

```javascript
const myPromise = new Promise((resolve, reject) => {
  let success = true;
  if (success) resolve("Success!");
  else reject("Error!");
});
```

- **Real-World Analogy:** It is like ordering an item that is out of stock. The store hands you a physical receipt pager ticket (`pending`). If the item arrives from the warehouse, the pager flashes green (`fulfilled`). If the delivery truck breaks down, the pager flashes red to signal a cancellation (`rejected`).

### 68. Explain Promise chaining. How do you pass data from one `.then()` to the next?

- **Definition:** Promise chaining is a pattern where multiple asynchronous operations are run in sequence. Each `.then()` block returns a brand-new Promise instance, and any value returned from its callback function is automatically passed as the resolved data input to the next `.then()` block down the chain.
- **Code Example:**

```javascript
fetchUser(1)
  .then((user) => user.id)
  .then((userId) => fetchUserOrders(userId)) // returns a new promise
  .then((orders) => console.log(orders))
  .catch((err) => console.error(err));
```

- **Real-World Analogy:** It is an Olympic relay race. The first runner completes a lap and passes a physical baton to the second runner. The second runner takes that baton, runs their lap, and passes it along to the next runner in line.

### 69. What is the difference between `Promise.all()`, `Promise.allSettled()`, `Promise.race()`, and `Promise.any()`?

- **Definition:**
  - `Promise.all()`: Fulfills only if **all** inputs fulfill; rejects immediately if **any** single input rejects.
  - `Promise.allSettled()`: Waits for **all** inputs to finish (either fulfill or reject) and returns an array of records describing the outcome of each.
  - `Promise.race()`: Settles as soon as the **first** promise in the input array either fulfills or rejects.
  - `Promise.any()`: Fulfills as soon as the **first** promise fulfills; rejects only if **all** promises reject.
- **Code Example:**

```javascript
const p1 = Promise.resolve("A");
const p2 = Promise.reject("Error");

// Promise.all([p1, p2]).catch(err => console.log("Fails fast"));
// Promise.allSettled([p1, p2]).then(res => console.log("Waits for both"));
```

- **Real-World Analogy:**
  - `all()` is a team mountain climb: everyone must reach the peak together, and if one climber gets hurt, the entire expedition is canceled.
  - `race()` is a sprint race: you only care about who crosses the finish line first, whether they win or trip and fall.

### 70. What is `async/await`, and how does it simplify working with promises?

- **Definition:** `async/await` is a syntactic feature built on top of Promises. The `async` keyword designates a function to automatically wrap its return value in a Promise, and the `await` keyword pauses execution until a promise settles, allowing asynchronous code to be read and structured like synchronous code.
- **Code Example:**

```javascript
async function getDashboardData() {
  try {
    const user = await fetch("/user");
    const data = await user.json();
    return data;
  } catch (err) {
    console.error(err);
  }
}
```

- **Real-World Analogy:** Instead of reading a Choose Your Own Adventure book where you are constantly flipped to page 42 or page 89 based on choices, it is like reading a standard, linear novel where you can read page by page smoothly from top to bottom.

### 71. How do you handle errors properly when using `async/await` syntax?

- **Definition:** Errors in `async/await` functions are handled using standard `try...catch` blocks wrapped around the expressions that await promises, catching both synchronous and asynchronous errors in one place.
- **Code Example:**

```javascript
async function safetyWrapper() {
  try {
    const res = await fetch(
      "[https://invalid-endpoint-url.com](https://invalid-endpoint-url.com)",
    );
    const data = await res.json();
  } catch (error) {
    console.error("Caught error gracefully:", error.message);
  }
}
```

- **Real-World Analogy:** It is like driving a car equipped with an automated emergency airbag system. You drive normally inside the safety zone, but if a crash happens, the system triggers the defensive wrap to contain the impact.

### 72. What is the difference between Microtasks and Macrotasks (Tasks) in the event loop?

- **Definition:** Microtasks have a higher priority than Macrotasks. The event loop checks and empties the entire Microtask Queue completely after every execution step, before moving on to execute the next single Macrotask from the Macrotask Queue.
  - **Microtasks:** `Promise.then` callbacks, `MutationObserver`, `queueMicrotask`.
  - **Macrotasks:** `setTimeout`, `setInterval`, `setImmediate`, UI rendering events.
- **Code Example:**

```javascript
setTimeout(() => console.log("Macro"), 0);
Promise.resolve().then(() => console.log("Micro"));
// Output Order: "Micro" executes before "Macro"
```

- **Real-World Analogy:** Imagine an airport gate. Macrotasks are standard passengers lining up to board the airplane one by one. Microtasks are first-class passengers who arrive late; the gate agent will halt the economy line completely and clear out all first-class passengers before letting the next economy passenger board.

### 73. How does the browser Fetch API handle network errors compared to HTTP error statuses (like 404 or 500)?

- **Definition:** The Fetch API promise will reject _only_ if a true network failure occurs (such as a total connection loss, a broken DNS lookup, or a CORS error). It does _not_ reject on standard HTTP error statuses like 404 or 500; instead, it resolves successfully, setting the `response.ok` property to `false`.
- **Code Example:**

```javascript
fetch("/missing-page")
  .then((res) => {
    if (!res.ok) console.log("HTTP Error like 404 seen, but Promise resolved!");
  })
  .catch((err) => console.log("Only runs on hardware/network failure"));
```

- **Real-World Analogy:** It is like hiring a courier service to deliver a package to a business office. If the courier drives to the building but finds a sign saying "Office permanently closed" (404), they successfully complete their job by returning to tell you the news. They only fail their delivery run if their delivery truck breaks down or sinks into a sinkhole along the route.

### 74. What are Generator Functions (`function*`), and how does the `yield` keyword operate?

- **Definition:** A generator function can pause its execution and resume it later, rather than running until it hits a return statement. It is declared using the `function*` syntax and uses the `yield` keyword to pause execution and return a value.
- **Code Example:**

```javascript
function* counterGen() {
  yield 1;
  yield 2;
  return 3;
}
const gen = counterGen();
console.log(gen.next()); // { value: 1, done: false }
console.log(gen.next()); // { value: 2, done: false }
```

- **Real-World Analogy:** A generator function is like a board game card deck. Instead of dealing out all 100 game cards face up onto the table at once, you call `next()` to draw a single card, pausing the state of the deck until you are ready to draw the next card.

### 75. What is an Async Generator, and how do you loop over it using `for await...of`?

- **Definition:** An Async Generator combines generator functions with asynchronous promises. The `yield` keyword pauses execution to wait for an asynchronous task to resolve before returning its value. You can iterate over these generators using the `for await...of` loop syntax.
- **Code Example:**

```javascript
async function* streamData() {
  yield fetch("/chunk1").then((r) => r.json());
  yield fetch("/chunk2").then((r) => r.json());
}
async function run() {
  for await (let chunk of streamData()) {
    console.log(chunk);
  }
}
```

- **Real-World Analogy:** It is like streaming a movie online. The media player doesn't wait for the entire 2-hour movie file to download completely before starting; it fetches and plays individual video data chunks as they arrive over the network.

---

## DOM & Browser Web APIs (76-85)

### 76. What is the Document Object Model (DOM)?

- **Definition:** The DOM is a programming interface for web documents. It represents the structural layout of an HTML page as a node tree graph, allowing scripting languages like JavaScript to dynamically read, modify, or delete elements and styles.
- **Code Example:**

```javascript
const header = document.createElement("h1");
header.innerText = "Hello World";
document.body.appendChild(header);
```

- **Real-World Analogy:** The raw HTML code is a flat text blueprint for a house. The DOM is the actual physical house built from that blueprint. JavaScript acts like an interior decorator who can move furniture, repaint walls, or knock down partitions inside the house.

### 77. What is the difference between `window` and `document` objects?

- **Definition:** The `window` object represents the browser window environment hosting the webpage; it serves as the global execution context root for client-side JavaScript. The `document` object is a property nested inside the `window` object that represents the actual HTML page loaded within that window tab frame.
- **Code Example:**

```javascript
console.log(window.innerHeight); // reads hardware window browser frame sizes
console.log(window.document.title); // reads the internal loaded HTML tab name
```

- **Real-World Analogy:** `window` is the physical television set enclosure unit itself. `document` is the specific movie or channel program actively playing on the screen surface at this moment.

### 78. What is Event Propagation? Explain Event Bubbling and Event Capturing.

- **Definition:** Event propagation is the lifecycle phases an event goes through when triggered on a DOM node.
  1.  **Capturing Phase:** The event travels down from the top root document node to the target element.
  2.  **Target Phase:** The event triggers directly on the targeted element.
  3.  **Bubbling Phase:** The event travels back up from the target element to the top root document node (this is the default behavior for most DOM events).
- **Code Example:**

```javascript
// Bubbling setup (default)
elem.addEventListener("click", () => {}, false);

// Capturing setup (third argument set to true)
elem.addEventListener("click", () => {}, true);
```

- **Real-World Analogy:** Imagine dropping a stone into a bucket of water containing nested cups. Event capturing is the stone sinking down through the water layers to hit the target cup at the bottom. Event bubbling is the resulting air bubbles rising from that bottom cup back up to the surface.

### 79. What is Event Delegation, and why is it highly beneficial for application performance?

- **Definition:** Event delegation is a technique where you attach a single event listener to a common parent element to manage events for all of its existing or future child elements. It leverages event bubbling to inspect `event.target` and handle events efficiently without attaching individual listeners to every single child node.
- **Code Example:**

```javascript
const list = document.getElementById("myList");
list.addEventListener("click", (event) => {
  if (event.target.tagName === "LI") {
    console.log("Clicked list text:", event.target.innerText);
  }
});
```

- **Real-World Analogy:** Instead of hiring 100 individual security guards to stand watch over 100 separate apartment doors in a building complex, you hire one security guard to sit at the main building entrance lobby desk to check everyone walking inside.

### 80. What is the difference between `event.preventDefault()` and `event.stopPropagation()`?

- **Definition:** `event.preventDefault()` stops the browser's default behavior for an event (such as preventing a form from submitting or a link from navigating). `event.stopPropagation()` stops the event from traveling further up or down the DOM tree, halting event bubbling or capturing.
- **Code Example:**

```javascript
// Stops link from changing URL page route
link.addEventListener("click", (e) => e.preventDefault());

// Stops parent wrapper from triggering its own click handlers
button.addEventListener("click", (e) => e.stopPropagation());
```

- **Real-World Analogy:** `event.preventDefault()` is like telling a customer "No, you cannot buy that item" when they try to check out, stopping the default transaction. `event.stopPropagation()` is like telling a customer "Do not tell anyone else what happened here," preventing the news from spreading to anyone else in the building.

### 81. How can you find out if `event.preventDefault()` was called on an element?

- **Definition:** You can check the value of the boolean property `event.defaultPrevented` on the event object inside any event handler function wrapper.
- **Code Example:**

```javascript
form.addEventListener("submit", (e) => {
  e.preventDefault();
  console.log(e.defaultPrevented); // true
});
```

- **Real-World Analogy:** It is like checking a package delivery manifest to see if a customer has already stamped an official "Cancellation Approved" ink label across the document.

### 82. What is the difference between the `DOMContentLoaded` event and the window `load` event?

- **Definition:** `DOMContentLoaded` fires as soon as the HTML document is parsed and the DOM tree is built, without waiting for external assets like images or stylesheets to finish loading. The window `load` event fires later, only after the HTML document _and_ all external assets (like images, scripts, and stylesheets) have loaded completely.
- **Code Example:**

```javascript
document.addEventListener("DOMContentLoaded", () => console.log("DOM built!"));
window.addEventListener("load", () => console.log("Everything loaded!"));
```

- **Real-World Analogy:** `DOMContentLoaded` is like finishing the framing and structural walls of a new house; you can walk inside and look around. The window `load` event is like waiting for the paint to dry, the furniture to arrive, and the appliances to be plugged in before officially moving in.

### 83. Compare `localStorage`, `sessionStorage`, and `Cookies` in terms of capacity, lifecycle, and security.

- **Definition:**
  - `localStorage`: Stores around 5-10MB of data per origin; persistent until explicitly cleared via code or by deleting browser cache.
  - `sessionStorage`: Stores around 5MB of data; cleared automatically as soon as the specific browser tab is closed.
  - `Cookies`: Store a maximum of 4KB of data; sent along with every HTTP network request, and accept an explicit expiration date.
- **Comparison Table:**
  | Feature | LocalStorage | SessionStorage | Cookies |
  | :--- | :--- | :--- | :--- |
  | **Capacity** | 5-10 MB | 5 MB | 4 KB |
  | **Lifecycle** | Persistent | Tab closing | Custom expiration |
  | **Network** | Client only | Client only | Sent with HTTP requests |
- **Real-World Analogy:** `localStorage` is a heavy storage locker in your garage where you keep long-term tools. `sessionStorage` is a temporary locker at a theme park that empties automatically when you leave for the day. `Cookies` are like a visitor badge pinned to your shirt; it's small, but you show it to the security guard every single time you walk through a door.

### 84. What are Data Attributes (`data-*`) on HTML elements, and how do you access them via JavaScript?

- **Definition:** Data attributes allow you to store custom metadata values directly on HTML elements. In JavaScript, you can access these values via the element's `dataset` property, which converts kebab-case attribute names into camelCase object properties.
- **Code Example:**

```html
<!-- HTML -->
<div id="user" data-user-role="admin"></div>
```

```javascript
// JavaScript
const el = document.getElementById("user");
console.log(el.dataset.userRole); // "admin" (camelCase lookup)
```

- **Real-World Analogy:** It is like writing a hidden tracking code or price note on the bottom of a coffee mug using a permanent marker so you can check its origin details whenever you pick it up.

### 85. Explain the concepts of Debouncing and Throttling. What are their primary use cases?

- **Definition:** Both techniques optimize performance by limiting how often a function executes.
  - **Debouncing:** Delays function execution until a specified amount of time has passed since the last time the event was triggered (e.g., waiting for a user to stop typing in a search box).
  - **Throttling:** Ensures a function executes at most once every specified time interval (e.g., limiting how often a scroll event handler runs).
- **Code Example:**

```javascript
// Debounce Implementation
function debounce(func, delay) {
  let timer;
  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => func.apply(this, args), delay);
  };
}
```

- **Real-World Analogy:** Debouncing is an automatic elevator door waiting for people to stop walking in; it resets its timer every time a new person steps aboard and only closes when the doorway has been clear for 5 seconds. Throttling is a water drip faucet that drops exactly one droplet of water every 2 seconds, no matter how hard you turn or shake the handle.

---

## Modern ES6+ Features & Tooling (86-93)

### 86. What are the key features introduced in the major ECMAScript 2015 (ES6) revision?

- **Definition:** ES6 was a major overhaul of the JavaScript language. Key features include `let` and `const` for block scoping, Arrow Functions, Classes, Template Literals, Destructuring, the Spread/Rest operators, Promises, Native Modules (`import`/`export`), and new collection types like `Map` and `Set`.
- **Code Example:**

```javascript
// Combines Arrow Function, Template Literal, and Const
const printMessage = (msg) => `Log: ${msg}`;
```

- **Real-World Analogy:** It is like upgrading from an old flip phone to a modern smartphone. The foundational purpose remains the same, but you get built-in tools like a camera, apps, and touch controls that make tasks much easier to perform.

### 87. What are `Symbol` data types, and what makes them completely unique?

- **Definition:** A Symbol is a primitive data type that guarantees a completely unique identifier value. Symbols are primarily used as private object property keys to ensure they never collide with other keys, even if they share the same descriptive label string.
- **Code Example:**

```javascript
const sym1 = Symbol("key");
const sym2 = Symbol("key");
console.log(sym1 === sym2); // false (guaranteed unique!)

const obj = { [sym1]: "Hidden value" };
```

- **Real-World Analogy:** It is like generating a DNA finger print record. Even if two people share the exact same first and last name ("key"), their biological DNA fingerprints are unique and cannot be duplicated.

### 88. What is the purpose of the `Proxy` object in JavaScript? Give an example use case.

- **Definition:** A `Proxy` wraps an object to intercept and customize its fundamental behavior operations (such as property lookups, assignments, or function invocations) using handler hooks called "traps".
- **Code Example:**

```javascript
const target = { price: 100 };
const validatorProxy = new Proxy(target, {
  set(obj, prop, value) {
    if (prop === "price" && value < 0) throw new Error("Invalid Price");
    obj[prop] = value;
    return true;
  },
});
// validatorProxy.price = -50; // Throws error error automatically
```

- **Real-World Analogy:** A Proxy is like hiring an accountant to manage your business ledger. Instead of letting people write directly in the ledger book, they must pass numbers to the accountant, who reviews the entries for errors before writing them down.

### 89. What is the `Reflect` API, and how does it complement the `Proxy` object?

- **Definition:** `Reflect` is a built-in object that provides helper methods for interceptable JavaScript operations. Its methods match the handler traps of `Proxy` objects, making it easy to forward operations to the target object within a proxy handler.
- **Code Example:**

```javascript
const target = { name: "John" };
const proxy = new Proxy(target, {
  get(obj, prop, receiver) {
    console.log(`Property ${prop} read event`);
    return Reflect.get(obj, prop, receiver); // Forwards operation perfectly
  },
});
```

- **Real-World Analogy:** If a `Proxy` is like a custom building guard intercepting incoming packages, `Reflect` is the official handbook detailing the standard procedures for forwarding those packages to the correct department inside.

### 90. Explain the differences between CommonJS modules (`require`/`module.exports`) and ES6 Modules (`import`/`export`).

- **Definition:** CommonJS is the traditional module format used by Node.js; it resolves modules synchronously at runtime. ES6 Modules (ESM) are the standard native module system for modern JavaScript; they are static and analyzed at compile time, which enables performance optimizations like tree-shaking.
- **Code Example:**

```javascript
// CommonJS Syntax
const utils = require("./utils");
module.exports = { value: 42 };

// ES6 Modules (ESM) Syntax
import { item } from "./utils.js";
export const value;
```
---

### 91. What is "Tree Shaking" in modern JavaScript bundlers, and how does it optimize file sizes?

#### Definition
**Tree Shaking** is a dead-code elimination technique used during the compilation phase. Modern bundlers (like Webpack, Rollup, or Vite) leverage the static nature of ES6 modules (`import` and `export`) to scan your application's dependency graph. If a function or module is exported but never imported or invoked anywhere else, it is dropped from the final production bundle.

#### Real-World Analogy
Imagine buying a live plant from a garden center. Before bringing it inside, you shake it gently. The dead leaves and brittle twigs fall off, leaving only the healthy, living components. Your plant is now lighter, cleaner, and takes up exactly the right amount of space.

#### Code Example
```javascript
// utilities.js
export function calculateTotal(price, tax) {
    return price + (price * tax);
}

// This function is never imported or used in the app
export function legacyFormatCurrency(amount) {
    return "$" + amount.toFixed(2);
}

// main.js
import { calculateTotal } from './utilities.js';
console.log(calculateTotal(100, 0.08));

// Production Build: 'legacyFormatCurrency' is completely shaken out.
```

### 92. What is the role of a Transpiler like Babel in modern web workflows?
**Definition**

A Transpiler (source-to-source compiler) reads JavaScript code written using modern ECMAScript features (ES6+) and translates it into an older, widely compatible version (like ES5). This allows developers to use cutting-edge syntax without breaking performance or throwing syntax errors in older browsers or environments.

**Real-World Analogy**
Imagine writing a book in modern, evolving slang. If you want older generations or people from different regions to understand it perfectly, you hire a translator to rewrite the book into standard, timeless grammar while keeping the exact same story intact.

```javascript
// Modern Source Code (ES6+)
const user = { name: "Alice" };
const city = user?.address?.city ?? "Unknown";

// Transpiled Output (ES5 equivalent produced by Babel)
var user = { name: "Alice" };
var _user$address;
var city = (_user$address = user === null || user === void 0 ? void 0 : user.address) !== null && _user$address !== void 0 ? _user$address.city : "Unknown";
```

93. What is the difference between feature detection, feature mimicking, and polyfilling?
Definition
Feature Detection: Checking if an API exists in the browser before running code that relies on it.

Polyfilling: Injecting a fallback script that copies a modern, standard native API for older browsers that lack it.

Feature Mimicking (Shim): Creating an external custom wrapper or library to replicate a behavior, though it may not match the standard global syntax.

Real-World Analogy
Feature Detection: Checking your dashboard to see if your car has a built-in GPS before navigating.

Polyfilling: If your car lacks a built-in GPS, you mount an aftermarket dashboard screen that mimics the original manufacturer's console experience exactly.

Feature Mimicking: Holding your smartphone in your lap to navigate—it solves the same problem, but it doesn't integrate natively into the car's dashboard system.

Code Example
```javascript
// 1. Feature Detection
if (typeof Array.prototype.includes === "function") {
    console.log("Browser supports .includes natively!");
}

// 2. Polyfilling (Adding support manually if missing)
if (!Array.prototype.includes) {
    Array.prototype.includes = function(searchElement) {
        return this.indexOf(searchElement) !== -1;
    };
}

// 3. Feature Mimicking (Shim / Custom Utility Function)
function customIncludesShim(array, element) {
    return array.indexOf(element) !== -1;
}
```

94. How does the try...catch...finally block execute, and when does the finally block run?
Definition
The try block wraps code that might cause a runtime exception. If an error is thrown, execution immediately shifts to the catch block. The finally block is guaranteed to run always, completing right after try or catch executes, regardless of whether an error occurred, was caught, or if a return statement was issued.

Real-World Analogy
Think of accessing a secure ATM to withdraw money:

Try: You insert your card and request a withdrawal.

Catch: If your account balance is insufficient, the machine catches the problem and displays an error message.

Finally: No matter whether you successfully got your money or encountered an error, the machine always ejects your card at the very end so you don't leave it behind.

Code Example

```javascript
function openFileStream() {
    try {
        console.log("Opening connection to system file...");
        throw new Error("Disk read permissions denied.");
        return "Success";
    } catch (error) {
        console.error("Error encountered:", error.message);
        return "Failed";
    } finally {
        // Runs even after 'return' statements above
        console.log("Cleanup: Closing file stream to prevent memory leaks.");
    }
}
openFileStream();
```

95. How do you instantiate and throw a custom error using the built-in Error object?
Definition
You can signal exceptional runtime problems by using the throw keyword followed by an instance of the Error object. For structural code patterns, you can create a custom error class by extending the built-in Error prototype and overriding its properties like name.

Real-World Analogy
When checking out at a grocery store, a cash register handles standard barcodes. If an item has a torn barcode that won't scan, the cashier doesn't just stop working; they raise a specific "Damaged Label" alert flag to prompt human intervention.

Code Example

```javascript
// Extending the native Error class
class CustomValidationError extends Error {
    constructor(message) {
        super(message);
        this.name = "CustomValidationError";
    }
}

function registerUser(username) {
    if (username.length < 5) {
        throw new CustomValidationError("Username must be at least 5 characters long.");
    }
    return "User registered successfully!";
}

try {
    registerUser("abc");
} catch (err) {
    console.error(`[${err.name}] -> ${err.message}`);
}
```

96. How does Garbage Collection work in JavaScript? Explain the Mark-and-Sweep algorithm.
Definition
JavaScript utilizes an automatic memory management process called Garbage Collection. The standard engine strategy is the Mark-and-Sweep algorithm. The collector begins at the "roots" (global object, active variables in execution stack) and marks every referenced object as reachable. It then sweeps through memory to deallocate and destroy any objects left unmarked.

Real-World Analogy
Imagine a public park after a concert. The park rangers start at the entrance gates and map out all the officially designated paths and benches. Any items found on those designated paths are kept. Any stray pieces of trash left out on unreferenced, unvisited areas of open grass are swept away into the garbage bins.

Code Example

```javascript
let user = {
    name: "John",
    profile: { age: 30 }
};

// The profile object is reachable from the root variable 'user'
user = null; 

// The entire original object { name: "John", profile: ... } 
// is now disconnected from the root. The Mark-and-Sweep 
// collector will remove it during the next GC cycle.
```

97. What are the most common causes of Memory Leaks in client-side JavaScript applications?
Definition
A memory leak occurs when an application keeps references to objects that are no longer required for active operations. Because they remain tied to a root reference, the Garbage Collector cannot claim them, causing the application's RAM usage to climb continuously.

Real-World Analogy
Imagine subscribing to physical newspapers. If you move out of your house but forget to cancel your subscription, papers will keep stacking up on your porch indefinitely, filling up space until your doorway is completely blocked.

Code Example

```javascript
// Cause 1: Forgotten Interval/Timer
function setupDataPoller() {
    let heavyData = new Array(1000000).fill("data");
    setInterval(() => {
        // References heavyData continuously
        console.log("Polling logic active...");
    }, 1000); 
}

// Cause 2: Detached DOM Elements
let elements = {
    button: document.getElementById("action-btn")
};
document.body.removeChild(document.getElementById("action-btn"));
// The button node is removed from the screen, but it cannot be 
// garbage collected because it is still referenced in the 'elements' object.
```

98. What are Web Workers, and how do they allow you to run CPU-intensive scripts off the main execution thread?
Definition
JavaScript runs on a single main thread, meaning massive calculations can freeze user interfaces. Web Workers let developers spawn background threads that operate isolated from the main thread. They execute code in a separate global context and communicate exclusively via structured message passing (postMessage and onmessage).

Real-World Analogy
Imagine a restaurant kitchen with only one chef. If a complex order requires chopping 50 pounds of onions, the chef stops cooking all other orders, making guests wait. Instead, the chef hires an assistant in a backroom to chop the onions, handing over the chopped onions when completed so the main chef never stops cooking.

Code Example

```javascript
// main.js (Main UI Thread)
const worker = new Worker('heavyTask.js');

worker.postMessage({ number: 40 }); // Send data to worker

worker.onmessage = function(event) {
    console.log("Result received from background worker:", event.data);
};

// heavyTask.js (The Web Worker File)
self.onmessage = function(event) {
    const num = event.data.number;
    // Perform massive CPU intensive calculation (e.g., Fibonacci)
    let result = num * 2; 
    self.postMessage(result); // Pass result back
};
```

99. What is "Strict Mode" ("use strict"), and what are some of the key errors it catches early?
Definition
Strict Mode is a configuration directive introduced in ES5 that enforces strict operational variants of JavaScript parsing. It turns silent mistakes or poor syntax habits into explicit runtime errors. It is enabled by writing "use strict"; at the top of a file or function script block.

Real-World Analogy
Driving an automatic car down an open road lets you make small handling mistakes without stalling out. Turning on "Strict Mode" is like driving a manual sports car with a sensitive clutch—if you use incorrect gear patterns or make minor mistakes, the car immediately stalls to prevent bad driving habits.

Code Example

```javascript
"use strict";

// Error 1: Accidental Global Variables
try {
    secretValue = 42; // Throws ReferenceError because variable isn't declared
} catch (e) { console.error(e.message); }

// Error 2: Eliminates 'this' coercion to global object
function checkContext() {
    console.log(this); // Logs: undefined (instead of the window object)
}
checkContext();
```

100. Name three distinct code optimization strategies to improve the runtime performance of complex JavaScript animations or calculations.
Definition
requestAnimationFrame Integration: Aligns rendering calculations with the monitor’s native display refresh rate (60Hz/144Hz) to avoid layout stutter.

Debouncing / Throttling: Reduces the throughput rate of event callback executions triggered by erratic window activity (scrolling, text inputs).

DOM Virtualization / Fragment Batching: Avoids triggering multiple consecutive layout recalculations (reflows) by batching screen updates offscreen before updating the active DOM.

Real-World Analogy
If you are moving bricks to build a patio in your backyard, running outside to place one single brick at a time is highly inefficient. Instead, you load a wheelbarrow full of bricks offscreen, roll it over to the patio site, and layout the whole structure in one single trip.

Code Example

```javascript
// Optimization Strategy: Batching DOM Operations with DocumentFragments
const listContainer = document.getElementById("item-list");
const fragment = document.createDocumentFragment(); // Virtual offscreen node

for (let i = 0; i < 1000; i++) {
    const li = document.createElement("li");
    li.textContent = `Row Item Number ${i}`;
    fragment.appendChild(li); // Appends to fragment, causing ZERO browser layout reflows
}

// Single layout reflow triggered on the live DOM page layout
listContainer.appendChild(fragment);
```