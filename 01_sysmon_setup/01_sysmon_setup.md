# 01 — Sysmon Setup

---

## Scenario

In this module, I focused on establishing endpoint-level visibility using Sysmon on a Windows 10 virtual machine. The goal was to implement a well-tuned, real-world logging agent that provides detailed telemetry on system activity. This mirrors the foundational steps of endpoint detection in a real SOC environment.

---

## What I Did

```powershell
# Downloaded Sysmon from Sysinternals
# Extracted Sysmon64.exe to C:\Users\Kai\Downloads\Sysmon

# Downloaded SwiftOnSecurity’s community config
Invoke-WebRequest -Uri https://raw.githubusercontent.com/SwiftOnSecurity/sysmon-config/master/sysmonconfig-export.xml -OutFile sysmonconfig.xml

# Installed Sysmon using the config (ran as Administrator)
cd C:\Users\Kai\Downloads\Sysmon
Sysmon64.exe -accepteula -i C:\Users\Kai\sysmonconfig.xml

# Verified active config
Sysmon64.exe -c

# Simulated normal and suspicious activity
whoami
ipconfig /all
notepad
powershell -Command "Get-Process"
mkdir C:\Temp\testfolder
echo "Hello" > C:\Temp\testfolder\test.txt
Remove-Item C:\Temp\testfolder\test.txt

# Simulated suspicious file creation
echo "malicious test" > C:\Users\Kai\AppData\Roaming\svchost.ps1

# Viewed logs in Event Viewer
# Event Viewer → Applications and Services Logs → Microsoft → Windows → Sysmon → Operational
```

---

## What I Learned

- Sysmon provides deep process and file-level visibility that is essential for effective detection on Windows endpoints.
- The SwiftOnSecurity config is tuned to ignore noise like basic `C:\Temp\` file writes, which explains why my `test.txt` was not logged.
- However, creating a `.ps1` file in `AppData\Roaming` triggered **Event ID 11** as expected — a realistic mimic of adversary behavior.
- Viewing logs through Event Viewer confirmed that process and file creation telemetry was being recorded.
- I verified the active Sysmon configuration using `Sysmon64.exe -c`, ensuring the community ruleset was applied.

---

## Why It Matters

SOC analysts rely on endpoint telemetry to identify, triage, and respond to threats. This lab simulates the first step in building a monitored environment where detection rules can be tested and validated. Installing Sysmon with a tuned config shows that I understand both the value of logging and the importance of reducing noise. This foundational step will be reused across all future endpoint detection and response (EDR) simulations.
    
---
