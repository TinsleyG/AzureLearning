---
title: Blob Storage
type: docs
weight: 5
prev: docs/az204/azureFunctions
next: docs/az204/azureCosmosDb
---

## Blob Storage


#### **Segment 1: Azure Blob Storage Basics**
1. **Overview:**
   - Introduction to Azure Blob Storage, its configuration, and management.
   - Focus on its application for static site hosting, redundancy, and security.

2. **Configuring Blob Storage:**
   - **Storage Account Creation:** Requires a unique name and resource group assignment.
   - **Standard vs. Premium Tiers:**
     - Standard: Preferred for general storage needs.
     - Premium: Designed for virtual drives with limited features compared to Standard.
   - **Redundancy Options:** 
     - **LRS (Locally Redundant Storage):** Guards against drive/rack failures.
     - **ZRS (Zone Redundant Storage):** Protects against data center failures.
     - **GRS (Geo-Redundant Storage):** Enables failover to secondary regions.
     - **GZRS (Geo-Zone Redundant Storage):** Combines GRS and ZRS benefits.

3. **Security and Networking Features:**
   - Enforce HTTPS for REST operations.
   - Control public access at the storage and container levels.
   - Utilize shared access signatures (SAS) for fine-grained access control.

4. **Advanced Features:**
   - **Soft Delete and Versioning:** Protect against accidental deletions and enable point-in-time restores.
   - **Blob Change Feed:** Track changes for event-driven scenarios.
   - **Customer-Managed Keys (CMKs):** Add an optional second encryption layer.

---

#### **Segment 2: Blob Types and Data Storage**
1. **Blob Types:**
   - **Block Blobs:** For text and binary data, with chunk-based management.
   - **Append Blobs:** Optimized for logging, allowing only append operations.
   - **Page Blobs:** Used for random access, e.g., virtual hard drives.

2. **Access Tiers:**
   - **Hot:** High transfer rate, suitable for frequently accessed data.
   - **Cool and Cold:** Cost-effective for infrequently accessed data (30-180 days).
   - **Archive:** For long-term storage with delayed retrieval.

3. **Practical Scenarios:**
   - Store videos, images, audio files, or data requiring long-term retention and flexibility.
   - Mimic folder-like organization using blob naming conventions.

---

#### **Segment 3: API Usage and Lifecycle Management**
1. **REST API Operations:**
   - Retrieve metadata headers for containers and blobs using `GET` or `HEAD`.
   - Overwrite metadata using `PUT`.
   - Manage tiers and rehydrate archived blobs, illustrating potential delays and costs.

2. **Lifecycle Management:**
   - Automate tier transitions and data archiving.
   - Optimize costs by managing blob versions and implementing granular control.

3. **Encryption and Authentication:**
   - **Data at Rest:** Protected by Storage Service Encryption (SSE).
   - **Data in Transit:** Encrypted with HTTPS or SMB.
   - Access control options include Role-Based Access Control (RBAC), Azure AD, and SAS tokens.

---

#### **Segment 4: Azure Cosmos DB**
1. **Configurations and Basics:**
   - Introduces Cosmos DB for managing globally distributed data.
   - Encourages developers to explore the DP‑420 course for in-depth understanding.

2. **Practical Use Cases:**
   - Hands-on labs to solidify knowledge using the Azure SDKs for Python and Cosmos DB.

3. **Exam Insights:**
   - Highlights the importance of mastering redundancy options, lifecycle management, and API operations for the AZ‑204 certification.

---

#### **Key Takeaways:**
1. **Blob Storage Highlights:**
   - Covered redundancy levels (LRS, ZRS, GRS, GZRS), soft delete, and change feed.
   - Reviewed the distinct blob types and access tiers with practical use cases.

2. **Practical API Operations:**
   - Demonstrated retrieving and updating metadata, as well as manual rehydration.

3. **Security Focus:**
   - Outlined encryption, access control options, and SAS token usage.

4. **Lifecycle and Cost Optimization:**
   - Emphasized the importance of lifecycle management to control costs and ensure data protection.

Here's a refined version of the transcript for clarity and improved flow:

---

## Blob Lifecycle 

### **Quick Review: Storage Tiers**
Azure Blob Storage offers four storage tiers:  

- **Hot:** High access rates, higher storage cost.  
- **Cool:** Lower access frequency, lower storage cost.  
- **Archive:** Minimal access, lowest storage cost, but higher access cost and latency.  
- **Premium:** High performance, ideal for low-latency scenarios.

As a reminder, while you can manually change blob tiers, this approach doesn’t scale well. That’s where **lifecycle management policies** come in.

---

### **Lifecycle Management Policies**
Imagine this scenario:  
- Data is frequently accessed for a few days after being uploaded.  
- Access slows after a couple of weeks.  
- After 30 days, the data is rarely accessed.  

**Optimal Storage Strategy:**  
- Hot tier: Immediately after upload.  
- Cool tier: After two weeks of inactivity.  
- Archive tier: After 30 days.

Lifecycle management policies let you automate these transitions based on data age, helping you optimize costs and performance.

---

### **Setting Up Lifecycle Management Policies**
Policies are composed of rules defined in JSON. Each rule includes:  
- **Parameters:** Rule name and status.  
- **Filters:** Determine which blobs are impacted.  
- **Actions:** Define operations, such as tier transitions or deletions, based on conditions like the number of days since last modification.

Here’s how to create a lifecycle policy in the Azure portal:  
1. Navigate to your storage account.  
2. Select **Lifecycle Management**.  
3. Add a rule, specifying actions and conditions (e.g., move blobs to the cool tier after 45 days of no modification).  
4. Optionally, set filters to apply the rule to specific containers or folders.  
5. Save the policy, and view or edit the JSON representation if needed.

To create a policy using Azure CLI, define the JSON in a file and use the following command:  
```bash
az storage account management-policy create --account-name <account-name> --policy @<policy-file>
```

---

### **Blob Storage Client Libraries**
While the AZ-204 exam doesn’t heavily emphasize SDKs, understanding the **Blob Storage object model** and common classes can be helpful.

#### **Object Model Overview**  
1. **Storage Account:** The foundational infrastructure, equivalent to a pantry.  
2. **Blob Containers:** Organizational units within accounts, like shelves or bins.  
3. **Blobs:** The individual pieces of data, analogous to pantry items.  

#### **Key Classes**  
- **Blob Service Client:** Operates at the storage account level.  
- **Container Client:** Works with blob containers.  
  - .NET: `BlobContainerClient`  
  - Python: `ContainerClient`  
- **Blob Client:** Manages individual blobs.  
- **BlobClientOptions (.NET only):** Configures blob client settings.  
- **BlobUriBuilder (.NET only):** Modifies URIs for blobs or containers.

#### **Creating Clients**
Here’s how to create client objects for each level:  
- **Blob Service Client:**  
  - **.NET:** `new BlobServiceClient(connectionString)`  
  - **Python:** `BlobServiceClient.from_connection_string(connection_string)`  
- **Container Client:**  
  - **.NET:** `new BlobContainerClient(connectionString, containerName)`  
  - **Python:** `ContainerClient.from_connection_string(connection_string, container_name)`  
- **Blob Client:**  
  - **.NET:** `new BlobClient(connectionString, containerName, blobName)`  
  - **Python:** `BlobClient.from_connection_string(connection_string, container_name, blob_name)`

---

### **Tasty Takeaways**
1. Lifecycle policies optimize storage costs and performance by automating tier transitions.  
2. Policies are defined in JSON with parameters, filters, and action sets.  
3. Blob Storage’s object model is hierarchical: Account → Container → Blob.  
4. Client libraries support operations at each level, with key classes available in both Python and .NET.  

### Example filters
Here are some useful Azure Blob Storage lifecycle management policy filters, along with examples of scenarios where they might be applied:


### **1. Tier-Based Aging Filters**
Transition blobs to cooler storage tiers based on their age since the last modification.  

#### Example:  
Move blobs to the **cool** tier after 30 days and to the **archive** tier after 90 days.  

**Filter JSON:**  
```json
{
  "filters": {
    "blobTypes": ["blockBlob"],
    "prefixMatch": ["/logs/"]
  },
  "actions": {
    "baseBlob": {
      "tierToCool": {
        "daysAfterModificationGreaterThan": 30
      },
      "tierToArchive": {
        "daysAfterModificationGreaterThan": 90
      }
    }
  }
}
```

**Use Case:** Archiving old logs or files that are no longer frequently accessed.

---

### **2. Delete Old Blobs**
Automatically delete blobs after a certain period.  

#### Example:  
Delete blobs that are older than 180 days.  

**Filter JSON:**  
```json
{
  "filters": {
    "blobTypes": ["blockBlob"],
    "prefixMatch": ["/temp/"]
  },
  "actions": {
    "baseBlob": {
      "delete": {
        "daysAfterModificationGreaterThan": 180
      }
    }
  }
}
```

**Use Case:** Managing temporary files or old backups to free up storage space.

---

### **3. Apply Filters to Specific Containers**
Limit lifecycle rules to specific containers by using prefix matching.  

#### Example:  
Move files from the **reports** container to the archive tier after 60 days.  

**Filter JSON:**  
```json
{
  "filters": {
    "blobTypes": ["blockBlob"],
    "prefixMatch": ["reports/"]
  },
  "actions": {
    "baseBlob": {
      "tierToArchive": {
        "daysAfterModificationGreaterThan": 60
      }
    }
  }
}
```

**Use Case:** Handling financial or compliance-related documents with specific retention policies.

---

### **4. Conditional Rules for Blob Names**
Create filters based on naming patterns.  

#### Example:  
Archive blobs with names starting with "backup-" after 90 days.  

**Filter JSON:**  
```json
{
  "filters": {
    "blobTypes": ["blockBlob"],
    "prefixMatch": ["backup-"]
  },
  "actions": {
    "baseBlob": {
      "tierToArchive": {
        "daysAfterModificationGreaterThan": 90
      }
    }
  }
}
```

**Use Case:** Managing backups that follow a consistent naming convention.

---

### **5. Filter by Blob Types**
Apply rules to specific blob types (e.g., block blobs, append blobs, page blobs).  

#### Example:  
Transition **block blobs** to cool storage after 15 days and delete **append blobs** after 60 days.  

**Filter JSON:**  
```json
[
  {
    "filters": {
      "blobTypes": ["blockBlob"]
    },
    "actions": {
      "baseBlob": {
        "tierToCool": {
          "daysAfterModificationGreaterThan": 15
        }
      }
    }
  },
  {
    "filters": {
      "blobTypes": ["appendBlob"]
    },
    "actions": {
      "baseBlob": {
        "delete": {
          "daysAfterModificationGreaterThan": 60
        }
      }
    }
  }
]
```

**Use Case:** Differentiating lifecycle policies based on how the data is structured or accessed.

---

### **6. Exclude Specific Data**
Exclude certain blobs or containers from lifecycle policies using prefixes.  

#### Example:  
Apply rules to all blobs except those in the **critical** folder.  

**Filter JSON:**  
```json
{
  "filters": {
    "blobTypes": ["blockBlob"],
    "prefixMatch": ["!critical/"]
  },
  "actions": {
    "baseBlob": {
      "tierToArchive": {
        "daysAfterModificationGreaterThan": 90
      }
    }
  }
}
```

**Use Case:** Ensuring critical files are excluded from automated lifecycle transitions.

## Static Site Hosting

**Summary:**  

This segment introduces **static site hosting in Azure Blob Storage**, detailing how to enable it, configure it, and manage basic monitoring and security. 

1. **Static Site Hosting Overview**:  
   - Available on **general-purpose v2** or **block blob storage accounts**.  
   - Stores site content (HTML, CSS, JS, images) in the `$web` container, created automatically when static hosting is enabled.  
   - Supports **custom domains** without extra cost but lacks features like CORS, custom headers, or Azure AD integration unless paired with a CDN or Azure Static Web Apps.  

2. **Setup Steps**:  
   - **In Portal**:  
     - Enable static website under **Static Website settings**.  
     - Provide the index and error page file names (e.g., `home.html`, `oops.html`).  
     - Upload content to the `$web` container.  
   - **Using Azure CLI**:  
     - Update blob service properties to enable static hosting and specify file names.  
     - Upload content and retrieve website endpoints with the `az storage blob` commands.  

3. **Monitoring and Security**:  
   - Enable metrics to track traffic and file access in the `$web` container.  
   - Configure filters for granular insights.  
   - Note: Static website endpoints use anonymous access, unaffected by container-level public access settings.  

4. **Review**:  
   - Benefits: Low-cost hosting with custom domains.  
   - Limitations: No advanced features (e.g., CORS, Azure AD auth) without a CDN or other services.  