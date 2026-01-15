# Artifact 02 — TCP Connect Scan (-sT) against Port 80

**Command:**
```bash
sudo nmap -sT -Pn -p 80 10.66.148.87 -vv

Starting Nmap 7.94SVN ( https://nmap.org ) at 2026-01-14 18:54 PST
Initiating Parallel DNS resolution of 1 host. at 18:54
Completed Parallel DNS resolution of 1 host. at 18:54, 0.15s elapsed
Initiating Connect Scan at 18:54
Scanning 10.66.148.87 [1 port]
Discovered open port 80/tcp on 10.66.148.87
Completed Connect Scan at 18:54, 0.18s elapsed (1 total ports)
Nmap scan report for 10.66.148.87
Host is up, received user-set (0.18s latency).
Scanned at 2026-01-14 18:54:42 PST for 1s

PORT   STATE SERVICE REASON
80/tcp open  http    syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.36 seconds




