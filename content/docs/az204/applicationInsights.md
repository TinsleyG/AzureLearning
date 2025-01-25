---
title: Azure Key Vault
type: docs
weight: 10
prev: docs/az204/azureKeyVault
next: docs/az204/azureCaching
---

### **1. Application Insights Overview**  
- **Purpose**: Provides expanded observability for Azure applications through **metrics, logs, and distributed traces**.  
- **Integration**: Works seamlessly with Azure-hosted resources like App Services, Azure Functions, and Azure Kubernetes, but can also monitor apps hosted outside of Azure.  

#### Key Features Highlighted:
- **Live Metrics**: Monitor real-time activity and performance.  
- **Availability Tests**: Add simple ping tests or multi-step tests to track uptime.  
- **Application Map**: Visualize distributed tracing data to identify service interactions and bottlenecks.  
- **Failures and Anomalies**: Detect and address issues proactively.  
- **Usage Analytics**: Gain insights into user behavior with tools like:  
  - **Funnels**: Track user conversions and drop-off rates (e.g., shopping cart abandonment).  
  - **User Flows**: Analyze individual user navigation patterns.  
  - **Retention Analysis**: Monitor how often users return to your app and their activity levels.  

---

### **2. Instrumentation Options**  
Instrumenting applications allows you to gather telemetry data for monitoring and insights. Options include:  

#### **Auto-Instrumentation**  
- **What it does**: Automatically collects telemetry without modifying your code.  
- **Key advantage**: Simplifies setup for existing applications.  

#### **Manual Instrumentation**  
- **What it involves**: Adding the Application Insights SDK to your code for greater control.  
- **Example**: Amy showcased a .NET Console app with manual instrumentation (link provided in the segment).  

#### **Combining Both**  
- Auto and manual instrumentation can work together, but settings like **data sampling** may require careful coordination to avoid conflicts.

---

### **3. Sampling in Application Insights**  
Sampling reduces telemetry data to manage costs and prevent resource throttling:  
- **Ingestion Sampling**: Configured at the service endpoint (e.g., percentage of data to ingest).  
- **Adaptive Sampling**: Default setting in the .NET SDK and Azure Functions, which adjusts telemetry volume dynamically.  
- **Fixed-Rate Sampling**: Manually set sampling percentage, applicable to both server-side and client-side data.  

---

### **4. DevOps Integration**  
Application Insights integrates with both **GitHub** and **Azure DevOps** to create work items based on telemetry data, enhancing the monitoring and development workflow.  

---

### **5. Lab Focus**  
- **Hands-On Activities**: Setting up Application Insights, configuring availability tests, and creating alerts/notifications.  
- **Goal**: Prepare for the AZ-204 exam by mastering monitoring configurations and insights interpretation.

---

### **6. Key Takeaways**  
- Azure Monitor is a foundational tool for gathering metrics, logs, and traces.  
- Application Insights builds on Azure Monitor with additional capabilities for:  
  - Proactive monitoring.  
  - Deep application analytics.  
  - User behavior insights.  
- Instrumentation can be tailored for runtime environments or development pipelines.  
- Sampling is a critical feature for large-scale applications.  

Here’s a concise breakdown of your text into key points:

---

### **Segment Overview**  
- Continuation of the Application Insights demo with a focus on tests, logs, metrics, and troubleshooting.  
- Covered differences between **Azure Monitor** and **Application Insights** (Application Insights is a subset of Azure Monitor).  

---

### **Log-Based Metrics vs. Standard Metrics**  
- **Log-Based Metrics**:  
  - Use **Kusto Query Language** (KQL) for detailed analysis.  
  - Offer more depth but may have slower performance.  
  - Auto-instrumentation sends data automatically, whereas SDK-based apps require explicit event configuration.  
  - Can be impacted by sampling techniques.  

- **Standard Metrics**:  
  - Pre-aggregated and not affected by sampling.  
  - Provide faster performance and near real-time alerting.  

**Namespace Selector**: Used to toggle between log-based and standard metrics.  

---

### **Availability Testing**  
- **Classic Test**:  
  - Ping testing for uptime and performance.  

- **Standard Test**:  
  - Includes advanced checks like:  
    - SSL certificate validity.  
    - HTTP request verbs (GET, POST, etc.).  
    - Custom headers and data.  
  - Can be used on any site, even those not owned by you (e.g., third-party APIs).  

- **Custom Track Availability Test**:  
  - Done via the SDK using the `TrackAvailability` method.  

---

### **Alerts and Notifications**  
- Alert Rules consist of:  
  1. **Scope**: The resource being monitored.  
  2. **Condition**: The trigger event for the alert.  
  3. **Notifications/Actions**: Actions (e.g., sending emails, triggering Logic Apps) defined using **Action Groups**.  

**Best Practice**: Use granular, targeted action groups for better management and scalability.  

---

### **Application Map for Troubleshooting**  
- Visual interface showing app components (nodes) and their dependencies.  
- Highlights:  
  - Health KPIs.  
  - Alert statuses for each component.  
  - Ability to drill down into Azure services for detailed diagnostics (e.g., SQL database advisor tips).  

---

### **Takeaways**  
- Explored standard vs. log-based metrics, availability tests, and alerting.  
- Application Map provides advanced troubleshooting capabilities.  
- Encouraged hands-on practice in the lab for deeper understanding.  