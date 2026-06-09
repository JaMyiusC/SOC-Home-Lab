**<ins>Overview<ins>**

In this scenario I simulated a brute force attack against a Windows Server 2022 domain controller using Hydra from a Kali Linux attacker machine. The goal was to generate failed logon activity and detect it in Splunk as a SOC analyst would in a real environment.

**<ins>Environment<ins>**

**Role→Machine→IP**

Attacker → Kali Linux → 192.168.100.50

Victim → Windows Server 2022 → 192.168.100.20

SIEM → Splunk Enterprise → 192.168.100.20:8000

EDR → Wazuh → 192.168.100.4

**<ins>Attack Details<ins>**

- Tool Used: Hydra v9.7

- Protocol Targeted: RDP (Remote Desktop Protocol) — Port 3389

- Attack Type: Dictionary brute force

- Target Accounts: Administrator, admin, administrator

- Total Attempts: 30

- Result: No valid credentials found (detection was the goal)

**Command executed on Kali**: hydra -L ~/users.txt -P ~/passwords.txt rdp://192.168.100.20 -V -f

**<ins>Detection — Splunk (SIEM)<ins>**

Will continue documentation here tomorrow... 
