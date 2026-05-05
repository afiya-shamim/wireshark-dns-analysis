# 🔍 DNS Traffic Analysis using Wireshark

## 📌 Project Overview
Captured and analyzed DNS traffic for `www.bing.com` using Wireshark to understand modern DNS resolution, CNAME chaining, and CDN-based infrastructure behavior.

## 🛠️ Tools Used
- Wireshark
- Windows 11

## 🎯 Key Findings
1. **DNS Query Type**: HTTPS (Type 65) request observed
2. **CNAME Chain Discovered**:
   www.bing.com  
   → www-www.bing.com.trafficmanager.net  
   → www.bing.com.edgekey.net  
   → e86303.dscx.akamaiedge.net  

3. **No Direct IP Resolution**:
   The DNS response did not include an A record, indicating multi-step resolution.

4. **Modern DNS Behavior**:
   Use of traffic management and CDN infrastructure for request routing.

## 🔐 SOC Relevance
- DNS analysis helps identify suspicious redirections and anomalies
- CNAME chains can indicate complex infrastructure or evasion techniques
- Useful in detecting DNS-based attacks (tunneling, beaconing)

## 📸 Screenshots
* Frame 20 (DNS Query)
<img width="1362" height="721" alt="Capture" src="https://github.com/user-attachments/assets/f5b2114f-d5b6-415f-89f7-d939121df7a6" />
* DNS Response (Frame 23)
<img width="1362" height="721" alt="Project1 b" src="https://github.com/user-attachments/assets/ad24e820-9e9f-460c-b276-c8b7070572e8" />
Note: Frame 20 represents the DNS query and Frame 23 represents the corresponding DNS response for Transaction ID 0x77ac.


## 🚀 Skills Demonstrated
- DNS Protocol Analysis
- Packet Inspection using Wireshark
- Understanding of CNAME chaining
- Basic Threat Analysis

---
**👩‍💻 Author:** Afiya Shamim  
