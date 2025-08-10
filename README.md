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

📷 **Screenshot:** `<!-- ADD SS HERE -->`

---

## ✅ Step 5: Scan a Live Host and Discover Open Ports

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

📷 **Screenshot:** `<!-- ADD SS HERE -->`

---

## ✅ Step 6: Scanning Specific Ports on Multiple IPs

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

📷 **Screenshot:** `<!-- ADD SS HERE -->`

---

## ✅ Step 7: Aggressive OS Detection & Service Version Detection

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

📷 **Screenshot:** `<!-- ADD SS HERE -->`

---

## ✅ Step 8: Verbose Scan

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

📷 **Screenshot:** `<!-- ADD SS HERE -->`

---

## ✅ Step 9: Script Scan using `-sC`

### 🧠 Command Used:
```bash
nmap -sC 172.16.220.11
```

**📖 Explanation:**
- Runs **default NSE scripts** for deeper information.

**📊 Output Summary:**
- **22/tcp** – SSH (ssh-hostkey script failed)  
- **80/tcp** – HTTP (no HTML title found)  
- MAC vendor: Netgear  

📷 **Screenshot:** `<!-- ADD SS HERE -->`

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
