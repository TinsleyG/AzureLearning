---
title: Implement Containerized Solutions
type: docs
weight: 2
prev: docs/az204/virtualMachines
next: docs/az204/azureCosmosDb
---


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

In summary, this segment covers how to store, manage, and automate containerized code in Azure using **ACR**, **Docker CLI**, **Dockerfiles**, and **ACR Tasks**, with a focus on Azure CLI commands, Docker commands, and container service tiers.