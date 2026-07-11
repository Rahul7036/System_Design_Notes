# **Vertical Scaling (Scale Up)**

**Vertical Scaling (Scale Up)** is the process of increasing the resources of an **existing server** to handle more traffic and workload.

Instead of adding more servers, we make the **same server more powerful**.

---

## **How is Vertical Scaling Done?**

The resources of the existing server are upgraded, such as:

* CPU (More cores)  
* RAM (More memory)  
* Storage (SSD → NVMe SSD)  
* Network Bandwidth

Only the server's hardware/resources are upgraded.

---

## **Architecture**

**Before**

Clients  
   |  
   |  
\+---------+  
| Server  |  
\+---------+

**After Vertical Scaling**

Clients  
   |  
   |  
\+----------------------+  
| High Capacity Server |  
\+----------------------+

There is still only **one server**.

---

# **Why Do We Need Vertical Scaling?**

As the number of users increases, the server may experience:

* High CPU utilization  
* High memory usage  
* Slow disk operations  
* Network bottlenecks

Instead of redesigning the architecture, we increase the server's capacity.

---

# **Advantages**

### **1\. Simple to Implement**

No architectural changes are required.

### **2\. No Application Code Changes**

The application usually runs without modification.

### **3\. Better Performance**

More CPU, RAM, and faster storage improve response time and throughput.

### **4\. Easy to Manage**

Only one server needs monitoring and maintenance.

### **5\. No Load Balancer Required**

Since there is only one server, requests are sent directly to it.

---

# **Disadvantages**

### **1\. Hardware Limit**

A server can only be upgraded up to its maximum supported CPU, RAM, and storage capacity.

---

### **2\. Single Point of Failure (SPOF)**

If the only server fails, the entire application becomes unavailable.

Clients  
   |  
   |  
Server ❌

Application Down

---

### **3\. Downtime**

Hardware upgrades often require shutting down or restarting the server.

---

### **4\. Expensive**

High-end enterprise servers become increasingly expensive as resources are upgraded.

---

### **5\. Limited Scalability**

Once the server reaches its maximum hardware capacity, it cannot be scaled further.

---

# **When Should We Use Vertical Scaling?**

* Small applications  
* Medium-sized applications  
* Development and testing environments  
* MVPs (Minimum Viable Products)  
* Internal company tools  
* Low to moderate traffic applications

---

# **When Should We Avoid Vertical Scaling?**

* Applications with millions of users  
* Systems requiring high availability  
* Global applications  
* Applications requiring fault tolerance  
* Very high traffic systems

---

# **Interview Definition (30-Second Answer)**

**Vertical Scaling (Scale Up)** is the process of increasing the computing resources (CPU, RAM, Storage, or Network Bandwidth) of an existing server to handle increased traffic. It is simple to implement and provides better performance but is limited by hardware capacity and introduces a Single Point of Failure (SPOF).

---

# **Key Interview Points to Remember**

* **Scale Up \= Upgrade the existing server**  
* **Only one server is used**  
* **Increase CPU, RAM, Storage, or Network**  
* **No load balancer required**  
* **Minimal or no application code changes**  
* **Easy to implement and manage**  
* **Limited by hardware capacity**  
* **Single Point of Failure (SPOF)**  
* **Suitable for small to medium-scale applications**  
* **Not suitable for internet-scale systems with millions of users**

# 

# **Horizontal Scaling (Scale Out)**

**Horizontal Scaling (Scale Out)** is the process of increasing the number of servers to handle more traffic and workload.

Instead of upgrading a single server, we **add multiple servers** and distribute requests among them.

---

## **How is Horizontal Scaling Done?**

New servers are added to the existing infrastructure.

Example:

**Before**

         Clients  
              |  
              |  
          \+---------+  
          | Server1 |  
          \+---------+

**After Horizontal Scaling**

              Clients  
                   |  
             \+--------------+  
             | Load Balancer |  
             \+--------------+  
              /      |      \\  
             /       |       \\  
      \+---------+ \+---------+ \+---------+  
      | Server1 | | Server2 | | Server3 |  
      \+---------+ \+---------+ \+---------+

Instead of making **Server1** more powerful, we add **Server2** and **Server3**.

---

# **Why Do We Need Horizontal Scaling?**

When a single server reaches its hardware limit, adding more CPU or RAM is no longer sufficient.

Instead, we distribute traffic across multiple servers to:

* Handle more concurrent users  
* Increase system capacity  
* Improve availability  
* Improve fault tolerance

---

# **What is a Load Balancer?**

A **Load Balancer** sits between clients and servers.

Its job is to distribute incoming requests across multiple servers.

Client Request

        |  
        v  
\+----------------+  
| Load Balancer  |  
\+----------------+  
     /   |   \\  
    /    |    \\  
 S1      S2    S3

Without a Load Balancer, one server may become overloaded while others remain idle.

---

# **Advantages**

### **1\. Almost Unlimited Scalability**

If traffic increases, simply add more servers.

1 Server

↓

5 Servers

↓

20 Servers

↓

100 Servers

---

### **2\. High Availability**

If one server fails, other servers continue serving requests.

Server1 ❌

Server2 ✅

Server3 ✅

The application remains available.

---

### **3\. Fault Tolerance**

Failure of one server does not bring down the entire system.

Traffic is automatically routed to healthy servers.

---

### **4\. Better Performance**

Requests are divided among multiple servers, reducing the load on each server.

Example:

Instead of one server handling **3000 requests/sec**,

Server1 → 1000 requests/sec

Server2 → 1000 requests/sec

Server3 → 1000 requests/sec

---

### **5\. Zero/Minimal Downtime**

Servers can be added or removed without shutting down the application.

---

# **Disadvantages**

### **1\. More Complex Architecture**

Requires multiple components such as:

* Load Balancer  
* Multiple Servers  
* Health Checks  
* Monitoring  
* Auto Scaling

---

### **2\. Higher Operational Complexity**

Managing multiple servers is more difficult than managing a single server.

---

### **3\. Data Consistency Challenges**

When multiple servers process requests, keeping data synchronized becomes challenging.

Solutions include:

* Shared Database  
* Replication  
* Distributed Cache

---

### **4\. Requires Stateless Applications**

Any server should be able to handle any request.

User-specific data (sessions) should not be stored on individual servers.

---

### **5\. Increased Infrastructure Cost**

More servers mean higher costs for:

* Compute  
* Networking  
* Monitoring  
* Maintenance

---

# **Stateless vs Stateful**

## **Stateless (Preferred)**

Every request is independent.

Any server can handle any request.

Client

      |

Load Balancer

   /      \\

S1        S2

No server stores user-specific session data.

---

## **Stateful (Not Preferred)**

A user's session is stored on a specific server.

If that server fails, the user's session is lost.

User A → Server1

User B → Server2

Scaling and failover become difficult.

---

# **When Should We Use Horizontal Scaling?**

* High traffic applications  
* Millions of users  
* Cloud-native applications  
* Microservices  
* E-commerce platforms  
* Social media platforms  
* Streaming services

---

# **When Should We Avoid Horizontal Scaling?**

* Small applications  
* MVPs  
* Internal tools  
* Low traffic systems  
* Simple applications where a single server is sufficient

---

# **Vertical Scaling vs Horizontal Scaling**

| Feature | Vertical Scaling | Horizontal Scaling |
| ----- | ----- | ----- |
| Method | Upgrade existing server | Add more servers |
| Number of Servers | One | Multiple |
| Load Balancer | Not Required | Required |
| Scalability | Limited by hardware | Nearly unlimited |
| High Availability | No | Yes |
| Fault Tolerance | Low | High |
| Single Point of Failure | Yes | No (if designed correctly) |
| Downtime During Scaling | Usually Yes | Minimal or No |
| Complexity | Low | High |
| Best For | Small/Medium Applications | Large-scale Applications |

---

# **Interview Definition (30-Second Answer)**

**Horizontal Scaling (Scale Out)** is the process of adding multiple servers to distribute traffic and increase system capacity. A **Load Balancer** routes requests among the servers, improving scalability, availability, and fault tolerance. It is the preferred approach for large-scale distributed systems because it can handle increasing traffic by simply adding more servers.

---

# **Key Interview Points to Remember**

* **Scale Out \= Add more servers**  
* **Requires a Load Balancer**  
* **Distributes requests across multiple servers**  
* **Provides High Availability**  
* **Provides Fault Tolerance**  
* **Supports nearly unlimited scalability**  
* **More complex than Vertical Scaling**  
* **Preferred for large-scale systems like Netflix, Amazon, and Google**  
* **Applications should ideally be stateless**  
* **Foundation of modern distributed system design**

# **Stateless Servers**

A **Stateless Server** is a server that **does not store any client-specific information (state)** between requests.

Every request contains all the information needed to process it.

**Each request is treated as a completely new request.**

---

# **What is "State"?**

**State** refers to any information about a user or previous requests that the server remembers.

Examples of state:

* User login session  
* Shopping cart  
* User preferences  
* OTP verification status  
* Game progress

If this information is stored on the server, the server is **stateful**.

If it is stored elsewhere (database/cache/client), the server is **stateless**.

---

# **How Does a Stateless Server Work?**

Every request contains everything the server needs.

Request 1  
User ID  
JWT Token  
Request Data  
        |  
        v  
     Server  
        |  
    Response

\----------------------------

Request 2  
User ID  
JWT Token  
Request Data  
        |  
        v  
     Server  
        |  
    Response

The server does **not remember** Request 1 while processing Request 2\.

---

# **Example**

### **Login Request**

POST /login

Username  
Password

Server verifies credentials and returns:

JWT Token

---

### **Fetch Profile**

GET /profile

Authorization: Bearer JWT

Server verifies the JWT and returns the profile.

The server doesn't remember the user from the login request—it simply validates the JWT in each request.

---

# **Why Do We Need Stateless Servers?**

Stateless servers make **Horizontal Scaling** possible.

Example:

                Clients  
                     |  
             \+----------------+  
             | Load Balancer  |  
             \+----------------+  
              /      |      \\  
             /       |       \\  
      \+---------+ \+---------+ \+---------+  
      | Server1 | | Server2 | | Server3 |  
      \+---------+ \+---------+ \+---------+

Since no server stores user-specific data:

* Request 1 → Server1  
* Request 2 → Server3  
* Request 3 → Server2

Everything still works.

---

# **Advantages**

## **1\. Easy Horizontal Scaling**

Any server can process any request.

---

## **2\. High Availability**

If one server fails, another server handles the next request.

---

## **3\. Better Load Distribution**

The Load Balancer can send requests to any available server.

---

## **4\. Easy Deployment**

Servers can be added or removed without affecting users.

---

## **5\. Fault Tolerance**

Failure of one server does not cause users to lose their session.

---

# **Disadvantages**

## **1\. Every Request Carries Extra Data**

Each request must include authentication information (e.g., JWT token), making requests slightly larger.

---

## **2\. Repeated Authentication**

The server validates the token on every request, adding a small processing overhead.

---

## **3\. External Storage Required**

State must be stored outside the application server, such as:

* Database  
* Redis Cache  
* Client (JWT)

---

# **Where is the State Stored?**

Instead of storing state on the server, it is stored externally.

Client  
   |  
JWT Token  
   |  
Load Balancer  
   |  
Any Server  
   |  
Database / Redis

This allows every server to access the same data.

---

# **Real-World Examples**

Stateless services are commonly used in:

* REST APIs  
* Microservices  
* Cloud-native applications  
* Kubernetes deployments  
* AWS Lambda functions

---

# **Stateless vs Stateful**

| Feature | Stateless | Stateful |
| ----- | ----- | ----- |
| Stores user session | No | Yes |
| Horizontal Scaling | Easy | Difficult |
| Load Balancer | Can route to any server | May require sticky sessions |
| Server Failure | User unaffected | User session may be lost |
| Fault Tolerance | High | Lower |
| Preferred for Distributed Systems | Yes | No |

---

# **Interview Definition (30-Second Answer)**

**A Stateless Server** is a server that does not store client-specific information between requests. Every request contains all the information needed to process it, allowing any server in the system to handle any request. This makes stateless servers ideal for horizontally scalable and highly available distributed systems.

---

# **Key Interview Points to Remember**

* **Does not store user session or request history**  
* **Every request is independent**  
* **Request contains all required information**  
* **Works well with Load Balancers**  
* **Enables Horizontal Scaling**  
* **Improves High Availability and Fault Tolerance**  
* **State is stored in a Database, Redis, or Client (JWT)**  
* **Preferred architecture for modern distributed systems**

# **Load Balancer**

A **Load Balancer** is a component that sits between clients and servers and distributes incoming requests across multiple servers.

Its main goal is to ensure that **no single server becomes overloaded**.

---

# **Why Do We Need a Load Balancer?**

Imagine we have three application servers.

Without a Load Balancer:

         Clients  
             |  
             |  
         \+---------+  
         | Server1 |  ❌ Overloaded  
         \+---------+

         \+---------+  
         | Server2 |  ✅ Idle  
         \+---------+

         \+---------+  
         | Server3 |  ✅ Idle  
         \+---------+

One server handles most requests while others remain underutilized.

With a Load Balancer:

             Clients  
                  |  
        \+----------------+  
        | Load Balancer  |  
        \+----------------+  
          /     |      \\  
         /      |       \\  
\+---------+ \+---------+ \+---------+  
| Server1 | | Server2 | | Server3 |  
\+---------+ \+---------+ \+---------+

Requests are evenly distributed.

---

# **Responsibilities of a Load Balancer**

A Load Balancer performs several important tasks:

* Distributes incoming requests  
* Prevents server overload  
* Improves availability  
* Detects unhealthy servers  
* Routes traffic only to healthy servers  
* Supports horizontal scaling

---

# **How Does It Work?**

### **Step 1**

A client sends a request.

Client

   |

GET /login

---

### **Step 2**

The request reaches the Load Balancer.

Client

   |

Load Balancer

---

### **Step 3**

The Load Balancer selects one of the available servers.

         Load Balancer  
         /      |      \\  
        /       |       \\  
Server1     Server2     Server3

---

### **Step 4**

The selected server processes the request and returns the response.

Client

↓

Load Balancer

↓

Server2

↓

Response

The client never communicates directly with the application servers.

---

# **Benefits of Using a Load Balancer**

## **1\. Better Resource Utilization**

Traffic is evenly distributed across servers.

---

## **2\. High Availability**

If one server fails, requests are routed to healthy servers.

Server1 ❌

Server2 ✅

Server3 ✅

Users usually don't notice the failure.

---

## **3\. Fault Tolerance**

Failure of one server doesn't bring down the application.

---

## **4\. Horizontal Scalability**

New servers can be added easily.

Before

Server1  
Server2

↓

After

Server1  
Server2  
Server3  
Server4

The Load Balancer starts routing traffic to the new servers.

---

## **5\. Reduced Response Time**

Traffic is shared among servers, reducing the load on each server.

---

# **Health Checks**

A Load Balancer continuously checks whether servers are healthy.

Example:

Server1 ✅ Healthy

Server2 ❌ Down

Server3 ✅ Healthy

Requests are sent only to Server1 and Server3.

---

# **Load Balancing Algorithms**

## **1\. Round Robin**

Requests are distributed one after another.

Request1 → Server1

Request2 → Server2

Request3 → Server3

Request4 → Server1

Request5 → Server2

Simple and commonly used.

---

## **2\. Least Connections**

The server with the fewest active connections receives the next request.

Example:

Server1 : 20 Connections

Server2 : 8 Connections

Server3 : 15 Connections

Next request goes to **Server2**.

Useful when request processing times vary.

---

## **3\. Weighted Round Robin**

Servers with higher capacity receive more requests.

Example:

Server1 Weight \= 3

Server2 Weight \= 2

Server3 Weight \= 1

Distribution:

S1

S1

S1

S2

S2

S3

Useful when servers have different hardware configurations.

---

## **4\. IP Hash**

The client's IP address determines which server handles the request.

Example:

User A → Server2

User B → Server1

User A → Server2

Useful for session persistence.

---

# **Types of Load Balancers**

## **1\. Layer 4 (Transport Layer)**

* Works at the TCP/UDP level  
* Uses IP address and Port Number  
* Faster because it doesn't inspect HTTP data

Example:

TCP

UDP

---

## **2\. Layer 7 (Application Layer)**

* Works at the HTTP/HTTPS level  
* Can inspect URLs, headers, cookies, and HTTP methods  
* Supports intelligent routing

Example:

/login

/profile

/orders

Layer 7 can route requests based on URL paths.

---

# **Hardware vs Software Load Balancers**

## **Hardware Load Balancer**

* Physical networking device  
* Very high performance  
* Expensive  
* Used in traditional data centers

Examples:

* F5 BIG-IP  
* Citrix ADC

---

## **Software Load Balancer**

Runs as software.

Popular examples:

* Nginx  
* HAProxy  
* Envoy  
* Traefik

Cloud providers also offer managed Load Balancers.

---

# **Real-World Example**

Suppose an e-commerce website receives **100,000 requests per minute**.

Clients

↓

Load Balancer

↓

10 Application Servers

The Load Balancer distributes requests so no single server becomes a bottleneck.

If one server crashes, traffic is automatically redirected to the remaining servers.

---

# **Interview Definition (30-Second Answer)**

A **Load Balancer** is a component that distributes incoming client requests across multiple application servers to prevent overload, improve availability, enable horizontal scaling, and ensure fault tolerance. It also performs health checks and routes traffic only to healthy servers.

---

# **Key Interview Points to Remember**

* **Sits between clients and servers**  
* **Distributes incoming requests**  
* **Prevents server overload**  
* **Enables Horizontal Scaling**  
* **Provides High Availability**  
* **Improves Fault Tolerance**  
* **Performs Health Checks**  
* **Common algorithms: Round Robin, Least Connections, Weighted Round Robin, IP Hash**  
* **Layer 4 works with TCP/UDP; Layer 7 works with HTTP/HTTPS**  
* **Common software load balancers: Nginx, HAProxy, Envoy**

# **Databases**

A **database** is an organized collection of data that allows applications to **store, retrieve, update, and delete data efficiently**. Databases provide persistence, consistency, security, and support for concurrent access by multiple users.

---

# **SQL (Relational Database)**

A **SQL (Structured Query Language) database** stores data in **tables** consisting of rows and columns. Tables are connected using **relationships**, which is why SQL is called a **Relational Database**.

### **Key Characteristics**

* Data is stored in **tables**.  
* Uses **Primary Keys (PK)** and **Foreign Keys (FK)** to create relationships.  
* Supports **JOINs** to retrieve data from multiple related tables.  
* Follows a **fixed schema**.  
* Ensures **ACID** properties for reliable transactions.  
* Best suited for applications requiring strong consistency and complex relationships.

### **Example**

Users Table

UserID (PK) | Name  
\-------------------  
1           | Rahul  
2           | John

Orders Table

OrderID | UserID (FK) | Amount  
\-------------------------------  
101     | 1           | 500  
102     | 2           | 700

Here, `Orders.UserID` references `Users.UserID`, creating a relationship.

---

# **Why is SQL called a Relational Database?**

Because data is divided into multiple tables that are **related** using **Primary Keys** and **Foreign Keys**. This reduces data duplication and maintains data integrity.

---

# **Primary Key (PK)**

* Uniquely identifies each row in a table.  
* Cannot contain duplicate values.  
* Cannot be NULL.

Example:

UserID  
\-------  
1  
2  
3

---

# **Foreign Key (FK)**

* A column that references the Primary Key of another table.  
* Establishes relationships between tables.  
* Maintains referential integrity.

Example:

Orders.UserID → Users.UserID

---

# **Fixed Schema**

A **schema** defines the structure of a table, including:

* Column names  
* Data types  
* Constraints

In SQL, the schema is defined **before** data is inserted.

Example:

Users

ID      INT  
Name    VARCHAR  
Age     INT

If you want to add a new column:

ALTER TABLE Users  
ADD Address;

Schema must be modified first.

---

# **Why SQL Uses a Fixed Schema**

* Ensures data consistency.  
* Prevents invalid data.  
* Makes relationships easier to maintain.  
* Ideal for structured data.

Examples:

* Banking  
* Airline Reservation  
* Hospital Management  
* Payroll Systems  
* Inventory Management

---

# **NoSQL (Non-Relational Database)**

NoSQL databases do **not** require a fixed schema.

Each record (document) can have different fields.

Example:

{  
  "name": "Rahul",  
  "age": 26  
}

{  
  "name": "John",  
  "city": "Hyderabad",  
  "hobbies": \["Bike", "Cricket"\]  
}

Both documents are valid.

---

# **Why NoSQL?**

Useful when data structure changes frequently.

Example:

Amazon Products

Laptop

RAM  
Processor  
SSD

Shirt

Color  
Size  
Fabric

Phone

Battery  
Camera  
Display

Different products have different attributes, making NoSQL a better choice.

---

# **SQL vs NoSQL**

| SQL | NoSQL |
| ----- | ----- |
| Relational | Non-Relational |
| Tables | Documents / Key-Value / Graph / Column |
| Fixed Schema | Flexible Schema |
| Supports JOINs | Limited or No JOINs |
| ACID Transactions | Usually BASE/Eventual Consistency (database dependent) |
| Vertical Scaling | Horizontal Scaling |
| Best for structured data | Best for unstructured/semi-structured data |

---

# **When to Use SQL**

Use SQL when:

* Strong consistency is required.  
* Data has complex relationships.  
* Transactions must be reliable.  
* ACID compliance is important.

Examples:

* Banking  
* Payments  
* Airline Booking  
* Hospital Systems  
* Inventory  
* Payroll

---

# **When to Use NoSQL**

Use NoSQL when:

* Schema changes frequently.  
* Massive scalability is required.  
* Data is semi-structured or unstructured.  
* High read/write throughput is needed.

Examples:

* Social Media  
* Chat Applications  
* Product Catalogs  
* IoT  
* Logging Systems  
* Caching

---

# **Vertical Scaling**

Vertical scaling means **increasing the resources of a single server**.

Example:

Before

CPU : 4  
RAM : 8 GB

↓

After

CPU : 32  
RAM : 128 GB

Advantages:

* Simple to implement.  
* No application changes required.  
* Easy database management.

Disadvantages:

* Hardware has a limit.  
* Expensive.  
* Single point of failure.

---

# **ACID Properties**

ACID ensures database transactions are **reliable, consistent, and safe**, even during failures.

---

## **A – Atomicity (All or Nothing)**

A transaction is treated as a **single unit**.

Either:

* Every operation succeeds.  
* Or everything is rolled back.

Example:

Transfer ₹1000

Deduct Rahul

↓

Add John

If "Add John" fails,

Rollback:

Rahul \= Original Balance  
John \= Original Balance

**Memory Trick:** **All or Nothing**

---

## **C – Consistency (Rules are Never Broken)**

Every transaction must preserve database rules and constraints.

Examples:

* Account balance cannot become negative.  
* Age cannot store text.  
* Primary Key cannot be duplicated.

The database always moves from one **valid state** to another **valid state**.

**Memory Trick:** **Rules are Never Broken**

---

## **I – Isolation (Transactions Don't Interfere)**

Multiple transactions executing simultaneously should behave as if they were executed one after another.

Example:

Two users trying to buy the last movie ticket.

Only one transaction should succeed.

**Memory Trick:** **Users Don't Interfere**

---

## **D – Durability (Committed Data Never Disappears)**

Once the database confirms:

Transaction Successful

The data is permanently stored.

Even if:

* Server crashes  
* Power failure occurs  
* Database restarts

The committed data remains.

**Memory Trick:** **Committed \= Permanent**

---

# **ACID Memory Trick**

Atomicity   → All or Nothing

Consistency → Rules are Never Broken

Isolation   → Transactions Don't Interfere

Durability  → Committed Data Never Disappears

---

# **Interview Answer: Why do Banks Prefer SQL?**

Banks use SQL databases because they require:

* Strong consistency.  
* ACID-compliant transactions.  
* Reliable money transfers.  
* Complex relationships between accounts, customers, and transactions.  
* High data integrity and security.

---

# **Interview Answer: SQL vs NoSQL**

**Choose SQL** when your application requires strong consistency, complex relationships, JOIN operations, and ACID transactions (e.g., banking, payments, airline booking).

**Choose NoSQL** when your application requires flexible schemas, horizontal scalability, and can handle rapidly changing or semi-structured data (e.g., chat apps, social media feeds, product catalogs).

---

## **⭐ FAANG Revision (30 Seconds)**

SQL  
• Relational Database  
• Tables  
• PK & FK  
• Fixed Schema  
• JOINs  
• ACID  
• Vertical Scaling  
• Best for Banking, Payments, Inventory

NoSQL  
• Non-Relational  
• Flexible Schema  
• Horizontal Scaling  
• Documents/Key-Value/Graph  
• Best for Chat, Social Media, Product Catalogs

ACID  
A → All or Nothing  
C → Rules Never Broken  
I → Transactions Don't Interfere  
D → Committed Data Never Disappears

These notes are concise enough for revision while still containing the depth expected in backend and FAANG system design interviews.

**📘 Database Scaling & Optimization Notes**

## **1\. SQL vs NoSQL**

### **SQL (Relational Database)**

* Stores data in tables (rows & columns)  
* Uses a predefined (fixed) schema  
* Supports relationships using Primary Key & Foreign Key  
* Follows ACID properties  
* Best for applications requiring consistency and complex relationships  
* Examples: MySQL, PostgreSQL

### **NoSQL**

* Stores data as Documents, Key-Value, Graph, or Column Family  
* Flexible schema  
* Easy horizontal scaling  
* Best for large-scale applications with rapidly changing data  
* Examples: MongoDB, Cassandra, Redis

---

## **2\. Why is SQL called a Relational Database?**

* Data is stored in multiple related tables.  
* Tables are connected using **Primary Keys** and **Foreign Keys**.  
* Supports JOIN operations to combine related data.  
* Maintains relationships and data integrity.

Example:

Users  
\------  
UserID (PK)  
Name

Orders  
\-------  
OrderID  
UserID (FK)  
Amount

One user can have many orders.

---

# **3\. ACID Properties**

### **A \- Atomicity**

* Transaction executes completely or not at all.  
* No partial updates.

Example:

* Money deducted but not credited ❌  
* Entire transaction rolls back.

---

### **C \- Consistency**

* Database always remains in a valid state.  
* Rules and constraints are never violated.

Example:

* Duplicate Primary Keys are not allowed.

---

### **I \- Isolation**

* Multiple transactions should not interfere with each other.  
* Users should not see incomplete changes.

---

### **D \- Durability**

* Once a transaction is committed, data is permanently saved.  
* Data survives crashes and power failures.

---

# **4\. Indexing**

### **What is an Index?**

An index is a separate data structure that stores:

Indexed Column Value  
        \+  
Pointer to Actual Row

Purpose:

* Speeds up data retrieval.  
* Avoids Full Table Scan.

---

### **Without Index**

Search Rahul

↓

Check Row1

↓

Check Row2

↓

Check Row3

↓

...

Time Complexity: **O(n)**

---

### **With Index**

Search Rahul

↓

Index

↓

Pointer

↓

Actual Row

Time Complexity: **O(log n)** (B-Tree)

---

### **Why INSERT is Slower?**

Whenever data changes:

* Table is updated.  
* Index is also updated.

More indexes \= More write operations.

---

### **When to Create an Index?**

* Frequently searched columns  
* WHERE  
* JOIN  
* ORDER BY  
* GROUP BY

Examples:

* Email  
* UserID  
* ProductID

---

### **Avoid Indexing**

* Small tables  
* Frequently updated columns  
* Columns with very few unique values (Gender, Status)

---

# **5\. B-Tree Index**

Default index used by most SQL databases.

Characteristics:

* Sorted  
* Balanced Tree  
* Search → O(log n)  
* Supports:  
  * \=  
  * \<  
  * BETWEEN  
  * ORDER BY  
  * LIKE 'abc%'

---

# **6\. Hash Index**

Uses a Hash Function.

Value

↓

Hash Function

↓

Bucket

↓

Row Pointer

Characteristics:

* Exact match only (=)  
* Average lookup O(1)  
* Does NOT support:  
  * Range Queries  
  * ORDER BY  
  * BETWEEN  
  * LIKE 'abc%'

---

### **Why B-Tree is Preferred?**

Because B-Tree supports both exact searches and ordered/range queries, making it suitable for general-purpose indexing.

---

# **7\. Clustered vs Non-Clustered Index**

### **Clustered Index**

* Table data is physically stored in index order.  
* Only ONE clustered index per table.

---

### **Non-Clustered Index**

* Separate structure.  
* Stores indexed values \+ row pointers.  
* Multiple non-clustered indexes are allowed.

---

# **8\. Composite (Compound) Index**

Index created on multiple columns.

Example:

INDEX(Name, Department)

Supports:

WHERE Name='Rahul'

WHERE Name='Rahul'  
AND Department='IT'

Does NOT efficiently support:

WHERE Department='IT'

because of the **Leftmost Prefix Rule**.

---

### **Leftmost Prefix Rule**

For:

INDEX(A, B, C)

Efficient:

* A  
* A \+ B  
* A \+ B \+ C

Not Efficient:

* B  
* C  
* B \+ C

---

# **9\. Sharding**

### **Definition**

Splitting one large database into multiple smaller databases.

Each database stores only a portion of the data.

Purpose:

* Horizontal Scaling  
* Better Performance  
* Increased Storage

---

### **Types**

#### **Range-based**

1-1M → DB1

1M-2M → DB2

Simple but may create hot shards.

---

#### **Geographic**

India → DB1

USA → DB2

Useful for global applications.

---

#### **Hash-based**

UserID % NumberOfShards

Provides even distribution.

---

### **Shard Key**

Column used to decide which shard stores the data.

Examples:

* UserID  
* CustomerID  
* Region

---

### **Advantages**

* Horizontal Scaling  
* Better Performance  
* More Storage  
* Reduced Load

---

### **Disadvantages**

* Complex JOINs  
* Distributed Transactions  
* Rebalancing Data  
* Increased Application Complexity

---

# **10\. Replication**

### **Definition**

Keeping multiple copies of the same database.

Purpose:

* High Availability  
* Backup  
* Disaster Recovery

Remember:

Sharding \= Split Data

Replication \= Copy Data

---

# **11\. Primary-Replica (Master-Slave)**

Architecture:

Writes → Primary

Reads → Replica

Flow:

Application

↓

Primary

↓

Replica(s)

Advantages:

* Reduces read load  
* Improves availability  
* Simple architecture  
* No write conflicts

Disadvantage:

* If Primary fails, writes stop until failover.

---

# **12\. Master-Master Replication**

Architecture:

Primary A ⇄ Primary B

Both databases:

* Read  
* Write

Advantages:

* Lower latency for global users  
* No single write location

Disadvantages:

* Write conflicts  
* Complex conflict resolution  
* Harder to maintain

---

# **13\. Read Replicas**

Purpose:

* Offload read traffic from Primary.

Flow:

Writes → Primary

Reads → Replica1

Reads → Replica2

Reads → Replica3

Best for:

* Product Search  
* News Feed  
* User Profiles  
* Reports

---

# **14\. Replication Lag**

Definition:

Delay between data being written to Primary and reaching Replica.

Causes:

* Network latency  
* Disk writes  
* Processing time

Problem:

* Replica may return stale (old) data.

Use Primary for:

* Login after password change  
* Payment confirmation  
* Bank balance  
* Recent orders

Use Replica for:

* Product catalog  
* News feed  
* Search  
* User profiles

---

# **15\. Failover**

Definition:

When the Primary fails, a Replica is promoted to become the new Primary.

Flow:

Primary ❌

↓

Replica becomes Primary ✅

Purpose:

* High Availability  
* Minimal Downtime

Types:

* Automatic Failover  
* Manual Failover

Old Primary:

* Usually rejoins as a Replica after recovery.

---

# **⭐ FAANG Interview One-Liners**

SQL  
\----  
• Relational database with fixed schema and ACID.

Index  
\-----  
• Speeds up reads but slows writes.

B-Tree  
\------  
• Default SQL index.  
• Supports range queries and sorting.

Hash Index  
\----------  
• Best for exact-match lookups only.

Composite Index  
\---------------  
• Multi-column index.  
• Follows Leftmost Prefix Rule.

Sharding  
\--------  
• Splits data across multiple databases for horizontal scaling.

Replication  
\-----------  
• Copies the same data across databases for availability.

Primary-Replica  
\---------------  
• Writes → Primary  
• Reads → Replicas

Master-Master  
\-------------  
• Multiple Primaries can handle writes.  
• More complex due to write conflicts.

Read Replica  
\------------  
• Handles read traffic to reduce load on Primary.

Replication Lag  
\---------------  
• Delay before Replicas receive latest updates.

Failover  
\--------  
• Promotes a Replica to Primary when the Primary fails.

**3\. Caching**

## **What is Caching?**

Cache is a **temporary, fast storage** used to store **frequently accessed data** so future requests can be served faster without querying the database every time.

### **Why do we need Cache?**

* Reduce response time (low latency)  
* Reduce database load  
* Improve application performance  
* Improve scalability

### **Why is Cache Faster?**

* Databases primarily read data from **Disk (SSD/HDD)**.  
* Cache systems like **Redis** store data in **RAM (Memory)**.  
* **RAM is much faster than Disk**, so reading from cache is much quicker.

---

## **Basic Architecture**

User  
  │  
Backend Server  
  │  
Redis (Cache)  
  │  
Database

Backend always checks **Redis first**.

---

## **Cache Hit**

Requested data is found in the cache.

User  
  │  
Backend  
  │  
Redis ✅  
  │  
Return Response

* No database call  
* Fast response

---

## **Cache Miss**

Requested data is not found in the cache.

User  
  │  
Backend  
  │  
Redis ❌  
  │  
Database  
  │  
Store in Redis  
  │  
Return Response

---

## **What is Redis?**

Redis is an **in-memory database** (stores data in RAM).

Think of Redis like PostgreSQL or MySQL—it's another software/service that your backend connects to.

Python Backend  
      │  
      ├── Redis  
      └── PostgreSQL

### **Redis stores data as Key-Value pairs**

user:101      Rahul  
product:20    iPhone  
order:99      Delivered

Example:

redis.set("user:101", user\_data)  
redis.get("user:101")

---

## **Is Redis a Separate Server?**

Usually, **Yes**.

Development:

Laptop  
 ├── Backend  
 ├── Redis  
 └── Database

Production:

Server 1 → Backend  
Server 2 → Redis  
Server 3 → Database

---

# **Cache Levels**

## **1\. Browser Cache (Client-side)**

Stores static files in the user's browser.

Examples:

* Images  
* CSS  
* JavaScript  
* Fonts

Purpose:  
Avoid downloading the same static files repeatedly.

---

## **2\. CDN Cache**

Stores static content at servers located around the world.

Examples:

* Images  
* Videos  
* CSS  
* JavaScript

Purpose:  
Serve content from the nearest geographical location.

---

## **3\. Application Cache (Redis)**

Cache placed between the backend and the database.

Purpose:

* Cache API responses  
* User details  
* Product information  
* Frequently accessed data

---

## **4\. Database Cache**

Internal cache maintained by the database to reduce repeated disk reads.

Usually handled automatically by the database.

---

## **Request Flow**

User  
  │  
Browser Cache  
  │  
CDN  
  │  
Backend  
  │  
Redis  
  │  
Database Cache  
  │  
Disk

Each layer tries to serve the request before it reaches the next one.

---

# **Cache Strategies**

## **1\. Cache-Aside (Lazy Loading) ⭐ Most Common**

Flow:

Request  
   │  
Check Cache  
   │  
Found?  
 ├── Yes → Return  
 └── No  
        │  
    Read Database  
        │  
 Store in Cache  
        │  
     Return

### **Advantages**

* Only caches required data  
* Saves memory  
* Most commonly used strategy

### **Disadvantage**

* First request is slower (Cache Miss)

---

## **2\. Write-Through**

Whenever data is updated:

Application  
     │  
Update Cache  
     │  
Update Database

### **Advantages**

* Cache always remains up to date.

### **Disadvantages**

* Slower writes because both cache and database must be updated.

---

## **3\. Write-Behind (Write-Back)**

Flow:

Application  
      │  
Update Cache  
      │  
Return Success  
      │  
Background Process  
      │  
Update Database

### **Advantages**

* Very fast writes.

### **Disadvantages**

* If Redis crashes before writing to the database, data may be lost.

---

# **TTL (Time To Live)**

TTL defines how long a cache entry should remain before it expires automatically.

Example:

user:101

TTL \= 300 seconds

After 5 minutes:

Redis automatically removes the key.

Next request becomes a Cache Miss and fetches fresh data from the database.

Purpose:

* Prevent stale data  
* Free memory automatically

---

# **Cache Invalidation**

Cache may contain outdated (stale) data after the database is updated.

Ways to keep cache fresh:

### **1\. Time-based Expiry**

Use TTL so data expires automatically.

---

### **2\. Event-driven Invalidation**

Whenever the database is updated:

Update Database  
      │  
Delete / Update Cache

---

### **3\. Cache Busting**

Explicitly remove or refresh cache after updates.

---

# **Interview Keywords**

* Cache  
* Redis  
* RAM  
* Low Latency  
* Cache Hit  
* Cache Miss  
* Cache-Aside  
* Write-Through  
* Write-Behind  
* TTL  
* Cache Invalidation  
* Key-Value Store

---

# **30-Second Interview Summary**

**Caching stores frequently accessed data in a fast in-memory store like Redis to reduce database load and improve response time. The backend checks the cache first. If the data exists (Cache Hit), it returns immediately. Otherwise (Cache Miss), it fetches the data from the database, stores it in Redis, and returns it. Common cache strategies include Cache-Aside, Write-Through, and Write-Behind. TTL and cache invalidation ensure cached data remains fresh.**

# **Message Queues**

## **What is a Message Queue?**

A **Message Queue (MQ)** is middleware that enables asynchronous communication between services.

Instead of one service calling another service directly, it sends a **message** to the queue. Another service consumes the message whenever it is ready.

Producer  
    │  
    ▼  
Message Queue  
    │  
    ▼  
Consumer

---

# **Why do we use Message Queues?**

## **1\. Decoupling**

Without MQ

Order Service  
      │  
      ├──► Payment  
      ├──► Email  
      ├──► SMS  
      ├──► Inventory  
      └──► Analytics

Every service depends on every other service.

With MQ

Order Service  
      │  
      ▼  
 Message Queue  
      │  
 ┌────┼────────┐  
 ▼    ▼        ▼  
Email SMS Inventory ...

Each service works independently.

---

## **2\. Asynchronous Processing**

Producer sends the message and immediately continues.

Consumer processes it later.

Producer

↓

Queue

↓

Consumer

---

## **3\. Traffic Spike Handling**

Suppose

Producer : 20,000 messages/sec

Consumer : 2,000 messages/sec

The queue temporarily stores excess messages until consumers catch up.

---

## **4\. Reliability**

If a consumer is unavailable, messages remain in the queue until processing resumes.

---

## **5\. Scalability**

Consumers can be increased independently.

          Queue

      ┌─────┼─────┐

      ▼     ▼     ▼

     C1    C2    C3

---

# **Core Components**

## **Producer**

Application that publishes messages.

Responsibilities

* Create message  
* Send to broker  
* Doesn't wait for processing

---

## **Consumer**

Application that receives messages.

Responsibilities

* Read message  
* Process it  
* Send acknowledgement

---

## **Broker**

Middleware responsible for

* Receiving messages  
* Storing messages  
* Delivering messages  
* Retrying failed deliveries  
* Replication  
* Ordering  
* Acknowledgements

Examples

* Kafka  
* RabbitMQ  
* Amazon SQS  
* Google Pub/Sub

---

## **Queue**

Temporary storage containing messages waiting for processing.

---

# **Message Lifecycle**

Producer

↓

Broker

↓

Queue

↓

Consumer

↓

ACK

↓

Delete Message

---

# **Acknowledgement (ACK)**

Consumer informs broker that processing completed successfully.

Consumer

↓

ACK

↓

Broker deletes message

Without ACK

Consumer crashes

↓

Broker keeps message

↓

Retries later

---

# **Retry Mechanism**

If processing fails

Attempt 1

↓

Failed

↓

Attempt 2

↓

Failed

↓

Attempt 3

Retry count is configurable.

---

# **Dead Letter Queue (DLQ)**

Messages that exceed retry limits are moved to another queue.

Main Queue

↓

Retry

↓

Retry

↓

Retry

↓

Dead Letter Queue

Purpose

* Corrupted messages  
* Invalid payloads  
* Debugging  
* Manual processing

---

# **Delivery Guarantees**

## **At Most Once**

0 or 1 delivery

Characteristics

* No duplicates  
* Possible message loss

---

## **At Least Once**

1 or more deliveries

Characteristics

* No silent loss  
* Duplicate processing possible

Requires

* Idempotent consumers

---

## **Exactly Once**

Exactly one successful processing

Requires

* Transactions  
* Idempotency  
* Offset management

Very difficult in distributed systems.

---

# **Idempotency**

Processing the same message multiple times should produce the same final state.

Usually implemented using

* Unique transaction ID  
* Message ID  
* Database constraints

---

# **Point-to-Point Queue**

Producer

↓

Queue

↓

Consumer A

Consumer B

Consumer C

Only one consumer receives each message.

Used for

* Background jobs  
* Task processing

---

# **Publish Subscribe**

Publisher

↓

Topic

↓

Subscriber A

Subscriber B

Subscriber C

Every subscriber receives a copy.

---

# **FIFO**

First In First Out

1

2

3

↓

1

2

3

RabbitMQ provides FIFO queues.

Kafka guarantees ordering only inside a partition.

---

# **Back Pressure**

Occurs when

Producer Rate

\>

Consumer Rate

Solutions

* Increase consumers  
* Increase partitions  
* Throttle producers

---

# **Horizontal Scaling**

Producer

↓

Queue

↓

Consumer1

Consumer2

Consumer3

Consumer4

---

# **Kafka**

Apache Kafka is a distributed event streaming platform.

Best suited for

* Event streaming  
* Log aggregation  
* Analytics  
* Event sourcing  
* Metrics collection

---

# **Kafka Architecture**

                        PRODUCERS  
                   ┌────────┼────────┐  
                   │        │        │  
                   ▼        ▼        ▼  
                ┌──────────────────────────┐  
                │      Kafka Cluster       │  
                │                          │  
                │  Broker 1   Broker 2     │  
                │  Broker 3   Broker 4     │  
                └──────────┬───────────────┘  
                           │  
                    Topics (Logical)  
                           │  
             ┌─────────────┴─────────────┐  
             │                           │  
         Orders Topic               Users Topic  
             │  
     ┌───────┼─────────┐  
     ▼       ▼         ▼  
Partition0 Partition1 Partition2  
     │         │          │  
     │         │          │  
Offsets    Offsets    Offsets  
0 1 2 3    0 1 2      0 1

     │         │          │  
     └─────────┼──────────┘  
               ▼  
        Consumer Group  
     ┌───────────────┐  
     │ C1 │ C2 │ C3  │  
     └───────────────┘

---

# **Kafka Components**

## **Producer**

Publishes messages to topics.

---

## **Broker**

Kafka server.

A cluster usually contains multiple brokers.

Responsibilities

* Store messages  
* Replication  
* Serve consumers  
* Partition management

---

## **Topic**

Logical category of messages.

Examples

Orders

Payments

Users

---

## **Partition**

Each topic is divided into partitions.

Orders

│

├── Partition 0

├── Partition 1

└── Partition 2

Benefits

* Parallel processing  
* Horizontal scalability  
* High throughput

---

## **Offset**

Every message receives a sequential number.

Offset

0

1

2

3

4

Consumers track offsets.

Broker doesn't track consumer progress.

---

## **Consumer Group**

Consumers sharing work.

Topic

↓

P0

P1

P2

P3

↓

C1

C2

Possible assignment

C1

P0

P2

C2

P1

P3

One partition is consumed by only one consumer within the same consumer group.

---

# **Replication**

Each partition has replicas.

Leader

↓

Follower

↓

Follower

Leader handles

* Reads  
* Writes

Followers continuously replicate.

If leader crashes

Follower becomes leader.

---

# **Kafka Data Flow**

Producer

↓

Broker

↓

Topic

↓

Partition

↓

Consumer Group

↓

Consumers

---

# **Kafka Advantages**

* Extremely high throughput  
* Persistent storage  
* Horizontal scaling  
* Replication  
* Fault tolerance  
* Event replay  
* Durable storage

---

# **Kafka Limitations**

* Complex setup  
* Higher operational overhead  
* Limited routing flexibility

---

# **RabbitMQ**

RabbitMQ is a general-purpose message broker implementing AMQP.

Best suited for

* Background jobs  
* Task queues  
* RPC  
* Email processing  
* Microservices

---

# **RabbitMQ Architecture**

                Producer  
                     │  
                     ▼  
               ┌───────────┐  
               │ Exchange  │  
               └─────┬─────┘  
      ┌──────────────┼──────────────┐  
      ▼              ▼              ▼  
   Queue A       Queue B       Queue C  
      │              │              │  
      ▼              ▼              ▼  
 Consumer A     Consumer B     Consumer C

---

# **RabbitMQ Components**

## **Producer**

Publishes messages.

Producer never sends directly to queues.

---

## **Exchange**

Responsible for routing messages.

Producer

↓

Exchange

↓

Queue

---

## **Queue**

Stores messages until consumers process them.

---

## **Consumer**

Reads messages from queues.

---

## **Binding**

Connects

Exchange

↓

Queue

Defines routing rules.

---

# **Exchange Types**

## **Direct Exchange**

Routes using exact routing key.

Producer

↓

Exchange

↓

email

↓

Email Queue

---

## **Fanout Exchange**

Broadcasts to every queue.

Exchange

↓

Queue1

Queue2

Queue3

---

## **Topic Exchange**

Routes using wildcard patterns.

order.\*

order.created

payment.\*

---

## **Headers Exchange**

Uses message headers for routing.

Rarely used.

---

# **RabbitMQ Flow**

Producer

↓

Exchange

↓

Queue

↓

Consumer

↓

ACK

↓

Delete

---

# **RabbitMQ Advantages**

* Low latency  
* Reliable delivery  
* Rich routing  
* Easy retries  
* Simple deployment

---

# **RabbitMQ Limitations**

* Lower throughput than Kafka  
* Not intended for event streaming  
* Limited message replay

---

# **Kafka vs RabbitMQ**

| Feature | Kafka | RabbitMQ |
| ----- | ----- | ----- |
| Primary Model | Distributed Log | Message Queue |
| Storage | Persistent Log | Queue |
| Throughput | Extremely High | High |
| Latency | Low | Very Low |
| Ordering | Per Partition | FIFO Queue |
| Routing | Basic | Advanced |
| Replay Messages | Yes | No |
| Consumer Model | Pull | Push (default) |
| Message Retention | Configurable | Removed after ACK |
| Scalability | Partition-based | Consumer/Queue-based |
| Best For | Streaming | Task Queues |

---

# **Amazon SQS**

AWS managed queue service.

Types

* Standard Queue  
* FIFO Queue

Features

* Managed by AWS  
* Highly available  
* Durable  
* Auto scaling

---

# **Google Pub/Sub**

Google Cloud messaging service.

Architecture

Publisher

↓

Topic

↓

Subscription

↓

Consumers

---

# **Common Interview Questions**

### **Why use Message Queues?**

* Service decoupling  
* Asynchronous processing  
* Reliability  
* Traffic spike handling  
* Independent scaling  
* Fault tolerance

---

### **When to choose Kafka?**

* Event streaming  
* Analytics  
* Event sourcing  
* Logging  
* High throughput pipelines

---

### **When to choose RabbitMQ?**

* Background jobs  
* Email systems  
* RPC  
* Task queues  
* Complex routing

---

### **What is Consumer Lag?**

Consumer Lag

\=

Latest Offset

\-

Committed Offset

Large lag indicates consumers are slower than producers.

---

### **Why use a Dead Letter Queue?**

To isolate messages that repeatedly fail processing so they do not block normal message flow.

---

### **Quick Revision**

Producer → Sends messages

Broker → Receives and stores messages

Queue → Holds messages

Consumer → Processes messages

ACK → Confirms successful processing

Retry → Reprocess failed messages

DLQ → Stores permanently failed messages

Point-to-Point → One consumer receives the message

Publish-Subscribe → Every subscriber receives a copy

Kafka → Distributed event streaming platform

RabbitMQ → AMQP-based message broker

Topic → Logical category (Kafka)

Partition → Parallel unit inside a topic

Offset → Position of a message in a partition

Consumer Group → Consumers sharing partitions

Exchange → Routes messages to queues (RabbitMQ)

Binding → Connects exchange to queue

Direct Exchange → Exact routing

Fanout Exchange → Broadcast

Topic Exchange → Pattern-based routing

Headers Exchange → Header-based routing

At Most Once → Possible loss, no duplicates

At Least Once → Possible duplicates, minimal loss

Exactly Once → Requires transactions and idempotency

Idempotency → Processing a duplicate message produces the same final result

# **Content Delivery Network (CDN)**

## **Definition**

A **Content Delivery Network (CDN)** is a globally distributed network of **Edge Servers** that cache copies of content (images, CSS, JavaScript, videos, fonts, PDFs, etc.) closer to end users. Instead of every request going to the origin server, users receive content from the nearest edge server, reducing latency, improving page load times, and decreasing load on the origin infrastructure.

---

# **Why do we need a CDN?**

Imagine our application is hosted in **Hyderabad (India)**.

Users access it from:

* India  
* USA  
* Germany  
* Australia  
* Japan

Without a CDN, every request for:

* Images  
* CSS  
* JavaScript  
* Videos  
* Fonts

must travel all the way to Hyderabad.

### **Problems**

* High latency  
* Slow website loading  
* Increased bandwidth usage  
* Heavy load on origin server  
* Poor global user experience

The farther the user is from the server, the longer the network latency.

---

# **Solution**

Instead of storing files only on the origin server, create cached copies at multiple locations around the world.

Origin Server  
      |  
\--------------------------------------  
|      |      |      |      |  
USA   Europe India Japan Australia  
Edge   Edge   Edge   Edge   Edge

Users always download content from the nearest Edge Server.

---

# **CDN Architecture**

                   User

                      |

                DNS Lookup

                      |

        Finds Nearest CDN Edge Server

                      |

                Edge Server

              Cache Available?

             /               \\  
            /                 \\

      YES (Cache Hit)      NO (Cache Miss)

            |                   |

     Return Cached File    Contact Origin Server

                                |

                          Download Content

                                |

                      Store in Edge Cache

                                |

                         Return to User

---

# **Complete Production Architecture**

                   Users  
       (India, USA, Europe, Japan)

                     |

                 Internet

                     |

             DNS Resolution

                     |

      \-----------------------------  
      |           CDN             |  
      |                           |  
      |  POP India                |  
      |     Edge Server           |  
      |                           |  
      |  POP USA                  |  
      |     Edge Server           |  
      |                           |  
      |  POP Europe               |  
      |     Edge Server           |  
      \-----------------------------

                     |

              Origin Server

        (EC2 / Nginx / Apache)

                     |

               Load Balancer

                     |

           Application Servers

                     |

          Redis / Database / S3

---

# **Components of CDN**

## **1\. Origin Server**

The Origin Server is the original source of all content.

It contains:

* Backend application  
* Images  
* Videos  
* CSS  
* JavaScript  
* APIs  
* Databases

Examples:

* EC2  
* S3  
* Nginx  
* Apache  
* Kubernetes Application

Whenever an edge server doesn't have the requested file, it fetches it from the origin.

---

## **2\. Edge Server**

An Edge Server is a cache server located close to users.

Its job is to:

* Store cached files  
* Serve users quickly  
* Reduce requests reaching the origin

Example:

A user in New York should ideally get data from a New York Edge Server rather than Hyderabad.

---

## **3\. POP (Point of Presence)**

A POP is a physical CDN location or data center.

Example:

Mumbai POP

   |  
   |--- Edge Server 1  
   |--- Edge Server 2  
   |--- Edge Server 3

Many Edge Servers exist inside one POP.

### **Interview Question**

Difference between POP and Edge Server?

**POP**

* Physical location  
* Contains multiple servers

**Edge Server**

* Actual machine serving cached content  
* Exists inside a POP

---

# **Request Lifecycle**

Suppose a user opens:

https://example.com/logo.png

### **Step 1**

Browser requests:

logo.png

↓

DNS resolves the domain.

↓

Nearest CDN Edge Server is selected.

---

### **Step 2**

Edge Server checks cache.

Is logo.png available?

Two possibilities.

---

## **Scenario 1: Cache Hit**

User

↓

Edge Server

↓

logo.png Found

↓

Return Immediately

No request goes to the Origin Server.

Latency:

5–20 ms

---

## **Scenario 2: Cache Miss**

User

↓

Edge Server

↓

Not Found

↓

Origin Server

↓

Download File

↓

Store in Cache

↓

Return to User

The next user receives the cached version.

---

# **Cache Hit**

Definition:

A Cache Hit occurs when the requested content is already available in the Edge Server.

Advantages:

* Very fast response  
* Lower latency  
* Reduced server load  
* Less bandwidth usage

---

# **Cache Miss**

Definition:

A Cache Miss occurs when the requested content is unavailable in the Edge Server.

The Edge Server:

1. Contacts Origin  
2. Downloads file  
3. Stores file locally  
4. Returns file

Future requests become Cache Hits.

---

# **Cache Fill (Cache Population)**

After a Cache Miss:

Origin

↓

Edge Stores Copy

↓

Future Users

↓

Cache Hit

This process is called:

* Cache Fill  
* Cache Population  
* Cache Warming (when done proactively)

---

# **TTL (Time To Live)**

Every cached object has an expiry time.

Example:

logo.png

TTL \= 24 Hours

For the next 24 hours:

Edge Server

↓

Serves Cached Copy

After TTL expires:

Edge

↓

Requests Latest Version

↓

Origin

↓

Updates Cache

TTL ensures stale content is eventually refreshed.

---

# **Cache Invalidation**

Suppose you changed:

logo.png

But TTL is:

30 Days

Users still receive the old image.

Solution:

Invalidate Cache

This removes the cached copy immediately.

Next request:

Origin

↓

Latest Image

↓

Edge Cache Updated

---

# **Cache Purge**

Cache Purge removes cached data manually.

It can be:

Entire CDN

OR

Specific File

Example:

Purge:

logo.png

Only that object is removed.

---

# **Versioning (Best Practice)**

Instead of replacing:

style.css

Use:

style\_v2.css

or

style.css?v=2

Benefits:

* Users automatically receive the latest version.  
* No need to purge cache.  
* Common practice in production deployments.

---

# **Static Content**

Static files rarely change.

Examples:

* Images  
* Videos  
* CSS  
* JavaScript  
* Fonts  
* PDFs  
* ZIP files  
* Audio

These are ideal CDN candidates.

---

# **Dynamic Content**

Dynamic content changes based on the user.

Examples:

* Shopping cart  
* User profile  
* Bank balance  
* Order history  
* OTP  
* Dashboard  
* Payment status

These are generally **not cached** because the response is user-specific.

---

# **Can APIs be cached?**

Yes.

Example:

GET /countries

Everyone receives the same response.

Perfect for caching.

---

Example:

GET /exchange-rates

Can be cached for 1 minute.

---

Example:

GET /my-orders

Cannot be cached because each user has different orders.

---

# **Benefits of CDN**

### **1\. Lower Latency**

Users receive content from nearby servers.

---

### **2\. Faster Website**

Static assets load significantly faster.

---

### **3\. Reduced Origin Load**

Thousands of requests never reach the application server.

---

### **4\. Reduced Bandwidth Cost**

Cached content is served by Edge Servers.

---

### **5\. Better User Experience**

Pages load faster, improving customer satisfaction.

---

### **6\. Higher Availability**

Even if the origin experiences temporary issues, cached content may still be served from Edge Servers.

---

# **CDN Flow (Interview Diagram)**

                User

                   |

             DNS Resolution

                   |

      Nearest CDN Edge Server

                   |

        Is File Available?

          /            \\

        Yes            No

        |               |

 Return Cached      Contact Origin

     File                |

                     Download File

                          |

                    Store in Cache

                          |

                     Return to User

---

# **CDN vs Origin Server**

| Origin Server | CDN Edge Server |
| ----- | ----- |
| Stores original content | Stores cached copies |
| Runs backend application | Serves cached content |
| Handles database requests | No database |
| Can become overloaded | Reduces origin traffic |
| Usually one or a few regions | Hundreds of global locations |

---

# **Popular CDN Providers**

* **Cloudflare**  
* **Amazon CloudFront**  
* **Akamai**  
* **Fastly**  
* **Google Cloud CDN**  
* **Azure CDN**

---

# **AWS CloudFront Architecture**

            Browser

                |

          CloudFront DNS

                |

      Nearest Edge Location

                |

          Cache Hit?

          /       \\

        Yes       No

        |          |

Return Cached   Fetch from S3

    File         EC2 / ALB

                   |

            Store in Cache

                   |

            Return Response

---

# **Real-World Example**

Suppose you upload:

vacation.mp4

It is stored in an S3 bucket (Origin).

### **First User (USA)**

USA User

↓

USA Edge

↓

Cache Miss

↓

S3

↓

Download

↓

Store in USA Edge

↓

Return Video

### **Second User (USA)**

USA User

↓

USA Edge

↓

Cache Hit

↓

Return Immediately

The second request never reaches S3.

---

# **CDN in System Design Interviews**

Whenever designing systems like:

* Netflix  
* YouTube  
* Amazon  
* Instagram  
* Facebook  
* Spotify

Always mention a CDN for:

* Images  
* Videos  
* CSS  
* JavaScript  
* Fonts  
* Static downloads

This reduces latency, minimizes origin server load, lowers bandwidth costs, and improves scalability.

---

# **Interview Questions**

### **What is a CDN?**

A globally distributed network of Edge Servers that caches content close to users, reducing latency and improving performance.

---

### **What is an Edge Server?**

A server near users that stores cached copies of content.

---

### **What is a POP?**

A physical CDN location containing multiple Edge Servers.

---

### **What is a Cache Hit?**

The requested content is available in the Edge Server and is served without contacting the Origin Server.

---

### **What is a Cache Miss?**

The content is unavailable in the Edge Server, so it is fetched from the Origin Server, cached, and then returned.

---

### **What is TTL?**

TTL (Time To Live) is the duration for which cached content remains valid before it expires and must be refreshed from the Origin Server.

---

### **What is Cache Invalidation?**

The process of removing cached content before its TTL expires so that users receive the latest version immediately.

---

### **Why use Versioning instead of Purging?**

Versioning creates a new file name or URL (e.g., `app.css?v=2`), ensuring clients fetch the updated asset without waiting for cache expiry or manually purging caches. This is generally the preferred production approach.

---

# **30-Second Interview Summary**

User Request  
      |  
      v  
DNS resolves to nearest CDN Edge Server  
      |  
      v  
Cache Hit?  
   |          |  
 Yes         No  
   |          |  
Serve      Fetch from Origin  
Cached     Cache at Edge  
Content         |  
   \\\_\_\_\_\_\_\_\_\_\_\_\_/  
         |  
     Faster Response

Origin \= Original content  
Edge Server \= Cached content  
POP \= Physical CDN location  
TTL \= Cache expiry time  
Cache Invalidation \= Remove stale cache  
Versioning \= Preferred way to deploy updated static assets

**CONSISTENCY**

Problem:  
Multiple database replicas may temporarily have different data.

Strong Consistency:  
\- Every read sees the latest write.  
\- Waits for replication.  
\- High latency.  
\- No stale reads.  
\- Used in Banking, Payments, Ticket Booking.

Eventual Consistency:  
\- Reads may return stale data temporarily.  
\- Replicas synchronize over time.  
\- Low latency.  
\- High availability.  
\- Used in Social Media, DNS, CDN metadata, Product Catalogs.

CAP Theorem:  
C \= Consistency  
A \= Availability  
P \= Partition Tolerance

During a partition:  
\- CP → Prefer consistency, may reject requests.  
\- AP → Prefer availability, may return stale data.  
\- Pure CA is not realistic for distributed systems because network partitions are always possible.

PACELC:  
If Partition:  
    Choose Availability or Consistency.  
Else:  
    Choose Latency or Consistency.

Strong Consistency:  
Write → Wait for replicas → Respond.

Eventual Consistency:  
Write → Respond immediately → Replicate asynchronously.

**REST (Representational State Transfer)**

Why REST?  
\- REST provides a standard way for clients and servers to communicate over HTTP.  
\- It exposes resources through URLs and uses HTTP methods to perform operations.  
\- Most public APIs today are REST APIs.

What is a Resource?  
\- A resource is any object or data exposed by the server.  
\- Examples:  
    User  
    Product  
    Order  
    Payment  
    Comment

Resource URLs:  
    /users  
    /products  
    /orders  
    /payments

REST is Resource-Based:  
\- URLs represent resources, not actions.

Good:  
    GET /users/10  
    POST /users  
    PUT /users/10  
    PATCH /users/10  
    DELETE /users/10

Bad:  
    /getUser  
    /createUser  
    /deleteUser

HTTP Methods (Verbs):

GET  
\- Retrieve data.  
\- Does not modify data.  
Example:  
    GET /users/10

POST  
\- Create a new resource.  
Example:  
    POST /users

PUT  
\- Replace the entire resource.  
Example:  
Current:  
{  
  "name":"Rahul",  
  "age":25  
}

PUT:  
{  
  "name":"Rahul",  
  "age":26  
}

Entire object is replaced.

PATCH  
\- Update only specific fields.  
Example:  
{  
  "age":26  
}

Only the age changes.

DELETE  
\- Remove a resource.  
Example:  
    DELETE /users/10

Stateless Nature:  
\- REST is stateless.  
\- The server does not remember previous requests.  
\- Every request must contain all required information (Authentication token, headers, request data, etc.).  
\- Each request is independent.

Example:  
Request 1:  
    GET /profile

Request 2:  
    GET /orders

The server treats Request 2 independently of Request 1\.

Typical REST Architecture:

Client  
   |  
HTTP Request  
   |  
REST API  
   |  
Business Logic  
   |  
Database  
   |  
HTTP Response (JSON)

Data Format:  
\- JSON is the most commonly used response format.  
Example:  
{  
  "id":1,  
  "name":"Rahul"  
}

Advantages:  
\- Simple and easy to understand.  
\- Stateless, making horizontal scaling easier.  
\- Uses standard HTTP protocol.  
\- Widely supported across languages and frameworks.  
\- Easy to cache GET requests.  
\- Excellent for CRUD operations.  
\- Ideal for public APIs.

Disadvantages:  
\- Multiple endpoints may be required.  
\- Can suffer from:  
    \- Over-fetching (receiving more data than needed)  
    \- Under-fetching (making multiple API calls to get all required data)  
\- Less efficient for complex relationships compared to GraphQL.

Common HTTP Status Codes:

200 OK  
\- Request successful.

201 Created  
\- Resource created successfully.

204 No Content  
\- Request successful but no response body.

400 Bad Request  
\- Invalid request from client.

401 Unauthorized  
\- Authentication required or invalid token.

403 Forbidden  
\- User authenticated but lacks permission.

404 Not Found  
\- Resource does not exist.

409 Conflict  
\- Resource conflict (e.g., duplicate entry).

500 Internal Server Error  
\- Server-side error.

When to Use REST:  
\- Public APIs  
\- CRUD applications  
\- E-commerce  
\- Banking APIs  
\- Social media APIs  
\- Mobile and Web applications  
\- Microservices (external communication)

Interview Points:  
\- REST is resource-based.  
\- Uses standard HTTP methods (GET, POST, PUT, PATCH, DELETE).  
\- Stateless: every request is independent.  
\- Typically exchanges data using JSON.  
\- Easy to scale because the server stores no client session.  
\- Best suited for CRUD-based applications.

**GraphQL**

Why was GraphQL introduced?  
\- GraphQL was developed by Facebook to overcome limitations of REST APIs.  
\- It allows clients to request exactly the data they need.  
\- Helps reduce unnecessary network calls and data transfer.  
\- Particularly useful for mobile applications and complex UIs.

Problems with REST:

1\. Over-fetching  
\- The server returns more data than the client needs.  
\- Wastes bandwidth and increases response size.

Example:  
Client needs:  
    Name  
    Followers

REST Response:  
{  
  "id":1,  
  "name":"Rahul",  
  "email":"rahul@gmail.com",  
  "phone":"9999999999",  
  "address":"Hyderabad",  
  "followers":500  
}

The client only needed:  
    Name  
    Followers

2\. Under-fetching  
\- A single API response is not enough.  
\- The client must make multiple API calls to gather all required data.

Example:  
GET /product/10  
GET /seller/5  
GET /reviews/10  
GET /ratings/10

Multiple network requests increase latency.

What is GraphQL?  
\- GraphQL is a query language for APIs.  
\- The client specifies exactly which fields it wants.  
\- The server returns only those fields.  
\- Eliminates over-fetching and significantly reduces under-fetching.

Single Endpoint:  
Unlike REST, GraphQL generally exposes a single endpoint.

Example:  
/graphql

The query determines what data is returned.

How GraphQL Works:

Client  
   |  
POST /graphql  
   |  
GraphQL Server  
   |  
Resolvers  
   |  
Database / Other Services  
   |  
Response

Resolvers:  
\- Resolver functions fetch the requested data.  
\- Every field in a GraphQL query is resolved by a resolver.  
\- Resolvers can retrieve data from:  
    Database  
    REST APIs  
    Microservices  
    External APIs  
    Cache

Types of Operations:

Query  
\- Used to read data.  
\- Similar to HTTP GET in REST.

Example:  
query{  
    user(id:1){  
        name  
        email  
    }  
}

Mutation  
\- Used to create, update or delete data.  
\- Similar to POST, PUT, PATCH and DELETE in REST.

Example:  
mutation{  
    createUser(name:"Rahul"){  
        id  
        name  
    }  
}

Subscription  
\- Used for real-time updates.  
\- Maintains a persistent connection.  
\- Server pushes updates automatically.

Common use cases:  
    Chat applications  
    Live notifications  
    Stock prices  
    Sports scores  
    Live dashboards

Advantages:  
\- No over-fetching.  
\- Minimal under-fetching.  
\- Client controls response structure.  
\- Single endpoint.  
\- Reduces network requests.  
\- Excellent for mobile applications.  
\- Ideal when data comes from multiple services.

Disadvantages:  
\- More complex than REST.  
\- Difficult to cache.  
\- Expensive queries can affect performance.  
\- Requires query validation and complexity limits.  
\- More difficult to monitor and debug.

REST vs GraphQL

REST  
\- Multiple endpoints.  
\- Server decides response.  
\- Over-fetching possible.  
\- Under-fetching possible.  
\- Easier to cache.  
\- Simpler implementation.

GraphQL  
\- Single endpoint.  
\- Client decides response.  
\- No over-fetching.  
\- Greatly reduces under-fetching.  
\- Complex caching.  
\- More flexible but more complex.

When to Use GraphQL:  
\- Social media applications.  
\- Mobile applications.  
\- Dashboards.  
\- Analytics platforms.  
\- Applications needing data from multiple resources.  
\- Frontends requiring different response shapes.

When NOT to Use GraphQL:  
\- Simple CRUD applications.  
\- Small APIs.  
\- Public APIs where REST is sufficient.  
\- Simple microservices with straightforward endpoints.

Interview Points:  
\- GraphQL is a query language for APIs.  
\- Client controls the response shape.  
\- Uses a single endpoint (/graphql).  
\- Solves over-fetching.  
\- Greatly reduces under-fetching.  
\- Uses Resolvers to fetch data.  
\- Query \= Read.  
\- Mutation \= Create/Update/Delete.  
\- Subscription \= Real-time server push.

**gRPC (Google Remote Procedure Call)**

Why was gRPC introduced?  
\- Google developed gRPC for efficient communication between microservices.  
\- REST APIs were simple but became inefficient for large-scale internal communication.  
\- gRPC provides faster, smaller and strongly-typed communication.

Problem with REST in Microservices:  
\- Microservices communicate thousands or millions of times per second.  
\- REST uses JSON, which is text-based.  
\- JSON payloads are larger.  
\- Parsing JSON consumes more CPU.  
\- HTTP/1.1 introduces additional overhead.

Google wanted:  
\- Faster communication  
\- Smaller payloads  
\- Lower latency  
\- Less CPU usage  
\- Streaming support  
\- Strong contracts between services

What is RPC?  
RPC stands for Remote Procedure Call.

\- A function running on another machine can be called as if it were a local function.  
\- Developers call methods instead of manually creating HTTP requests.

Example:

Normal Function:  
add(5,3)

RPC:  
GetUser(10)

Although GetUser() executes on another server, it appears like a local function call.

What is gRPC?  
\- gRPC is Google's implementation of Remote Procedure Call.  
\- It automatically handles:  
    Network communication  
    Serialization  
    Deserialization  
    Connection management  
\- Developers simply call methods.

REST vs gRPC Communication

REST

Order Service  
      |  
HTTP Request  
      |  
JSON  
      |  
User Service

gRPC

Order Service  
      |  
GetUser(10)  
      |  
Protocol Buffers  
      |  
User Service

Protocol Buffers (Protobuf)

What is Protobuf?  
\- Protocol Buffers are Google's binary serialization format.  
\- They define the structure of messages exchanged between client and server.  
\- Data is converted into compact binary format before transmission.

Advantages:  
\- Smaller payload  
\- Faster serialization  
\- Faster deserialization  
\- Lower bandwidth usage  
\- Lower CPU usage

.proto File  
\- Defines the contract between client and server.  
\- Specifies:  
    Services  
    Methods  
    Request messages  
    Response messages

Example:

service UserService{  
    rpc GetUser(UserRequest)  
        returns(UserResponse);  
}

Both client and server generate code automatically from the .proto file.

Strong Contract  
\- Client and server agree on the message format before communication.  
\- Data types are validated during code generation.  
\- Reduces runtime errors.

Example:

REST:  
{  
   "id":"10"  
}

Is id a String or Integer?  
Cannot know until runtime.

gRPC:

int32 id

Type is fixed and validated.

HTTP/2

gRPC uses HTTP/2 by default.

Advantages:

1\. Multiplexing  
\- Multiple requests share the same TCP connection.  
\- Requests and responses can be processed simultaneously.

2\. Persistent Connection  
\- One connection is reused for many requests.  
\- No need to repeatedly establish new connections.

3\. Header Compression  
\- Repeated HTTP headers are compressed.  
\- Reduces network bandwidth.

How gRPC Works

Client  
   |  
Generated Client Stub  
   |  
Protocol Buffers  
   |  
HTTP/2  
   |  
Generated Server Stub  
   |  
Business Logic  
   |  
Database

Client and server code is automatically generated from the .proto file.

Types of gRPC Calls

1\. Unary RPC  
\- One request  
\- One response  
\- Similar to REST request-response.

Example:  
GetUser()

2\. Server Streaming  
\- One request  
\- Multiple responses

Use Cases:  
\- Video streaming  
\- Log streaming  
\- News feed

3\. Client Streaming  
\- Multiple requests  
\- One response

Use Cases:  
\- File upload  
\- Audio upload  
\- Sensor data upload

4\. Bidirectional Streaming  
\- Multiple requests  
\- Multiple responses simultaneously

Use Cases:  
\- Chat applications  
\- Online gaming  
\- Live collaboration  
\- IoT devices

Advantages  
\- Very fast.  
\- Binary communication.  
\- Small payload size.  
\- Strongly typed.  
\- Efficient code generation.  
\- Supports streaming.  
\- Excellent for microservices.  
\- Lower CPU and bandwidth usage.

Disadvantages  
\- Difficult to debug manually.  
\- Binary data is not human-readable.  
\- Browser support is limited.  
\- Learning curve is higher.  
\- Requires .proto files.

REST vs gRPC

REST  
\- JSON  
\- Human-readable  
\- HTTP/1.1 (commonly)  
\- Easy to debug  
\- Public APIs  
\- No built-in streaming  
\- Slower

gRPC  
\- Protocol Buffers  
\- Binary format  
\- HTTP/2  
\- Faster  
\- Internal microservices  
\- Built-in streaming  
\- Strong contracts

When to Use gRPC  
\- Internal microservices  
\- High-performance backend systems  
\- Distributed systems  
\- Real-time streaming  
\- Low-latency applications  
\- High request throughput

When NOT to Use gRPC  
\- Public APIs  
\- Browser-based applications  
\- Simple CRUD APIs  
\- Small projects where REST is sufficient

Interview Points  
\- gRPC \= Google Remote Procedure Call.  
\- Used mainly for service-to-service communication.  
\- Uses Protocol Buffers instead of JSON.  
\- Uses HTTP/2 by default.  
\- Faster due to binary serialization and HTTP/2 features.  
\- Uses .proto files to define contracts.  
\- Supports Unary, Server Streaming, Client Streaming and Bidirectional Streaming.

**WebSockets**

Why were WebSockets introduced?  
\- HTTP follows a request-response model.  
\- The server cannot send data unless the client first sends a request.  
\- Real-time applications require instant communication.  
\- WebSockets provide a persistent, two-way communication channel between client and server.

Problem with HTTP:  
\- Every request opens a connection.  
\- Server sends a response.  
\- Connection closes.  
\- For new data, the client must send another request.  
\- Inefficient for real-time applications.

Example:

Client  
   |  
GET /messages  
   |  
Server  
   |  
Response  
   |  
Connection Closed

This repeats for every request.

Real-Time Problem:  
Suppose Rahul sends a chat message.

With HTTP:  
\- The receiver does not automatically receive the message.  
\- The client must repeatedly ask:

"Any new message?"  
"No."

"Any new message?"  
"No."

"Any new message?"  
"Yes."

This wastes:  
\- CPU  
\- Network bandwidth  
\- Battery  
\- Server resources

What is WebSocket?  
\- WebSocket is a communication protocol that provides a persistent connection between client and server.  
\- After the connection is established, both client and server can send messages at any time.  
\- No need to repeatedly open new HTTP connections.

Persistent Connection:

Client \====================== Server

The connection remains open until either side closes it.

WebSocket Handshake

A WebSocket connection begins as an HTTP request.

Client:

GET /chat  
Upgrade: websocket

Server:

101 Switching Protocols

After the handshake:  
\- HTTP communication stops.  
\- WebSocket communication begins.

This process is called the WebSocket Handshake.

Full-Duplex Communication

What is Duplex?  
\- Data can travel in both directions.

What is Full-Duplex?  
\- Client and server can send messages simultaneously.  
\- Neither side has to wait for the other.

Example:

Client  ⇄  Server

Both can send and receive messages at the same time.

This makes WebSockets ideal for chat and live applications.

WebSocket Lifecycle

1\. Connect  
\- Client sends HTTP Upgrade request.

2\. Open  
\- Server accepts the request.  
\- Persistent WebSocket connection is established.

3\. Message Exchange  
\- Client and server exchange unlimited messages.

4\. Close  
\- Either side closes the connection.

Architecture

Client  
   |  
HTTP Upgrade Request  
   |  
WebSocket Server  
   |  
Persistent Connection  
   |  
Application Logic  
   |  
Database

How WebSockets Scale

Single Server:

Client1  
Client2  
Client3  
     |  
WebSocket Server

Large Scale:

               Load Balancer  
                      |  
        \----------------------------  
        |            |            |  
      WS-1         WS-2         WS-3  
        |            |            |

If users are connected to different WebSocket servers, a message broker is used.

Example:

User A  
   |  
WS-1  
   |  
Redis Pub/Sub / Kafka  
   |  
WS-3  
   |  
User B

The broker forwards messages between WebSocket servers.

Common Use Cases  
\- Chat applications  
\- Live notifications  
\- Online gaming  
\- Stock market updates  
\- Live sports scores  
\- Ride tracking (Uber, Ola)  
\- Food delivery tracking (Swiggy, Zomato)  
\- Collaborative editing (Google Docs)  
\- Trading applications

Advantages  
\- Real-time communication.  
\- Very low latency.  
\- Full-duplex communication.  
\- Persistent connection.  
\- Reduces repeated HTTP requests.  
\- Efficient for frequent updates.

Disadvantages  
\- Harder to scale than REST.  
\- Open connections consume server memory.  
\- Load balancing is more complex.  
\- Reconnection handling is required.  
\- Heartbeat/Ping-Pong mechanism needed to detect dead connections.

Heartbeat (Ping-Pong)

Problem:  
A client may disconnect unexpectedly (network failure, laptop sleep, Wi-Fi loss).

Solution:  
Server periodically sends a Ping frame.

Client replies with a Pong frame.

If no Pong is received within a timeout:  
\- Server assumes the client disconnected.  
\- Connection is closed and resources are released.

REST vs WebSocket

REST  
\- Request-Response  
\- Stateless  
\- Connection closes after every request  
\- Client always initiates communication  
\- Best for CRUD operations

WebSocket  
\- Persistent connection  
\- Stateful connection  
\- Connection remains open  
\- Both client and server can initiate communication  
\- Best for real-time communication

When to Use WebSockets  
\- Chat applications  
\- Multiplayer games  
\- Live dashboards  
\- Live notifications  
\- Collaborative applications  
\- IoT devices  
\- Financial trading systems

When NOT to Use WebSockets  
\- Simple CRUD applications  
\- Public REST APIs  
\- Applications with infrequent communication  
\- Static websites

Interview Points  
\- WebSocket is a communication protocol.  
\- Starts with an HTTP Upgrade handshake.  
\- Uses one persistent connection.  
\- Supports full-duplex communication.  
\- Server can push data without waiting for a client request.  
\- Ideal for real-time applications.  
\- Large systems use multiple WebSocket servers with Redis Pub/Sub or Kafka for message routing.

**Long Polling**

What is Long Polling?  
\- Long Polling is an HTTP-based communication technique.  
\- It is NOT a separate protocol.  
\- The client sends an HTTP request.  
\- If no new data is available, the server keeps the request open.  
\- The server responds only when:  
    \- New data becomes available, or  
    \- A timeout occurs.  
\- After receiving the response, the client immediately sends another request.

Why was Long Polling introduced?  
\- HTTP follows a request-response model.  
\- Servers cannot push data to clients using normal HTTP.  
\- Constant polling wastes network and server resources.  
\- Long Polling reduces unnecessary requests by keeping the request open.

Problem with Normal Polling

Polling:  
\- Client repeatedly asks the server for updates at fixed intervals.

Example:

Every 2 seconds:

Client  
   |  
Any new message?  
   |  
Server  
   |  
No

Client  
   |  
Any new message?  
   |  
Server  
   |  
No

Client  
   |  
Any new message?  
   |  
Server  
   |  
Yes

Problems:  
\- Many unnecessary requests.  
\- Most responses are "No new data."  
\- Wastes CPU, bandwidth and battery.  
\- Higher server load.

How Long Polling Works

Step 1:  
Client sends a request.

Step 2:  
Server checks for new data.

Step 3:  
If no data is available:  
\- Server keeps the request open.  
\- Does NOT immediately respond.

Step 4:  
When new data arrives:  
\- Server immediately sends the response.

Step 5:  
Connection closes.

Step 6:  
Client immediately creates another Long Poll request.

Architecture

Client  
   |  
HTTP Request  
   |  
Server  
   |  
Wait...  
   |  
New Data?  
   |  
Yes  
   |  
Response  
   |  
Connection Closed  
   |  
Client Sends Next Request

Timeout

If no new data arrives within a predefined timeout:

Server  
   |  
Timeout Response  
   |  
Connection Closed

Client immediately starts another Long Poll request.

Long Polling Lifecycle

1\. Client sends request.  
2\. Server waits.  
3\. Data arrives OR timeout occurs.  
4\. Server responds.  
5\. Connection closes.  
6\. Client sends another request.

Advantages  
\- Works over standard HTTP.  
\- Easy browser support.  
\- Fewer unnecessary requests than polling.  
\- Easier to implement than WebSockets.  
\- Better user experience than traditional polling.

Disadvantages  
\- Still creates many HTTP requests.  
\- Higher latency than WebSockets.  
\- More server resources than REST.  
\- Scaling becomes difficult for many concurrent clients.  
\- Not true real-time communication.

Polling vs Long Polling

Polling  
\- Server immediately responds.  
\- Client repeatedly sends requests.  
\- Many unnecessary requests.  
\- Higher latency.

Long Polling  
\- Server waits before responding.  
\- Fewer unnecessary requests.  
\- Better responsiveness.  
\- Lower latency than polling.

Long Polling vs WebSocket

Long Polling  
\- HTTP-based technique.  
\- Request waits until data or timeout.  
\- Connection closes after every response.  
\- Client sends another request.  
\- Near real-time.

WebSocket  
\- Separate communication protocol.  
\- One persistent connection.  
\- Connection remains open.  
\- Client and server communicate anytime.  
\- True real-time.

When to Use Long Polling  
\- Legacy applications.  
\- Browsers or environments where WebSockets are unavailable.  
\- Firewalls or proxies blocking WebSockets.  
\- Applications with infrequent real-time updates.

When NOT to Use Long Polling  
\- Chat applications with heavy traffic.  
\- Online gaming.  
\- Stock trading.  
\- Live dashboards.  
\- Applications requiring continuous bidirectional communication.

Interview Points  
\- Long Polling is NOT a protocol.  
\- It is an HTTP communication technique.  
\- Server keeps the request open until data arrives or timeout occurs.  
\- Client immediately creates another request after every response.  
\- Better than Polling but less efficient than WebSockets.

| Technology | Remember It As |
| ----- | ----- |
| **REST** | "Give me this resource." |
| **GraphQL** | "Give me exactly these fields." |
| **gRPC** | "Call this remote function." |
| **WebSockets** | "Let's stay connected and talk anytime." |
| **Long Polling** | "I'll wait here until you have something for me." |

| Feature | REST | GraphQL | gRPC | WebSockets | Long Polling |
| ----- | ----- | ----- | ----- | ----- | ----- |
| **What is it?** | API Architecture | Query Language for APIs | Remote Procedure Call (RPC) Framework | Communication Protocol | HTTP Communication Technique |
| **Main Purpose** | CRUD operations | Fetch exactly the required data | Fast service-to-service communication | Real-time two-way communication | Near real-time updates over HTTP |
| **Communication Style** | Request → Response | Request → Response | Function Call (RPC) | Persistent Connection | Request waits → Response |
| **Protocol Used** | HTTP | HTTP | HTTP/2 | WebSocket Protocol | HTTP |
| **Data Format** | JSON | JSON | Protocol Buffers (Binary) | Text/Binary Frames | JSON/XML/Text |
| **Connection** | Opens and closes for every request | Opens and closes for every request | Persistent HTTP/2 connection | One long-lived persistent connection | Connection stays open until data/timeout, then closes |
| **Who Starts Communication?** | Client | Client | Client | Both Client & Server | Client |
| **Can Server Push Data?** | ❌ No | ❌ No (except Subscriptions) | ✅ Yes (Streaming) | ✅ Yes | ✅ Yes (only after client request is waiting) |
| **Real-Time Support** | ❌ No | ❌ No | ✅ Yes (Streaming) | ✅ Excellent | ✅ Moderate |
| **Streaming Support** | ❌ No | Subscription only | ✅ Built-in | ✅ Continuous | ❌ No |
| **Latency** | Medium | Medium | Low | Very Low | Medium |
| **Performance** | Good | Good | Excellent | Excellent | Better than Polling |
| **Human Readable?** | ✅ Yes | ✅ Yes | ❌ No | Usually Yes | ✅ Yes |
| **Strong Contract?** | ❌ No | Schema | ✅ `.proto` file | ❌ No | ❌ No |
| **Caching Support** | ✅ Excellent | ⚠️ More Complex | ❌ Rare | ❌ No | ❌ No |
| **State** | Stateless | Stateless | Stateless | Stateful (connection maintained) | Stateless (each request is independent) |
| **Scalability** | Easy | Easy | Easy | Harder (persistent connections) | Moderate |
| **Learning Curve** | Easy | Medium | Medium–High | Medium | Easy |
| **Best For** | Public APIs, CRUD | Mobile apps, Dashboards | Internal Microservices | Chat, Gaming, Live Tracking | Legacy real-time systems |

**Rate Limiting**

What is Rate Limiting?  
\- Rate Limiting is a technique used to control the number of requests a client can make within a specified time period.  
\- It protects servers from overload, abuse, and malicious attacks.  
\- If a client exceeds the allowed limit, the server rejects additional requests.

Example:  
Limit \= 100 Requests / Minute

Requests 1–100 → Allowed  
Request 101 → Rejected (HTTP 429 Too Many Requests)

Definition  
\- Controls how many requests are allowed within a fixed time interval.  
\- Helps maintain system stability and fairness among users.

Why was Rate Limiting introduced?  
Without Rate Limiting:  
\- A single user can overload the server.  
\- Malicious users can launch brute-force attacks.  
\- APIs become vulnerable to abuse.  
\- Infrastructure costs increase.  
\- Legitimate users experience slower responses.

Rate Limiting solves these problems by restricting excessive requests.

Problems Solved by Rate Limiting

1\. Prevents Server Overload  
\- Protects CPU, Memory and Database resources.  
\- Prevents traffic spikes from crashing the system.

2\. Prevents Brute Force Attacks  
Example:  
POST /login

Without limits:  
An attacker can try millions of passwords.

With Rate Limiting:  
Only 5 login attempts per minute.

3\. Prevents API Abuse  
Example:  
Search API

Without limits:  
Bots can scrape the entire website.

With limits:  
100 requests per minute.

4\. Controls Infrastructure Cost  
Example:  
AI APIs  
SMS APIs  
Email APIs

Each request has a cost.

Rate Limiting prevents excessive usage.

5\. Fair Resource Sharing  
Ensures one user cannot consume all server resources.  
Every client receives a fair share of system capacity.

Real-World Examples

Login API  
\- 5 Login Attempts / Minute

OTP API  
\- 3 OTP Requests / Hour

Payment API  
\- 10 Payment Requests / Minute

Search API  
\- 100 Searches / Minute

ChatGPT API  
\- Requests per Minute (RPM)  
\- Tokens per Minute (TPM)

File Upload API  
\- Upload limits per hour/day

Where is Rate Limiting Implemented?

Typical Architecture

           Client  
              |  
        Load Balancer  
              |  
        Rate Limiter  
              |  
        API Gateway  
              |  
       Backend Services  
              |  
          Database

Why before the Backend?  
\- Reject unwanted requests early.  
\- Save CPU cycles.  
\- Reduce database load.  
\- Reduce network traffic.  
\- Improve system performance.

How Rate Limiting Works

Step 1:  
Client sends a request.

Step 2:  
Rate Limiter identifies the client.

Step 3:  
Checks current request count.

Step 4:  
If within limit:  
\- Forward request to backend.

Step 5:  
If limit exceeded:  
\- Reject request.  
\- Return HTTP 429 Too Many Requests.

Example

Limit \= 5 Requests / Minute

Request 1 → Allowed  
Request 2 → Allowed  
Request 3 → Allowed  
Request 4 → Allowed  
Request 5 → Allowed  
Request 6 → HTTP 429 Too Many Requests

How Does the Server Identify Users?

Rate Limiting can be applied using:

1\. IP Address  
Example:  
192.168.x.x

Useful for anonymous users.

2\. User ID  
Example:  
User \= Rahul

Common after login.

3\. API Key  
Used for public APIs.

Each API Key has its own request quota.

4\. JWT / Access Token  
Common in authenticated applications.

5\. Device ID  
Common in mobile applications.

HTTP Response When Limit Exceeds

Status Code:  
429 Too Many Requests

Optional Header:  
Retry-After: 60

Meaning:  
Client should retry after 60 seconds.

Distributed Rate Limiting

Problem

Multiple Servers

        Load Balancer  
        /     |     \\  
   Server1 Server2 Server3

Each server maintains its own counter.

Example:

Limit \= 5 Requests

User sends:  
5 requests → Server1  
5 requests → Server2  
5 requests → Server3

Total \= 15 Requests

Incorrect because the limit should have been 5\.

Solution

Use a shared datastore.

Common Choice:  
Redis

Architecture

            Load Balancer  
          /      |      \\  
     Server1  Server2  Server3  
          \\      |      /  
              Redis  
        (Shared Counter)

Every server checks the same request count.

Benefits of Redis  
\- Extremely fast.  
\- In-memory storage.  
\- Supports atomic operations.  
\- Supports key expiration (TTL).  
\- Perfect for request counters.

What Should Be Stored?

Example:

Key:  
user123

Value:  
Current Request Count

Example:

user123 → 4 Requests

TTL:  
60 Seconds

After TTL expires:  
Counter resets automatically.

Common Rate Limiting Algorithms

1\. Fixed Window Counter  
2\. Sliding Window Log  
3\. Sliding Window Counter  
4\. Token Bucket  
5\. Leaky Bucket

(Algorithms determine HOW request counts are maintained.)

Advantages  
\- Protects servers.  
\- Prevents abuse.  
\- Prevents brute-force attacks.  
\- Ensures fairness.  
\- Improves availability.  
\- Controls infrastructure cost.  
\- Prevents sudden traffic spikes.

Disadvantages  
\- Legitimate users may occasionally be throttled.  
\- Choosing the wrong algorithm can cause unfair limits.  
\- Distributed implementation is more complex.  
\- Requires additional infrastructure (Redis).

Common Use Cases  
\- Login APIs  
\- OTP Services  
\- Payment Systems  
\- AI APIs  
\- Public APIs  
\- Search APIs  
\- File Upload APIs  
\- Social Media APIs  
\- Email Services

Interview Points  
\- Rate Limiting controls request frequency.  
\- Common response code: HTTP 429 Too Many Requests.  
\- Redis is commonly used for distributed rate limiting.  
\- Rate Limiting is usually implemented before backend services.  
\- Rate Limiting protects servers from overload and abuse.  
\- Algorithms define how request limits are tracked.

\=========================================================  
RATE LIMITING ALGORITHMS  
\=========================================================

1\. Fixed Window Counter  
\-----------------------

Idea:  
\- Count requests in a fixed time interval.  
\- Counter resets when the interval ends.

Example:  
Limit \= 5 Requests / Minute

12:00 \- 12:01  
5 Requests → Allowed  
6th Request → HTTP 429

12:01 \- 12:02  
Counter resets to 0\.

Advantages:  
✓ Simple  
✓ Fast  
✓ Low memory usage

Disadvantages:  
✗ Boundary Burst Problem  
(User can send requests at the end of one window and beginning of the next.)

Best Use Cases:  
\- Basic APIs  
\- Internal services  
\- Simple applications

\=========================================================

2\. Sliding Window Log  
\---------------------

Idea:  
\- Store the timestamp of every request.  
\- Count requests in the last N seconds.

Example:

Current Time \= 12:01:00

Check requests between:  
12:00:00 → 12:01:00

Advantages:  
✓ Very accurate  
✓ Solves Boundary Burst Problem

Disadvantages:  
✗ High memory usage  
(Stores every request timestamp.)

Data Structure:  
Queue / Deque (FIFO)

Best Use Cases:  
\- Authentication APIs  
\- Payment APIs  
\- Security-sensitive systems

\=========================================================

3\. Sliding Window Counter  
\-------------------------

Idea:  
\- Optimized version of Sliding Window Log.  
\- Stores only:  
  • Previous window count  
  • Current window count  
\- Uses an estimate instead of exact timestamps.

Advantages:  
✓ Low memory usage  
✓ Better scalability  
✓ Nearly as accurate as Sliding Window Log

Disadvantages:  
✗ Approximate (not 100% accurate)

Best Use Cases:  
\- Large-scale distributed systems  
\- APIs with millions of users

\=========================================================

4\. Token Bucket  
\---------------

Idea:  
\- Bucket contains tokens.  
\- Each request consumes one token.  
\- Tokens refill at a fixed rate.  
\- No token → Reject request.

Example:

Bucket Capacity \= 5 Tokens

🪙🪙🪙🪙🪙

Request →  
Use one token.

After 5 requests →  
Bucket empty →  
HTTP 429

Tokens refill automatically over time.

Advantages:  
✓ Allows short traffic bursts  
✓ Low memory usage  
✓ Widely used in production

Disadvantages:  
✗ Burst traffic is still allowed.

Best Use Cases:  
\- Public APIs  
\- AI APIs  
\- Cloud services  
\- API Gateways

\=========================================================

5\. Leaky Bucket  
\---------------

Idea:  
\- Incoming requests are stored in a queue.  
\- Requests leave the queue at a fixed rate.  
\- If the queue is full, new requests are rejected.

Example:

100 Requests  
      ↓  
 Queue  
      ↓  
Process 10 Requests / Second

Advantages:  
✓ Smooth traffic  
✓ Prevents sudden spikes  
✓ Stable server load

Disadvantages:  
✗ Does not allow bursts  
✗ Requests may wait in the queue

Best Use Cases:  
\- Payment systems  
\- Database writes  
\- Messaging systems  
\- Background job processing

\=========================================================  
