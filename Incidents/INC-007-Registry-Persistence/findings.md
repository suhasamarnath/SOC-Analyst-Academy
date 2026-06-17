# INC-007: Registry Run Key Persistence Analysis

### 🛡️ Triage Summary
On 2026-06-17, an active endpoint alert flagged an unauthorized modification to the Windows Registry initialization keys (Event ID 4688). The adversary executed the native `reg.exe` utility with elevated system privileges to plant a startup autorun execution hook disguised as a routine security component.

### 🔍 Indicators of Compromise (IOCs)
| Indicator Type | Value / Parameters | Context / Purpose |
| :--- | :--- | :--- |
| **Process Name** | `reg.exe` (PID: 9512) | Native registry manipulation utility |
| **Target Registry Path**| `HKLM\Software\Microsoft\Windows\CurrentVersion\Run` | Registry subkey that forces programs to run automatically at user logon |
| **Value Name (`/v`)** | `SecurityUpdate` | Masquerading technique to evade detection by system administrators |
| **Target Payload (`/d`)**| `C:\Users\Public\update.exe` | Staged malicious binary executed upon boot |

### 🛑 Containment & Remediation Playbook
1. **Registry Remediation:** Executed a mandatory removal command (`reg delete "HKLM\Software\Microsoft\Windows\CurrentVersion\Run" /v "SecurityUpdate" /f`) to kill the autorun configuration.
2. **Binary Eradication:** Deleted and wiped the persistent artifact file located at `C:\Users\Public\update.exe`.
3. **Boot Scan Deployment:** Triggered an EDR aggressive aggressive boot-time scan on the machine to confirm no additional deep-level persistence wrappers were loaded.

### 🖼️ Evidence & Artifacts
Below is the high-fidelity process log audit captured inside Zui:

![Registry Persistence Evidence](../../Screenshots/REGISTRY_TRIAGE.png)
