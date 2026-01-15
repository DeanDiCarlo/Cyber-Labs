# Evidence 01 — TCP SYN Scan (-sS) Against Port 80

**Target:** 10.66.148.87  
**Date:** 2026-01-14  
**Goal:** Validate HTTP reachability via raw TCP SYN scan and observe SYN-ACK behavior.

---

## Commands Used

```bash
sudo nmap -sS -Pn -p 80 10.66.148.87
sudo nmap -sS -Pn -p 80 10.66.148.87 -vv

Starting Nmap 7.94SVN ( https://nmap.org ) at 2026-01-14 18:54 PST 
Initiating Parallel DNS resolution of 1 host. at 18:54 
Completed Parallel DNS resolution of 1 host. at 18:54, 0.00s elapsed 
Initiating SYN Stealth Scan at 18:54 Scanning 10.66.148.87 [1 port]
Discovered open port 80/tcp on 10.66.148.87 
Completed SYN Stealth Scan at 18:54, 0.13s elapsed (1 total ports) 
Nmap scan report for 10.66.148.87 Host is up, received user-set (0.10s latency). 
Scanned at 2026-01-14 18:54:27 PST for 1s 

PORT STATE SERVICE REASON 
80/tcp open http syn-ack ttl 126 
Read data files from: /usr/bin/../share/nmap 
Nmap done: 1 IP address (1 host up) scanned in 0.18 seconds 
Raw packets sent: 1 (44B) | Rcvd: 1 (44B)

Starting Nmap 7.94SVN ( https://nmap.org ) at 2026-01-14 18:54 PST
Nmap scan report for 10.66.148.87
Host is up (0.094s latency).

PORT   STATE SERVICE
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 0.35 seconds

