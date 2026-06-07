**<ins>Phase 1 - VirtualBox NAT Network Setup<ins>**

**<ins>Objective<ins>**

Configure an isolated virtual network for all lab VMs to communicate securely without exposing the host machine.

**<ins>Tools Used<ins>**

- VirtualBox Version 7.2.8 r173730

**<ins>Network Configuration<ins>**

- Network Name → cyberlab

- Subnet → 192.168.100.0/24

- Gateway → 192.168.100.1

- DHCP → Disabled (static IPs per VM)

**<ins>Steps Taken<ins>**

1. Opened VirtualBox → Tools → Network Manager
2. Selected NAT Networks tab → clicked Create
3. Named network cyberlab with subnet 192.168.100.0/24
4. Applied settings

**<ins>Screenshots<ins>**

<img width="1920" height="1030" alt="image" src="https://github.com/user-attachments/assets/e42a665d-b41f-4979-a403-382834b22adc" />

**<ins>Key Takeaways<ins>**

This phase of the project provided my first hands-on experience with Oracle VirtualBox and virtual network administration. While I have previous experience working with VMware environments, this lab allowed me to become familiar with VirtualBox. Through configuring a NAT Network, I learned how to create an isolated environment where multiple virtual machines can communicate securely without exposing the lab directly to external networks. I also gained practical experience with network planning concepts such as subnetting, gateway configuration, and static IP addressing. Building this network established the foundation for future security monitoring, threat detection, and investigation activities within the lab while helping me develop a stronger understanding of how enterprise environments can be simulated in a home lab setting.
