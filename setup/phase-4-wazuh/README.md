**<ins>Phase 4 — Wazuh EDR Setup<ins>**

**<ins>Objective<ins>**

Deploy Wazuh as the EDR solution to monitor endpoint activity, detect suspicious behavior, and complement Splunk's network-level visibility with host-level detection.

**<ins>Tools Used<ins>**

- Wazuh OVA (pre-built virtual appliance)

**<ins> VM Configuration<ins>**

- RAM → 4GB
- CPUS → 2
- IP Address → 192.168.100.4
- Web UI → https://192.168.100.4
- Network → cyberlab(NAT)

**<ins>Steps Taken<ins>**

1. OVA Import into VirtualBox

Downloaded the Wazuh virtual appliance and imported the OVA file into Oracle VirtualBox. Reviewed the appliance settings and allocated 4GB of RAM and 2 vCPUs to ensure sufficient resources for monitoring and analysis. After deployment, verified that the virtual machine booted successfully and that all core Wazuh components were installed.

2. Network Configuration

Configured the Wazuh virtual machine to use the existing cyberlab NAT network and assigned it a static IP address of 192.168.100.4. Verified network connectivity between the Wazuh server and other lab systems, ensuring the platform could communicate with monitored endpoints and provide access to the web management interface.

3. Wazuh Agent Install on Windows Server

Installed the Wazuh agent on the Windows Server 2022 system and configured it to communicate with the Wazuh manager. Registered the endpoint with the server and verified that telemetry data was being collected from the host. This enabled centralized monitoring of system activity and security events from the Windows environment.

4. Verifying Agent Connection

Confirmed successful agent registration through the Wazuh dashboard and verified that the Windows Server endpoint was actively reporting data. Reviewed collected events and ensured that monitoring capabilities such as file integrity monitoring, registry monitoring, vulnerability detection, and security event collection were functioning as expected.

Wazuh Monitoring Capabilities Enabled

- File integrity monitoring
- Registry change detection
- Rootkit detection
- Vulnerability scanning
- Malware detection (YARA rules)

**<ins>Screenshots<ins>**

<img width="592" height="700" alt="image" src="https://github.com/user-attachments/assets/4fc3c63b-f637-4e80-b9eb-b0b8587484da" />

<img width="804" height="606" alt="image" src="https://github.com/user-attachments/assets/00019227-15a8-4d44-9f60-d44d2b095bf2" />

<img width="1029" height="773" alt="Screenshot 2026-06-06 224315" src="https://github.com/user-attachments/assets/7af9fc0b-aa8f-436d-a23f-fcc9c8a06d30" />

<img width="1027" height="769" alt="Screenshot 2026-06-06 224455" src="https://github.com/user-attachments/assets/55ec0988-37a2-4800-98d5-a41b24ba8a26" />

<img width="1021" height="770" alt="Screenshot 2026-06-06 224703" src="https://github.com/user-attachments/assets/7acc129a-f4e8-4264-a3dd-f69844785ffd" />


**<ins>Issues Encountered<ins>**

After shutting down and later restarting the Wazuh virtual machine, the web dashboard became inaccessible and displayed API connection errors when accessed from the Windows Server. Upon investigation, I discovered that several Wazuh services had not automatically started during the boot process. The issue was resolved by manually starting the Wazuh Manager, Indexer, and Dashboard services using systemctl commands within the Wazuh appliance. After verifying the services were running and allowing time for initialization, connectivity to the dashboard was restored. To prevent the issue from occurring again, I configured the Wazuh services to start automatically whenever the virtual machine boots. This troubleshooting exercise provided valuable experience diagnosing service availability issues within a Linux-based security platform.

**<ins>Key Takeaways<ins>**

This phase provided hands-on experience deploying and managing an Endpoint Detection and Response (EDR) platform within a cybersecurity lab environment. I learned how host-based monitoring complements centralized log collection by providing deeper visibility into endpoint activity, file changes, system modifications, and potential security threats. Additionally, I gained experience deploying agents, validating endpoint connectivity, and monitoring security telemetry from managed systems. Troubleshooting the service startup issue also strengthened my understanding of Linux service management and highlighted the importance of ensuring critical security services are configured to start automatically after system reboots. Together, these skills expanded my understanding of endpoint monitoring and layered defensive security practices.
