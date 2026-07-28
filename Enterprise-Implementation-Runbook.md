# AZ-500 Enterprise Implementation Runbook

# Lab 01: Secure Networking Using Network Security Groups (NSGs) and Application Security Groups (ASGs)

*Author:* Isioma Napoleon Peter

*Certification:* Microsoft Certified: Azure Security Engineer Associate (AZ-500)

*Cloud Platform:* Microsoft Azure

*Region:* East US

---

# Document Control

| Item | Value |
|------|-------|
| Document Type | Enterprise Implementation Runbook |
| Audience | Cloud Engineers, Security Engineers, Students |
| Objective | Deploy and secure a two-tier Azure environment using Network Security Groups (NSGs) and Application Security Groups (ASGs) |
| Lab Status | Completed |

---

# Executive Summary

This document provides a complete implementation guide for deploying a secure two-tier Microsoft Azure environment using Virtual Networks, Network Security Groups (NSGs), Application Security Groups (ASGs), and Virtual Machines.

The deployment demonstrates secure network segmentation, workload isolation, and controlled communication between the application tier and the database tier using Microsoft Azure security best practices.

---

# Business Scenario

An organisation is deploying a web application consisting of a public web server and a private database server.

To secure the environment:

- Internet users must access only the web server.
- The database server must never be exposed directly to the Internet.
- SQL traffic must be allowed only from the web server.
- Firewall rules should reference workloads instead of IP addresses whenever possible.

---

# Solution Architecture



                     Internet
                         │
                 HTTP (80) / HTTPS (443)
                         │
                  nsg-frontend
                         │
                 FrontendSubnet
                  10.0.2.0/24
                         │
                     VM-WEB
                  App-SGs-Web
                         │
                     TCP 1433
                         │
                  nsg-backend
                         │
                 BackendSubnet
                  10.0.3.0/24
                         │
                     VM-DB
                  App-SGs-DB



---

# 1. Create the Resource Group

## Objective

Create a logical container that will contain every Azure resource used throughout this deployment.

### Navigation

Azure Portal

→ Resource Groups

→ Create

### Configuration

| Setting | Value |
|---------|-------|
| Resource Group | rg-secure-networking |
| Region | East US |

Click *Review + Create*.

Click *Create*.

Wait until Azure reports that the deployment completed successfully.

### Screenshot

![Create Resource Group](images/AZURE-Create_resource_group.png)

### Validation

Verify that:

- Resource Group = *rg-secure-networking*
- Provisioning State = *Succeeded*

---

# 2. Create the Virtual Network

## Objective

Create the Azure Virtual Network that will host both application tiers.

### Navigation

Azure Portal

→ Resource Groups

→ rg-secure-networking

→ Create

→ Virtual Network

### Configuration

| Setting | Value |
|---------|-------|
| Name | secure-network-vnet |
| Region | East US |
| Address Space | 10.0.0.0/16 |

Create the following subnets:

| Subnet | Address Range |
|---------|---------------|
| FrontendSubnet | 10.0.2.0/24 |
| BackendSubnet | 10.0.3.0/24 |

Click *Review + Create*.

Click *Create*.

### Screenshot

![Create Virtual Network](images/AZURE_Create_VNET.png)

### Screenshot

![Backend Subnet](images/AZURE_Add_subnet.png)

### Validation

Verify:

- secure-network-vnet exists.
- FrontendSubnet exists.
- BackendSubnet exists.

### Screenshot

![Virtual Network Created](images/AZURE_Created_VNET.png)
