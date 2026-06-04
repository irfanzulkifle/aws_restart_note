# Week 4 Summary — April 20–24, 2026
**AWS re/Start Cohort 3: Project CloudIgnite**

---

## What We Learned

### Bash Scripting (Mon Apr 20)
- **Script basics:** Shebang (`#!/bin/bash`), `echo`, `read`, variables, `chmod +x`, `./script.sh`
- **Conditionals:** `if/elif/else/fi`, comparison operators (`-eq`, `-gt`, `-lt`), file test operators (`-f`, `-e`, `-d`)
- **Loops:** `for` (range/list), `while`, `until`, `break`, `continue`
- **Other:** `exit` codes, command substitution (`$(date)`), `printf`
- **Lab:** Backup script using `tar -czvf` with date-stamped filenames
- **Linux package management:** `yum` (Amazon Linux), `apt` (Ubuntu/Debian)
- **AWS CLI installation:** Download, unzip, install, configure with `aws configure`

### System Logs & Networking Intro (Tue Apr 21)
- **Log severity levels:** Emergency (0) → Debug (7); stored in `/var/log/`
- **Key log files:** `syslog`, `secure`, `kern.log`, `boot.log`, `cron.log`, `httpd/`
- **Log commands:** `cat`, `tail -f`, `grep`, `lastlog`
- **Internet history:** Packet switching → TCP → dial-up → WWW
- **Network concepts:** Node, client, server, LAN, switch, router, modem
- **OSI Model (7 layers):** Application (7), Presentation (6), Session (5), Transport (4), Network (3), Data Link (2), Physical (1)

### Networking & VPC Deep Dive (Wed Apr 22)
- **Network components:** NIC, switch (Layer 2), router (Layer 2–3), modem
- **Cables:** Fiber optic, coaxial, twisted pair (CAT6/RJ45)
- **Network types:** LAN vs WAN; VPC ≈ LAN in the cloud
- **Topologies:** Bus, star, mesh, hybrid
- **Amazon VPC:** Logically isolated virtual network; public vs private subnets; CIDR blocks; Internet Gateway; VPC Peering
- **Protocols:** TCP (connection-oriented, 3-way handshake SYN→SYN-ACK→ACK) vs UDP (connectionless, fast)
- **IP addressing:** IPv4 (32-bit), IPv6 (128-bit), public vs private IP, DHCP, static/Elastic IP
- **Subnetting:** CIDR notation, formula for host count
- **Port numbers:** 22 (SSH), 80 (HTTP), 443 (HTTPS), 20/21 (FTP), 53 (DNS), 3389 (RDP)

### VPC Labs & Troubleshooting (Thu Apr 23)
- **Private IP ranges (RFC 1918):** `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`
- **Lab 261:** Public vs Private IP troubleshooting — OSI-based diagnosis
- **Lab 262:** Elastic IP Address — static public IP that persists across stop/start
- **VPC fundamentals:** Subnets, route tables, IGW, Security Groups, NACLs
- **Security Group vs NACL:** Instance-level/stateful vs Subnet-level/stateless

### VPC Labs & Security Components (Fri Apr 24)
- **NAT Gateway:** Outbound-only internet for private subnets; requires Elastic IP
- **Route tables:** `0.0.0.0/0 → IGW` makes a subnet public
- **Internet Gateway:** Required for public subnet internet access
- **Security Groups:** Default deny all inbound; stateful; allow-only rules
- **NACLs:** Default allow all; stateless; both allow and deny rules
- **Lab 263:** Create VPC with public subnet (manual VPC build)
- **Lab 264:** Fix broken VPC (full troubleshooting checklist)

### Key CLF-C02 Connections
- VPC, subnets (public/private), Security Groups, NACLs, Internet Gateway, NAT Gateway, Route Tables, CIDR blocks, Elastic IP, TCP vs UDP, key port numbers

---

## Daily Notes
- [April 20](./2026-04-20.md) — Bash Scripting, Linux Software Management, AWS CLI Installation
- [April 21](./2026-04-21.md) — System Logs, Bash Challenge Lab, Intro to Networking & OSI Model
- [April 22](./2026-04-22.md) — Networking Fundamentals, VPC, TCP/UDP, IP Addressing, Ports
- [April 23](./2026-04-23.md) — IP Addressing, Elastic IP, VPC Fundamentals, CIDR Calculation
- [April 24](./2026-04-24.md) — NAT Gateway, Route Tables, Security Groups, NACLs, VPC Labs
