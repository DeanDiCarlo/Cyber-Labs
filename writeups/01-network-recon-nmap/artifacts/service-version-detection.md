# Artifact 07 — Service/Version Detection (-sV) using --top-ports 20

**Command:**
```bash
sudo nmap -sV -Pn --top-ports 20 10.66.148.87 -vv

Starting Nmap 7.94SVN ( https://nmap.org ) at 2026-01-14 18:58 PST
NSE: Loaded 46 scripts for scanning.
Initiating Parallel DNS resolution of 1 host. at 18:58
Completed Parallel DNS resolution of 1 host. at 18:58, 0.02s elapsed
Initiating SYN Stealth Scan at 18:58
Scanning 10.66.148.87 [20 ports]
Discovered open port 21/tcp on 10.66.148.87
Discovered open port 135/tcp on 10.66.148.87
Discovered open port 3389/tcp on 10.66.148.87
Discovered open port 53/tcp on 10.66.148.87
Discovered open port 80/tcp on 10.66.148.87
Completed SYN Stealth Scan at 18:58, 1.91s elapsed (20 total ports)
Initiating Service scan at 18:58
Scanning 5 services on 10.66.148.87
Completed Service scan at 18:59, 11.31s elapsed (5 services on 1 host)
NSE: Script scanning 10.66.148.87.
NSE: Starting runlevel 1 (of 2) scan.
Initiating NSE at 18:59
Completed NSE at 18:59, 0.47s elapsed
NSE: Starting runlevel 2 (of 2) scan.
Initiating NSE at 18:59
Completed NSE at 18:59, 0.33s elapsed
Nmap scan report for 10.66.148.87
Host is up, received user-set (0.10s latency).
Scanned at 2026-01-14 18:58:52 PST for 14s

PORT     STATE    SERVICE       REASON          VERSION
21/tcp   open     ftp           syn-ack ttl 126 FileZilla ftpd
22/tcp   filtered ssh           no-response
23/tcp   filtered telnet        no-response
25/tcp   filtered smtp          no-response
53/tcp   open     domain        syn-ack ttl 126 Simple DNS Plus
80/tcp   open     http          syn-ack ttl 126 Microsoft IIS httpd 10.0
110/tcp  filtered pop3          no-response
111/tcp  filtered rpcbind       no-response
135/tcp  open     msrpc         syn-ack ttl 126 Microsoft Windows RPC
139/tcp  filtered netbios-ssn   no-response
143/tcp  filtered imap          no-response
443/tcp  filtered https         no-response
445/tcp  filtered microsoft-ds  no-response
993/tcp  filtered imaps         no-response
995/tcp  filtered pop3s         no-response
1723/tcp filtered pptp          no-response
3306/tcp filtered mysql         no-response
3389/tcp open     ms-wbt-server syn-ack ttl 126 Microsoft Terminal Services
5900/tcp filtered vnc           no-response
8080/tcp filtered http-proxy    no-response
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 14.39 seconds
           Raw packets sent: 36 (1.584KB) | Rcvd: 6 (264B)

