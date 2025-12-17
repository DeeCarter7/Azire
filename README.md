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

****This setup mirrors how enterprise envirnments ensure availability and resilience for identity services****

## Architecture & Azure Resources
Azure Resource Group
![Azure Resource Group](images/azure-resource-group.png)

Virtual Network & Subnet
![Virtual Network & Subnet](images/VirtualNetwork.png)

Virtual Machines (DC01 & DC02)
![Virtual Machines DC01](images/DC01 VM Overview.png)
![Virtual Machines DC02](images/DC02 VM Overview.png)

## Domain Controller 1 (DC01) Setup
1. Virtual Machine Deployment
   - Deployed Windows Server VM named DC01
   - Assigned static private IP
   - Placed in Azure Virtual Network
WHY:
Domain Controllers require stable IP addresses for DNS and authentication services.

2. Install Active Directory Domain Services (AD DS)
   - Installed AD DS role via Server Manager
   - Accepted required features

3. Promoted DC01 to Domain Controller
   - Created new forest: corp.local
   - Installed DNS Server role
   - Enabled Global Catalog
   - Set DSRM password  
WHY:
This establishes the identity authority for the environment.

## Domain Controller 2 (DC02) Setup
1. Virtual Machine Deployment
   - Deployed Windows Server VM named DC02
   - Placed in same VNet/Subnet
   - Static private IP assigned

2. DNS Configuration (Critical Step)
DC02 initially could not detect the domain.
Fix:

Force DC01 to use DC01 for DNS, then joined the domain (corp.local) first, and then promoted

STEP 1: Fix DNS on DC02

Inside DC02 VM (not Azure Portal):

1. Press Windows + Run (Open Run)
2. Type ncpa.cpl
3. Right-click Ethernet
4. Click Properties
5. Double-Click Internet Protocol Version 4 (IPv4)
6. Set:
 - Preferred DNS Server > DC01 Private IP
 - Alternate DNS > (Leave Blank)

Click OK > Close

STEP 2: Restart DC02

Restart the VM.

DNS Changes will not fully apply until reboot

STEP 3: Join DC02 to the Domain first

I found that after updating the DNS, successfully pinging both DC01 and corp.local multiple times, and multiple failed attempts to promote DC02, this was the step that was missing.

On DC02: 

1. Open Server Manager
2. Click Local Server
3. Click the Computer Name
4. Click Change
5. Select Domain
6. Type: Corp.Local
7. When prompted for credentials, use DC01's credentials.
8. Restart when prompted

STEP 4: Promote DC02 to Domain Controller (Success)

After reboot:

1. Login as DC01 (DC01 Credentials)
2. Open Server Manager
3. Access AD DS on Dashboard
4. Click Promote this server to a domain controller
5: Select: Add a domain controller to an existing domain
6: Domain: corp.local

The domain was detected and auto-populated the credentials. On the next page, the sites list loaded ( I was also having an issue with that).

Currently still looking into root cause. Will update once I understand what happened. 

## Test OUS and Test Users
I created serveral Organizational Units (OUs) and a test user and ITAdmin.
![OUs and Test User](OUsandTestUser.png)

## Tools & Technologies
- Microsoft Azure
- Windows Server
- Active Directory Doamin Services (AD DS)
- DNS
- Azure Virtual Networking
- Powershell/Terminal

## Future Enhancements
- Add a domain-joined Windows Client
- Enabled advanced auditing
- Forward logs to a SIEM
- Simulate authentication attacks
  
## Key Skills Demonstrated
- Active Directory administration
- Azure VM and networking configuration
- DNS troubleshooting
- Domain controller promotion and replication
- Enterprise identity fundamentals

## Why This Lab Matters
Active Directory is a critical component of enterprise environments and a frequent target during cyber attacks. Understanding how AD is built, replicated, and managed is essential for SOC analysts, blue team members, and IT professionals. It documents not just what was built, but how challenges were identified and resolved, reflecting real-world troubleshooting and learning. 

## Documentation
See **Azure_Active_Directory_Lab.pdf** for a full step-by-step breakdown of what was built and why. 
