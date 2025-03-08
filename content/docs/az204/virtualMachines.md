---
title: Virtual Machines
type: docs
weight: 1
prev: docs/az204/
next: docs/az204/implementContainerizedSolutions
---

1. **Microsoft Shared Responsibility Model**:
   - Defines the division of responsibilities between Microsoft and the customer across service categories: On-premises, Infrastructure as a Service (IaaS), Platform as a Service (PaaS), and Software as a Service (SaaS).
   - In IaaS (which includes virtual machines), Microsoft manages the physical layer, but the customer is responsible for the operating system, network controls, and other aspects.

2. **Virtual Machines**:
   - Virtual machines (VMs) are part of IaaS, with multiple configuration options including different sizes (small for testing or large for machine learning) and prebuilt images (e.g., Microsoft SQL Server).
   - Custom images can also be used for VM deployment.
   - Deploying VMs through the Azure portal provides insights into required and optional deployment elements, which can also be replicated through code-based deployment.

3. **Code Deployment**:
   - **Imperative Code**: Specifies step-by-step instructions to create resources (e.g., using Azure CLI or PowerShell). It’s intuitive but less flexible.
   - **Declarative Code**: Describes the desired end state, and Azure ensures the infrastructure meets that state. It’s idempotent (the same result no matter how many times executed).
     - **Azure CLI and PowerShell** (imperative code)
     - **ARM Templates and Bicep** (declarative code, specific to Azure)
     - **Terraform**: Multi-cloud option for declarative code, uses HCL.
     - **Ansible**: Uses YAML for declarative code but is a Python-based tool.

4. **VM Deployment Example**:
   - Using the Azure CLI (imperative) to create a VM involves specifying resource groups, VM names, and configurations.
   - Bicep (declarative) provides a cleaner syntax for VM metadata, operating system profile, and storage configuration.

5. **Tools and Languages**:
   - Bicep: A simplified syntax for Azure resource deployment, compared to JSON in ARM templates.
   - Terraform: A multi-cloud declarative tool using HCL.
   - Ansible: A tool using YAML for declarative configuration but based on Python.

This summary covers the important points about Azure VM configurations, deployment methods, and code approaches for the AZ-204 exam.