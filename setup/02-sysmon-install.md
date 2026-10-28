\# Sysmon Installation



\- Sysmon v15.22 installed on Windows10-Victim

\- Config: SwiftOnSecurity sysmonconfig-export.xml (schema 4.91)



Install command:sysmon64.exe -accepteula -i sysmonconfig-export.xml

Verified via:



sc query sysmon64



and Event Viewer → Applications and Services Logs → Microsoft → Windows → Sysmon → Operational

