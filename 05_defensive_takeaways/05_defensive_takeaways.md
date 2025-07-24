# 05 — Defensive Takeaways

---

## Scenario

After enabling enhanced logging in prior modules, including Sysmon and native Windows Event Logs, I analyzed the resulting data to understand what detections were possible from normal and malicious activity. I simulated scheduled tasks, PowerShell execution, and failed logons to observe what Windows logs natively and what needs to be configured.

---

## What I Did

```
# Enabled ScriptBlock and Module Logging via Registry
New-Item -Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging" -Force
Set-ItemProperty -Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging" -Name "EnableScriptBlockLogging" -Value 1 -Force

New-Item -Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ModuleLogging" -Force
Set-ItemProperty -Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ModuleLogging" -Name "EnableModuleLogging" -Value 1 -Force
New-ItemProperty -Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ModuleLogging" -Name "ModuleNames" -Value "*" -PropertyType MultiString -Force
```

- Rebooted to activate logging
- Simulated various attacker behaviors:
  - Created scheduled task: `schtasks /create /sc once /tn test /tr "notepad.exe" /st 23:59`
  - Ran PowerShell commands
  - Triggered failed logons with `runas /user:fakeadmin cmd`
- Opened Event Viewer and filtered logs across:
  - Security
  - System
  - PowerShell
  - Task Scheduler (Operational)
  - Sysmon (Operational)
- Identified key event IDs and examined:
  - 4625 (Failed logon)
  - 4104 (PowerShell execution)
  - 106 & 200 (Scheduled Task creation/launch)
  - 4688 (New Process)
  - 53504 (Named pipe activity after enabling logging)

---

## What I Learned

- Native Windows logging provides rich signals for detection — but only when properly configured.
- ScriptBlock Logging (4104) must be enabled manually and requires a reboot to take effect.
- MITRE techniques become visible through correct log channels:
  - 4688 → T1059.001 (Command Line Execution)
  - 4104 → T1059.001 (PowerShell)
  - 106/200 → T1053.005 (Scheduled Task)
  - 4625 → T1110.001 (Brute Force)
  - 53504 → T1021.002 (Named Pipes)
- Troubleshooting was essential — logging misconfigurations can result in critical blind spots.

---

## Why It Matters

Effective detection in a SOC relies on having the right logs at the right time. This module taught me not just how to simulate and interpret attacker behavior, but how to ensure the system is even capable of logging it. Misconfigured logging = missed attacks. This exercise made clear that registry settings, reboots, and validation checks are not optional — they’re operational essentials. I also saw how different logs correlate to specific MITRE ATT&CK techniques, forming the backbone of structured detection logic.

---
