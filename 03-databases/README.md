# 🗄️ Databases

A **database** is an organized collection of data that allows applications to **store, retrieve, update, and delete data efficiently**.

---

## Topics

| File | Description |
|------|-------------|
| [SQL vs NoSQL](./sql-vs-nosql.md) | Choosing the right database type |
| [ACID Properties](./acid-properties.md) | Transaction reliability guarantees |
| [Indexing](./indexing.md) | Speeding up queries with indexes |
| [Sharding](./sharding.md) | Splitting data horizontally |
| [Replication](./replication.md) | Copying data for availability |

---

## Quick Decision Guide

```mermaid
graph TD
    A["Choosing a Database"] --> B{Need ACID\nTransactions?}
    B -->|Yes| C{Complex\nRelationships?}
    B -->|No| D{Need Massive\nHorizontal Scale?}

    C -->|Yes| E["✅ SQL\nMySQL / PostgreSQL"]
    C -->|No| F["Could be either"]

    D -->|Yes| G["✅ NoSQL\nMongoDB / Cassandra"]
    D -->|No| H{Data Structure?}

    H -->|"Structured"| E
    H -->|"Flexible / Unstructured"| G
```

---

## ⭐ FAANG Quick Revision

**SQL**
- Relational Database
- Tables with rows & columns
- Primary Key & Foreign Key
- Fixed Schema
- Supports JOINs
- ACID compliant
- Vertical Scaling preferred
- Best for: Banking, Payments, Inventory

**NoSQL**
- Non-Relational
- Flexible Schema
- Horizontal Scaling
- Documents / Key-Value / Graph / Column
- Best for: Chat, Social Media, Product Catalogs
