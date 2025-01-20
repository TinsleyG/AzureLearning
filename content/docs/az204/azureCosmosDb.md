---
title: Azure CosmosDB
type: docs
weight: 6
prev: docs/az204/blobStorage
next: docs/az204/apiManagement
---

### Azure AZ-204 Exam: Overview of Cosmos DB  

Azure Cosmos DB is a globally distributed, NoSQL database platform designed for low-latency performance, scalability, and high availability. While Cosmos DB has its own dedicated certification (DP-420), the AZ-204 exam expects candidates to have a foundational understanding of its core concepts. Here's a detailed breakdown of what you need to know for the exam:  

---

#### **Core Features of Cosmos DB**  
1. **Global Distribution**:  
   - Enables worldwide data distribution, improving disaster recovery and user experience.  
   - Benefits include redundant backups for resilience and reduced latency for users closer to the data source.  

2. **Multi-Modal Capabilities**:  
   - Supports various NoSQL APIs, including JSON, key-value, wide-column, and graph databases.  
   - Offers flexibility for diverse workloads and use cases.  

3. **Performance Guarantees**:  
   - Single-digit millisecond response times for reads and writes.  
   - 99.999% uptime backed by a service-level agreement (SLA), ensuring reliability.  

4. **Scalability**:  
   - Automatically scales based on demand, supporting high-throughput workloads without manual intervention.  
   - Multi-master distribution allows seamless failover and consistent write operations across multiple regions.  

---

#### **Pricing and Throughput**  
Cosmos DB pricing is based on **compute** and **storage**, billed hourly.  
- **Request Units (RUs)**:  
  - RUs measure throughput by combining CPU, IOPS, and memory.  
  - Throughput is expressed as RU/s (Request Units per second).  
  - Common configurations:  
    1. **Provisioned Manual**: For predictable workloads.  
    2. **Provisioned Autoscale**: Automatically adjusts throughput for variable workloads.  
    3. **Serverless**: Ideal for unpredictable or low-volume workloads.  

---

#### **Consistency Levels**  
Cosmos DB offers five consistency levels to balance data accuracy, latency, and performance:  
1. **Strong Consistency**:  
   - Guarantees the most recent data across all regions.  
   - Ideal for applications requiring linear data consistency.  

2. **Bounded Staleness**:  
   - Ensures ordered data reads within a defined lag (time or version).  
   - Suitable for globally distributed applications balancing performance and consistency.  

3. **Session Consistency** (default for most apps):  
   - Guarantees read-your-own-writes within a session.  
   - Best for scenarios requiring immediate local consistency.  

4. **Consistent Prefix**:  
   - Ensures reads follow the order of writes without defining a staleness threshold.  
   - Optimized for performance with minimal latency.  

5. **Eventual Consistency**:  
   - Provides no guarantees on order or timing but ensures eventual synchronization.  
   - Ideal for low-latency, high-throughput applications (e.g., social media).  

Consistency can be adjusted at the account level and weakened for specific requests via the SDK.  

---

#### **Free Tier**  
Azure Cosmos DB offers a limited free tier to test its features, including importing smaller legacy data stores. While the free tier is restricted in capacity, it provides an opportunity to evaluate its potential before committing to higher tiers.  

---

#### **Key Takeaways**  
- Azure Cosmos DB is a highly scalable, globally distributed NoSQL database.  
- Key topics include global distribution, throughput measured in RUs, and five consistency levels.  
- Understanding how to balance cost, consistency, and performance is crucial for enterprise applications.  
- Familiarity with provisioning throughput and consistency levels will help optimize solutions effectively for the AZ-204 exam.  

Here’s the polished version of your Cosmos DB-focused session:

---


**Welcome to the Cosmos DB Data Management Session!**  
In this segment, we’ll cover essential aspects of Cosmos DB data management to help you grasp its core concepts and prepare for real-world use or certifications.  

### **What We’ll Cover**  
1. **Cosmos DB APIs and Use Cases**  
   - Overview of supported APIs and their applications.
2. **Partition Design**  
   - Understanding logical and physical partitions and their significance.
3. **Cosmos DB C# SDK Basics**  
   - Common conventions and coding patterns.
4. **Server-Side Objects**  
   - User-defined functions (UDFs), triggers, and stored procedures in JavaScript.
5. **The Cosmos DB Change Feed**  
   - How it works and its practical applications.

---

### **Cosmos DB APIs**  
Cosmos DB supports multiple data models through APIs:  
- **NoSQL API (Core API)**: Native to Cosmos DB and ideal for JSON-based data.  
- **MongoDB API**: Uses BSON documents for MongoDB compatibility.  
- **Cassandra API**: Designed for wide-column database scenarios.  
- **Table API**: Simplifies migration from Azure Table Storage.  
- **Gremlin API**: Handles graph data with nodes and edges.  
- **PostgreSQL API**: Supports distributed PostgreSQL-based workloads.  

💡 **Tip**: Use the Core API unless you need compatibility with existing systems or open-source ecosystems.

---

### **Partition Design in Cosmos DB**  
- **Account Level**: Set API, enable global distribution, and define consistency levels.  
- **Database Level**: Manage security and optional throughput settings.  
- **Container Level**: Use partition keys to logically group data (e.g., by customer ID, product ID).  
- **Logical vs. Physical Partitions**: Logical partitions map to physical partitions, which are implemented as replica sets for scalability.  

---

### **Coding in Cosmos DB with C# SDK**  
The three key classes are:  
1. **CosmosClient**: Connects to your Cosmos account.  
2. **Database**: Manages databases and permissions.  
3. **Container**: Performs CRUD operations on data.  

Examples:  
- **Connecting**: Use a connection string or separate endpoint and key.  
- **CRUD Operations**: Use `CreateItemAsync`, `ReadItemAsync`, `UpsertItemAsync`, and `DeleteItemAsync`.  

🔑 **Conventions**:  
- Each item should include an `ID` and a partition key.  
- Use `Options` classes to configure properties like consistency levels.

---

### **Server-Side Objects in Cosmos DB**  
1. **User-Defined Functions (UDFs)**: Custom JavaScript functions for lightweight operations.  
2. **Stored Procedures**: Handle transactions with ACID guarantees.  
3. **Triggers**: Pre-triggers validate data, and post-triggers modify or log changes.

---

### **The Cosmos DB Change Feed**  
The change feed captures inserts and updates but not deletions. Key components include:  
- **Monitored Container**: Source data for the feed.  
- **Lease Container**: Tracks feed state and coordinates processing.  
- **Compute Instance**: Hosts the change feed processor.  
- **Delegate**: Custom logic for processing data.  

**Use Cases**:  
- Event-driven applications (e.g., retail, gaming).  
- Stream processing with tools like Azure Stream Analytics.  
- ETL workflows with Azure Blob Storage or Data Lake.  

---

### **Review**  
We’ve covered:  
1. Cosmos DB infrastructure, including APIs, partitions, and the NoSQL hierarchy.  
2. Coding patterns for CRUD operations using the C# SDK.  
3. Server-side objects for advanced use cases.  
4. The change feed and its implementation for event-driven and ETL scenarios.  

Sure! Here's a summary:

### **Partition Key in Cosmos DB (CustomerID Example)**

- The **partition key** determines how data is logically grouped and physically distributed in Cosmos DB. 
- Using `CustomerID` as the partition key in a **Transactions container** groups all transactions for a specific customer into the same logical partition.

---

### **Key Benefits:**
1. **Efficient Queries**  
   - Fetching all transactions for a customer targets a single partition, improving query performance.
   - Example:  
     ```sql
     SELECT * FROM Transactions WHERE CustomerID = 'C001'
     ```

2. **Data Locality**  
   - Data for each customer is stored together, minimizing cross-partition operations.

3. **Scalability**  
   - Spreads data across partitions for many customers, avoiding performance bottlenecks.

4. **Atomic Transactions**  
   - Batch operations are possible within a single partition (e.g., adding or updating multiple transactions for the same customer).

---

### **Use Case Example:**
- **Customer Container**: Partition Key = `CustomerID`
- **Transactions Container**: Partition Key = `CustomerID`

| **CustomerID** | **TransactionID** | **Amount** | **Date**       |
|----------------|--------------------|------------|----------------|
| C001           | T001               | 150.75     | 2025-01-01     |
| C001           | T002               | 75.50      | 2025-01-05     |
| C002           | T003               | 300.00     | 2025-01-02     |

---

### **When It’s Ideal**
- Querying or processing data for a single customer (e.g., `CustomerID = C001`).
- Performing transactional updates for a customer's data.
- 
Visualization
Customers Container
Partition Key (CustomerID)	Data
C001	{ "CustomerID": "C001", "Name": "John Doe", "Email": "john.doe@example.com" }
C002	{ "CustomerID": "C002", "Name": "Jane Smith", "Email": "jane.smith@example.com" }
Transactions Container
Partition Key (CustomerID)	Data
C001	{ "TransactionID": "T1001", "CustomerID": "C001", "Amount": 150.75 }, { "TransactionID": "T1002", "CustomerID": "C001", "Amount": 75.50 }
C002	{ "TransactionID": "T2001", "CustomerID": "C002", "Amount": 300.00 }