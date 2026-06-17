# Enterprise Incident Response Playbook Framework

This directory centralizes the standard operating procedures (SOPs) utilized across the `SOC-Analyst-Academy` case studies.

## 🛑 Tier-1 Containment & Remediation Matrix

| Incident Type | Initial Action | Triage & Eradication Command / Step |
| :--- | :--- | :--- |
| **Phishing Triage** | Host Isolation | Logically isolate endpoint via EDR console; revoke compromised session tokens. |
| **PowerShell Abuse** | Process Kill | Force-terminate anomalous process trees via PID handles. |
| **Account Discovery** | Session Termination | Invalid and kill active tokens originating from unauthorized network utility calls. |
| **Network Discovery** | Host Firewall Restriction | Block outbound broadcast and ICMP traffic at the local host level. |
| **Persistence Hooks** | Task & Registry Deletion | `schtasks /delete /tn "TaskName" /f`<br>`reg delete "HKLM\...Run" /v "Value" /f` |
| **Malware / LOLBins** | Binary Quarantine | Securely wipe or quarantine malicious payloads from world-writable directories (`\Public\`, `\Temp\`). |
| **Defense Evasion** | Volatile Memory Capture | Isolate host instantly to preserve memory artifacts before log deletion attempts can expand. |