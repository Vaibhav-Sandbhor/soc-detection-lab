\# Splunk Universal Forwarder Setup (Windows)



Installed via .msi, pointed at Ubuntu SIEM (192.168.254.129:9997).



\## inputs.conf



\[WinEventLog://Security]

disabled = false

index = main



\[WinEventLog://System]

disabled = false

index = main



\[WinEventLog://Application]

disabled = false

index = main



\[WinEventLog://Microsoft-Windows-Sysmon/Operational]

disabled = false

index = main





\## Issues hit and fixed



1\. \*\*Network mismatch\*\* — Windows adapter was on NAT (192.168.142.x) while

&#x20;  Ubuntu was on Host-only (192.168.254.x); no connectivity between them.

&#x20;  Fix: both VMs set to Host-only network.



2\. \*\*Sysmon channel access denied (errorCode=5)\*\* — Security/System/Application

&#x20;  logs forwarded fine, but Sysmon channel subscription failed with

&#x20;  "Access is denied". Root cause: forwarder service account lacked

&#x20;  permission to read the Sysmon event channel.

&#x20;  Fix: changed service to run as LocalSystem:



sc config SplunkForwarder obj= LocalSystem





Verified all 4 sources arriving in Splunk:



index=main | stats count by source

