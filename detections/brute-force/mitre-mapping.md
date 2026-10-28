\# MITRE ATT\&CK Mapping



\*\*Technique:\*\* T1110 — Brute Force

\*\*Sub-technique:\*\* T1110.001 — Password Guessing



\## Description

Adversaries attempt to gain access to accounts by systematically guessing

passwords, typically using automated tools against exposed authentication

services (RDP, SMB, SSH, web logins).



\## Data source

Windows Security Event Log, Event ID 4625 (An account failed to log on)



\## Why this detection works

A single failed login is normal human error. A burst of 5+ failed logins

against the same account from the same source within a 1-minute window is

not — it reflects automated password-guessing behavior, not manual entry.

