\# MITRE ATT\&CK Mapping



\*\*Technique:\*\* T1059 — Command and Scripting Interpreter

\*\*Sub-technique:\*\* T1059.001 — PowerShell



\## Description

Adversaries abuse PowerShell for execution, often using obfuscation

(Base64 encoding), execution policy bypass, and hidden windows to evade

detection and user visibility while running malicious commands.



\## Data source

Sysmon Event ID 1 (Process Creation), CommandLine field



\## Why this detection works

Legitimate admin use of PowerShell rarely combines -EncodedCommand,

\-WindowStyle Hidden, and -ExecutionPolicy Bypass in the same invocation.

This combination is a well-documented pattern in attacker tooling

(e.g. Empire, Cobalt Strike PowerShell stagers) and is a strong signal

even before decoding the payload.

