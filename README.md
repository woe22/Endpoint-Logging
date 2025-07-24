# Endpoint Logging

## ✅ Modules

### 01 — Sysmon Setup
Configured Microsoft Sysmon using the SwiftOnSecurity community config to enhance visibility beyond default logs. Verified configuration, tested logging coverage, and collected sample events.

### 02 — Event Log Analysis  
Explored high-value event logs in Windows. Simulated logon attempts, PowerShell execution, and scheduled tasks. Manually confirmed the presence of event IDs like 4625, 4688, and 4104 via Event Viewer.

### 03 — MITRE Mapping  
Mapped key observed events to the MITRE ATT&CK framework (e.g., T1059, T1053, T1078). This step simulates how a SOC analyst would correlate system activity to adversary behaviors.

### 04 — PowerShell Logging  
Enabled and verified Script Block Logging (4104) and Module Logging (4103) via Group Policy registry keys. Reviewed correlation between logs and attacker simulation commands.

### 05 — Further Detection & Expansion  
Wrapped up the logging lab with a focus on broader detection opportunities. Simulated additional suspicious activity and confirmed visibility across all configured log sources.

---

## ⚠️ Disclaimer

This lab is intended strictly for educational and professional development purposes. All activities were conducted in a controlled lab environment on non-production systems. No malicious tools or techniques were deployed outside of approved simulations. Unauthorized use of the methods described here in real-world environments is unethical and may be illegal.
