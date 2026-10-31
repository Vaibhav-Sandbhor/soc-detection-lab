\# Investigation: LOLBin Abuse via certutil.exe



\## Summary

Simulated a LOLBin technique on Windows10-Victim using certutil.exe

to download a remote file, mimicking how attackers abuse trusted

system binaries to bypass detection tools focused on browsers/PowerShell.



\## Timeline

\- 2026-10-31 23:14:21 — certutil.exe executed with -urlcache -split -f

&#x20; flags, downloading a remote file to httpdownload.txt, spawned from

&#x20; cmd.exe under user svaib



\## Detection

Built an SPL query filtering Sysmon EventCode=1 for certutil.exe

processes containing -urlcache, -decode, or -split flags. Correctly

isolated the test event.



\## Notes

\- certutil is a native, digitally-signed Microsoft binary — this is

&#x20; exactly why LOLBin techniques are dangerous, since signature-based

&#x20; and allowlist-based defenses often miss them entirely.

\- Parent process (cmd.exe) and user context matter here too; in a real

&#x20; investigation, an unexpected parent (e.g. a Word document spawning

&#x20; cmd.exe spawning certutil.exe) would be a much stronger signal than

&#x20; certutil usage alone.



\## Next steps

\- Extend detection to other common LOLBins: bitsadmin, mshta, rundll32,

&#x20; regsvr32

\- Add parent-process context to reduce false positives in environments

&#x20; where certutil is used legitimately by IT admins

