## Final takeaways / Notes

1. The goal of this lab was to practice network recon using Nmap, learning how different scan types behave and how all of the results can be interpreted.

2. Host Discovery vs. Scanning
- Host discovery wasn't as straight forward as simply scanning, using ICMP pings and other techniques were not effective in the test environment because of host port rules, whether that is firewall or whatever else. -Pn was important because it forces Nmap to treat the host as online even if no return packets are recieved. Port scanning then can proceed even when the initial discovery probes just get filtered out.

3. Scan Types
- SYN Scan (-sS) or the stealthy scan: 
    - Process:
    - Syn -> Syn/Ack = open
    - Syn -> RST = closed
    - No response = filtered
    - It uses the response behavior of an almost fake or generally just an unfulfilled TCP handshake to determine the status of network ports.

- TCP Scan (-sT):
    - Completes a full TCP handshake Syn -> Syn/Ack -> Ack
    - This scan can be watched easily with wireshark because of the full handshake
    - It checks how the full OS-level connection behaves.

- Null / Fin / Xmas Scans (-sN, -sF, -sX):
    - These scans weren't generally as useful because they would pretty much always return open|filtered because their detection is based on getting no response either from sending a null content packet, sending a finale signal packet, or a combination of FIN, PSH, and URG packets to try to elicit a closure response or no response at all for the sake of stealthy port scanning and bypassing basic firewalls.

4. Important Options
- -p (port, -p- "all ports" or -p 1-20)
- -Pn (bypass discovery failures)
- -vv (verbose to watch the process and understand the output better)
- -T4 (Aggressive timing, it helped me speed up a 16 minute scan by several minutes)
- -sV (detect service banners and versions, I found not only the open ports but what was running on that interface, giving me actual intelligence on a foreign system)
- --top-ports (with a number specification worked very well in scanning quickly for common locations)

5. Nmap Scripting Engine (NSE)
- I explored the libraries as well as the script.db which is greppable and found dependencies and script details quite well.
    - https://nmap.org/book/nse.html  (documentation)
    - https://nmap.org/nsedoc  (script database)    

