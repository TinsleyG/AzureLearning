---
title: Azure Security
type: docs
weight: 8
prev: docs/az204/apiManagement
next: 
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