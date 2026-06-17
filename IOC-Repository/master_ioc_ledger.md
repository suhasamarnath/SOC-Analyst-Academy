# Centralized Indicators of Compromise (IOC) Repository

This master ledger tracks hostile artifacts, malicious network infrastructure, and rogue processes uncovered during active incident triage.

## 📓 Global Threat Intelligence Ledger

| Incident Context | Indicator Type | Value / Observable | Threat Context / Scope |
| :--- | :--- | :--- | :--- |
| **INC-001** | URL / Domain | `http://legit-banking-update.com/login` | Phishing Landing Page Credential Harvester |
| **INC-002** | Command String | `powershell.exe -nop -w hidden -c...` | Malicious obfuscated download cradle |
| **INC-003** | Command String | `powershell.exe -EncodedCommand...` | Base64 encoded payload hiding execution string |
| **INC-005** | IP Address | `192.168.1.1` | Network scan gateway confirmation check |
| **INC-006** | Task Object | `Microsoft\Windows\UpdateService` | Persistence via masqueraded Scheduled Task |
| **INC-007** | Registry Key | `HKLM\...Run\SecurityUpdate` | Persistence via malicious Registry Run value |
| **INC-008** | IP Address | `104.244.42.1` | External staging server delivering malware payloads |
| **INC-009** | Executable Path | `C:\Users\Public\malware.exe` | Untrusted background binary staging location |