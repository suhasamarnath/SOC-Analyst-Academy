# INC-008: Living off the Land Binaries (LOLBins) Abuse Investigation

### 🛡️ Triage Summary
On 2026-06-17, an active endpoint monitoring rule triggered on an anomalous execution pattern involving a native cryptographic system binary (Event ID 4688). The adversary abused `certutil.exe` to bypass perimeter firewalls and fetch a malicious executable from external infrastructure, exploiting trusted built-in binaries to evade typical proxy restrictions.

### 🔍 Indicators of Compromise (IOCs)
| Indicator Type | Value / Parameters | Context / Purpose |
| :--- | :--- | :--- |
| **Process Name** | `certutil.exe` (PID: 10214) | Native Windows Certificate Services utility used as a download vector |
| **Command Flags**| `-urlcache -f` | Forces the binary to fetch an external URL and bypass local cache checks |
| **Remote Source** | `http://104.244.42.1/malware.exe` | Known malicious staging IP address pulling a secondary payload |
| **Output Path** | `C:\Users\Public\malware.exe` | Staging location for the dropped malicious binary |

### 🛑 Containment & Remediation Playbook
1. **Payload Isolation:** Located and securely quarantined `C:\Users\Public\malware.exe` from the filesystem to prevent execution.
2. **Network Block:** Verified the connection to `104.244.42.1` was stopped and updated perimeter firewalls to reject all future outbound traffic to this subnet.
3. **SIEM Rule Enhancement:** Tuned endpoint behavioral tracking to automatically flag whenever administrative processes like `certutil.exe` or `bitsadmin.exe` contain external network parameters in their command strings.

### 🖼️ Evidence & Artifacts
Below is the high-fidelity process log audit captured inside Zui:

![LOLBins Investigation Evidence](../../Screenshots/LOLBINS_TRIAGE.png)
