**Phase 1 — VirtualBox NAT Network Setup**

**Objective**
Configure an isolated virtual network for all lab VMs to communicate securely without exposing the host machine.

**Tools Used**
VirtualBox Version 7.2.8 r173730

**Network Configuration**
Network Name → cyberlab
Subnet → 192.168.100.0/24
Gateway → 192.168.100.1
DHCP → Disabled (static IPs per VM)

**Steps Taken**
1. Opened VirtualBox → Tools → Network Manager
2. Selected NAT Networks tab → clicked Create
3. Named network cyberlab with subnet 192.168.100.0/24
4. Applied settings

**Screenshots**

**Key Takeaways**
