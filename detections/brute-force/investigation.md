\# Investigation: SMB Brute-Force Attempt



\## Summary

Simulated a brute-force attack from Kali (192.168.254.128) against the

Windows10-Victim endpoint (192.168.254.130), targeting SMB (port 445)

using Hydra with the rockyou.txt wordlist against the local account `svaib`.



\## Timeline

\- 2026-10-28 12:54:22 to 12:54:24 — 13 failed SMB authentication attempts

&#x20; logged in under 2 seconds, all from 192.168.254.128, all targeting `svaib`



\## Detection

Built an SPL query filtering Windows Security EventCode=4625, grouping by

1-minute windows, source IP, and account name, alerting on >5 failures.

Detection cleanly isolated the attack with zero false positives in this

environment.



\## Notes

\- Initially attempted RDP (port 3389) brute-force; Hydra's RDP module

&#x20; (marked experimental) failed to establish connections even after

&#x20; disabling Network Level Authentication. Switched to SMB, which Hydra

&#x20; handled reliably.

\- Account\_Name in Windows 4625 events is a multivalue field (Subject +

&#x20; Target account) — required `mvfilter()` to isolate the actual

&#x20; targeted account for clean grouping.



\## Next steps

\- Add a real-time alert in Splunk based on this search

\- Test detection against a slower, low-and-slow brute-force pattern to

&#x20; check for evasion

