# Day 02 – Wireshark Malware Traffic Analysis

**Exercise Source:** Malware-Traffic-Analysis.net – 2025‑01‑22

**Focus:** HTTP malware delivery, host identification, C2 analysis

**Tooling:** Wireshark, Kali Linux CLI


## Objective

Analyze a real-world packet capture to:

* Identify the infected Windows host
* Reconstruct the malware infection chain
* Extract host, network, and attacker indicators
* Distinguish attacker-owned C2 infrastructure from abused legitimate services


## Environment Overview

* **LAN Segment:** `10.1.17.0/24`
* **Default Gateway:** `10.1.17.1`
* **Active Directory Domain:** `BLUEMOONTUESDAY`
* **Domain Controller:** `10.1.17.2`


## Initial Observations

On initial review of the PCAP, a Windows client at `10.1.17.215` establishes a full TCP handshake with the external IP `5.252.153.241`. Shortly after, the client issues HTTP GET requests to:

```
/api/file/get-file
```

This behavior strongly indicates malicious payload retrieval from an external server.


## Victim Host Identification

### IP Address

* `10.1.17.215`

### MAC Address

* `00:d0:b7:26:4a:74` (Intel NIC)

Identified by inspecting Ethernet II headers on packets sourced from the infected client.

### Hostname

NBNS broadcast traffic from `10.1.17.215` to the broadcast address `10.1.17.255` reveals the NetBIOS name:

```
DESKTOP-L8C5GSJ<20>
```

The `<20>` suffix indicates the file server service; the base name `DESKTOP-L8C5GSJ` is the Windows hostname.

### Windows User Account

* `shutchenson`

The username was observed earlier in the infection chain during HTTP traffic associated with the phishing / fake authentication page, not during the malware payload or C2 stages.


## Infection Chain Summary

1. Victim browses to a phishing site impersonating Google Authenticator
2. Credential or identity data is exposed
3. Victim is redirected to a fake software download page
4. Malicious payloads are retrieved from attacker infrastructure
5. Persistence is established
6. Ongoing C2 communication begins
7. TeamViewer is installed and abused for interactive remote access


## Fake Software / Phishing Infrastructure

### Likely Fake Google Authenticator Domain

* `authenticator.org`

This domain was identified via DNS queries originating from the infected host prior to payload delivery. The domain mimics a legitimate Google service but is not owned by Google.


## Command-and-Control (C2) Analysis

### Attacker-Owned C2 Servers

The following IP addresses exhibit sustained post-infection beaconing behavior consistent with command-and-control activity:

* `5.252.153.241`
* `45.125.66.32`
* `45.125.66.252`

These hosts receive repeated HTTP requests containing execution status messages and system activity indicators.

### Abused Legitimate Infrastructure (Not Attacker-Owned C2)

* `185.188.32.26` – TeamViewer DynGate relay
* `199.232.214.172` – Microsoft Edge / BITS update infrastructure

Although these IPs exhibit high-volume or persistent traffic, packet inspection confirms they belong to legitimate services and are being abused rather than directly controlled by the attacker.


## Key Wireshark Filters Used

```text
http && ip.src == 10.1.17.215
dns && ip.src == 10.1.17.215
nbns
http.request.uri contains "message"
http && !(ip.dst == 5.252.153.241)
```


## Lessons Learned

* Malware analysis must consider the full timeline, including pre‑infection phishing activity
* Usernames often appear during phishing or form submission stages, not payload execution
* C2 identification requires behavioral analysis, not just suspicious traffic volume
* Legitimate services (TeamViewer, Microsoft CDNs) are commonly abused by attackers


## Additional Learning Resources

* Customizing Wireshark Column Display
  [https://unit42.paloaltonetworks.com/unit42-customizing-wireshark-changing-column-display/](https://unit42.paloaltonetworks.com/unit42-customizing-wireshark-changing-column-display/)

* Identifying Hosts and Users
  [https://unit42.paloaltonetworks.com/using-wireshark-identifying-hosts-and-users/](https://unit42.paloaltonetworks.com/using-wireshark-identifying-hosts-and-users/)

* Display Filter Expressions
  [https://unit42.paloaltonetworks.com/using-wireshark-display-filter-expressions/](https://unit42.paloaltonetworks.com/using-wireshark-display-filter-expressions/)

* Exporting Objects from a PCAP
  [https://unit42.paloaltonetworks.com/using-wireshark-exporting-objects-from-a-pcap/](https://unit42.paloaltonetworks.com/using-wireshark-exporting-objects-from-a-pcap/)


