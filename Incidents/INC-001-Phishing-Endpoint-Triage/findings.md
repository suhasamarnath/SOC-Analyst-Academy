# INC-001: Phishing Endpoint Triage Findings

### 🛡️ Triage Summary
On 2026-06-17, a corporate endpoint (192.168.10.45) initiated an unauthorized HTTP GET request following an external phishing link interaction. The connection resulted in a successful file download of a suspected malicious payload disguised as a critical system update.

### 🔍 Indicators of Compromise (IOCs)
| Indicator Type | Malicious Value | Context / Notes |
| :--- | :--- | :--- |
| **Source IP** | `192.168.10.45` | Compromised Internal Endpoint |
| **Destination IP** | `104.244.42.1` | Adversary Infrastructure Hosting Server |
| **Malicious Domain**| `update.security-critical-patch.top` | Spoofed Domain (Phishing Landing Site) |
| **Dropped Payload** | `patch_update.exe` | Executable Malicious Binary |
| **HTTP Status** | `200 OK` | Download successfully completed |

### 🛑 Containment & Mitigation Playbook (Remediation)
To prevent lateral movement and block ongoing communication with the malicious infrastructure, the following corporate network and host-level actions were initiated:

1. **Host Isolation:** Isolated the compromised endpoint (`192.168.10.45`) from the primary network segment via the EDR (Endpoint Detection and Response) console to prevent potential internal pivoting.
2. **Network Block:** Deployed an immediate outbound block rule on the edge firewalls for IP address `104.244.42.1` and domain name `update.security-critical-patch.top`.
3. **DNS Sinkholing:** Configured the internal DNS servers to sinkhole requests to the malicious `.top` domain, ensuring any other internal machines hitting the link redirect safely to a loopback address (`127.0.0.1`).
4. **Credential Revocation:** Force-reset the active user session tokens and corporate domain credentials associated with endpoint asset `C123456789` due to potential credential harvesting.

### 🖼️ Evidence & Artifacts
Below is the high-fidelity network traffic analysis captured within the Zui (Brim) log parsing engine, isolating the malicious HTTP GET request line:

![Zui Triage Evidence](zui_triage.png)