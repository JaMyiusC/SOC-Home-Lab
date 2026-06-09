**<ins>Overview<ins>**

In this scenario I simulated a brute force attack against a Windows Server 2022 domain controller using Hydra from a Kali Linux attacker machine. The goal was to generate failed logon activity and detect it in Splunk as a SOC analyst would in a real environment.

**<ins>Environment:<ins>**  **(Role→Machine→IP)**

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

**Search Query Used:** index=windows_logs EventCode=4625

**What Was Detected**

Splunk immediately began ingesting EventCode 4625 (Failed Logon) events from **LAB-DC01** in real time as the attack was running.

**<ins>Key fields extracted from the event:<ins>** **(Field→Value)** 

EventCode → 4625 - An acouunt failed to log on

Account Name → admin

Workstation Name → kali-attacker

Source Network Address → 192.168.100.50 

Logon Type → 3(Network logon)

Failure Reason → Unknown user name or bad password

Authentication Package → NTLM

Status Code → 0xC000006D

Sub Status → 0xC0000064

**<ins>Analyst Observations<ins>**
- Multiple failed logon events appeared within seconds of the attack starting
- Source IP 192.168.100.50 (Kali) was clearly visible in the Network Information field
- Logon Type 3 indicates a remote/network-based authentication attempt — not local
- NTLM authentication package used — consistent with RDP brute force behavior
- The attacker machine hostname kali-attacker was captured, however a real attacker would likely spoof this

**<ins>Splunk Searches & Findings<ins>**
-Failed logons by source: index=windows_logs EventCode=4625 | table _time, Source_Network_Address, Account_Name, host
-Failed logons by account: index=windows_logs EventCode=4625 | stats count by Account_Name | sort -count
-Check for successful logon following failures: index=windows_logs (EventCode=4624 OR EventCode=4625) | table _time, EventCode, Account_Name, Source_Network_Address

**<ins>MITRE ATT&CK Mapping:<ins>** **(Tactic→Technique→ID)**

Credential Access→Brute Force→T1110

Credential Access→Password Guessing→T1110.001

Initial Access→Valid Accounts→T1078

**<ins>Key Event ID's Referenced:<ins>** **(EventID→Description→Where)**

4625→Failed logon attempt→Windows Security Log

4624→Successful logon attempt→Windows Security Log

4648→Logon attempt with explicit credentials→Windows Security Log

**<ins>Timeline:<ins>** **(Time→Event)

- 21:13:23→Hydra launched from Kali (192.168.100.50)
- 21:13:23→First EventCode 4625 detected in Splunk\
- 21:13:34→Hydra completed 30 attempts - no valid credentials found
- 21:13:34→All failed logon events visible in Splunk

**<ins>Containment & Mitigation Recommendations<ins>**

As a SOC analyst responding to this alert I would reccomend the following:

1. Block the source IP - immediately block 192.168.100.50 at the firewall level
2. Lock the targeted accounts - temporarily lock admin and Administrator accounts pending investigation
3. Enable Account Lockout Policy - configure GPO to lock accounts after 5 failed attempts within 30 minutes
4. Disable NTLM where possible - enforce NTLMv2 or move to Kerberos-only authentication
5. Restrict RDP access - limit RDP to specific trusted IPs only, disable for all others
6. Enable MFA on RDP - implement multi-factor authentication for all remote desktop access
7. Alert rule - create a Splunk alert that triggers when more than 5 EventCode 4625 events occur from the same source IP within 5 minutes

**<ins>Dectection Rule (Splunk Alert)<ins>**

To automate detection of future brute force attempts, save this an alert in Spunk: 

index=windows_logs EventCode=4625
| stats count by src_ip, user
| where count > 5
| table src_ip, user, count

**Alert settings:**
- Run every: 5 minutes
- Trigger when: number of results > 0
- Action: Send email / log to notable events

**<ins>Lessons Learned<ins>**
- Logon Type 3 is a key indicator of network-based authentication — important to distinguish from interactive logons (Type 2)
- NTLM authentication in a modern environment is a red flag — most enterprise environments should be using Kerberos
- The attacker's hostname was captured in the log — in a real investigation this would be pivoted on immediately
- Speed of detection — Splunk captured the first failed logon within milliseconds of the attack starting, showing the value of real-time SIEM monitoring
- Without an account lockout policy configured, a brute force attack can run indefinitely — this is a critical hardening gap

**<ins>Screenshots<ins>**

<img width="1025" height="729" alt="Screenshot 2026-06-08 210808" src="https://github.com/user-attachments/assets/d6f889b3-b0b5-4c82-b293-560fa3c96ff9" />

<img width="1917" height="1072" alt="image" src="https://github.com/user-attachments/assets/28245813-8bd4-466d-866b-17f2430498c0" />

<img width="1919" height="1069" alt="Screenshot 2026-06-08 211136" src="https://github.com/user-attachments/assets/16e465c7-89af-4935-b7c0-bd62602f5438" />

<img width="953" height="1054" alt="Screenshot 2026-06-08 211314" src="https://github.com/user-attachments/assets/16da6b84-d79b-4f63-bdbd-f40018a318d6" />

<img width="1028" height="731" alt="Screenshot 2026-06-08 211554" src="https://github.com/user-attachments/assets/e3b910b5-c063-4026-a02e-03d60a89afef" />

<img width="1025" height="732" alt="Screenshot 2026-06-08 212444" src="https://github.com/user-attachments/assets/d9cb7162-5443-4bc1-a36f-58744306366f" />

<img width="1026" height="730" alt="image" src="https://github.com/user-attachments/assets/54aaa930-3df2-4544-b294-1a9902b3400b" />

<img width="1023" height="726" alt="Screenshot 2026-06-09 084952" src="https://github.com/user-attachments/assets/6908b4af-d641-44da-8534-2244a62c680e" />

<img width="1023" height="727" alt="image" src="https://github.com/user-attachments/assets/9f5aba93-bc3d-4fbe-a850-27b1ab15edfd" />










