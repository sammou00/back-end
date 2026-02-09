# 🧱 MONTH 1 — Backend Foundations (Node.js + TypeScript)

**Goal:**
By the end of this month, you _understand what Node is actually doing_, not just how to use it.

---

## 📅 WEEK 1 — Node.js Runtime & Event Loop (Deep)

This week is about **how Node breathes**.

### Topics 1

- Node.js runtime vs browser JS
- Call stack, heap
- Event loop phases (timers, I/O, check, close)
- Microtasks vs macrotasks
- `process.nextTick` vs `Promise`
- Blocking vs non-blocking code

### Practice (non-negotiable) 1

- Write code that **logs execution order**
- Break the event loop _on purpose_
- Compare sync vs async CPU tasks

### Output 1

- A **markdown doc** explaining the event loop _in your own words_
- Small scripts demonstrating each phase

🧠 **Senior signal**: You can predict execution order _before_ running code.

---

## 📅 WEEK 2 — Async Patterns, Streams & Backpressure

Now we deal with **data flow**, not just callbacks.

### Topics 2

- Streams (readable, writable, transform)
- Pipe vs manual flow
- Backpressure (very important)
- AbortController & cancellation
- Memory impact of streams vs buffers

### Practice 2

- Stream a large file (simulate big data)
- Build a transform stream
- Intentionally cause memory pressure, then fix it

### Output 2

- CLI script that processes large files **without blowing memory**

🧠 **Senior signal**: You know _why_ streams exist, not just how to use them.

---

## 📅 WEEK 3 — Worker Threads, Clustering & Performance

This week separates **Node users** from **Node engineers**.

### Topics 3

- CPU-bound vs I/O-bound work
- Worker threads
- Clustering
- Load distribution
- When NOT to use workers

### Practice 3

- Benchmark CPU task in:
  - main thread
  - worker thread

- Use `cluster` to scale HTTP server locally

### Output 3

- Simple benchmark report (numbers + explanation)

🧠 **Senior signal**: You know Node’s limits and how to work around them.

---

## 📅 WEEK 4 — TypeScript for Backend (No Frontend BS)

TypeScript is **not optional** here.

### Topics 4

- Advanced types
- Generics
- Utility types
- Discriminated unions
- Type-safe APIs
- Runtime validation (zod)

### Practice 4

- Define domain models with strict types
- Validate input at boundaries
- Map validated data → domain objects

### Output 4

- Small API with:
  - zero `any`
  - strict TS config
  - runtime validation

🧠 **Senior signal**: Compiler catches bugs _before_ runtime.

---

## 🗓️ DAILY STRUCTURE (repeatable)

**Per day (~6–8h):**

- 2–3h learning (docs > videos)
- 3h coding
- 30 min reading (Node docs, blog posts)
- 30 min code review (your own)

---

## ✅ END OF MONTH 1 — YOU SHOULD BE ABLE TO

- Explain the Node.js event loop clearly
- Avoid blocking the main thread
- Use streams safely
- Scale CPU work correctly
- Write **strict, type-safe backend code**
- Debug async issues without panic 😌

---

## 🔍 MINI SENIOR CHECK (be honest)

If I ask you:

> “Why is this Node server slow under load?”

You should ask back:

- Is it CPU or I/O bound?
- Are we blocking the event loop?
- Are we leaking memory?
- Are streams applying backpressure?
- Are workers misused?

If those questions feel **natural**, you’re on track.

---
