\# Investigation: Obfuscated PowerShell Execution



\## Summary

Simulated an attacker-style PowerShell invocation on Windows10-Victim:

Base64-encoded command, execution policy bypass, hidden window — a

pattern consistent with post-exploitation tooling.



\## Timeline

\- 2026-10-31 22:57:32 and 22:57:52 — two powershell.exe process creations

&#x20; logged via Sysmon, both using -NoProfile -ExecutionPolicy Bypass

&#x20; -WindowStyle Hidden -EncodedCommand



\## Detection

Built an SPL query filtering Sysmon EventCode=1 for powershell.exe

processes containing obfuscation/evasion flags in the CommandLine field.

Correctly isolated both simulated attack events with zero false positives.



\## Decoding the payload

Extracted the Base64 string from CommandLine using rex, then decoded it

outside Splunk (base64decode is unsupported in this Splunk version) via:



\[System.Text.Encoding]::Unicode.GetString(\[Convert]::FromBase64String("..."))



Decoded command revealed: Write-Host 'Simulated recon...'; whoami /all

— consistent with attacker reconnaissance behavior post-execution.



\## Notes

\- PowerShell encodes -EncodedCommand payloads as UTF-16LE, not standard

&#x20; UTF-8 — a plain base64 decode without UTF-16LE conversion produces

&#x20; garbled output.

\- This Splunk instance does not support the base64decode() SPL function;

&#x20; decoding was performed external to Splunk as a workaround.



\## Next steps

\- Build an alert for any -EncodedCommand usage regardless of other flags

\- Test against PowerShell obfuscation techniques beyond Base64

&#x20; (e.g. string concatenation, character substitution)

