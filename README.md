# 🔐 Home SOC Lab — Threat Detection & Incident Response

A hands-on Security Operations Center (SOC) lab built to practice real-world
threat detection, log analysis, and incident response — simulating the daily
workflow of a SOC Analyst.

## 📋 Overview

This project simulates a small SOC environment end to end: attack simulation →
log collection → detection → automated alerting → incident documentation.

## 🏗️ Architecture

- **Windows 11** (host machine) — running Splunk Enterprise (SIEM)
- **Windows 10** (VirtualBox VM) — victim machine, instrumented with Sysmon
- **Kali Linux** (VirtualBox VM) — attacker machine
- **Network** — VirtualBox Host-Only Adapter connecting all machines
- **Splunk Universal Forwarder** — ships Windows/Sysmon logs to Splunk
- **Atomic Red Team** — simulates MITRE ATT&CK techniques

![Lab Architecture](screenshots/lab-network.jpg)

## 🛠️ What I Did

1. Built an isolated host-only network connecting the VMs
2. Installed Sysmon with the SwiftOnSecurity config for detailed process logging
3. Configured Splunk to receive forwarded Windows Event Logs and Sysmon logs
4. Simulated MITRE ATT&CK technique **T1059.001** (PowerShell abuse, including
   a Mimikatz-style credential access simulation) using Atomic Red Team
5. Built a Splunk detection search and mapped findings to MITRE ATT&CK
6. Configured a Splunk alert that successfully triggered on the live attack

## 🎯 MITRE ATT&CK Techniques Simulated

| Technique ID | Name | Tactic |
|---|---|---|
| T1059.001 | Command and Scripting Interpreter: PowerShell | Execution |
| T1003 | OS Credential Dumping (Mimikatz simulation) | Credential Access |

## 🔍 Detection

Search used to catch the simulated attack in Splunk:

```spl
index=main sourcetype="WinEventLog:Microsoft-Windows-Sysmon/Operational"
EventCode=1 CommandLine="*mimikatz*"
```

![Detection Result](screenshots/detection-result.jpg)

## 🚨 Alert

Built and validated a Splunk alert ("Suspicious PowerShell") that
automatically triggers when this activity is detected.

![Triggered Alert](screenshots/triggered-alert.jpg)

## 📄 Incident Report

Full incident report with timeline, severity assessment, and remediation
recommendations: [incident-report.pdf](reports/incident-report.pdf)

## 🧰 Tools Used

Splunk · Sysmon · VirtualBox · Kali Linux · Windows 10/11 · Atomic Red Team ·
MITRE ATT&CK

## 📚 Lessons Learned

- Hands-on experience configuring a full SIEM log pipeline end to end
- Troubleshot real issues including Windows Event Log permission errors,
  service configuration problems, and log forwarding failures
- Practiced mapping raw log data to MITRE ATT&CK and writing a structured
  incident report

## 📬 Contact

[Your Name] — [Your LinkedIn URL] — [Your Email]
