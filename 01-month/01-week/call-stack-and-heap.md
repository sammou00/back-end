# Call Stack vs Heap (Node.js / JavaScript)

![Image](https://miro.medium.com/1%2A-MMBHKy_ZxCrouecRqvsBg.png)

![Image](https://felixgerschau.com/static/b452488bd7eeac0405c48f164da6280d/5a190/stack-heap-pointers.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2A_x4mkpWcBs72s5BcdJe4Wg.png)

Think of memory as **two very different spaces**, with very different rules.

---

## 1️⃣ Call Stack — _“What is running right now?”_

The **call stack** is:

- Where function calls are tracked
- LIFO (Last In, First Out)
- Very fast
- Very limited in size

### Example 1

```js
function a() {
  b();
}

function b() {
  c();
}

function c() {
  console.log("hello");
}

a();
```

### Stack evolution

```bash
call a()
→ call b()
→ call c()
→ console.log
← return c
← return b
← return a
```

Only **one thing runs at a time**.

---

### What lives on the call stack?

- Function calls
- Local variables (primitives)
- Execution context
- Return addresses

### Stack overflow (classic bug)

```js
function boom() {
  boom();
}
boom();
```

💥 `Maximum call stack size exceeded`

This has **nothing** to do with async or libuv — it’s pure JS.

---

## 2️⃣ Heap — _“Where data lives”_

The **heap** is:

- Large, dynamic memory area
- Stores objects, arrays, functions
- Managed by garbage collection
- Slower than stack

### Example 2

```js
const user = {
  name: "Sam",
  age: 35,
};
```

`user` (the reference) → stack
The object itself → heap

---

### Key rule (very important)

> **Stack holds references, heap holds data**

```js
const a = { x: 1 };
const b = a;

b.x = 99;
console.log(a.x); // 99
```

Both `a` and `b` point to **the same heap object**.

---

## 3️⃣ Stack vs Heap — side-by-side

| Aspect   | Call Stack      | Heap        |
| -------- | --------------- | ----------- |
| Purpose  | Track execution | Store data  |
| Speed    | Very fast       | Slower      |
| Size     | Small           | Large       |
| Lifetime | Function scope  | Until GC    |
| Errors   | Stack overflow  | Memory leak |

---

## 4️⃣ Async confusion (clear this now)

This code:

```js
setTimeout(() => {
  console.log("later");
}, 0);

console.log("now");
```

### What happens?

1. `setTimeout` is called → pushed to stack
2. Timer registered → stack clears
3. `console.log("now")` runs
4. Stack empties
5. Callback is pushed later

👉 **Async does NOT mean parallel execution on the stack**

Only **one stack** exists.

---

## 5️⃣ Memory leaks — heap problem, not stack

This is dangerous in Node servers:

```js
const cache = [];

setInterval(() => {
  cache.push(new Array(1e6).fill("data"));
}, 1000);
```

Stack is fine.
Heap grows forever.
💥 Process crashes.

**Backend devs fear heap leaks more than stack overflows.**

---

## 6️⃣ Garbage Collection (high level)

- JS automatically frees unused heap memory
- Objects are collected when unreachable
- GC pauses can affect performance

Important:

> **GC does NOT run on the call stack**
> It pauses JS execution.

This matters for **latency-sensitive APIs**.

---

## 7️⃣ Node-specific insight (very important)

In Node:

- One call stack per process
- Shared heap
- Blocking the stack blocks **everything**
- Heap leaks kill long-running servers

That’s why:

- CPU-heavy loops are dangerous
- Large objects must be handled carefully
- Streams exist

---

## 8️⃣ Senior mental model (lock this in)

- **Call stack** → _control flow_
- **Heap** → _data lifetime_
- **libuv** → _who waits_
- **Event loop** → _when callbacks run_

If you can mentally place a bug into one of these buckets, you’re thinking like a senior.

---

## 🧪 Tiny exercise (don’t run it)

```js
function outer() {
  const big = new Array(1e6).fill("x");
  return function inner() {
    console.log(big[0]);
  };
}

const fn = outer();
```

Ask yourself:

- Where is `big` stored?
- Why is it **not freed**?
- What concept causes this?

(Answer: closure + heap retention)

---
