---
title: Azure CosmosDB
type: docs
prev: docs/az204/
---

### Overview of Azure Cosmos DB
Azure Cosmos DB is a globally distributed, multi-model database service by Microsoft, designed to handle large-scale applications with low-latency and high-availability requirements. It’s known for providing flexible data modeling options, high throughput, and consistency controls, making it suitable for mission-critical workloads.

### Key Features
1. **Global Distribution**: Cosmos DB allows you to distribute data globally across Azure regions, automatically replicating your data for fast, low-latency access and higher availability. For the AZ-204 exam, understand how to configure replication and data residency.

2. **Multi-Model Support**: Cosmos DB supports various data models, including:
   - **Document (NoSQL)**: Used with JSON objects, commonly accessed with the Core (SQL) API.
   - **Key-Value**: Supported by the Table API, similar to Azure Table Storage.
   - **Graph**: Used with the Gremlin API, for graph-based data.
   - **Column-Family**: Supported by the Cassandra API for column-based storage.
   - **Wide-Column**: Allows for a flexible schema on a per-entity basis.

3. **APIs**: Cosmos DB is accessed via different APIs:
   - **Core (SQL) API**: Most common, for querying JSON data with SQL-like syntax.
   - **MongoDB API**: Allows MongoDB applications to work with Cosmos DB.
   - **Cassandra API**: Provides compatibility with Cassandra column-family databases.
   - **Gremlin API**: Supports graph-based databases.
   - **Table API**: Mimics Azure Table Storage for key-value data models.

4. **Partitioning**: Cosmos DB uses a horizontal partitioning model for scalability, distributing data across multiple partitions. Each partition is identified by a “partition key.” Understanding how to select a good partition key is crucial, as it affects scalability and performance.

5. **Consistency Levels**: Cosmos DB offers five consistency levels, balancing latency and data consistency:
   - **Strong**: Ensures linearizability, but with higher latency.
   - **Bounded Staleness**: Guarantees consistency within a defined lag (time or updates).
   - **Session**: Provides consistency within a session, ensuring repeatable reads.
   - **Consistent Prefix**: Guarantees no out-of-order reads, slightly faster than strong.
   - **Eventual**: Offers the lowest latency with eventual consistency across regions.

6. **Request Units (RUs)**: Cosmos DB uses Request Units (RUs) as a measure of throughput, which encompasses reads, writes, and storage operations. You need to provision RUs based on workload needs, with the option of **autoscaling** for dynamic adjustment of RU capacity.

7. **Time to Live (TTL)**: TTL is a feature that automatically deletes documents after a specified time, useful for managing transient data.

### Security and Access
1. **Encryption**: Data is encrypted both at rest and in transit, with Microsoft-managed keys or customer-managed keys through Azure Key Vault.
2. **Role-Based Access Control (RBAC)**: Cosmos DB integrates with Azure AD to support role-based permissions, and it has built-in roles like Cosmos DB Owner, Reader, and Contributor.
3. **Private Endpoints**: For secure connectivity to Cosmos DB, you can use Azure Private Link to create private endpoints within a VNet.

### Monitoring and Troubleshooting
1. **Azure Monitor Integration**: Cosmos DB provides integration with Azure Monitor for tracking metrics like latency, throughput, storage, and RU/s usage.
2. **Diagnostic Logs**: Enable diagnostic logs to monitor detailed activity and diagnose issues within your Cosmos DB instances.
3. **Alerts**: You can set up alerts based on metrics such as RU/s consumption or latency to stay ahead of potential performance or scaling issues.

### Data Migration and ETL
Cosmos DB provides tools like **Data Migration Tool** and **Azure Data Factory** for data import/export and migration from other databases. It also supports Spark and Synapse Analytics for analytics on Cosmos DB data.

### Exam Focus Tips
- **APIs and Data Models**: Be able to distinguish among the different APIs and understand their use cases.
- **Global Distribution**: Understand how to configure global distribution and replication.
- **Partitioning and Scaling**: Know the implications of partition keys on scalability and performance.
- **Consistency Levels**: Be familiar with the five consistency levels and when to use each.
- **Throughput (RUs)**: Understand RUs, how they are provisioned, and autoscaling.
- **Security**: Know access control, RBAC, and encryption options.
- **Monitoring**: Be prepared to configure and interpret metrics in Azure Monitor.