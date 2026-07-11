# 🛡️ Rate Limiting

**Rate Limiting** is a technique used to control the **number of requests a client can make within a specified time period**. It protects servers from overload, abuse, and malicious attacks.

---

## What is Rate Limiting?

```
Limit = 100 Requests / Minute

Requests 1–100  → ✅ Allowed
Request 101     → ❌ HTTP 429 Too Many Requests
```

---

## Why Do We Need Rate Limiting?

```mermaid
graph TD
    Without["Without Rate Limiting"]
    Without --> P1["Single user can overload server"]
    Without --> P2["Brute-force password attacks possible"]
    Without --> P3["Bots can scrape entire website"]
    Without --> P4["Infrastructure costs skyrocket"]
    Without --> P5["Legitimate users get slow responses"]

    With["With Rate Limiting ✅"]
    With --> S1["Server protected from spikes"]
    With --> S2["Max 5 login attempts/min"]
    With --> S3["100 search requests/min"]
    With --> S4["Cost controlled"]
    With --> S5["Fair resource sharing"]
```

---

## Problems Rate Limiting Solves

### 1. Prevents Server Overload
Protects CPU, Memory, and Database resources. Prevents traffic spikes from crashing the system.

### 2. Prevents Brute Force Attacks
```
POST /login

Without rate limiting:
  Attacker tries millions of passwords

With rate limiting:
  Only 5 login attempts per minute ✅
```

### 3. Prevents API Abuse
```
Search API

Without limits: Bots scrape the entire website
With limits:    100 requests/minute
```

### 4. Controls Infrastructure Cost
```
AI APIs, SMS APIs, Email APIs
Each request has a cost.
Rate Limiting prevents excessive usage.
```

### 5. Fair Resource Sharing
Ensures one user cannot consume all server resources. Every client gets a fair share.

---

## Real-World Rate Limiting Examples

| API | Limit |
|-----|-------|
| Login API | 5 attempts / minute |
| OTP API | 3 requests / hour |
| Payment API | 10 requests / minute |
| Search API | 100 searches / minute |
| ChatGPT API | RPM (requests/min) + TPM (tokens/min) |
| File Upload | Limit per hour/day |

---

## Where is Rate Limiting Implemented?

```mermaid
graph TD
    Client --> LB["Load Balancer"]
    LB --> RL["Rate Limiter ← implemented here"]
    RL --> AG["API Gateway"]
    AG --> BS["Backend Services"]
    BS --> DB["Database"]
```

**Why before the backend?**
- Reject unwanted requests early
- Save CPU cycles
- Reduce database load
- Improve overall system performance

---

## How Rate Limiting Works

```mermaid
flowchart TD
    C["Client sends request"] --> ID["Rate Limiter identifies client\n(IP, UserID, API Key)"]
    ID --> Check{"Within\nlimit?"}
    Check -->|"Yes"| Forward["Forward to backend ✅"]
    Check -->|"No"| Reject["Return HTTP 429\nToo Many Requests ❌"]
```

---

## How Does the Server Identify Users?

| Method | Example | When Used |
|--------|---------|-----------|
| **IP Address** | `192.168.x.x` | Anonymous users |
| **User ID** | `user_123` | After login |
| **API Key** | `sk-abc123` | Public API access |
| **JWT Token** | `Bearer eyJ...` | Authenticated apps |
| **Device ID** | `device_abc` | Mobile apps |

---

## HTTP Response When Limit Exceeded

```http
HTTP/1.1 429 Too Many Requests
Retry-After: 60

{
  "error": "Rate limit exceeded",
  "message": "Try again in 60 seconds"
}
```

---

## Distributed Rate Limiting

### The Problem

With multiple servers, each maintaining its own counter:

```mermaid
graph TD
    Client["Client: 5 req limit"] --> LB["Load Balancer"]
    LB --> S1["Server 1\nCounter: 5 requests"]
    LB --> S2["Server 2\nCounter: 5 requests"]
    LB --> S3["Server 3\nCounter: 5 requests"]

    note["Total: 15 requests allowed\nBut limit should be 5! ❌"]
    style note fill:#ff4444,color:#fff
```

### The Solution — Shared Redis Counter

```mermaid
graph TD
    LB["Load Balancer"]
    LB --> S1["Server 1"]
    LB --> S2["Server 2"]
    LB --> S3["Server 3"]
    S1 & S2 & S3 --> Redis["Redis\n(Shared Counter)\n✅ Atomic operations\n✅ TTL support\n✅ In-memory speed"]
```

Every server checks the **same request count** in Redis.

### Redis Key Structure

```
Key:   user123
Value: 4  (current request count)
TTL:   60 seconds

After 60 seconds → counter resets automatically
```

---

## Rate Limiting Algorithms Overview

| Algorithm | Mechanism | Best For |
|-----------|-----------|---------|
| **Fixed Window Counter** | Count in fixed time window | Simple APIs |
| **Sliding Window Log** | Track exact timestamps | Security-sensitive |
| **Sliding Window Counter** | Estimate with window overlap | Large-scale distributed |
| **Token Bucket** | Tokens refill at fixed rate | Public APIs, bursts allowed |
| **Leaky Bucket** | Fixed outflow rate | Payment systems, smooth traffic |

> See [Algorithms](./algorithms.md) for detailed explanations of each.

---

## ✅ Advantages

- Protects servers from overload
- Prevents abuse and brute-force attacks
- Ensures fairness among users
- Improves availability
- Controls infrastructure cost
- Prevents sudden traffic spikes

---

## ❌ Disadvantages

- Legitimate users may occasionally be throttled
- Wrong algorithm choice can cause unfair limits
- Distributed implementation adds complexity (requires Redis)

---

## Common Use Cases

```mermaid
mindmap
  root((Rate Limiting))
    Login APIs
    OTP Services
    Payment Systems
    AI APIs
    Public APIs
    Search APIs
    File Upload APIs
    Social Media APIs
    Email Services
```

---

## 💡 30-Second Interview Answer

> **Rate Limiting** controls how many requests a client can make in a given time period. It protects servers from overload and abuse by returning **HTTP 429** when limits are exceeded. In distributed systems, a shared **Redis** instance is used as the counter store so all servers apply the same limit. Common algorithms include **Token Bucket** (allows bursts) and **Sliding Window** (most accurate).

---

## 🔑 Key Interview Points

- Rate limiting controls **request frequency** within a time window
- Common response: **HTTP 429 Too Many Requests**
- **Redis** is used for **distributed rate limiting** (shared atomic counter)
- Implemented **before** backend services (at load balancer or API gateway level)
- Clients identified by: IP, UserID, API Key, JWT, Device ID
- `Retry-After` header tells clients when to retry

---

## 🔗 Related Topics

- [Algorithms](./algorithms.md) — Fixed Window, Sliding Window, Token Bucket, Leaky Bucket
- [Load Balancer](../02-load-balancing/load-balancer.md) — Rate limiting often sits here
- [Caching Basics](../04-caching/caching-basics.md) — Redis also used for caching
