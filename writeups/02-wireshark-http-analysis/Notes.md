PCAP ingame notes: 
On first glance at the pcap there appears to be a client at 10.1.17.215 that makes a full TCP handshake with malicious IP 5.252.153.241 then an HTTP get request is made for api/file/get-file.

Now I went into a packet where the infected client is the source and found that the MAC address is Intel_26:4a:74 (00:d0:b7:26:4a:74)

Looking into the nbns traffic there is traffic between 10.1.17.215 the infected computer and 10.1.17.255 which is the broadcast address naming the infected computer DESKTOP-L8C5GSJ<20> a file server<20>, well just workstation action as the host name of the infected windows client

I've been checking HTTP packets' TCP streams and trying to find a user account name for the infected Windows client and I'm not sure if it is explicitly mentioned over the network, or at least I'm not sure where else to look right now.

The likely domain name for the fake Google Authenticator page I found in the DNS packets using (dns && ip.src == 10.1.17.215 && dns.qry.name contains "auth") this helped me locate: google-authenticator.burleson-appliance.net

The IP address of the C2 server appears to be consistent with the social media posts, 5.252.153.241. 

Final Answers:

    What is the IP address of the infected Windows client?
    - 10.1.17.215
    What is the mac address of the infected Windows client?
    -Intel_26:4a:74 (00:d0:b7:26:4a:74)
    What is the host name of the infected Windows client?
    - DESKTOP-L8C6GSJ
    What is the user account name from the infected Windows client?
    - Not identified in the traffic
    What is the likely domain name for the fake Google Authenticator page?
    - google-authenticator.burleson-appliance.net
    What are the IP addresses used for C2 servers for this infection?
    - 5.252.153.241
    - I think this 185.188.32.26 might also qualify as C2, but it seems to be what he is connecting through (DynGate)


IP address: 10.1.17.215
Host name: DESKTOP-L8C5GSJ
MAC address: 00:d0:b7:26:4a:74
Windows user account name: shutchenson

Probable fake software site for initial malware download:
• authenticatoor.org

2025-01-22 - TRAFFIC ANALYSIS EXERCISE ANSWERS
IP addresses used for C2 traffic:
• 5.252.153.241
• 45.125.66.32
• 45.125.66.252 


So I wasn't exactly on the money yet, but I am getting better with filtering and searching with wireshark. 

I am now going to read through the additional tutorials listed with the exercise. 

https://unit42.paloaltonetworks.com/unit42-customizing-wireshark-changing-column-display/
https://unit42.paloaltonetworks.com/using-wireshark-identifying-hosts-and-users/
https://unit42.paloaltonetworks.com/using-wireshark-display-filter-expressions/
https://unit42.paloaltonetworks.com/using-wireshark-exporting-objects-from-a-pcap/
