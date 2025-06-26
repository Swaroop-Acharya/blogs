# 🧠 JavaScript & Node.js Event Loop Deep Dive

---

## ✅ Level 1: Event Loop Basics (Browser & Node.js)

- JavaScript is **single-threaded**.
- The **Call Stack** runs synchronous code (LIFO).
- The **Web APIs** handle asynchronous tasks like `setTimeout`, `fetch`, etc.
- The **Callback Queue** holds completed async callbacks.
- The **Event Loop**:
  - Watches the call stack.
  - If it's empty, it moves tasks from the **callback queue** to the **call stack**.
- **Microtasks** (`Promise.then`, `queueMicrotask`) always run **before** macrotasks (`setTimeout`, `setInterval`).

### Example Output:
```js
console.log("Start");

setTimeout(() => console.log("Timeout"), 0);
Promise.resolve().then(() => console.log("Promise"));

console.log("End");
```
**Output:**
```
Start
End
Promise
Timeout
```

---

## 🔁 Microtasks vs Macrotasks

| Queue Type    | Examples                             | Priority |
|---------------|--------------------------------------|----------|
| Microtask     | `Promise.then`, `queueMicrotask()`   | Higher   |
| Macrotask     | `setTimeout`, `setInterval`, I/O     | Lower    |

- Microtasks are executed **after the current call stack**, but **before any macrotasks**.

---

## ⚠️ Level 3: Microtask Starvation

### Code:
```js
function repeat() {
  Promise.resolve().then(repeat);
}
repeat();

setTimeout(() => {
  console.log("This will never run");
}, 0);
```

### Why It Fails:
- `repeat()` keeps scheduling itself as a **microtask**.
- **Microtasks never stop** → Event loop **never reaches macrotasks** → `setTimeout` never runs.
- This is called **microtask starvation**.

---

## ⚙️ Level 4: Node.js Event Loop Phases

The Node.js event loop has structured **phases** in each tick:

| Phase               | Description                                                        |
|---------------------|--------------------------------------------------------------------|
| **1. Timers**       | Executes `setTimeout`, `setInterval` callbacks                     |
| **2. I/O callbacks**| Executes system-level I/O callbacks (like `fs.readFile`)           |
| **3. idle/prepare** | Internal use only                                                  |
| **4. Poll**         | Waits for incoming I/O (like file or network)                      |
| **5. Check**        | Executes `setImmediate` callbacks                                  |
| **6. Close Callbacks** | Executes `.on('close')` events (sockets, streams)             |

- **Microtasks (Promises)** run **after each phase**.

---

## 🧪 Node.js Example

```js
const fs = require('fs');

fs.readFile(__filename, () => {
  setTimeout(() => console.log('timeout'), 0);
  setImmediate(() => console.log('immediate'));
});

Promise.resolve().then(() => console.log('promise'));
```

**Output:**
```
promise
immediate
timeout
```

> `promise` → microtask  
> `setImmediate` runs before `setTimeout` (because in I/O phase)  
> `setTimeout` runs in next tick's **Timers** phase

---

## 🔁 Summary Table

| Task                  | Type         | Phase/Queue           |
|-----------------------|--------------|------------------------|
| `setTimeout`          | Macrotask    | Timers Phase           |
| `setImmediate`        | Macrotask    | Check Phase            |
| `Promise.then`        | Microtask    | After every phase      |
| `fs.readFile`         | I/O          | I/O Callback Phase     |
| Event Loop            | Infinite loop| Manages tasks and queues|

---

## 📌 Key Concepts

- The **Call Stack** is LIFO.
- **Microtasks** run before macrotasks.
- **Event loop phases** in Node.js give structure to async handling.
- **Microtask starvation** can freeze the app.
