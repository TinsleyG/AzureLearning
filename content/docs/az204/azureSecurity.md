---
title: Azure Security
type: docs
weight: 8
prev: docs/az204/apiManagement
next: docs/az204/azureKeyVault
---

## Understanding Authentication and Authorization

1. **Azure Security Overview**
   - Authentication and authorization patterns.
   - Secure storage solutions and issuing **Shared Access Signatures (SAS)** for Azure Storage.
   - Interaction with **Microsoft Graph** for managing user identities.  
   - Focus on **Azure Key Vault** and **managed identities** with a hands-on lab.

2. **Understanding Authentication and Authorization**
   - The **Microsoft Identity platform** implements **OAuth 2.0** for user authentication.
   - OAuth workflow:
     1. User tries to access a web app.
     2. Redirects to **Azure Active Directory (Azure AD)** for authentication.
     3. Successful authentication provides a token for authorization.  
   - **Delegated Permissions** (user-based) vs. **App-only Permissions** (background apps).  

3. **OAuth Roles in Azure**
   - **Resource Owner**: Entity requesting access, manages data and access controls.  
   - **Resource Server**: Stores data and handles authorization tokens.  
   - **Authorization Server**: Manages authentication (e.g., Azure AD or external providers like Google).  

4. **Azure AD App Registration**
   - Registering apps in Azure AD enables OAuth authentication.  
   - Key steps:
     - Define supported account types.
     - Set redirect URLs (if needed).
     - Collect **Application IDs** for OAuth integration.
   - Enabling **conditional access policies** like multifactor authentication (MFA).

---

### **Role-Based Access Control (RBAC)**
- RBAC provides coarse-grained access control.
- **Role Definitions**:
  - Define permissions (e.g., create database, read, write).
  - Can include both control plane and data plane permissions.
- **Role Assignments**:
  - Assign roles to users, apps, or services (called **security principals**).  
  - Examples of built-in roles:
    - **Owner**: Full control, including permissions management.
    - **Contributor**: Read, write, delete access but no permissions management.
    - **Reader**: Read-only access.  

---

### **Access Control Lists (ACLs)**
- ACLs provide finer-grained access compared to RBAC.  
- Useful for managing access to specific resources within an account.  

---

### **Custom Role Creation**
- Use **JSON** files to define custom roles with specific actions.
- Role assignment via Azure CLI:
  - `az role definition create` for role creation.  
  - `az role assignment create` to assign roles at various scopes (e.g., specific resource groups).  

---

### **Key Takeaways**
- OAuth 2.0 powers Azure AD’s authentication for apps.  
- **RBAC** offers coarse-grained access control, while **ACLs** allow fine-grained permissions.  
- Tools like Azure CLI, PowerShell, and REST APIs streamline role and access management.  


## Secure Storage Solutions

### **Introduction**
- The segment focuses on **Shared Access Signatures (SAS)** in Azure Storage and their secure management.
- Key topics covered:
  1. What SAS tokens are and how they work.
  2. Steps to create SAS tokens and manage them securely.
  3. Using **Storage Access Policies** to enhance security and manage SAS tokens efficiently.

---

### **Shared Access Signatures (SAS) Overview**
- SAS tokens are **keys that grant permissions** to Azure Storage resources.
- Shared via a **SAS URL**, which should be used over **HTTPS** to ensure security.
- SAS follows the **principle of least privilege**, granting only the necessary permissions.

---

### **Levels of SAS Tokens**
1. **Account Level**  
   - Grants broad, owner-like permissions.  
   - Rarely recommended due to high risk.
2. **Service Level**  
   - Provides access to a specific service (e.g., blob containers, tables, queues).  
3. **User Level**  
   - The most secure option, leveraging **Azure Active Directory (Azure AD)** for delegated access.  

---

### **SAS Token Components**
- The SAS URL contains details about:
  - **Resource being accessed** (e.g., a blob or file).  
  - **Permissions** (e.g., read, write, delete).  
  - **Validity timeframe** (start and end times).  
  - **Storage API version** and resource type (e.g., blob only).  
  - **Signature (sig)**: A unique key for authentication.  

---

### **Generating SAS Tokens**
1. Ensure the storage account is enabled for key access:
   - Check settings in the **Configuration** section of the storage account.
2. Generate SAS tokens:
   - Go to **Shared Access Signature** in the storage account menu.
   - Define access level (e.g., account or individual blob).  
   - Set permissions, time range, and allowed protocols (preferably **HTTPS only**).  
3. Save the **SAS URL** securely after generation, as it cannot be retrieved again.

---

### **Revoking or Modifying SAS Tokens**
- Challenges arise if:
  - Permissions or expiration dates need to change.  
  - A token is compromised.  
- **Best practice**: Use **Storage Access Policies** to manage SAS tokens dynamically.

---

### **Storage Access Policies**
- Serve as a form of **Access Control List (ACL)** for managing SAS tokens securely.
- Steps to use access policies:
  1. Create a policy and define permissions, start time, and expiration time.
  2. When generating a SAS token, assign it to the policy.
  3. Adjust the policy as needed to:
     - Revoke or extend permissions.
     - Apply changes to all SAS tokens linked to the policy.  

---

### **Key Takeaways**
1. **SAS Tokens** provide flexible and secure access to Azure Storage resources.
2. **Service-level and user-delegated SAS tokens** are recommended over account-level SAS for better security.
3. **Access Policies** enhance token management by enabling dynamic permission updates without regenerating SAS tokens.
4. Always use **HTTPS** for SAS URL communication to ensure data security.


### Detailed Overview of Managed Identities and Secure Communication in Azure

---

### **Introduction to Managed Identities**
Managed identities in Azure enable secure, credential-free communication between Azure resources. These identities are authenticated by Azure Active Directory (Azure AD) and eliminate the need to manage credentials. They provide seamless access to resources supporting Azure AD authentication, such as Azure Key Vault and Azure Storage.

In this segment, the focus is on:
1. Understanding the **two types of managed identities**.
2. Walking through authentication workflows.
3. Configuring managed identities for secure communication.
4. Demonstrating code snippets for acquiring and using access tokens.

---

### **The Two Types of Managed Identities**
1. **System-Assigned Managed Identities**:
   - Tied directly to an Azure resource (e.g., a container app or VM).
   - Share a lifecycle with the associated resource:
     - When the resource is deleted, the identity is deleted.
   - One-to-one relationship between the resource and its identity.
   - Common use cases:
     - Workloads focused on a single resource.
     - Scenarios requiring isolation of identities.

2. **User-Assigned Managed Identities**:
   - Created as standalone Azure resources.
   - Can be assigned to multiple Azure resources.
   - Independent lifecycle:
     - Deleting a resource does not delete the identity.
   - Many-to-many relationship between resources and identities.
   - Common use cases:
     - Scenarios where multiple resources need to share a single identity.
     - Setting up permissions for assets before resources are created.
     - Frequently spun-up and torn-down resources requiring consistent permissions.

**Summary of Differences**:
| Feature                     | System-Assigned            | User-Assigned              |
|-----------------------------|----------------------------|----------------------------|
| Lifecycle                   | Tied to the resource       | Independent                |
| Relationship                | One-to-one                | Many-to-many               |
| Common Use Case             | Single-resource workloads  | Shared identities across resources |

---

### **Authentication Workflow for Managed Identities**
1. **Identity Creation**:
   - Initiate through the Azure Portal, CLI, or other code interfaces.
   - Azure Resource Manager creates a service principal in Azure AD and configures the identity.

2. **Resource Access Configuration**:
   - Use the service principal to grant access to Azure resources (e.g., Azure Key Vault, Azure SQL Database).

3. **Token Retrieval**:
   - Code hosted on the Azure resource requests an access token from Azure AD.
   - The token is used to authenticate and connect to the target resource without managing credentials.

---

### **Practical Example: Configuring Managed Identities**
**Scenario**: Connect a web app to an Azure Storage account using a system-assigned identity.

1. **Enable System-Assigned Identity**:
   - Navigate to the **Identity** section of the web app in the Azure Portal.
   - Set the identity status to "On" and save.

2. **Grant Access to the Storage Account**:
   - Go to the storage account’s **Access Control (IAM)** section.
   - Add a role assignment:
     - Choose a role (e.g., Storage Blob Data Contributor).
     - Select **Managed identity** as the member type.
     - Assign the web app’s managed identity.

3. **Authenticate in Code**:
   - Use the **DefaultAzureCredential** class to connect to the blob service:
     ```csharp
     var client = new BlobServiceClient(new DefaultAzureCredential());
     ```

4. **User-Assigned Identity**:
   - For user-assigned identities, pass the identity’s ID to the credential instantiation:
     ```csharp
     var options = new DefaultAzureCredentialOptions
     {
         ManagedIdentityClientId = "<User-Assigned-Identity-ID>"
     };
     var client = new BlobServiceClient(new DefaultAzureCredential(options));
     ```

---

### **Key Benefits of Managed Identities**
1. **Credential-Free Authentication**:
   - No need to store or manage secrets or access keys.
2. **Simplified Permissions Management**:
   - Use role-based access control (RBAC) to configure access.
3. **Enhanced Security**:
   - Minimized attack surface by removing hardcoded credentials.
4. **Flexible Identity Lifecycle**:
   - System-assigned identities are resource-specific.
   - User-assigned identities offer reusability and consistency across multiple resources.

---

### **Additional Concepts Reviewed in the Episode**
1. **Authentication and Authorization**:
   - Key terminologies like OAuth, ACLs (Access Control Lists), and RBAC.
2. **SAS Tokens**:
   - Temporary credentials for accessing Azure Storage.
3. **Microsoft Graph**:
   - Using managed identities to access Microsoft 365 data and intelligence.
4. **Azure Key Vault**:
   - How managed identities streamline access to Key Vault for secrets, keys, and certificates.