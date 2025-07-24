# 04 — PowerShell Logging

---

## ️ Scenario

In this module, I configured PowerShell logging on my Windows host to enhance visibility into command execution. The goal was to enable both Script Block Logging and Module Logging and confirm their success through Event Viewer. I documented key event IDs and verified that verbose script content was being captured, which is essential for identifying malicious PowerShell behavior during forensic investigations or SOC triage.

---

##  What I Did

```powershell
# Created required registry keys for ScriptBlockLogging
New-Item -Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell" -Force
New-Item -Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging" -Force

# Enabled ScriptBlockLogging
Set-ItemProperty -Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging" -Name "EnableScriptBlockLogging" -Value 1 -Force

# Created and configured ModuleLogging
New-Item -Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ModuleLogging" -Force
Set-ItemProperty -Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ModuleLogging" -Name "EnableModuleLogging" -Value 1 -Force
New-ItemProperty -Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ModuleLogging" -Name "ModuleNames" -Value "*" -PropertyType MultiString -Force
```

- Rebooted the machine to apply registry changes.
- Opened **Event Viewer** > **Applications and Services Logs** > **Microsoft** > **Windows** > **PowerShell** > **Operational**.
- Verified the presence of:
- `Event ID 4103` – PowerShell pipeline execution
- `Event ID 4104` – ScriptBlock logging (including registry write commands)
- `Event ID 53504` – PowerShell IPC startup (correlating with the configured logging policy)

---

##  What I Learned

- **ScriptBlock Logging** (4104) captures PowerShell commands including dynamically executed or obfuscated input, which is critical for blue team visibility.
- **Event ID 53504** indicates that PowerShell has initialized its IPC listening thread, often appearing after enabling detailed logging policies.
- These logs provide high-fidelity telemetry that can be used in incident detection and digital forensics.
- Registry-based logging configuration takes effect system-wide and persists across sessions after reboot.

---

##  Why It Matters

Enabling PowerShell logging equips defenders with deeper insight into script execution. Many adversaries leverage PowerShell for stealthy actions (T1059.001). By enabling and validating logging mechanisms, I created a defensible position that can detect unauthorized or suspicious PowerShell activity early in the attack chain.

Correlations:
- `4104` entries confirmed visibility into my registry changes during logging setup.
- `53504` appeared as a direct result of PowerShell initializing IPC after those changes.
- Visuals captured show real logs corresponding to benign but traceable script activity.

---
