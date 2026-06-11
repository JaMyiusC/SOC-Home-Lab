**<ins>Overview</ins>**

In this scenario I simulated a credential harvesting attack using Responder on Kali Linux to perform LLMNR/NBT-NS poisoning against the Windows Server 2022 victim machine. The goal was to capture NTLM hashes by intercepting authentication requests and observe how this attack appears from a defender's perspective.

**<ins>Environment:</ins>**  (Role → Machine → IP)

Attacker→Kali Linux→192.168.100.50

Victim→Windows Server 2022 (LAB-DC01)→192.168.100.20

SIEM→Splunk Enterprise→192.168.100.20:8000

EDR→Wazuh→192.168.100.4

**<ins>What is LLMNR/NBT-NS Poisoning?</ins>**

LLMNR (Link-Local Multicast Name Resolution) and NBT-NS (NetBIOS Name Service) are Windows protocols used to resolve hostnames when DNS fails. When a machine tries to reach a hostname that doesn't exist, it broadcasts a request to the entire network asking "does anyone know where FAKESERVER is?"

Responder intercepts that broadcast and responds "I'm FAKESERVER!" Windows then automatically tries to authenticate with the attacker machine, sending its NTLMv2 hash in the process. The attacker captures the hash without the user typing a single credential.

This is one of the most common attack techniques in real enterprise environments and is why LLMNR and NBT-NS should be disabled in every organization.

**<ins>Attack Details</ins>**

- Tool Used: Responder

- Attack Type: LLMNR/NBT-NS Poisoning - Credential Harvesting

- Target: Windows Server 2022 (LAB-DC01) - 192.168.100.20

- Protocol Poisoned: LLMNR, NBT-NS, MDNS

- Credentials Captured: NTLMv2 Hash - LAB\Administrator

(Will continue documentation from this point...)
