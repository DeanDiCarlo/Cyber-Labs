# Artifact 03 — TCP NULL Scan (-sN) against Port 80

**Command:**
```bash
sudo nmap -sN -Pn -p 80 10.66.148.87

Starting Nmap 7.94SVN ( https://nmap.org ) at 2026-01-14 18:54 PST
Nmap scan report for 10.66.148.87
Host is up.

PORT   STATE         SERVICE
80/tcp open|filtered http

Nmap done: 1 IP address (1 host up) scanned in 2.12 seconds

