# 🔒 ACID Properties

ACID ensures database transactions are **reliable, consistent, and safe**, even during failures.

---

## Overview

```mermaid
graph LR
    ACID["ACID Properties"]
    ACID --> A["A — Atomicity\nAll or Nothing"]
    ACID --> C["C — Consistency\nRules Never Broken"]
    ACID --> I["I — Isolation\nNo Interference"]
    ACID --> D["D — Durability\nCommitted = Permanent"]
```

---

## A — Atomicity (All or Nothing)

A transaction is treated as a **single unit**.

Either:
- ✅ Every operation succeeds, OR
- ❌ Everything is rolled back

### Example — Bank Transfer

```mermaid
sequenceDiagram
    participant App as Application
    participant DB as Database

    App->>DB: BEGIN TRANSACTION
    App->>DB: Deduct ₹1000 from Rahul
    App->>DB: Add ₹1000 to John

    alt All steps succeed
        DB-->>App: COMMIT ✅
    else Any step fails
        DB-->>App: ROLLBACK ❌
        Note over DB: Rahul's balance restored<br/>John's balance unchanged
    end
```

**Memory Trick: All or Nothing**

---

## C — Consistency (Rules are Never Broken)

Every transaction must preserve database rules and constraints.

The database always moves from one **valid state** to another **valid state**.

### Examples of Consistency Rules

| Rule | Example |
|------|---------|
| Balance constraint | Account balance cannot become negative |
| Type constraint | Age column cannot store text |
| Uniqueness | Primary Key cannot be duplicated |
| Referential integrity | Foreign key must reference a valid row |

```mermaid
graph LR
    V1["Valid State A\n(Before Transaction)"] -->|"Transaction"| V2["Valid State B\n(After Transaction)"]
    V1 -.->|"Invalid Transaction"| X["❌ Rejected\n(Rules Violated)"]
    style X fill:#ff4444,color:#fff
    style V2 fill:#22c55e,color:#fff
```

**Memory Trick: Rules are Never Broken**

---

## I — Isolation (Transactions Don't Interfere)

Multiple transactions executing simultaneously should behave as if they were executed **one after another**.

### Example — Movie Ticket Booking

```mermaid
sequenceDiagram
    participant U1 as User A
    participant DB as Database
    participant U2 as User B

    U1->>DB: Check last seat available
    U2->>DB: Check last seat available
    U1->>DB: Book the seat
    U2->>DB: Book the seat
    Note over DB: ❌ Only ONE transaction succeeds<br/>The other is rolled back
```

Without isolation, both users might book the same last seat simultaneously.

**Memory Trick: Transactions Don't Interfere**

---

## D — Durability (Committed Data Never Disappears)

Once the database confirms `Transaction Successful`, the data is **permanently stored**.

Even if:
- Server crashes
- Power failure occurs
- Database restarts

The committed data remains safe.

```mermaid
graph TD
    T["Transaction Committed ✅"] --> P["Data Permanently Written\nto Disk / WAL"]
    P --> R["Even after Crash/Restart\nData is Safe 🔒"]
    style T fill:#22c55e,color:#fff
    style R fill:#22c55e,color:#fff
```

**Memory Trick: Committed = Permanent**

---

## ACID Memory Trick Summary

| Property | Memory Trick | What It Means |
|----------|-------------|---------------|
| **Atomicity** | All or Nothing | Entire transaction succeeds or entire transaction rolls back |
| **Consistency** | Rules Never Broken | DB stays in a valid state before and after every transaction |
| **Isolation** | No Interference | Concurrent transactions behave as if sequential |
| **Durability** | Committed = Permanent | Committed data survives crashes and failures |

---

## Why Banks Prefer SQL (with ACID)

Banks use ACID-compliant SQL databases because they require:

- ✅ **Strong consistency** — Money must always be in exactly one account
- ✅ **Atomicity** — Transfers are all-or-nothing
- ✅ **Isolation** — Two transfers at the same time don't corrupt data
- ✅ **Durability** — Once a transaction is confirmed, it's permanent

---

## 💡 30-Second Interview Answer

> ACID properties ensure that database transactions are reliable. **Atomicity** means a transaction is all-or-nothing. **Consistency** ensures the database remains in a valid state. **Isolation** prevents concurrent transactions from interfering with each other. **Durability** guarantees that committed data survives system failures.

---

## 🔑 Key Interview Points

- **A — Atomicity**: All or Nothing — no partial updates
- **C — Consistency**: Rules are never violated — DB stays valid
- **I — Isolation**: Concurrent transactions don't see each other's intermediate states
- **D — Durability**: Committed data is permanent even after crashes
- SQL databases are **ACID-compliant** by default
- NoSQL databases often sacrifice ACID for performance (BASE model)
- Banks, payment systems, and airline bookings require ACID

---

## 🔗 Related Topics

- [SQL vs NoSQL](./sql-vs-nosql.md) — When ACID matters
- [Replication](./replication.md) — How durability is maintained across replicas
