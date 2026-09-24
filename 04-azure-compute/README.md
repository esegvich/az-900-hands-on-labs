# Section 4: Azure Compute Options

## 📋 Lab Overview

This lab provided hands-on experience exploring Azure compute options, Virtual Machine configuration, pricing, optimization, and cost management.

The lab focused on planning Azure infrastructure before deployment rather than actually deploying a Virtual Machine. The exercises included configuring a resource group, exploring VM settings, comparing VM pricing, reviewing Azure Advisor, comparing compute services, and exploring Cost Management.

## 🎯 Learning Objectives

- Explore Azure Virtual Machine configuration options
- Configure resource groups and resource tags
- Compare VM sizes and pricing
- Explore Azure Advisor recommendations
- Compare IaaS, PaaS, and serverless compute services
- Explore Azure Cost Management
- Understand Azure tag inheritance
- Understand Azure VM sizing and SLA concepts

---

# 1. Create a Resource Group with Tags

## Overview

I created a resource group for the CloudFirst Retail development environment and applied tags for organization and cost tracking.

### Resource Group Configuration

| Setting | Value |
|---|---|
| Resource Group | `rg-cloudfirst-dev` |
| Region | East US |
| Environment | Development |
| Project | CloudFirst-Retail |
| CostCenter | IT-Development |

### Tags

- `Environment = Development`
- `Project = CloudFirst-Retail`
- `CostCenter = IT-Development`

## Screenshots

<!-- Add screenshot here -->

## Key Takeaway

Azure tags are metadata that can be used to organize resources and track costs.

**Important AZ-900 concept:** Tags do not automatically inherit from a resource group to the resources inside it. Tags must be applied to the individual resource or enforced through Azure Policy.

---

# 2. Explore Virtual Machine Configuration

## Overview

I explored the configuration process for an Azure Virtual Machine without actually deploying it. This allowed me to examine VM sizing, storage, networking, security, management, monitoring, and cost considerations without incurring deployment costs.

## VM Configuration

| Setting | Value |
|---|---|
| VM Name | `vm-cloudfirst-dev` |
| Region | East US |
| Image | Ubuntu Server 24.04 LTS |
| VM Size | B1s |
| vCPU | 1 |
| RAM | 1 GiB |
| Authentication | Password |
| Username | `azureuser` |
| Inbound Port | SSH (22) |
| OS Disk | Standard SSD |

## VM Size

The B1s VM is part of the **B-series**, which is designed for burstable and cost-effective workloads.

- B-series → Burstable
- 1 → 1 vCPU
- `s` → Standard

## Storage Options

I explored the available OS disk types:

| Disk Type | General Characteristics |
|---|---|
| Standard HDD | Lowest cost, lowest performance |
| Standard SSD | Balanced cost and performance |
| Premium SSD | Higher performance and 99.9% SLA for a single-instance VM |

For this development environment, I selected **Standard SSD**.

## Networking

Azure automatically configured several supporting resources for the VM:

- Virtual Network
- Subnet
- Network Interface
- Public IP
- Network Security Group

The VM was configured to allow **SSH (port 22)**.

### Security Consideration

Opening SSH directly to the internet can increase exposure. In a production environment, access could instead be restricted by source IP or use Azure Bastion.

## Management & Monitoring

I explored:

- Microsoft Defender for Cloud
- Managed Identity
- Microsoft Entra ID login
- Auto-shutdown
- Azure Backup
- Guest OS updates
- Boot diagnostics
- OS guest diagnostics

## Screenshots

<!-- Add VM Basics screenshot -->

<!-- Add VM Size screenshot -->

<!-- Add Disk screenshot -->

<!-- Add Networking screenshot -->

<!-- Add Management screenshot -->

<!-- Add Monitoring screenshot -->

## Key Takeaways

- Azure VMs are an **IaaS** service.
- VM configuration affects both performance and cost.
- Azure automatically creates several supporting resources when configuring a VM.
- Development environments can use smaller, less expensive VM sizes.
- VM configuration should be planned before deployment.

---

# 3. Compare VM Sizes & Pricing

## Overview

I used the **Azure Pricing Calculator** to compare different VM sizes and understand how VM specifications affect cost.

## VM Comparison

| VM | vCPU | RAM | Example Use |
|---|---:|---:|---|
| B1s | 1 | 1 GiB | Development / variable workloads |
| D2s v3 | 2 | 8 GiB | General-purpose workloads |
| E2s v3 | 2 | 16 GiB | Memory-intensive workloads |

### Pricing Options

I also explored different purchasing options:

- Pay-as-you-go
- 1-year reserved
- 3-year reserved

Reserved pricing can reduce costs for workloads that are expected to run consistently.

## Screenshots

<!-- Add Pricing Calculator screenshot -->

<!-- Add VM comparison screenshot -->

## Key Takeaway

The Azure Pricing Calculator can be used to estimate costs **before deploying resources** and compare different configurations.

### VM Families

- **B-series:** Burstable
- **D-series:** General purpose
- **E-series:** Memory optimized
- **F-series:** Compute optimized
- **M-series:** Very large memory configurations

---

# 4. Explore Azure Advisor

## Overview

I explored **Azure Advisor**, which provides recommendations for optimizing Azure resources.

Azure Advisor organizes recommendations into five categories:

1. Cost
2. Security
3. Reliability
4. Operational Excellence
5. Performance

## What I Observed

Because this was a new environment with little or no resource usage, there were few or no recommendations available.

This is expected because Advisor needs usage data before it can provide meaningful recommendations.

## Screenshots

<!-- Add Azure Advisor screenshot -->

## Key Takeaway

Azure Advisor provides ongoing recommendations to help optimize Azure resources across cost, security, reliability, operational excellence, and performance.

---

# 5. Compare Azure Compute Services

## Overview

I explored three different Azure compute models:

- Virtual Machines
- Azure App Service
- Azure Functions

These services represent different levels of management responsibility.

## Compute Comparison

| Service | Model | Management | Best For |
|---|---|---|---|
| Virtual Machines | IaaS | High | Full OS control and legacy applications |
| App Service | PaaS | Medium | Web applications and APIs |
| Azure Functions | Serverless | Minimal | Event-driven code |

## Virtual Machines — IaaS

Virtual Machines provide the most control but require more management.

I am responsible for:

- Operating system
- Patches
- Applications
- Data
- Network configuration

Azure manages the underlying physical infrastructure.

## App Service — PaaS

App Service provides a managed platform for web applications and APIs.

Azure manages:

- Operating system
- Runtime
- Patching
- Infrastructure

I primarily manage:

- Applications
- Data

## Azure Functions — Serverless

Azure Functions is designed for event-driven workloads.

The developer primarily provides the code while Azure handles the underlying infrastructure, scaling, and runtime.

## Screenshots

<!-- Add App Service screenshot -->

<!-- Add Azure Functions screenshot -->

## Key Takeaway

The general relationship between these services is:

**More control → More management**

**Less management → Less control**

---

# 6. Review Azure Cost Management

## Overview

I explored Azure Cost Management + Billing to understand how Azure spending can be monitored and analyzed.

## Cost Analysis

I explored:

- Month-to-date costs
- Last 30 days
- Custom date ranges
- Accumulated costs
- Grouping by resource type
- Grouping by tags
- Cost filters

## Cost Tracking with Tags

I explored how tags can be used to analyze costs by:

- Environment
- Project
- Cost Center

## Budgets

Azure Cost Management allows budgets and spending alerts to be configured at different thresholds, such as:

- 50%
- 75%
- 90%
- 100%

## Screenshots

<!-- Add Cost Management screenshot -->

<!-- Add Cost Analysis screenshot -->

<!-- Add Budget screenshot if applicable -->

## Key Takeaway

Cost Management helps provide visibility and control over Azure spending.

---

# 🧹 Cleanup

Because I did not deploy the Virtual Machine, there were no running VM resources to clean up.

I removed the resource group:

`rg-cloudfirst-dev`

This ensured that the resources created during the lab were cleaned up.

---

# 🧠 Key AZ-900 Takeaways

## VM Sizing

| Series | Purpose |
|---|---|
| B | Burstable workloads |
| D | General-purpose workloads |
| E | Memory-optimized workloads |
| F | Compute-optimized workloads |
| M | Large memory workloads |

## Compute Services

| Requirement | Azure Service |
|---|---|
| Full OS control | Virtual Machine |
| Legacy application | Virtual Machine |
| Web application / API | App Service |
| Minimal management | App Service |
| Event-driven code | Azure Functions |
| Pay per execution | Azure Functions |

## Cost Tools

| Tool | Purpose |
|---|---|
| Pricing Calculator | Estimate costs before deployment |
| Azure Advisor | Optimization recommendations |
| Cost Management | Analyze actual Azure spending |
| TCO Calculator | Compare on-premises and Azure costs |

## Tagging

**Tags are name-value pairs used for organization and cost tracking.**

Important:

> Tags do NOT automatically inherit from resource groups.

---

# 📸 Lab Screenshots

Screenshots from this lab are included throughout the sections above to document the configurations and Azure services I explored.

---

# 📚 Resources

- Microsoft Azure Portal
- Azure Pricing Calculator
- Microsoft Azure Fundamentals (AZ-900) Hands-On Lab Guide

---

**Course:** Microsoft Azure Fundamentals (AZ-900)  
**Section:** 4 — Azure Compute Options  
**Status:** Completed