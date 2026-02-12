# 🧠 PHASE 1 — Core Backend Foundations (Month 1–2)

> This phase builds **real backend engineers**.
> Not framework users. Not tutorial followers.

Your mission in Phase 1 is to deeply understand:

- **How the web works**
- **How data behaves**
- **Why systems fail**

All of this **before** touching architecture, scalability, or distributed systems.

---

## 🎯 Phase 1 Objectives

By the end of Phase 1, you should be able to:

- Build a backend **without frameworks**
- Reason confidently about HTTP requests and responses
- Understand authentication, authorization, and CORS deeply
- Design and query relational and non-relational databases correctly
- Explain performance and consistency trade-offs in data modeling

---

> If you don’t understand HTTP, you don’t understand backend.

---

## 1️⃣ What HTTP Really Is

HTTP is:

- Stateless
- Request → Response based
- Header-driven
- Sometimes misleading (status codes can lie)

You must understand:

- Request line
- Headers vs body
- Method semantics (`GET`, `POST`, `PUT`, `PATCH`, `DELETE`)
- Why `GET` with a body is wrong
- Why `200 OK` can still represent failure

---

## 2️⃣ HTTP Versions (Conceptual Understanding)

| Version  | Why it exists                     |
| -------- | --------------------------------- |
| HTTP/1.1 | Simple, but head-of-line blocking |
| HTTP/2   | Multiplexing, header compression  |
| HTTP/3   | QUIC over UDP, reduced latency    |

You do **not** implement these manually.
You design systems that behave correctly under them.

---

## 3️⃣ REST, RPC, and GraphQL

Understand **when** and **why** each exists:

- **REST** — resource-oriented, cache-friendly
- **RPC** — action-oriented, explicit intent
- **GraphQL** — client-driven queries

You must be able to explain:

- Over-fetching vs under-fetching
- Versioning challenges
- Caching implications

---

## 🛠️ Practice — Raw HTTP Server (No Frameworks)

### Requirements

- Use Node.js built-in HTTP module only
- Parse:
  - URL
  - Method
  - Headers

- Return correct status codes
- Handle malformed requests

### Constraints

- ❌ No Express
- ❌ No Fastify
- ❌ No middleware libraries

---

## 4️⃣ Status Codes (Truth vs Appearance)

Implement endpoints that return:

- `200 OK`
- `201 Created`
- `400 Bad Request`
- `401 Unauthorized`
- `403 Forbidden`
- `404 Not Found`
- `500 Internal Server Error`

You must:

- Intentionally return incorrect status codes
- Observe the consequences
- Fix them and explain why

---

## 5️⃣ Authentication vs Authorization

You must clearly understand:

- **Authentication** → Who are you?
- **Authorization** → What are you allowed to do?

### Implement

- `/login` endpoint
- Issue a random token
- Store the token in memory
- Protect a private route

Compare:

- Header-based tokens
- Cookie-based tokens
- Sessions vs stateless approaches

---

## 6️⃣ CORS (Cross-Origin Resource Sharing)

You must **break it** to understand it.

### Tasks

- Create a frontend request
- Trigger a CORS error
- Fix it manually
- Explain:
  - Preflight requests
  - Allowed origins
  - Allowed headers
  - Credentials behavior

If you can explain CORS clearly, you’re already above mid-level.

---

## 🧪 Mini Project

Build a small API with:

- `/login`
- `/profile`
- `/health`
- Request logging
- Naive rate limiting

### Project constraints

- ❌ No database
- ✅ In-memory only

---

> Frameworks hide databases.
> Engineers understand them.

---

## 7️⃣ Core Database Concepts

You must deeply understand:

- ACID
- Transactions
- Isolation levels
- Locks
- Deadlocks
- Indexes
- Query planners

---

## 8️⃣ Indexes & Performance

Learn:

- B-Tree indexes
- Hash indexes
- Composite indexes
- When indexes **hurt** performance

Understand:

- How queries are executed
- Why `SELECT *` is dangerous
- How indexes affect writes

---

## 9️⃣ Common Data Problems

You must recognize and fix:

- N+1 queries
- Over-normalization
- Over-denormalization
- Missing indexes
- Inefficient joins

---

## 🔢 Databases Used

### Primary

- PostgreSQL

### Secondary

- MongoDB

You must understand **why** both exist and when to choose each.

---

## 🛠️ Project — Same API, Two Databases

Build the **same API twice**.

### Version A — PostgreSQL

- Normalized schema
- Transactions
- Indexes

### Version B — MongoDB

- Document-based schema
- Embedded vs referenced data

Compare:

- Performance
- Complexity
- Schema evolution
- Query simplicity

---

## 🧠 Key Questions You Must Answer

- When is SQL the right choice?
- When does NoSQL win?
- What does consistency actually cost?
- How does schema design affect performance?

---

## ⚠️ Optional Enhancements

### Optional Topics

- **Idempotency**
  - Especially for `POST` requests
  - Retries and duplicate submissions

- **Basic HTTP Caching Headers**
  - `ETag`
  - `Cache-Control`
  - High-level understanding only

- **Connection Lifecycle**
  - Keep-alive
  - Why connection reuse matters
  - No low-level socket tuning required

---

## ❗ Phase 1 Rule

> If you don’t understand the data,
> nothing above this layer matters.

---
