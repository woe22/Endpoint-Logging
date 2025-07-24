# 03 — MITRE Mapping

---

## Scenario

This module focused on mapping observed Windows event log activity to MITRE ATT&CK techniques. By connecting system events to attacker behavior, I practiced translating raw telemetry into structured threat intelligence — a critical SOC skill.

---

## What I Did

```powershell
# Simulated failed logon
runas /user:fakeadmin cmd

# Triggered PowerShell execution
powershell -Command "Get-Process"

# Created a scheduled task
schtasks /create /sc once /tn test /tr "notepad.exe" /st 23:59
```

I then used Event Viewer to review and filter logs for relevant event IDs across:

- **Security** → 4625 (Failed Logon), 4688 (Process Creation), 4648, 4672
- **PowerShell Operational** → 4104 (Script Block Logging)
- **Task Scheduler Operational** → 106, 200 (Task registration/launch)
- **Sysmon Operational** → Additional context on process behavior

---

## What I Learned

| Observed Event               | MITRE Tactic         | Technique                  |
|-----------------------------|----------------------|----------------------------|
| 4625 - Failed logon         | Credential Access     | T1110 - Brute Force        |
| 4104 - PowerShell execution | Execution             | T1059.001 - PowerShell     |
| 106/200 - Task creation     | Persistence           | T1053.005 - Scheduled Task |
| 4688 - Process creation     | Execution             | T1055 (related) - Injection|

---

## Why It Matters

Mapping logs to MITRE tactics and techniques helps standardize triage, detection, and reporting across teams. This process is foundational in security operations and threat hunting, making it a vital skill for SOC analysts.

---
