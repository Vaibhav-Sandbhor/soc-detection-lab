\# MITRE ATT\&CK Mapping



\*\*Technique:\*\* T1218 — System Binary Proxy Execution

\*\*Sub-technique:\*\* T1218.not applicable (certutil falls under general T1105/T1218 LOLBin usage)

\*\*Related:\*\* T1105 — Ingress Tool Transfer



\## Description

Adversaries abuse trusted, signed Windows binaries ("Living Off the Land

Binaries" / LOLBins) to perform malicious actions while evading detection

tools that only monitor for known-bad executables. certutil.exe, a

built-in certificate management tool, is commonly abused with -urlcache

to download remote payloads, since its network traffic and execution

look "trusted" to many security tools.



\## Data source

Sysmon Event ID 1 (Process Creation), Image + CommandLine fields



\## Why this detection works

certutil.exe has no legitimate reason to be used with -urlcache in most

enterprise environments — certificate management doesn't require

downloading arbitrary files from URLs. This flag combination is a

well-documented, high-confidence indicator of LOLBin abuse.

