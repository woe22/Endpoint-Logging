# 00 — Scenario: Endpoint Visibility & Logging

---

##  Objective

Set up endpoint-level visibility on a Windows machine using Sysmon and native Windows Event Logs. Simulate common adversary behaviors, and capture relevant events for detection and mapping to MITRE ATT&CK techniques.

---

##  Tools & Environment

- Windows 10 Virtual Machine
- Sysmon (Sysinternals)
- Event Viewer
- PowerShell
- MITRE ATT&CK Navigator

---

##  Lab Goals

- Install and configure Sysmon with a custom config
- Understand critical Windows event IDs
- Generate simulated malicious behavior (e.g., process creation, file modification)
- Identify events that would be valuable to forward to a SIEM
- Document findings and map to TTPs

---

##  Real-World Relevance

Endpoint logging is a core foundation for any SOC. Without detailed telemetry, detection and response are blind. This lab simulates what Tier 1 analysts often triage: real-time process activity, command-line execution, and persistence indicators.

---

