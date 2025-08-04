# 🔍 Network Scanning using Nmap – Internship Task

## 📌 Objective:
To perform network scanning using Nmap on a local network and identify all live hosts, open ports, and services.

---
## 🖥️ My Device Details:
- **Laptop IP (IPv4):** `192.168.29.126`
- **Default Gateway (Router IP):** `192.168.29.1`

---
## ✅ Step 1: Discover Live Hosts in the Network

### Command Used:
```bash
nmap -sn 192.168.29.0/24
This command performs a Ping Scan to discover which devices are active in the local network.

✅ Step 2: Port Scanning on Detected Devices
Devices Chosen:
192.168.29.1 – Default Gateway (Router)
192.168.29.89 – Another host on the network

Command Used:
nmap 192.168.29.1
This scans for open ports on the router.

✅ Step 3: Aggressive Scan with OS and Version Detection
Command Used:
nmap -sN -A 192.168.29.1
This performs a more detailed scan with:

OS detection
Version detection
Traceroute
Script scanning

✅ Conclusion:
Successfully identified live hosts in the network
Performed detailed scanning on devices
Detected open ports and services running on those ports



