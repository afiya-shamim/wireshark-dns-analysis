# 🔍 DNS Traffic Analysis using Wireshark
## 📌 Case 1: Bing DNS Analysis (CNAME Chain)

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

## 📌 Case 2: HTTPS Record Query (Frame 1107 → 1111)
#### 🔹 DNS Query Analysis
- Frame: 1107 → Response: 1111
- Source: 192.168.31.66 (Client)
- Destination: 192.168.31.1 (DNS Resolver)
- Protocol: UDP (Port 53)
- Query Type: HTTPS (Type 65)
- Domain: www.google.com
- Transaction ID: 0x5049

#### 🔹 DNS Response Analysis
- Status: No error (Flags: 0x8180)
- Answer RRs: 1
- TTL: 14861 seconds (~4 hours)
- Response Time: ~18 ms

#### 🔹 HTTPS Record Details
- SvcPriority: 1
- TargetName: <Root>
- ALPN: h2, h3

#### 🔹 Key Observations
1. No A/AAAA record present in this response (no direct IP provided)
2. HTTPS record returns service-level metadata, not address mapping
3. ALPN values (h2, h3) indicate supported application protocols (HTTP/2, HTTP/3)
4. `TargetName: <Root>` indicates no alias target specified in this record
5. SvcPriority 1 represents highest priority for this service endpoint

### 📸 Screenshots

#### HTTPS Query (Frame 1107)
<img width="1363" height="722" alt="1107 query" src="https://github.com/user-attachments/assets/55c950b8-6a7b-4963-b6e5-503d14fe02f8" />

#### HTTPS Response (Frame 1111)
<img width="1366" height="729" alt="1111 response" src="https://github.com/user-attachments/assets/921d333a-d4db-4ce7-a1cb-cf52b7b3159f" />

#### 🔹 Evidence
- Query Frame: 1107
- Response Frame: 1111
- Transaction ID: 0x5049

## 📌 Case 3: Google DNS Analysis (IPv6 - AAAA Record)

### 🔹 DNS Query Analysis
- Frame: 1108 → Response: 1110
- Source: 192.168.31.66 (Client)
- Destination: 192.168.31.1 (DNS Resolver)
- Protocol: UDP (Port 53)
- Query Type: AAAA (IPv6)
- Domain: www.google.com
- Transaction ID: 0x74bb

### 🔹 DNS Response Analysis
- Status: No error (Flags: 0x8180)
- Answer RRs: 8
- TTL: 3 seconds
- Response Time: ~5 ms

### 🔹 IPv6 Address Details
Example IPv6 addresses returned:
- 2001:4860:482d:7700::
- 2001:4860:482b:7700::
- 2001:4860:4828:7700::
- 2001:4860:4826:7700::

### 🔹 Key Observations
1. Direct IPv6 resolution observed (AAAA records returned)
2. Multiple IP addresses indicate load balancing and distributed infrastructure
3. No CNAME chain present in this response
4. Very short TTL (3 seconds) suggests highly dynamic IP rotation

### 📸 Screenshots

#### AAAA Query (Frame 1108)
<img width="1366" height="741" alt="1108 query" src="https://github.com/user-attachments/assets/3108e0b5-a31d-4bc2-8b8c-e8095748077e" />


#### AAAA Response (Frame 1110)
<img width="1364" height="730" alt="1110 response" src="https://github.com/user-attachments/assets/b5b41559-7f1a-4959-b0ac-94fa760714d5" />

### 🔹 Evidence
- Query Frame: 1108
- Response Frame: 1110
- Transaction ID: 0x74bb

## 📌 Case 4: Google DNS Analysis (IPv4 - A Record)

### 🔹 DNS Query Analysis
- Frame: 1109 → Response: 1112
- Source: 192.168.31.66 (Client)
- Destination: 192.168.31.1 (DNS Resolver)
- Protocol: UDP (Port 53)
- Query Type: A (IPv4 Address)
- Domain: www.google.com
- Transaction ID: 0x40e4

### 🔹 DNS Response Analysis
- Status: No error (Flags: 0x8180)
- Answer RRs: 8
- Response Time: ~19.9 ms
- TTL: 86 seconds

### 🔹 IPv4 Address Details
Multiple A records returned:
- 142.251.154.119  
- 142.251.151.119  
- 142.251.156.119  
- 142.251.157.119  
- 142.251.150.119  
- 142.251.152.119  
- 142.251.153.119  
- 142.251.155.119  

### 🔹 Key Observations
1. Multiple IPv4 addresses indicate load balancing across servers
2. Same domain resolves to different backend IPs (distributed infrastructure)
3. TTL 86 seconds shows moderate caching for IPv4 records
4. Direct A record resolution (no CNAME chain in this case)
5. Fast response time (~19 ms) from local DNS resolver

### 📸 Screenshots

#### A Record Query (Frame 1109)
<img width="1366" height="728" alt="1109 query" src="https://github.com/user-attachments/assets/883552b9-1cbb-442f-aec7-54cf2b10f662" />

#### A Record Response (Frame 1112)
<img width="1366" height="736" alt="1112 response" src="https://github.com/user-attachments/assets/fe2ff0b9-07e3-4bd6-bc1f-307612ef8c31" />

### 🔹 Evidence
- Query Frame: 1109
- Response Frame: 1112
- Transaction ID: 0x40e4

  ## 📌 Final Conclusion
This project demonstrates end-to-end DNS resolution analysis using Wireshark, covering A, AAAA, HTTPS records and CNAME chaining. It highlights how modern DNS systems use distributed infrastructure, CDN routing, and load balancing to optimize performance and reliability.
