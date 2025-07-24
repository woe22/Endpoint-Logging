# 02 — Event Log Analysis

---

## Scenario

In this lab, I focused on analyzing native Windows event logs to simulate what a SOC analyst would do when triaging alerts or investigating adversary activity. The goal was to generate relevant events and validate whether they appeared across key Windows log sources.

---

## What I Did

```powershell
# Trigger a successful logon
whoami

# Trigger a failed logon attempt
runas /user:fakeadmin cmd

# Create a scheduled task to mimic persistence
schtasks /create /sc once /tn test /tr "notepad.exe" /st 23:59

# Run a PowerShell command to trigger PowerShell logging
powershell -Command "Get-Process"

# Open Event Viewer and filter for relevant logs
# Event Viewer → Windows Logs → Security
# Event Viewer → Windows Logs → System
# Event Viewer → Applications and Services Logs → Microsoft → Windows → PowerShell
# Event Viewer → Applications and Services Logs → Microsoft → Windows → TaskScheduler → Operational

# Use "Filter Current Log..." to view:
# 4624 — Successful logon
# 4625 — Failed logon
# 4648 — Logon with explicit credentials
# 4672 — Admin privileges
# 4688 — New process created
# 4697 — New service created
# 7045 — New service installed
# 4104 — PowerShell script block logging
# 106  — Scheduled task registered
# 200  — Scheduled task launched
```

---

## What I Learned

- Failed and successful logons trigger distinct Security Event IDs (4624/4625)
- Scheduled task creation triggers Event ID 106 (registration) and 200 (launch)
- PowerShell execution triggers Event ID 4104 if logging is enabled
- Filtering logs in Event Viewer is essential for isolating meaningful security events
- Knowing what log sources and IDs correspond to attacker behavior is key to incident response

---

## Why It Matters

Blue teamers and SOC analysts rely heavily on Windows event logs for alert triage and detection engineering. This lab provided hands-on experience generating and analyzing common indicators of compromise (IOCs), helping reinforce log familiarity, and building investigative muscle for real-world security operations.
# 02 — Event Log Analysis

---

## Scenario

In this lab, I focused on analyzing native Windows event logs to simulate what a SOC analyst would do when triaging alerts or investigating adversary activity. The goal was to generate relevant events and validate whether they appeared across key Windows log sources.

---

## What I Did

```powershell
# Trigger a successful logon
whoami

# Trigger a failed logon attempt
runas /user:fakeadmin cmd

# Create a scheduled task to mimic persistence
schtasks /create /sc once /tn test /tr "notepad.exe" /st 23:59

# Run a PowerShell command to trigger PowerShell logging
powershell -Command "Get-Process"

# Open Event Viewer and filter for relevant logs
# Event Viewer → Windows Logs → Security
# Event Viewer → Windows Logs → System
# Event Viewer → Applications and Services Logs → Microsoft → Windows → PowerShell
# Event Viewer → Applications and Services Logs → Microsoft → Windows → TaskScheduler → Operational

# Use "Filter Current Log..." to view:
# 4624 — Successful logon
# 4625 — Failed logon
# 4648 — Logon with explicit credentials
# 4672 — Admin privileges
# 4688 — New process created
# 4697 — New service created
# 7045 — New service installed
# 4104 — PowerShell script block logging
# 106  — Scheduled task registered
# 200  — Scheduled task launched
```

---

## What I Learned

- Failed and successful logons trigger distinct Security Event IDs (4624/4625)
- Scheduled task creation triggers Event ID 106 (registration) and 200 (launch)
- PowerShell execution triggers Event ID 4104 if logging is enabled
- Filtering logs in Event Viewer is essential for isolating meaningful security events
- Knowing what log sources and IDs correspond to attacker behavior is key to incident response

---

## Why It Matters

Blue teamers and SOC analysts rely heavily on Windows event logs for alert triage and detection engineering. This lab provided hands-on experience generating and analyzing common indicators of compromise (IOCs), helping reinforce log familiarity, and building investigative muscle for real-world security operations.

---
