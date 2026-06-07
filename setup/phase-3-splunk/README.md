**<ins>Phase 3 — Splunk SIEM Setup<ins>**

**<ins>Objective<ins>**

Install and configure Splunk Enterprise (free tier) on Windows Server as the central SIEM for log aggregation, search, and detection.

**<ins>Tools Used<ins>**

- Splunk Enterprise (Free — 500MB/day)

**<ins>Configuration<ins>**

- Install location → C:\Program Files\Splunk
- Web → http://192.168.100.20:8000
- Index Name → windows_logs

**<ins>Log Sources Configured<ins>**

- Windows Security Event Log
- Windows System Event Log
- Windows Application Event Log
- Microsoft-Windows-Sysmon/Operational
- Microsoft-Windows-PowerShell/Operational

**<ins>Steps Taken<ins>**

1. Splunk Installation

Downloaded Splunk Enterprise and completed the installation on the Windows Server 2022 virtual machine. Configured administrative credentials, enabled Splunk services, and verified access to the web interface through the local management portal. After installation, confirmed that Splunk was operational and ready to receive log data.

2. Adding Log Sources

Configured Splunk to ingest Windows event logs and Sysmon telemetry for centralized monitoring. Created inputs for Security, System, and Application event logs, along with Microsoft-Windows-Sysmon/Operational and Microsoft-Windows-PowerShell/Operational logs. Assigned the appropriate source types and directed the data to the windows_logs index for analysis and searching.

3. Verifying Log Ingestion

Verified successful log ingestion by performing searches within Splunk and confirming that events from all configured log sources were being collected. Validated that Windows event logs, PowerShell logs, and Sysmon events were searchable and appearing in near real-time within the windows_logs index.


**<ins>Screenshots<ins>**

<img width="787" height="593" alt="Screenshot 2026-06-06 164120" src="https://github.com/user-attachments/assets/2677a21a-836f-4d12-8000-0c5284a16d6a" />

<img width="1023" height="775" alt="Screenshot 2026-06-06 190114" src="https://github.com/user-attachments/assets/d2322cf0-9205-4da7-9d09-d6e925ce2179" />

<img width="1025" height="726" alt="image" src="https://github.com/user-attachments/assets/b80c9304-e0ad-4fd6-a3a4-064ad266d554" />



**<ins>Issues Encountered<ins>**

During the initial configuration, log data was not appearing as expected because the index configuration was incorrect. After reviewing the data inputs and index assignments, I identified that the logs were being directed to the wrong destination. The issue was resolved by updating the input configuration to use the correct index and verifying that new events were being successfully ingested. This troubleshooting process reinforced the importance of validating index configurations before onboarding data sources.

**<ins>Key Takeaways<ins>**

This phase provided hands-on experience deploying and configuring a Security Information and Event Management (SIEM) platform within a home lab environment. I learned how centralized log collection improves visibility across systems and how multiple Windows log sources can be aggregated into a single platform for investigation and analysis. Additionally, I gained practical experience troubleshooting data ingestion issues, validating log pipelines, and performing searches to verify that security-relevant events were being captured correctly. This setup established the foundation for future threat detection, alerting, and incident investigation activities within the lab.
