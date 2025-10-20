# Scan-Your-Local-Network-for-Open-Ports



# Task 1 — Local Network Port Scanning 

**Author:** Aluri Rohith
**Date:** 2025-10-20  
**Tools:** Nmap 7.95, 

---

## Objective
Scan the local network to discover live hosts and open ports, document findings, and identify basic security risks associated with exposed services.

---

## Environment
- OS: Kali Linux (
- Local network range used: `192.168.0.1/24`  
- Nmap version: 7.95

> **Important:** Only scan networks and devices you own or have explicit permission to test.

---

## Files in this Repo
- `README.md` — this file  
- `scan_commands.txt` — commands used to perform scans  
- `scan_output.txt` — raw Nmap output (text)  
- `scan_output.html` — (optional) HTML-formatted Nmap output  
- `screenshots/` — screenshot(s) of terminal output (e.g., `nmap_screenshot.png`)  
- `analysis.md` — analysis and remediation suggestions

---

## Commands I used
```bash
# TCP SYN scan across subnet (used)
sudo nmap -sS 192.168.0.1/24 -oN scan_output.txt
