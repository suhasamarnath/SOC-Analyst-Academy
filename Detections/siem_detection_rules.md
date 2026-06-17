# SIEM Detection Rules & Signatures

This directory stores behavioral alerting logic mapped to common adversarial operations observed during tracking.

## 🔍 Behavioral Alerting Profiles

### 1. Local/Domain Reconnaissance Tracking
*   **Log Source:** Windows Security Event ID 4688 (Process Creation)
*   **Selection Logic:** `CommandLine` contains:
    *   `net user /domain`
    *   `net localgroup administrators`
*   **Severity:** Medium

### 2. Native System Binary Abuse (LOLBins)
*   **Log Source:** Windows Security Event ID 4688
*   **Selection Logic:** `ProcessName` IS `certutil.exe` AND `CommandLine` contains (`-urlcache` OR `-f`)
*   **Severity:** High

### 3. Anti-Forensics Defense Evasion
*   **Log Source:** Windows Security Event ID 4688
*   **Selection Logic:** `ProcessName` IS `wevtutil.exe` AND `CommandLine` contains (`cl` OR `clear-log`)
*   **Severity:** Critical (Triggers Immediate Host Isolation)  
