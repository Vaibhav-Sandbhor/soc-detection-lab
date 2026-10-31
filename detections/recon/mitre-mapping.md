\# MITRE ATT\&CK Mapping



\*\*Technique:\*\* T1082 — System Information Discovery

\*\*Related:\*\* T1087 — Account Discovery, T1018 — Remote System Discovery,

T1016 — System Network Configuration Discovery



\## Description

After gaining initial access, adversaries commonly enumerate the system,

local accounts, network configuration, and domain trust relationships to

understand their foothold and plan lateral movement. This typically

involves running several native Windows discovery commands (whoami, net,

systeminfo, ipconfig, nltest) in quick succession.



\## Data source

Sysmon Event ID 1 (Process Creation), Image + ParentImage fields



\## Why this detection works

Any single discovery command (e.g. one ipconfig check) is normal admin

behavior and not worth alerting on. The signal is in the clustering:

3 or more distinct discovery tools executed within a short window from

the same parent process is a strong behavioral indicator of a recon

sweep, not routine individual usage.

