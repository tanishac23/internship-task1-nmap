# 🔍 Task 1: Scan Your Local Network for Open Ports

## 📌 Objective
To discover live devices (hosts) and open ports on the local network using port scanning techniques, understand the potential exposure of services, and practice ethical reconnaissance.

---

## 🧰 Tools Used

| Tool     | Purpose |
|----------|---------|
| **Nmap** | Network Mapper – used for scanning and discovering hosts, services, and open ports |

---

## 🖥️ System Setup

- **Device**: Windows 10  
- **Network**: Connected to College Wi-Fi  
- **Interface Used**: Wi-Fi  
- **IPv4 Address**: `172.16.220.238`  
- **Subnet Mask**: `255.255.252.0`  
- **IP Range**: `172.16.220.0/22`

---

## ⚙️ What is Nmap?

**Nmap (Network Mapper)** is an open-source tool used in ethical hacking to:  
- Discover devices on a network  
- Find open ports  
- Detect services and operating systems  
- Perform security audits  

It is often used in the **reconnaissance and scanning phases** of penetration testing.

---

## 🔎 Step 1: Find Your IP and Subnet

### 🧠 Command:
```bash
ipconfig
```

**Output (Wi-Fi section):**
```
IPv4 Address. . . . . . . . . . . : 172.16.220.238
Subnet Mask . . . . . . . . . . . : 255.255.252.0
Default Gateway . . . . . . . . . : 172.16.220.1
```
📷 **Screenshot:** 
https://github.com/tanishac23/internship-task1-nmap/blob/main/images/IpConfigOutput.png

---

## 🔎 Step 2: Scanning Online Devices on My Network

### 🧠 Command Used:
```bash
nmap -sn 172.16.220.0/22
```

**📖 What this does:**
- `-sn`: Ping scan — discovers which devices are alive without scanning ports.  
- Sends ICMP Echo Requests, ARP requests, or TCP ACK/SYN to detect live devices.

**📊 Observation:**
- Scanned IP range: `172.16.220.0/22` (1024 addresses)  
- Scan time: ~21.47 seconds  
- Devices found: 62 online hosts  
- For each live host, details shown:  
  - IP Address  
  - Response Latency  
  - MAC Address (if available)  
  - Vendor Name  

📷 **Screenshot:** 
https://github.com/tanishac23/internship-task1-nmap/blob/main/images/PingSweep1.png
https://github.com/tanishac23/internship-task1-nmap/blob/main/images/PingSweep2.png

---

## ✅ Step 3: Scan a Live Host and Discover Open Ports

After identifying active devices, I scanned `172.16.220.11` for open ports.

### 🧠 Command Used:
```bash
nmap -sS 172.16.220.11
```

**📖 Explanation:**
- `-sS`: SYN scan (half-open scan), faster and stealthier than full connect scan.

**📊 Output Summary:**
- Host online (latency ~6.1 ms)  
- Open ports:
  - **22/tcp** – SSH
  - **80/tcp** – HTTP  
- MAC vendor: Netgear (likely a router or switch)  

📷 **Screenshot:** 
https://github.com/tanishac23/internship-task1-nmap/blob/main/images/SuccessfulPortScan.png

---

## ✅ Step 4: Scanning Specific Ports on Multiple IPs

### 🧠 Command Used:
```bash
nmap -sS -p 21,22,23,80,443 172.16.220.1-13
```

**📖 Explanation:**
- `-sS`: SYN scan  
- `-p 21,22,23,80,443`: Specific ports —  
  - 21: FTP  
  - 22: SSH  
  - 23: Telnet  
  - 80: HTTP  
  - 443: HTTPS  
- `172.16.220.1-13`: Scans IPs `.1` to `.13`

**📊 Output Summary:**
- Found devices with various ports open.
- Example: Some devices had only SSH & HTTP, some none.

📷 **Screenshot:** 
https://github.com/tanishac23/internship-task1-nmap/blob/main/images/SuccessfulPortScan.png

---

## ✅ Step 5: Aggressive OS Detection & Service Version Detection

### 🧠 Command Used:
```bash
nmap -A 172.16.220.11
```

**📖 What `-A` Does:**
- OS Detection  
- Version Detection  
- Script Scanning  
- Traceroute  

**📊 Output Summary:**
- Open ports:
  - **22/tcp** – SSH  
  - **80/tcp** – HTTP  
- OS Guess: Linux 3.X / 4.X  
- MAC Vendor: Netgear  

📷 **Screenshot:** 
https://github.com/tanishac23/internship-task1-nmap/blob/main/images/AggresiveScan1.png
https://github.com/tanishac23/internship-task1-nmap/blob/main/images/AggresiveScan2.png
https://github.com/tanishac23/internship-task1-nmap/blob/main/images/AggresiveScan3.png

---

## ✅ Step 6: Verbose Scan

### 🧠 Command Used:
```bash
nmap -v 172.16.220.11
```

**📖 Explanation:**
- `-v`: Verbose mode — shows real-time scanning process.

**📊 Output Summary:**
- ARP ping used for discovery  
- Parallel DNS resolution done  
- SYN scan completed  
- Open ports: **22** (SSH), **80** (HTTP)  
- MAC vendor: Netgear  

📷 **Screenshot:** 
https://github.com/tanishac23/internship-task1-nmap/blob/main/images/Verbosescan.png

---

## ✅ Step 7: Scanning Specific Ports on Multiple IPs

### 🧠 Command Used:
```bash
nmap -sS -p 21,22,23,80,443 172.16.220.1-13
```

**📖 Explanation:**
- -sS – SYN (stealth) scan, faster and less detectable.
-p 21,22,23,80,443 – Scan only these common ports:
21 → FTP
22 → SSH
23 → Telnet
80 → HTTP
443 → HTTPS
- 172.16.220.1-13 – Targets IPs from .1 to .13.

**📊 Output Summary:**
- Identified open ports on multiple hosts in the given range.
- Several devices responded with open services.
- Helps focus on high-value ports instead of scanning all 65,535.

📷 **Screenshot:** 
https://github.com/tanishac23/internship-task1-nmap/blob/main/images/multi_IP_SpecificPort1.png
https://github.com/tanishac23/internship-task1-nmap/blob/main/images/multi_IP_SpecificPort2.png

---

## 📌 Conclusion

This exercise demonstrated how **Nmap** can be used for:
- **Host Discovery** (`-sn`)
- **Port Scanning** (`-sS`)
- **Targeted Port Scans** (`-p`)
- **OS and Version Detection** (`-A`)
- **Verbose Monitoring** (`-v`)
- **Default Script Execution** (`-sC`)

By scanning my local network, I found multiple online devices, identified their open ports, and learned their OS and vendor details — essential skills for ethical hacking reconnaissance.
