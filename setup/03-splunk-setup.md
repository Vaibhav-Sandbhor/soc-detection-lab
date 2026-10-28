\# Splunk Server Setup (Ubuntu)



\- Splunk Enterprise 10.6.0 installed to /opt/splunk

\- Started with `splunk start --accept-license --run-as-root` (lab environment, root acceptable)

\- Boot-start enabled: `splunk enable boot-start --run-as-root`

\- Receiving port 9997 configured via Settings → Forwarding and receiving



\## Issue: Splunk repeatedly stopped / wouldn't stay running

Root cause: Ubuntu VM was underprovisioned at 2GB RAM. Splunk requires \~4GB

for stable operation; low memory caused the process to die silently.

Fix: increased Ubuntu VM RAM to 4096 MB in VMware settings.

