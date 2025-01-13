---
title: Azure App Service Overview
type: docs
weight: 2
prev: docs/az204/implementContainerServices
next: docs/az204/azureCosmosDb
---

##  Azure App Service Overview and Key Concepts

#### **Introduction**
- The Azure App Service is a **Platform as a Service (PaaS)** offering that simplifies building and deploying web apps and APIs without managing the underlying infrastructure.
- It supports a variety of application types and languages, making it a versatile choice for developers.

#### **Core Features of Azure App Service**
1. **Multiple Language Support**:
   - Compatible with languages like **.NET**, **.NET Core**, **Java**, **Ruby**, **Node.js**, **Python**, **PHP**, and more.
   - The list of supported runtimes is frequently updated, and experimental languages are often available.

2. **Deployment Options**:
   - **Manual Methods**: Use **FTP**, Git repos, or cloud drives like **Dropbox** and **OneDrive**.
   - **Automated CI/CD**: Integrate with **Azure DevOps**, **GitHub Actions**, **Bitbucket**, or local Git repositories.

3. **Built-In DevOps Features**:
   - Deployment slots for **seamless testing and rollouts**.
   - **Continuous Integration and Continuous Deployment (CI/CD)** capabilities.
   - Support for **identity and access management (IAM)** with minimal coding for complex authentication scenarios.

4. **Global Scale and High Availability**:
   - Includes **auto-scaling**, **custom domains**, **SSL support**, and **load balancing** (in higher tiers).

5. **Diagnostics Logging**:
   - Application logs can capture **specific runtime issues** for troubleshooting.
   - Logs can be stored in **Blob Storage** and include **web server diagnostics** and **detailed error messages**.
   - Temporary logs automatically turn off after 12 hours.

#### **Service Plans**
Azure App Service is structured around **service plans**, which define the scale and resources for hosted apps. Key points include:

1. **Shared Tiers (F1 and D1)**:
   - Share resources with other tenants.
   - **No SLA provided**, making these suitable only for testing workloads.
   - Not available for **Linux-based environments**.

2. **Dedicated Tiers (Basic, Standard, Premium)**:
   - Resources are dedicated to hosted applications.
   - Offer production SLAs, built-in **load balancing**, and **VNet connectivity**.
   - Higher tiers support features like **auto-scaling** and **private endpoints** (Premium).

3. **Isolated Tiers (Isolated and IsolatedV2)**:
   - Designed for applications needing maximum **performance, security, and isolation**.
   - Include all features of dedicated tiers and provide **full app isolation**.

#### **Scaling and App Isolation**
- **Scaling Options**:
  - **Scale Up**: Increase resources (CPU, memory) for all apps in a plan.
  - **Scale Out**: Add more instances for load distribution.
  - **Auto-Scaling**: Configure scaling based on metrics (e.g., CPU usage, traffic) or a time schedule.

- **App Isolation**:
  - Place apps in their own plans to scale independently or integrate with resources in different regions.
  - Useful for apps that consume significant resources or require high performance.

#### **Comparison to Other Services**
- Unlike **Infrastructure as a Service (IaaS)**, which requires full server management, the **PaaS model** of Azure App Service is likened to a **high-quality box mix**—providing ready-to-use tools for faster development with less effort.
- Focuses on minimizing operational overhead while delivering flexibility and scalability.

#### **Summary of Key Features and Benefits**
1. Azure App Service supports **virtually any application type**, from **web apps** to **REST APIs**.
2. Offers **tiered service plans** to meet different business and development needs:
   - Shared tiers for testing.
   - Dedicated tiers for production.
   - Isolated tiers for high-performance and security.
3. Comprehensive **logging and diagnostics tools** are available in all tiers, including the Free tier.
4. Simplifies deployment with flexible CI/CD pipelines and manual deployment options.
5. Built-in **auto-scaling** helps optimize resource usage during peak and off-peak periods.

## Summary of Azure App Service: Creating and Deploying a Web App  

In this segment, the focus is on creating and deploying web apps using Azure App Service, configuring settings, leveraging identity and access management (IAM) options, and integrating deployment slots into DevOps workflows. Below is a detailed breakdown of the content:  

#### **Key Steps in Web App Creation**  
- **Creation Process:**  
  - Utilize the Azure wizard interface for creating resources, including setting up an App Service Plan if one doesn’t already exist.  
  - Navigate to the Web App overview page for further configurations after creation.  

- **Custom Domains and TLS/SSL Settings:**  
  - Configure custom URLs via the **Custom Domains** section.  
  - Add and validate custom domains or purchase them through Azure.  
  - Manage TLS/SSL certificates (private/public keys) either by uploading existing ones or purchasing directly in Azure.  

#### **Configuration Options**  
- **Application Settings:**  
  - Manage secure settings exposed as environment variables for runtime use.  
  - Use these settings as an alternative to Azure Key Vault in specific cases.  
  - Configure secure connection strings, default page names, path mappings, and storage mounts.  

- **Authentication and IAM:**  
  - Built-in support for multiple identity providers (e.g., Microsoft, Google).  
  - Configure identity providers with minimal code through app registration.  
  - Assign managed identities to web apps for secure resource access without storing credentials.  

- **API Management:**  
  - Manage APIs related to the application directly from the Web App interface.  

#### **Code Deployment and DevOps Integration**  
- **Deployment Methods:**  
  - Choose between manual methods (FTP, Git, cloud storage) and automated CI/CD pipelines (Azure DevOps, GitHub Actions).  

- **Deployment Slots:**  
  - **Overview:**  
    - Live apps with separate hostnames used for staging, testing, and deploying updates.  
    - Available for App Service Plans in the Standard tier or higher.  
  - **Benefits:**  
    - Minimize production risk by deploying changes to staging slots for testing before swapping with production.  
    - Support pre-production testing, with features such as multi-phase swaps for warming up applications and reducing cold starts.  
  - **Configurations:**  
    - Set independent configurations for each slot.  
    - Certain settings (e.g., managed identities, custom domains) are tied to the production slot but can be overridden selectively.  
  - Deployment slots can be managed through the Azure portal, CLI, or PowerShell.  

#### **Review of Covered Features**  
- **Configuration Highlights:**  
  - General settings, path mapping, security certificates, and app features in production-level plans.  
- **IAM Options:**  
  - Built-in authentication provider setups and managed identity configurations.  
- **Deployment Features:**  
  - Manual and automated deployments with an emphasis on deployment slots as a DevOps strategy.

## Useful Commands

Here’s a list of useful Azure CLI commands for managing Azure App Services:

### **General App Service Management**
1. **Create a Web App**:
   ```bash
   az webapp create --resource-group <ResourceGroupName> --plan <AppServicePlanName> --name <WebAppName> --runtime "<Runtime>"
   ```
   Example runtime: `"DOTNETCORE:7.0"` or `"NODE:18-lts"`.

2. **Delete a Web App**:
   ```bash
   az webapp delete --resource-group <ResourceGroupName> --name <WebAppName>
   ```

3. **List Web Apps in a Resource Group**:
   ```bash
   az webapp list --resource-group <ResourceGroupName> --output table
   ```

4. **Show Details of a Web App**:
   ```bash
   az webapp show --resource-group <ResourceGroupName> --name <WebAppName>
   ```

### **App Service Plan**
1. **Create an App Service Plan**:
   ```bash
   az appservice plan create --name <PlanName> --resource-group <ResourceGroupName> --sku <Sku> --is-linux
   ```
   Example SKU: `B1`, `P1v2`, `S1`.

2. **List App Service Plans**:
   ```bash
   az appservice plan list --resource-group <ResourceGroupName> --output table
   ```

3. **Update an App Service Plan**:
   ```bash
   az appservice plan update --name <PlanName> --resource-group <ResourceGroupName> --sku <NewSku>
   ```

4. **Delete an App Service Plan**:
   ```bash
   az appservice plan delete --name <PlanName> --resource-group <ResourceGroupName>
   ```

### **Configuration Management**
1. **Set App Settings**:
   ```bash
   az webapp config appsettings set --resource-group <ResourceGroupName> --name <WebAppName> --settings <Key>=<Value>
   ```

2. **List App Settings**:
   ```bash
   az webapp config appsettings list --resource-group <ResourceGroupName> --name <WebAppName>
   ```

3. **Set Connection Strings**:
   ```bash
   az webapp config connection-string set --resource-group <ResourceGroupName> --name <WebAppName> --settings <ConnectionName>=<Value> --connection-string-type <Type>
   ```
   Example types: `SQLAzure`, `MySQL`, `PostgreSQL`.

4. **Enable HTTPS Only**:
   ```bash
   az webapp update --resource-group <ResourceGroupName> --name <WebAppName> --set httpsOnly=true
   ```

### **Deployment and Slots**
1. **Configure Deployment Source**:
   ```bash
   az webapp deployment source config --name <WebAppName> --resource-group <ResourceGroupName> --repo-url <RepoURL> --branch <BranchName>
   ```

2. **List Deployment Slots**:
   ```bash
   az webapp deployment slot list --resource-group <ResourceGroupName> --name <WebAppName> --output table
   ```

3. **Create a Deployment Slot**:
   ```bash
   az webapp deployment slot create --resource-group <ResourceGroupName> --name <WebAppName> --slot <SlotName>
   ```

4. **Swap Deployment Slots**:
   ```bash
   az webapp deployment slot swap --resource-group <ResourceGroupName> --name <WebAppName> --slot <SlotName> --target-slot <TargetSlot>
   ```

### **Monitoring and Logs**
1. **Enable Diagnostic Logs**:
   ```bash
   az webapp log config --name <WebAppName> --resource-group <ResourceGroupName> --web-server-logging filesystem
   ```

2. **Stream Logs**:
   ```bash
   az webapp log tail --name <WebAppName> --resource-group <ResourceGroupName>
   ```

3. **Get App Metrics**:
   ```bash
   az monitor metrics list --resource <ResourceID> --metric <MetricName>
   ```
   Example metrics: `CpuTime`, `Http2xx`.

### **Scaling**
1. **Scale App Service Plan**:
   ```bash
   az appservice plan update --name <PlanName> --resource-group <ResourceGroupName> --number-of-workers <InstanceCount>
   ```

2. **Enable Autoscale**:
   ```bash
   az monitor autoscale create --resource-group <ResourceGroupName> --resource <AppServicePlanName> --resource-type "Microsoft.Web/serverFarms" --min-count <MinInstances> --max-count <MaxInstances> --count <DefaultInstances>
   ```