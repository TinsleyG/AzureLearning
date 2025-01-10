---
title: Implement Containerized Solutions
type: docs
weight: 2
prev: docs/az204/virtualMachines
next: docs/az204/azureCosmosDb
---

## ACR - Azure Container Registry

### 1. **Containers in Azure**:
   - **Containers** are a lightweight way of packaging software code along with the operating system libraries and dependencies required to run that code, all bundled into a single executable. 
   - **Docker containers** are specifically supported by Azure services like **Azure Container Registry (ACR)** and **Azure Container Instances**.
   - The goal of using containers in Azure is to store, build, and run containerized applications in a flexible and consistent manner across different environments.

### 2. **Azure Container Registry (ACR)**:
   - **ACR** is the core service for storing container images in Azure.
   - **Service Tiers**:
     - **Basic**: Intended for developers and development processes. It is suitable for early-stage development or testing but lacks features needed for production.
     - **Standard**: The default service tier for production environments. It provides the necessary performance and scalability for most production workloads.
     - **Premium**: This tier offers higher throughput, more storage, and support for **Private Link**, which allows for secure connections between a virtual network and Azure services.
   - A **Unique Registry Name** is required when creating an ACR. The name must be globally unique.
   - **Creating an ACR**:
     - You create a registry using the Azure CLI command `az acr create` with the following parameters:
       - **resource-group**: The existing resource group where the registry will reside.
       - **name**: The globally unique name of the registry.
       - **sku**: The service tier (Basic, Standard, Premium).

### 3. **Working with Containers**:
   - **Docker CLI Commands**: You can use the Docker CLI to interact with ACR and manage container images:
     - **`docker pull`**: Fetches a container image from a remote registry into your local environment.
     - **`docker tag`**: Tags a local container image with a specific repository and version name so that it can be pushed to a registry.
     - **`docker push`**: Pushes the tagged container image to a registry like ACR.
   - **Dockerfiles**: A Dockerfile is a text file that defines the steps to build a Docker image. It contains a series of instructions such as installing dependencies, copying files, and setting environment variables. These can be used to automate the creation of container images.
     - **ACR Tasks**: ACR supports automation via **ACR Tasks**, which lets you automate the process of building and pushing container images from Dockerfiles. This avoids the need for a local Docker Engine and integrates into Azure’s DevOps pipeline.
     - ACR Tasks can be configured in YAML files and can be triggered on demand, on a schedule, or in response to events (e.g., changes in source code or base images).

### 4. **ACR Tasks**:
   - **ACR Tasks** automate container management workflows like building, testing, and pushing images to a registry.
   - ACR Tasks allow you to build images from Dockerfiles and then push those images to a container registry.
   - These tasks can be configured to run automatically in response to events (e.g., when there’s a new update to source code) or can be manually triggered on demand.
   - **YAML Configuration**: ACR Tasks use YAML files to define the workflow, similar to a recipe for automating image builds and pushes.

### 5. **Viewing Containers in ACR**:
   - To view all the container images stored in your ACR, use the command `az acr repository list`. This command lists all the repositories (containers) within the specified ACR.

### 6. **Key Exam Takeaways**:
   - **ACR** is a central Azure service for managing containerized code. It is tightly integrated with services like **Azure Container Instances** and **Azure Kubernetes Service**, but these are not the focus of the AZ-204 exam.
   - **Service Tiers** in ACR (Basic, Standard, and Premium) are important for choosing the appropriate level of performance and storage.
   - **Working with Docker CLI** is essential for pulling, tagging, and pushing container images to ACR.
   - **Dockerfiles** automate the creation of container images and are integral to using **ACR Tasks** for container management.
   - **ACR Tasks** provide a way to automate container image builds and pushes directly within Azure without needing a local Docker Engine.
   - Familiarity with **YAML configuration** for ACR Tasks and understanding how containers interact with ACR is important for the exam.

## ACI - Azure Container Instances

### 1. **Review of Azure Container Registry (ACR)**:
   - **ACR** is a core Azure service for managing and storing container images.
   - You need an ACR instance to **publish container images**. These images are then hosted on services like **Azure Container Instances** (ACI).
   - ACR offers three service tiers: Basic, Standard, and Premium, which provide varying levels of performance and features.
   - **Security**: ACR allows you to secure your containers to prevent unauthorized access or changes, ensuring that only authorized entities can modify or pull images.

### 2. **Overview of Azure Container Instances (ACI)**:
   - **ACI** is a Platform as a Service (PaaS) offering designed to run containers without requiring virtual machines (VMs).
   - **ACI benefits** include:
     - **Fast startup**: Containers can start within seconds, providing fast application deployment.
     - **No need to manage VMs**: ACI abstracts away VM management, freeing you from dealing with underlying infrastructure.
     - **Exposure to the internet**: ACI allows you to expose container groups to the internet with a public IP address and fully qualified domain name (FQDN).
     - **Hypervisor-level security**: Containers can be isolated at the hypervisor level to enhance security.
     - **Minimal storage requirements**: ACI only stores the minimum data required to manage containers, protecting customer data.
   - **Custom sizing**: You can allocate exact CPU cores and memory to containers, allowing for **resource optimization**.
   - **Persistent storage**: **Azure File shares** can be mounted to containers to provide persistent storage, ensuring state is maintained.
   - **Cross-platform**: ACI supports both **Linux** and **Windows** containers.

### 3. **ACI Use Cases**:
   - **Base building-block**: ACI is a simple solution for running containerized applications with **minimal orchestration**. It is ideal for simpler use cases but lacks the advanced features of services like **Azure Kubernetes Service (AKS)** or **Azure Container Apps**.
   - For **full container orchestration** (automatic scaling, service discovery, upgrades), **AKS** is recommended.
   - For **serverless, fully-managed container hosting**, **Azure Container Apps** is a better fit.

### 4. **Container Groups in ACI**:
   - **Container group** is the primary unit in ACI and can contain one or more containers.
   - **Shared resources**: All containers in a group share the same resources, such as CPU, memory, networking, and storage volumes.
   - **Lifecycle management**: Containers in a group share a common lifecycle, meaning they are started and stopped together.
   - **Port mapping**: Containers within a group can communicate with each other using **localhost** but cannot map individual ports externally. To expose a container externally, you need to expose the port both on the **IP address** and from the container itself.
   - **Multi-container groups**: These are useful when you want to split application functionality across multiple containers (e.g., separating front-end and back-end containers, or separating containers for logging and monitoring).

### 5. **Deploying Containers Using ACI**:
   - You can deploy **single-container** or **multi-container** groups using:
     - **Azure Resource Manager (ARM) templates** for more complex setups, especially when related services (like storage accounts) need to be deployed along with the container group.
     - **YAML files** for simpler, container-focused deployments.
   - **CPU and Memory Allocation**: ACI allocates resources based on the **requests** specified by each container within the group.
     - For example, if two containers request one CPU each, the container group will be allocated **two CPUs**.
   - **Restart Policies**:
     - **Always** (default): The container will restart continuously.
     - **Never**: The container will only run once.
     - **OnFailure**: The container will restart until it exits successfully.
   - **Environment Variables**: You can define environment variables for your container, with the option to use **secure environment variables** for sensitive data (similar to Docker's `--env` argument).
   - **Secrets management**: You can securely mount **secrets** using the `secrets-mount-path` parameter, ensuring sensitive data is stored securely.

### 6. **Mounting Persistent Storage**:
   - **Persistent storage**: ACI containers are **stateless** by default. To persist data, you need to mount a **file share** (e.g., from **Azure Files**) to a container.
   - **Linux containers** can mount file shares, with the container running as **root**.
   - For configurations requiring multiple mounts (e.g., mounting more than one file share), you should use **ARM templates** or **YAML files** instead of Azure CLI alone.

### 7. **Azure CLI and PowerShell Examples**:
   - **Azure CLI**: The `az container create` command is used to deploy a container instance. You provide details like resource group, container group name, image path, port assignments, and restart policies.
   - **PowerShell**: Similar to Azure CLI, PowerShell also allows for container creation with environment variables and restart policies.
   - **YAML Files**: You can reference YAML files for deployments, especially when needing to mount multiple volumes or for better automation and source control.

### 8. **Azure Portal**:
   - Once the container group is created, you can manage it via the **Azure Portal**. You can:
     - Start, stop, or restart containers.
     - Access monitoring tools for insights into container performance and health.
     - View detailed information about individual containers within the container group.

### 9. **Key Takeaways**:
   - **ACI** is a fast, lightweight container hosting service ideal for simple use cases, with fast startup, robust security, and resource optimization.
   - **Container groups** are the top-level construct in ACI and can contain one or more related containers, which share resources and lifecycle.
   - You can deploy containers using Azure CLI, PowerShell, ARM templates, or YAML files, with options for environment variables, secrets, and persistent storage.
   - For more complex scenarios, like full orchestration and automated scaling, consider **Azure Kubernetes Service (AKS)**, or for a fully-managed experience, **Azure Container Apps**.
   - The **Azure Portal** provides a convenient interface for managing container groups, including monitoring and troubleshooting.

## ACA - Azure Container Apps

Azure Container Apps is a serverless container service powered by Kubernetes, designed for microservices, event-driven apps, and long-running tasks. It abstracts the underlying infrastructure, making it suitable for scenarios requiring service discovery and traffic splitting. It differs from Azure Kubernetes Service (for more control) and Azure Container Instances (for simpler workloads).

### Key Features:
- **Serverless and Kubernetes-based**: It provides a fully managed service that handles scaling, failover, and OS upgrades.
- **Isolation with Environments**: Container Apps are deployed within an "environment," which offers shared virtual networks, logging, and resource management. Environments ensure isolation and manage app intercommunication.
- **Long-running and Background Tasks**: Suitable for tasks that need to run indefinitely or asynchronously, unlike typical short-lived container jobs.
- **Deployment**: Container Apps can be created using Azure CLI by registering the provider and using the `create` command with parameters like resource group, image path, target port, and ingress type (internal or external). It's crucial to follow the correct order of operations when creating resources.

### Secrets Management:
- **Managed Identity**: Since Container Apps don’t directly integrate with Azure Key Vault, managed identities are used to grant access to secrets stored in Key Vault, which is accessed via the Key Vault SDK.

### Scaling:
- **Scaling Rules**: Scaling can be configured in the Azure portal with rules such as HTTP (based on concurrent requests) or Azure Queue. Users can also define custom scaling conditions, and the environment supports automatic replica scaling.
- **Portal Interaction**: Scaling rules are configured via the "Edit and deploy" option in the portal, where users can adjust replica counts and set scaling conditions.

### Service Connectors:
- **Integration with Azure Services**: Azure Container Apps can connect to Azure services like Cosmos DB, Redis Cache, and Storage Queues using Service Connectors. Connections are established either via Azure CLI or through a guided portal experience. Service Connectors enable the integration of external services with containerized applications.
  
### Key Takeaways:
- **Serverless and Kubernetes-Powered**: Container Apps offer a serverless approach with Kubernetes-style management.
- **Environment-based Isolation**: Apps are grouped within environments for better resource management and isolation.
- **Secrets and Scaling Management**: Managed identities are used for secrets access, and scaling is configurable through predefined rules or custom conditions.
- **Service Connector Integration**: Facilitates easy connection with various Azure services for enhanced application functionality.

This overview illustrates how Azure Container Apps simplifies container management for complex, event-driven, and scalable applications, with integrated support for Azure services and flexible scaling options.