---
title: Azure Caching
type: docs
weight: 11
prev: docs/az204/applicationInsights
next: docs/az204/azureEventGrid
---

### **Caching for Performance and Scalability**

#### **Introduction to Caching:**
- **Caching Concept:** Compared to cooking and freezing food for future use.
- **Azure Cache for Redis:**  
  - **Purpose:** Provides an in-memory datastore to improve performance by caching frequently-accessed data for fast read/writes.  
  - **Placement:** Introduced between the app layer and the data layer.  
  - **Software:** Based on Redis.  

#### **Caching Patterns with Redis:**
1. **Data Cache Pattern:** Stores select data for fast access.  
2. **Cache-Aside Pattern:**  
   - Data is cached only when needed.  
   - Updates occur in both the cache and database.  
3. **Content Cache:** Ideal for static content like headers and banners.  
4. **Session Store:** Used for session-related data like shopping carts or user history.  
5. **Job & Message Queuing Cache Pattern:** Processes long-running operations sequentially.  
6. **Distributed Transactions:** Ensures atomic operations.  

#### **Setting up Azure Cache for Redis:**
- **Steps:**
  1. Choose a **resource group** and **unique name** for the Redis Cache.
  2. Select the **location** (same as your app’s region for performance).  
  3. Choose a **pricing tier** (e.g., Standard).  
  4. Retrieve the **connection string** under "Access Keys."  
- **Code Example (C# with StackExchange.Redis):**  
   - Connect with the connection string.  
   - Use `GetDatabase()` to retrieve a database.  
   - Use `StringSet` to cache a key-value pair and `StringGet` to retrieve it.  

---

### **Content Delivery Networks (CDN):**
- **Purpose:**  
  - Positions static assets (CSS, HTML, media files) closer to users to reduce latency.  
  - Speeds up delivery for globally-distributed users.  

#### **Setting up Azure CDN:**
1. Navigate to a **storage account** and select Azure CDN.  
2. Create a **profile** (a collection of endpoints).  
3. Define an **endpoint** (unique name, origin hostname, and pricing tier).  
4. Configure **caching rules** using the **Rules Engine.**

#### **Query String Caching Behavior:**  
1. **Ignore Query String (Default):**  
   - Cache is based on the first request regardless of query string values.  
2. **Bypass Caching:**  
   - No caching; always retrieves data from the source.  
3. **Unique URL Caching:**  
   - Every unique query string variation creates a unique cache entry.  

---

### **Azure Front Door:**
- **Advanced CDN Alternative:**  
   - Includes CDN functionality along with other features.  
   - Microsoft appears to be transitioning toward Front Door.  

---

### **Summary:**
- **Azure Cache for Redis:** Improves app performance with flexible caching patterns.  
- **Azure CDN:** Boosts content delivery for global users by caching static assets closer to them.  
- **Key Exam Points:**  
   - Understand caching patterns, query string behavior, and pricing tiers.  
   - Know that Azure Front Door may replace standard Azure CDN in the future.  