# 05 — Further Detection and Expansion

---

## Scenario

This module extends previous logging and detection work by reviewing additional event sources, simulating WMI activity, and scanning for suspicious system behavior. The goal is to mimic blue team triage processes for uncovering persistence, stealth, or misconfigurations that could aid an attacker.

---

## What I Did

```powershell
# Simulated benign WMI query for detection
Get-WmiObject -Namespace root\cimv2 -Class Win32_Process
```

- Opened Event Viewer and navigated to:
  - Windows Defender > Operational
  - Sysmon > Operational (Event ID 19, 20, 21 for WMI)
  - Security and System logs

- Filtered logs for:
  - 4698 — Task created
  - 7036 — Service state change
  - 1102 — Audit log cleared

- Verified script block and module logging persisted after reboot
- Investigated previously unseen event ID `53504` related to PowerShell behavior
- Confirmed no unexpected services or hidden tasks were added

---

## What I Learned

- WMI queries can trigger Sysmon detection under IDs 19–21 when configured
- Windows Defender logs add valuable insight into AV and signature activity
- Filtering event logs by IDs reveals both expected and anomalous actions
- 53504 events can appear under PowerShell logs when script block logging is active, validating that the registry changes were successful
- Task creation via `schtasks` appears under both Sysmon and TaskScheduler logs, reinforcing correlation

---

## Why It Matters

This module solidifies log review skills beyond static configurations, encouraging dynamic threat hunting behaviors. A SOC analyst must proactively pivot across different log sources, identify subtle persistence techniques, and verify the impact of registry-based logging enhancements. These techniques contribute to real-time detection and layered defense.


---
