# Capstone Summary

This portfolio is a 12 day build focused on practical cybersecurity fundamentals and professional documentation. Each day produces a writeup with evidence, tool output, and a clear explanation of what I observed and how I validated it.

## What I Built
- 12 structured lab writeups
- A repeatable workflow for recon, analysis, and documentation
- A set of artifacts and screenshots that support findings
- A skills progression across networking, web security fundamentals, and defensive triage

## Skills Matrix

| Day | Topic | Core Skills | Tools |
| --- | --- | --- | --- |
| 01 | Network recon | scanning, enumeration, service identification | nmap |
| 02 | Packet analysis | filtering, stream reconstruction, protocol understanding | wireshark |
| 03 | Linux log triage | parsing auth logs, identifying patterns | grep, awk, sort, uniq |
| 04 | Burp basics | intercepting traffic, request editing, repeater workflow | burp suite |
| 05 | SQLi fundamentals | identifying injection points, validating impact in lab | burp suite |
| 06 | XSS basics | reflected and stored testing in lab, context awareness | burp suite, browser dev tools |
| 07 | IDOR testing | authorization testing, object reference manipulation in lab | burp suite |
| 08 | Blue team triage | detection mindset, evidence collection, basic alert triage | logs, queries, notes |
| 09 | Traversal testing | path manipulation, encoding bypass awareness in lab | burp suite, curl |
| 10 | Auth and session | session review, token handling, auth flow analysis | burp suite |
| 11 | Nmap NSE vuln | script selection, safe scans, reporting | nmap NSE |
| 12 | Incident timeline | correlation, normalization, narrative building | grep, sorting, timeline notes |

## If You Only Read Three Writeups, Read These
- Day 01: network recon with Nmap
- Day 03: Linux SSH log triage
- Day 12: incident timeline reconstruction

## Interview Ready Stories
Use these as short stories you can expand on in interviews.

### Day 01: Recon and prioritization
- Situation: needed to quickly understand an unknown target in a lab scope
- Task: identify exposed services and prioritize next steps
- Action: performed layered scans and validated results with service enumeration
- Result: produced a clean service inventory and risk notes

### Day 03: Detecting brute force patterns
- Situation: reviewed auth logs for suspicious activity
- Task: identify repeated failed logins and likely attacker sources
- Action: used command line parsing to extract IPs and counts, then built a short timeline
- Result: generated a clear top IP list and recommended mitigations

### Day 12: Building an incident timeline
- Situation: multiple log sources with different timestamp formats
- Task: reconstruct sequence of events and summarize impact
- Action: normalized timestamps, correlated indicators, and wrote both technical and executive summaries
- Result: produced a coherent timeline and clear narrative of attacker behavior

## Notes on Evidence
All artifacts are sanitized and lab only. I avoid uploading raw sensitive files such as large PCAPs, secrets, tokens, or identifying information.
