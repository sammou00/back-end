# 🌐 HTTP — The Backbone of Backend Engineering

> If you truly understand HTTP, frameworks become optional.
> If you don’t, frameworks become dangerous.

This document explains HTTP **from first principles**, with the exact depth required for a strong backend foundation.

---

## 1️⃣ What HTTP Really Is

HTTP (Hypertext Transfer Protocol) is a **communication protocol** that defines how clients and servers talk to each other.

At its core, HTTP is:

### 🔹 Stateless

Each request is **independent**.

- The server does **not remember** previous requests
- Every request must contain **all required context**

Implications:

- Authentication data must be sent on every request
- Sessions, cookies, and tokens exist to _simulate_ state
- Stateless systems scale more easily

---

### 🔹 Request → Response Based

HTTP follows a strict pattern:

1. Client sends a **request**
2. Server processes it
3. Server sends a **response**
4. Connection may close or be reused

There is:

- No built-in streaming conversation
- No push (without extensions like WebSockets)

This shapes API design and error handling.

---

### 🔹 Header-Driven

Most HTTP behavior is controlled by **headers**, not the body.

Headers define:

- Authentication (`Authorization`)
- Content type (`Content-Type`)
- Caching (`Cache-Control`)
- CORS behavior
- Compression

> Many bugs are caused by incorrect or missing headers.

---

### 🔹 Sometimes Misleading

HTTP status codes describe **transport-level success**, not business success.

Examples:

- `200 OK` with an error message in JSON
- `404 Not Found` used for authorization hiding
- `500 Internal Server Error` masking application bugs

Correct backend design requires **semantic honesty**.

---

## 2️⃣ Anatomy of an HTTP Request

An HTTP request consists of **three main parts**.

---

### 🔹 Request Line

Example:

```bash
GET /api/users/42 HTTP/1.1
```

Contains:

- HTTP method (`GET`)
- Path (`/api/users/42`)
- Protocol version (`HTTP/1.1`)

The request line defines **intent**.

---

### 🔹 Headers

Key-value pairs that describe the request.

Examples:

```bash
Host: example.com
Authorization: Bearer <token>
Content-Type: application/json
Accept: application/json
```

Headers:

- Control behavior
- Provide metadata
- Affect security, caching, and routing

---

### 🔹 Body

The optional payload of the request.

Used mainly with:

- `POST`
- `PUT`
- `PATCH`

Typically contains:

- JSON
- Form data
- Binary data

Not all requests should have a body.

---

## 3️⃣ HTTP Methods — Semantics Matter

HTTP methods are **contracts**, not suggestions.

---

### 🔹 GET

- Retrieves data
- Must be **safe** and **idempotent**
- Should not modify server state

Why `GET` with a body is wrong:

- Not standardized
- Ignored by many servers and proxies
- Breaks caching assumptions

Use query parameters instead.

---

### 🔹 POST

- Creates a resource or triggers an action
- **Not idempotent** by default
- Used for operations with side effects

Common misuse:

- Using POST for updates
- Using POST when PUT or PATCH is correct

---

### 🔹 PUT

- Replaces a resource entirely
- **Idempotent**

If you send the same PUT request 10 times:

- The result is the same

---

### 🔹 PATCH

- Partially updates a resource
- Not necessarily idempotent

Used for:

- Small updates
- Field-level changes

---

### 🔹 DELETE

- Removes a resource
- Should be idempotent

Multiple DELETE requests should result in the same state.

---

## 4️⃣ Status Codes — Transport vs Meaning

Status codes describe **how the request was handled**, not whether the business logic succeeded.

Common categories:

- `2xx` — Request processed successfully
- `3xx` — Redirection
- `4xx` — Client error
- `5xx` — Server error

---

### 🔹 Why `200 OK` Can Mean Failure

Examples:

- Login failed, but request was processed
- Validation error returned in JSON
- Business rule violation

Correct APIs:

- Align status codes with reality
- Avoid hiding errors behind `200`

---

## 5️⃣ HTTP Versions (Conceptual Understanding)

You do **not** implement these manually.
You design systems that behave well under them.

---

| Version  | Why it exists                                      |
| -------- | -------------------------------------------------- |
| HTTP/1.1 | Simple, but suffers from head-of-line blocking     |
| HTTP/2   | Multiplexing multiple requests over one connection |
| HTTP/3   | Uses QUIC over UDP to reduce latency               |

---

### 🔹 Practical Implications

- Avoid large payloads
- Design APIs to be cache-friendly
- Don’t assume request order
- Be careful with long-running requests

---

## 🧠 Key Takeaways

- HTTP is simple, but unforgiving
- Headers control behavior
- Methods have meaning
- Status codes must be honest
- Statelessness is a feature, not a flaw
