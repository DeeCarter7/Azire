# Azure Active Directory Lab

## Overview
This lab demonstrates the deployment of an enterprise-style Active Directory environment using Microsoft Azure. The project focuses on identity management, DNS, redundancy, and domain controller replication.

## Objectives
- Deploy Windows Server virtual machines in Azure
- Install and configure Active Directory Domain Services (AD DS)
- Create a new AD forest and domain
- Promote a second domain controller for redundancy
- Configure DNS and validate AD replication
- Create Organizational Units and user accounts

## Architecture
- Azure Virtual Network
- Two Windows Server Domain Controllers (DC01, DC02)
- AD DS with DNS and Global Catalog enabled
- Multi–Availability Zone deployment

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
