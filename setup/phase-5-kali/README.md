**<ins>Phase 5 — Kali Linux Attacker Machine<ins>**

**<ins>Objective<ins>**

Deploy a Kali Linux VM as the attacker machine to simulate real-world threats against the Windows Server victim machine.

**<ins>Tools Used<ins>**

- Kali Linux (latest)

**<ins> VM Configuration<ins>**

- RAM → 2GB
- CPUS → 2
- Disk → 40GB(dynamic)
- IP Address → 192.168.100.50
- Network → cyberlab(NAT)

**<ins>Key Attack Tools Available<ins>**

- Nmap → Network reconnaissance
- Metasploit → Exploitation framework
- Hydra → Brute force attacks
- Responser → Credential harvesting
- CrackMapExec → Lateral movement

**<ins>Steps Taken<ins>**

1. VM Creation & OS Install

Created a new virtual machine in Oracle VirtualBox and allocated 2GB of RAM, 2 vCPUs, and a 40GB dynamically allocated virtual disk. Mounted the latest Kali Linux ISO and completed the operating system installation. After installation, performed initial system configuration and verified network connectivity within the lab environment.

2. Static IP Configuration

Configured a static IPv4 address to ensure consistent communication between the attacker machine and other systems within the cyberlab network. Assigned the IP address 192.168.100.50 and verified connectivity to the Windows Server and other lab components. This configuration provided a stable platform for conducting security testing and attack simulations.

3. Tool Verification & Updates

Updated the operating system and installed package repositories to ensure all tools were operating with the latest available versions. Verified the functionality of commonly used offensive security tools, including Nmap, Metasploit, Hydra, Responder, and CrackMapExec. Confirmed that each tool launched successfully and was ready for use during future attack simulations and detection testing.


**<ins>Screenshots<ins>**

<img width="591" height="692" alt="image" src="https://github.com/user-attachments/assets/aabf2c81-6203-43b5-a20d-aed7ed4d6e3b" />

<img width="806" height="615" alt="Screenshot 2026-06-06 230636" src="https://github.com/user-attachments/assets/74328fad-d828-451e-a132-a085899e02c4" />

<img width="1912" height="1044" alt="Screenshot 2026-06-07 091209" src="https://github.com/user-attachments/assets/cefe2179-a49f-4042-a466-8c6e90e32c42" />

<img width="1919" height="1031" alt="Screenshot 2026-06-07 091829" src="https://github.com/user-attachments/assets/632161c8-3b0e-4767-9abc-648e421677fd" />

**<ins>Key Takeaways<ins>**

This phase provided hands-on experience deploying and configuring a dedicated attacker workstation for cybersecurity testing. I gained a better understanding of how offensive security tools can be used to simulate real-world attack activity within a controlled environment. Configuring the Kali Linux system and validating commonly used reconnaissance, exploitation, and credential access tools helped establish a realistic source of adversary activity for future lab exercises. This machine will serve as the primary platform for generating attack telemetry, validating detections, and testing incident response workflows throughout the remainder of the project.
