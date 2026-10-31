\# SOC Detection \& Incident Response Lab



A simulated Security Operations Center built from scratch to practice log collection,

detection engineering, and incident investigation — mapped to MITRE ATT\&CK.



\## Architecture



\- \*\*Windows 10 (victim/endpoint)\*\* — VMware VM, Sysmon with SwiftOnSecurity config,

&#x20; Splunk Universal Forwarder shipping Security/System/Application/Sysmon logs

\- \*\*Ubuntu 22.04 (SIEM)\*\* — Splunk Enterprise 10.6, receiving on port 9997

\- \*\*Kali Linux (attacker)\*\* — used to simulate brute-force, PowerShell abuse, and

&#x20; recon techniques against the Windows endpoint

\- All VMs on an isolated VMware Host-only network (192.168.254.0/24), no internet

&#x20; exposure during attack simulation



\## What this demonstrates



\- End-to-end log pipeline setup: endpoint → forwarder → SIEM

\- Sysmon configuration and tuning for security-relevant telemetry

\- Detection engineering in SPL (Splunk Search Processing Language)

\- MITRE ATT\&CK technique mapping for each detection

\- Incident triage and investigation documentation

\- Real troubleshooting of a multi-VM lab environment (networking, resource

&#x20; constraints, Windows Event Log permissions) — see `/setup` for the full log



\## Detections built



| Technique | ATT&CK ID | Status |
|---|---|---|
| Brute-force authentication | T1110 | Complete |
| PowerShell abuse | T1059.001 | Complete |
| Suspicious process execution | T1218 | Complete |
| Reconnaissance (tool clustering) | T1082 / T1087 / T1018 | Complete |

\## Repo structure



\- `setup/` — environment build steps, including real issues hit and how they were fixed

\- `detections/` — one folder per technique, each with the SPL query, ATT\&CK mapping,

&#x20; and an investigation write-up

\- `screenshots/` — supporting evidence (Splunk searches, Event Viewer, attack output)

