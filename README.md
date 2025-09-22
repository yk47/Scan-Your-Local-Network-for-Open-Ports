# 📡 Task 1: Scan Your Local Network for Open Ports
## 🎯 Objective: Learn to discover open ports on devices in your local network to understand network exposure

### Prerequisites

- A machine on the target local network (your laptop/VM)
- Nmap installed (sudo apt install nmap / brew install nmap / Windows installer)
- Wireshark for packet capture
- Permission to scan the network and devices — only scan devices you own or have explicit permission for.

### 🗃️ Directory structure
```bash
Scan-Your-Local-Network-for-Open-Ports/
├── README.md
├── screenshots/
│ ├── 01-subnet.png
│ ├── 02-ping-sweep.png
│ ├── 03-top-ports.png
│ ├── 04-full-scan.png
│ ├── 05-machine-vuln.png
│ ├── 06-nmap-vuln.png
│ ├── 07-wireshark-port-scan-command.png
│ └── 08-wireshark-traffic-capture.png
└── scans/
├── host_full.nmap
└── host_full.xml
```

### 1.Find your IP & subnet
```bash
# Linux/macOS
ip addr show
# Or
ip a
```
<img width="1048" height="734" alt="01-subnet" src="https://github.com/user-attachments/assets/e3df241c-cf5e-4bbd-85b5-b8a3be4a820a" />

### 2.Ping sweep (discover live hosts)
```bash
sudo nmap -sn 192.168.1.1/24
# Or
sudo nmap -sn 192.168.0.1/24
```
<img width="1920" height="1051" alt="02-ping-sweep" src="https://github.com/user-attachments/assets/0924573b-e255-4d11-a9ca-00ab78706a32" />

### 3.Top ports scan (quick look)
```bash
sudo nmap -sS --top-ports 100 192.168.0.175
```
<img width="1920" height="1051" alt="03-top-ports" src="https://github.com/user-attachments/assets/c6187a86-bbd7-4998-91d3-9002721df813" />

### 4.Full TCP port scan + service/version detection
```bash
sudo nmap -sS -sV -p- -oA scans/host_full 192.168.0.175
```
<img width="968" height="662" alt="04-full-scan" src="https://github.com/user-attachments/assets/b0d42bfb-3507-4132-93d9-e094b070414f" />

### 5.Run vulnerability NSE scripts on specific services
```bash
sudo nmap --script=vuln -p22,80,443 192.168.0.175
```
<img width="1920" height="1051" alt="05-machine-vuln" src="https://github.com/user-attachments/assets/7774901b-569a-4ba3-96fc-cb57d7a6eecb" />

### 6.Run vulnerability NSE scripts on nmap.scanme.org
```bash
nmap -p- --open nmap.scanme.org
```
<img width="1920" height="1051" alt="06-nmap-vuln" src="https://github.com/user-attachments/assets/d858f155-07dd-4194-9601-52c1c57cc5f0" />

## 7.Capture with Wireshark while scanning
- Start a capture on the LAN interface (use a capture filter like host 192.168.1.25).
- Run the Nmap scan and then stop capture.

```bash
host 192.168.0.175 and (port 22 or port 80 or port 443 or portrange 1-65535)
```
<img width="1920" height="1051" alt="07-wireshark-port-scan-command" src="https://github.com/user-attachments/assets/07771259-6598-4ec0-baa7-65d9ca6525e1" />
<img width="1920" height="1080" alt="08-wireshark-traffic-capture" src="https://github.com/user-attachments/assets/ec337f3c-3dfa-4611-985e-58028f30bc29" />









