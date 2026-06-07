**<ins>Phase 2 — Windows Server 2022 Setup<ins>**

**<ins>Objective<ins>**

Deploy and configure a Windows Server 2022 VM as the primary victim/log source machine with Active Directory, Sysmon, and enhanced audit logging enabled.

**<ins>Tools Used<ins>**

- Windows Server 2022 Evaluation (180-day free license)
- Sysmon v15 (Sysinternals)
- SwiftOnSecurity Sysmon Config

**<ins>VM Configuration<ins>**

- RAM → 4GB

- CPUS → 2

- Disk → 60GB(dynamic)

- IP Address → 192.168.100.20

- Hostname → LAB-DC01

- Domain → lab.local

- Network → cyberlab(NAT)

**<ins>Steps Taken<ins>**

1. VM Creation & OS Install

Created a new virtual machine in Oracle VirtualBox and allocated 4GB of RAM, 2 vCPUs, and a 60GB dynamically allocated virtual disk. Mounted the Windows Server 2022 Evaluation ISO and completed the operating system installation. After installation, applied system updates, configured the server name as LAB-DC01, and verified network connectivity within the lab environment.

2. Static IP Configuration

Configured a static IPv4 address to ensure consistent communication between lab systems. Assigned the server IP address 192.168.100.20/24 and configured the appropriate gateway and DNS settings for the lab network. Verified connectivity using basic network troubleshooting tools and confirmed the server could communicate with other devices on the cyberlab network.

3. Active Directory Setup

Installed the Active Directory Domain Services (AD DS) role through Server Manager and promoted the server to a domain controller. Created a new forest using the domain name lab.local and completed the domain controller configuration process. Verified successful deployment by logging into the newly created domain and confirming Active Directory services were operational.

4. Audit Policy & Logging Configuration
Enabled the following audit policies via Group Policy:

- Logon/Logoff
- Account Logon
- Process Creation
- Privilege Use

Enabled PowerShell Script Block Logging via registry.

5. Sysmon Installation

- Downloaded Sysmon from Sysinternals
- Applied SwiftOnSecurity config
- Verified service running

**<ins>Screenshots<ins>**

(insert screenshots here)

**<ins>Key Takeaways<ins>**

This phase introduced me to the process of deploying and configuring a Windows Server environment from the ground up. I gained hands-on experience creating and managing a Windows Server virtual machine, configuring static network settings, and deploying Active Directory Domain Services to establish a domain environment. Additionally, I learned the importance of centralized logging and auditing through the implementation of Sysmon and enhanced audit policies. These configurations provide a strong foundation for future phases of the lab involving user management, log analysis, threat detection, and security monitoring.
