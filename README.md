# linux-threat-detection-kql
KQL-based Linux threat detection rules for Microsoft Sentinel focused on multi-stage intrusion detection, privilege escalation, and threat hunting using MITRE ATT&amp;CK mapping.
# Linux Threat Detection using Microsoft Sentinel (KQL)

## Overview

This repository contains a Microsoft Sentinel detection rule written in Kusto Query Language (KQL) designed to identify multi-stage Linux attack behavior involving:

- Suspicious use of file transfer utilities (curl, wget, rsync, etc.)
- Potential exploitation or unusual kernel interaction indicators
- Execution of ELF binaries in user-writable directories
- Privilege escalation attempts using `su`

The detection correlates network, process, and file telemetry to identify potential Linux local privilege escalation (LPE) activity.

---

## Detection Logic

This rule identifies a chained attack pattern:

1. A host uses common remote fetch utilities to retrieve external content
2. Suspicious process behavior involving `algif-aead` is observed
3. ELF binaries are created in `/home/` directories
4. A `su` privilege escalation attempt is executed from a user-owned process

The correlation of these behaviors may indicate post-exploitation activity.

---

## Data Sources

- DeviceNetworkEvents
- DeviceProcessEvents
- DeviceFileEvents

---

## Threat Model

This detection aligns with techniques from the MITRE ATT&CK framework:

- T1059 – Command and Scripting Interpreter
- T1105 – Ingress Tool Transfer
- T1068 – Exploitation for Privilege Escalation
- T1548 – Abuse Elevation Control Mechanism

---

## Use Cases

- Threat hunting in Linux environments
- Detection of post-compromise activity
- Monitoring suspicious privilege escalation attempts
- Identifying fileless or userland-based attack chains

---

## Notes

- This rule is behavior-based and may produce false positives in development or administrative environments.
- Recommended tuning is required for production deployment.

---
