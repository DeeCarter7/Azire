# Azure Active Directory Lab

## Overview
This project documents the deployment of a Windows Active Directory Domain Services (AD DS) environment hosted in Microsoft Azure. The lab simulates a real-world enterprise identity infrastructure using multiple domain controllers and DNS.

The purpose of this lab was to:
- Understand how Active Directory works in practive
- Learn why DNS is critical for practice
- Practice troubleshooting real AD issues
- Build a SOC-relevant lab suitable for Github and resumes

## Objectives
- Deploy Windows Server virtual machines in Azure
- Install and configure Active Directory Domain Services (AD DS)
- Create a new AD forest and domain
- Promote a second domain controller for redundancy
- Configure DNS and validate AD replication
- Create Organizational Units and user accounts

## Architecture
- Azure Resource Group
- Azure Virtual Network & Subnet
- Two Windows Server Domain Controllers
    - DC01 - Primary Domain Controller + DNS
    - DC02 - Secondary Domain Controller (Redundancy)
- AD DS with DNS and Global Catalog enabled
- Multi–Availability Zone deployment

  This setup mirrors how enterprise envirnments ensure availability and resilience for identity services

## Architecture & Azure Resources
![Azure Resource Group](images/azure-resource-group.png)
![Virtual Network & Subnet](images/VirtualNetwork.png)
Virtual Machines (DC01 & DC02)


## Key Skills Demonstrated
- Active Directory administration
- Azure VM and networking configuration
- DNS troubleshooting
- Domain controller promotion and replication
- Enterprise identity fundamentals

## Why This Lab Matters
Active Directory is a critical component of enterprise environments and a frequent target during cyber attacks. Understanding how AD is built, replicated, and managed is essential for SOC analysts, blue team members, and IT professionals.

## Documentation
See **Azure_Active_Directory_Lab.pdf** for a full step-by-step breakdown of what was built and why. 
