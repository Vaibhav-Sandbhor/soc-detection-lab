\# Investigation: Reconnaissance Command Burst



\## Summary

Simulated a post-compromise recon sweep on Windows10-Victim, running

whoami, net user, net localgroup administrators, systeminfo, and

ipconfig in rapid succession from a single cmd.exe session — mimicking

standard attacker enumeration behavior after initial access.



\## Timeline

\- 2026-10-31 23:26:17–23:26:22 — 6 recon tool invocations (4 distinct

&#x20; binaries: ipconfig, net, systeminfo, whoami) executed within 5 seconds,

&#x20; all spawned from the same cmd.exe parent process



\## Detection

Built a behavioral SPL query that bins Sysmon process-creation events

into 30-second windows and counts distinct recon tools per window,

alerting when 3+ distinct tools appear together. This approach correctly

flagged the attack burst while ignoring two earlier, unrelated standalone

command executions (an isolated ipconfig and whoami from hours earlier

in the session) that a simple single-command detection would have

falsely flagged.



\## Notes

\- This detection is pattern/behavior-based rather than keyword-based —

&#x20; a meaningful step up from the brute-force and PowerShell detections,

&#x20; which each matched on a single event's characteristics.

\- dc() (distinct count) in the stats command was key to avoiding false

&#x20; positives from repeated use of the same single tool.



\## Next steps

\- Expand the recon tool list (tasklist, net group, wmic, arp -a)

\- Correlate with the PowerShell/process-execution detections to catch

&#x20; recon performed via PowerShell cmdlets instead of native binaries

&#x20; (e.g. Get-LocalUser instead of net user)

