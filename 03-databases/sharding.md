# 🔀 Sharding

**Sharding** is the process of splitting one large database into multiple smaller databases. Each database stores only a **portion** of the data.

> **Memory Trick:**
> - Sharding = **Split** Data (horizontal partitioning)
> - Replication = **Copy** Data

---

## Why Do We Need Sharding?

```mermaid
graph TD
    Problem["Single DB Getting Too Large"]
    Problem --> P1["Too much data for one server"]
    Problem --> P2["Read/Write bottleneck"]
    Problem --> P3["Storage limit reached"]

    Solution["Sharding Solves This"]
    Solution --> S1["Horizontal Scaling"]
    Solution --> S2["Better Performance"]
    Solution --> S3["Increased Storage Capacity"]
    Solution --> S4["Reduced Load per DB"]
```

---

## Architecture

```mermaid
graph TD
    App["Application"] --> SR["Shard Router"]
    SR --> DB1["Shard 1\n(User IDs 1–1M)"]
    SR --> DB2["Shard 2\n(User IDs 1M–2M)"]
    SR --> DB3["Shard 3\n(User IDs 2M–3M)"]
```

Each shard is an independent database containing only a subset of the total data.

---

## Shard Key

The **Shard Key** is the column used to decide which shard stores the data.

**Common shard keys:**
- `UserID`
- `CustomerID`
- `Region`

> Choosing the right shard key is critical — a bad shard key leads to uneven data distribution (hot shards).

---

## Types of Sharding

### 1. Range-Based Sharding

```mermaid
graph LR
    SK["UserID"] --> D1["DB 1\n(1 – 1M)"]
    SK --> D2["DB 2\n(1M – 2M)"]
    SK --> D3["DB 3\n(2M – 3M)"]
```

| ✅ Advantages | ❌ Disadvantages |
|--------------|----------------|
| Simple to implement | May create **hot shards** (popular ranges get more traffic) |
| Easy range queries | Uneven distribution possible |

---

### 2. Hash-Based Sharding

```
Shard = UserID % NumberOfShards
```

```mermaid
graph LR
    SK["UserID"] --> HF["Hash Function\n(UserID % 3)"]
    HF --> D1["Shard 0\n(IDs ending in 0)"]
    HF --> D2["Shard 1\n(IDs ending in 1)"]
    HF --> D3["Shard 2\n(IDs ending in 2)"]
```

| ✅ Advantages | ❌ Disadvantages |
|--------------|----------------|
| Even data distribution | Range queries are hard |
| No hot shards | Resharding is complex when adding new shards |

---

### 3. Geographic Sharding

```mermaid
graph LR
    User["User Request"] --> Router["Router\n(based on location)"]
    Router --> D1["DB India\n(Indian Users)"]
    Router --> D2["DB USA\n(US Users)"]
    Router --> D3["DB Europe\n(EU Users)"]
```

| ✅ Advantages | ❌ Disadvantages |
|--------------|----------------|
| Low latency for regional users | Cross-region queries are complex |
| Regulatory compliance (data residency) | Uneven distribution if one region is larger |

---

## ✅ Advantages of Sharding

| Advantage | Description |
|-----------|-------------|
| **Horizontal Scaling** | Add more shards as data grows |
| **Better Performance** | Each shard handles a smaller dataset |
| **More Storage** | Unlimited total capacity |
| **Reduced Load** | Write/read load split across shards |

---

## ❌ Disadvantages of Sharding

| Disadvantage | Description |
|-------------|-------------|
| **Complex JOINs** | Joining data across shards is difficult |
| **Distributed Transactions** | Transactions spanning multiple shards are hard |
| **Rebalancing Data** | Moving data when adding/removing shards is complex |
| **Increased App Complexity** | Application must know how to route to the correct shard |

---

## ⭐ FAANG One-Liner

> **Sharding** splits data across multiple databases for horizontal scaling. Each shard stores a portion of data determined by the **Shard Key**. Hash-based sharding provides even distribution; range-based is simpler but may create hot shards.

---

## 💡 30-Second Interview Answer

> **Sharding** is the process of horizontally partitioning a database into multiple smaller shards, each containing a subset of the data. A **shard key** (such as UserID or Region) determines which shard stores each record. Sharding enables horizontal scaling and improves performance, but introduces complexity in JOINs, distributed transactions, and data rebalancing.

---

## 🔑 Key Interview Points

- Sharding = **split** data across multiple databases
- Replication = **copy** data across multiple databases
- **Shard Key** determines which shard holds the data
- **Hash-based** → even distribution, hard range queries
- **Range-based** → simple, but risk of hot shards
- **Geographic** → low latency for regional users
- Main challenges: complex JOINs, distributed transactions, rebalancing

---

## 🔗 Related Topics

- [Replication](./replication.md) — Sharding vs Replication
- [SQL vs NoSQL](./sql-vs-nosql.md) — NoSQL databases often have built-in sharding
- [Indexing](./indexing.md) — Each shard has its own indexes
