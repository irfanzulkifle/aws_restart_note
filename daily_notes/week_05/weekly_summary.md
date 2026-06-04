# Week 5 Summary — April 27–30, 2026
**AWS re/Start Cohort 3: Project CloudIgnite**

---

## What We Learned

### Networking Deep Dive (Mon Apr 27)
- **Subnet masks:** Bitwise AND operation to determine network membership
- **CIDR blocks:** `/16` = 65,536 addresses; larger prefix = smaller network; subnetting divides existing IPs
- **Application protocols:** HTTP (80), HTTPS (443), SSL/TLS, SMTP (send), POP/IMAP (receive), RDP (3389), SSH (22)
- **DNS:** Translates domain names to IP addresses (like a phone book)
- **Troubleshooting tools:** `ping` (Layer 3), `traceroute` (Layer 3), `nslookup` (DNS), `netstat` (Layer 4), `telnet` (port check, Layer 4), `curl`/`wget` (Layer 7)
- **Lab 265:** Network command exploration on EC2
- **Lab 266:** Connectivity troubleshooting — Apache not running + missing Security Group rule for port 80

### IoT & Enterprise Mobility (Tue Apr 28)
- **Wireless technologies:** Wi-Fi (WPA2), Bluetooth/BLE, 5G, Satellite
- **IoT:** Connected devices reporting data, monitored/controlled remotely
- **AWS IoT Core:** Supports HTTPS, MQTT, WSS, LoRaWAN
- **Amazon WorkSpaces:** Virtual desktop (Windows/Linux) accessible from any device; not the same as EC2
- **Lab 267:** Build VPC from scratch — 2 public + 2 private subnets, route tables, Security Group, EC2 with Apache

### Introduction to Security (Tue Apr 29 — continued)
- **CIA Triad:** Confidentiality, Integrity, Availability
- **Security terms:** Attacker, vulnerability, threat, breach, control
- **Threats:** Malware (virus, spyware, worm, trojan, ransomware), DDoS, Man-in-the-Middle, Phishing, Social Engineering
- **AWS Shared Responsibility Model:** AWS = "Security OF the Cloud" (hardware, infra); Customer = "Security IN the Cloud" (data, apps, IAM)
- **Security controls:** Preventive, Detective, Corrective
- **Security lifecycle:** Prevention → Detection → Response → Analyze
- **Prevention phase:** Identify assets (nmap, Systems Manager), assess vulnerabilities (CVE), implement countermeasures
- **Network hardening:** Default-deny firewalls, close unused ports, network segmentation
- **System hardening:** Patch OS, remove unused apps, monitor changes
- **Layered security:** Perimeter → Network → Endpoint → Application → Data
- **IAM:** Principle of least privilege, MFA, strong password policies

### Security Services & Hardening (Wed Apr 30)
- **Packet sniffing & Wireshark:** HTTPS encrypts captured packets; passwords only sent during login
- **VPN vs Firewall:** VPN encrypts data in transit; firewall controls port access
- **AWS firewall tools:** AWS Network Firewall, NACLs
- **IPS (Intrusion Prevention System):** Anomaly-based and signature-based detection
- **Amazon Inspector:** Scans EC2 and Lambda for vulnerabilities
- **AWS Trusted Advisor:** Best practice recommendations
- **Amazon GuardDuty:** Continuous AI-powered threat detection (VPC Flow Logs, DNS logs, CloudTrail)
- **AWS Shield:** DDoS protection (Standard = free, Advanced = paid)
- **AWS CloudTrail:** Audit logging of all API activity
- **AWS Security Hub:** Centralized security findings dashboard
- **Authentication vs Authorization:** Who you are vs what you can do
- **Lab 276:** Amazon Inspector — found and fixed outdated Python library in Lambda

### Key CLF-C02 Connections
- CIA Triad, Shared Responsibility Model, Security Groups, NACLs, Inspector, Trusted Advisor, GuardDuty, Shield, CloudTrail, Security Hub, IAM (least privilege, MFA), VPC security architecture

---

## Daily Notes
- [April 27](./2026-04-27.md) — Subnet Masks, CIDR, OSI Recap, TCP/UDP, Application Protocols, DNS, Troubleshooting Tools
- [April 28](./2026-04-28.md) — Wireless, IoT, Amazon WorkSpaces, VPC Lab 267, CIA Triad, Security Intro
- [April 29](./2026-04-29.md) — Security Threats, Shared Responsibility Model, Security Lifecycle, Network/System Hardening, IAM
- [April 30](./2026-04-30.md) — Wireshark, VPN vs Firewall, AWS Security Services, Amazon Inspector Lab, Cryptography Intro
