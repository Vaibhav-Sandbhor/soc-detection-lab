\# Environment Setup



\## VMs



| VM | OS | RAM | Network | Role |

|---|---|---|---|---|

| Windows10-Victim | Windows 10 Pro | 4 GB | Host-only (192.168.254.130) | Endpoint being monitored |

| Ubuntu 64-bit | Ubuntu 22.04 | 4 GB | Host-only (192.168.254.129) | Splunk Enterprise (SIEM) |

| Kali | Kali Linux 2025.2 | 2–4 GB | Host-only | Attacker machine |



All three on the same VMware Host-only virtual network, isolated from the internet

by default. Adapters are switched to NAT temporarily only when a VM needs to

download something (e.g. installers), then switched back.



\## Resource notes



Host machine: 16 GB RAM, single physical disk. Running Windows + Ubuntu + Kali

simultaneously is tight — Kali is kept powered off unless actively attacking.

Splunk on Ubuntu needs a real 4 GB VM allocation; with less, the Linux OOM killer

terminates `splunkd` under memory pressure.



\## Disk space



Host disk filled up twice during setup (VM snapshot and install operations failed

with "not enough disk space"). Resolved by deleting unused installer files

(old Windows ISO, duplicate app installers) and disabling unnecessary snapshots.

Lesson: dedicate 150GB+ of free space, ideally on a separate drive, before

running a multi-VM lab long-term.

