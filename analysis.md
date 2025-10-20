# Analysis — Nmap Scan (Task 1)

**Author:** Aluri Rohith
**Date:** 2025-10-20

## Quick summary
A TCP SYN scan across `192.168.0.1/24` discovered 3 responsive hosts:
- `192.168.0.1` — shows filtered/closed ports and three notable ports: 23(filtered), 80(open), 1900(open). MAC vendor: TP-Link Limited.
- `192.168.0.102` — host up; all scanned ports filtered (no-response). MAC vendor: AzureWave Technology.
- `192.168.0.103` — host up; scanned ports reported closed.

## Notable findings & risk assessment

### 192.168.0.1
- **23/tcp (telnet) — filtered**
  - **Risk:** If telnet were open it would provide plaintext remote access (insecure). Filtered means a device or firewall is interfering; investigate whether telnet is intentionally blocked or present.
  - **Recommendation:** Ensure telnet is disabled on managed devices. Use SSH (key-based) instead of telnet. Block telnet on firewall.

- **80/tcp (http) — open**
  - **Risk:** Exposed web server. If the web server or hosted web app is outdated or misconfigured, it may be vulnerable to common web attacks (OWASP Top 10).
  - **Recommendation:** Identify the web application, patch server & applications, force HTTPS, limit management interfaces, and consider a WAF or access restrictions for admin pages.

- **1900/tcp (UPnP / SSDP) — open**
  - **Risk:** UPnP can expose device control or be abused for network reconnaissance/amplification. Consumer routers often have UPnP enabled by default.
  - **Recommendation:** Disable UPnP on the router if not required. If needed, limit UPnP scope and monitor for unexpected behavior.

### 192.168.0.102
- **All ports filtered (no-response)**
  - **Risk:** Likely protected by host-based firewall or network filtering — this is generally good for reducing exposure. Investigate the device (MAC suggests AzureWave; possibly an IoT device or wireless client) and ensure it is fully patched.
  - **Recommendation:** Keep firmware updated, use strong Wi-Fi credentials, and ensure the device is on the correct VLAN/guest network if appropriate.

### 192.168.0.103
- **All scanned ports closed**
  - **Risk:** Closed ports are less of an exposure than open ports; continue to monitor. Confirm the host is running expected services.
  - **Recommendation:** Maintain host hardening and ensure no unnecessary services are enabled.

## Remediation & next steps
1. For `192.168.0.1`, identify the web app on port 80 and perform version/service detection (`nmap -sV`) to prioritise patching. Consider enabling HTTPS and restricting access to admin endpoints.
2. Disable unnecessary services (especially telnet and UPnP) on the router or device at `192.168.0.1`.
3. Lock down devices that show filtered ports (192.168.0.102) by confirming firewall rules and patching firmware.
4. Create a baseline by scheduling periodic scans and keep records of changes across scans.
5. If deeper vulnerability assessment is needed, run `nmap --script vuln` and/or use authenticated vulnerability scanners — only with permission.

## Evidence collected
- `scan_output.txt` — raw Nmap output (this repo)
- `nmap_screenshot.png` — screenshot of terminal output (place under `/screenshots`)

## Ethics & Permissions
Scans were performed only on devices/networks under my control (or with permission). No unauthorised scanning was performed.
