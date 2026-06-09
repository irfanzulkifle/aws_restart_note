# AWS Certified Cloud Practitioner (CLF-C02) — Exam Cheat Sheet
**Consolidated from Cohort 3: Project CloudIgnite lecture notes (Weeks 3–10)**

---

## Exam Format
- **65 questions** (50 scored + 15 unscored)
- **90 minutes**
- **Passing score:** 700 / 1000
- **Format:** Multiple choice, multiple response
- **Domains:** Cloud Concepts (24%), Security & Compliance (30%), Cloud Technology & Services (34%), Billing, Pricing & Support (12%)

---

## Table of Contents
1. [Domain 1: Cloud Concepts (24%)](#domain-1-cloud-concepts-24)
2. [Domain 2: Security and Compliance (30%)](#domain-2-security-and-compliance-30)
3. [Domain 3: Cloud Technology and Services (34%)](#domain-3-cloud-technology-and-services-34)
4. [Domain 4: Billing, Pricing, and Support (12%)](#domain-4-billing-pricing-and-support-12)
5. [Quick Reference Tables](#quick-reference-tables)
6. [Common Exam Gotchas](#common-exam-gotchas)

---

# Domain 1: Cloud Concepts (24%)

## What is Cloud Computing?
- On-demand delivery of IT resources over the internet with pay-as-you-go pricing
- No need to buy/own/maintain physical data centres

## Cloud Benefits
| Benefit | Description |
|---------|-------------|
| **Agility** | Quickly experiment with new ideas; spin up resources in minutes |
| **Elasticity** | Scale up/down based on demand; no over-provisioning |
| **Cost savings** | Pay only for what you use; no upfront hardware investment |
| **Global reach** | Deploy worldwide in minutes using AWS Regions and AZs |
| **High availability** | Multi-AZ deployments; automatic failover |
| **Fault tolerance** | System continues operating even when components fail |

## Cloud Deployment Models
| Model | Description |
|-------|-------------|
| **Cloud** | All resources in AWS (e.g., startup running entirely on AWS) |
| **Hybrid** | Mix of on-premises and AWS (e.g., bank keeping sensitive data on-prem) |
| **On-premises** | Private cloud; AWS Outposts for running AWS on-prem |

## Cloud Service Models
| Model | What AWS Manages | Example |
|-------|-----------------|---------|
| **IaaS** (Infrastructure) | Hardware, networking, virtualisation | **EC2** — you manage OS, apps, data |
| **PaaS** (Platform) | Everything except your code and data | **Lambda**, **Elastic Beanstalk** |
| **SaaS** (Software) | Everything | **Gmail**, **WorkSpaces**, **SageMaker** |

## Architecture Concepts
| Concept | Meaning |
|---------|---------|
| **High Availability** | System stays running even during failures (Multi-AZ) |
| **Fault Tolerance** | System continues operating without interruption (redundant components) |
| **Scalability** | Ability to grow capacity (vertical = bigger instance; horizontal = more instances) |
| **Elasticity** | Auto-scale up AND down based on demand |
| **Agility** | Speed at which you can provision and de-provision resources |

## Microservices vs Monolithic
| | Monolithic | Microservices |
|-|-----------|---------------|
| Structure | All-in-one | Each service independent |
| Scaling | Scale everything | Scale individual services |
| Failure | One failure affects all | Isolated failures |
| AWS services | — | ECS, EKS, Lambda, API Gateway |

## Infrastructure as Code (IaC)
- Define cloud infrastructure as code instead of clicking through the console
- Reproducible, version-controlled, consistent
- **AWS CloudFormation** (AWS-native IaC)
- **Terraform** (third-party, multi-cloud)

## AWS Cloud Adoption Framework (CAF)
- **Planning tool** for transitioning from on-premises to cloud
- **6 Perspectives** — 3 Business + 3 Technical

| Category | Perspective | Focus Areas |
|----------|-------------|-------------|
| **Business** | Business | IT finance, strategy, benefit realization, risk management |
| | People | Change management, training, skills readiness |
| | Governance | Project management, performance, license management |
| **Technical** | Platform | Compute (EC2), network (VPC), storage (EBS/S3), app design |
| | Security | IAM, data protection, security controls, incident response |
| | Operations | Monitoring, maintenance, performance, disaster recovery |

> Key: Even if technology is ready, failure to train people or align governance will cause migration to fail

## AWS Well-Architected Framework (WAF)
- **Design/operational tool** for building cloud systems efficiently, securely, cost-effectively
- Post-migration tool (CAF = planning, WAF = building/operating)

| Pillar | Core Question |
|--------|---------------|
| **Operational Excellence** | Are we delivering business value and improving? |
| **Security** | Are we protecting systems and data? |
| **Reliability** | Can the system recover and meet demand? |
| **Performance Efficiency** | Are we using resources efficiently? |
| **Cost Optimization** | Are we eliminating waste? |
| **Sustainability** | Is cloud usage environmentally responsible? |

### Well-Architected Design Principles
- **Stop guessing capacity** — use Auto Scaling
- **Test systems at production scale** — duplicate, test, shut down
- **Automate to ease experimentation** — code-based provisioning (Terraform, Python)
- **Allow for evolutionary architectures** — design for change
- **Drive architecture using data** — data-driven decisions
- **Improve through game days** — simulate failures, practice recovery

## Reliability & High Availability
| Term | Definition | Measurement |
|------|-----------|-------------|
| **Reliability** | System works as expected | MTBF = Time ÷ Failures |
| **Availability** | System is up and running | % uptime ("nines") |

### The "Nines" Scale
| Nines | % | Max Downtime/Year |
|-------|---|-------------------|
| 3-nines | 99.9% | ~8.7 hours |
| 4-nines | 99.99% | ~52 minutes |
| 5-nines | 99.999% | ~5 minutes |

### High Availability — 3 Prime Factors
1. **Fault Tolerance** — redundant components (Multi-AZ)
2. **Scalability** — Auto Scaling
3. **Recoverability** — restore after failure/disaster

### Traditional → AWS Service Mapping
| Traditional | AWS |
|-------------|-----|
| Physical server | EC2 |
| Load balancer | ELB |
| SAN storage | EBS |
| NAS storage | EFS |
| Tape backup | S3 |
| Active Directory | AWS Directory Service |

---

# Domain 2: Security and Compliance (30%)

## AWS Shared Responsibility Model

```
┌─────────────────────────────────────────────┐
│  CUSTOMER responsibility "IN the cloud"     │
│  ┌───────────────────────────────────────┐  │
│  │ Customer data                         │  │
│  │ Application code & installed software │  │
│  │ IAM (users, roles, policies)          │  │
│  │ OS, network, firewall config (EC2)    │  │
│  │ Client/server-side encryption         │  │
│  │ Security Group / NACL configuration   │  │
│  └───────────────────────────────────────┘  │
│                                             │
│  AWS responsibility "OF the cloud"          │
│  ┌───────────────────────────────────────┐  │
│  │ Physical data centres & hardware      │  │
│  │ Compute, storage, network infra       │  │
│  │ Hypervisor / virtualisation layer     │  │
│  │ Managed services' underlying OS       │  │
│  └───────────────────────────────────────┘  │
└─────────────────────────────────────────────┘
```

**Key exam rule:** AWS secures the infrastructure; YOU secure what you put ON the infrastructure.

## CIA Triad
| Pillar | Meaning | Threat It Prevents |
|--------|---------|-------------------|
| **Confidentiality** | Only authorised users access data | Unauthorised access |
| **Integrity** | Data cannot be tampered with | Data corruption / tampering |
| **Availability** | Data/services accessible when needed | DDoS / downtime |

## Security Lifecycle
```
Prevention → Detection → Response → Analyze → (back to Prevention)
```
- **Prevention:** Identify assets, assess vulnerabilities, implement countermeasures
- **Detection:** Monitor logs, detect unusual activity
- **Response:** Contain damage, act on threats
- **Analyze:** Review what happened, improve prevention

## Security Controls
| Type | Purpose | Example |
|------|---------|---------|
| **Preventive** | Stop attacks before they happen | Firewall, IAM policies, MFA |
| **Detective** | Identify attacks in progress/after | CloudTrail, GuardDuty, antivirus |
| **Corrective** | Recover after a breach | Backups, restore, incident response |

## Layered Security Model (Defence in Depth)
```
Perimeter → Network → Endpoint → Application → Data
```
| Layer | AWS Example |
|-------|-------------|
| Perimeter | Security Groups, AWS WAF |
| Network | NACLs, VPC routing |
| Endpoint | OS patching on EC2 |
| Application | AWS WAF (blocks SQLi, XSS) |
| Data | IAM, KMS, S3 encryption |

## IAM — Identity and Access Management

### Core Concepts
| Concept | Description |
|---------|-------------|
| **Root Account** | Full access to everything; use ONLY for initial setup; enable MFA |
| **IAM User** | Individual identity; use for day-to-day work |
| **IAM Group** | Collection of users; apply policies to group; **cannot nest groups** |
| **IAM Role** | Temporary delegated permissions; assumed by users/services (e.g., EC2 → S3) |
| **IAM Policy** | JSON document defining Allow/Deny on actions and resources |

### Key IAM Rules
- IAM is a **global** service (not region-specific)
- IAM is **free**
- **Principle of Least Privilege:** Grant only the minimum permissions needed
- **Explicit Deny > Explicit Allow > Implicit DenY**
- **Never store credentials inside EC2** — use IAM Roles instead
- Enable **MFA** on root account and all admin users
- Apply policies to **groups**, not individual users

### Authentication Factors
| Factor | Example |
|--------|---------|
| Something you **know** | Password, PIN |
| Something you **have** | Smart card, USB key, token |
| Something you **are** | Fingerprint, face recognition |

## Threat Types
| Threat | Description |
|--------|-------------|
| **Malware** | Virus, worm, trojan, ransomware, spyware, adware |
| **DDoS** | Floods server with requests; AWS Shield provides protection |
| **Phishing** | Impersonates legitimate site/person |
| **Man-in-the-Middle** | Intercepts traffic between client and server |
| **Social Engineering** | Manipulates people to reveal information |

## Encryption

### Types
| Type | Keys | Use Case |
|------|------|----------|
| **Symmetric** | Same key encrypts & decrypts | AWS KMS (default), AES, 3DES |
| **Asymmetric** | Public key encrypts, private key decrypts | SSL/TLS, RSA |

### In Transit vs At Rest
| | In Transit | At Rest |
|-|-----------|---------|
| What | Data moving between systems | Data stored on disk |
| How | HTTPS / TLS / VPN | KMS, S3 encryption, EBS encryption |

## Security Services — Know These Cold

| Service | What It Does | Exam Frequency |
|---------|-------------|----------------|
| **IAM** | Users, groups, roles, policies for access control | ⭐⭐⭐ Very High |
| **Security Groups** | Instance-level, **stateful** firewall (default: deny all inbound) | ⭐⭐⭐ Very High |
| **Network ACLs** | Subnet-level, **stateless** firewall (default: allow all) | ⭐⭐⭐ Very High |
| **AWS Shield** | DDoS protection; Standard (free) / Advanced (paid) | ⭐⭐ High |
| **Amazon GuardDuty** | Continuous **threat detection** (monitors VPC Flow Logs, DNS, CloudTrail) | ⭐⭐ High |
| **Amazon Inspector** | **Vulnerability scanning** for EC2 and Lambda | ⭐⭐ High |
| **AWS CloudTrail** | **Audit logging** of all API calls (who, when, what, where) | ⭐⭐⭐ Very High |
| **AWS Config** | **Compliance monitoring** — checks resource configs against rules | ⭐⭐ High |
| **AWS KMS** | **Key management** service for encryption keys | ⭐⭐ High |
| **AWS ACM** | **Certificate Manager** — manages SSL/TLS certificates; auto-renewal | ⭐ Medium |
| **AWS Security Hub** | Centralised security findings dashboard | ⭐ Medium |
| **AWS WAF** | Web Application Firewall — protects against SQLi, XSS, DDoS | ⭐ Medium |
| **AWS Network Firewall** | VPC-level traffic filtering | ⭐ Medium |
| **AWS Trusted Advisor** | Best practice **recommendations** (security, cost, performance) | ⭐⭐ High |

### Security Service Distinctions (Highly Tested)
| Service | One-Line Distinction |
|---------|---------------------|
| **Trusted Advisor** | Recommends best practices |
| **Inspector** | Scans for vulnerabilities |
| **GuardDuty** | Detects threats continuously |
| **Shield** | Protects against DDoS |
| **CloudTrail** | Logs all API activity |
| **AWS Config** | Monitors configuration compliance |
| **CloudWatch** | Monitors metrics and performance |

## Compliance

### Key Standards
| Standard | Domain |
|----------|--------|
| **PCI DSS** | Payment card data handling |
| **HIPAA** | Healthcare information (5 titles) |
| **GDPR** | EU personal data protection (strictest) |
| **PIPEDA** | Canadian personal data |

### AWS Compliance Tools
| Tool | Purpose |
|------|---------|
| **AWS Artifact** | Portal for accessing AWS compliance reports and documentation |
| **AWS Compliance Program** | 3 components: Business Risk Management, Control Automation, Certifications & Attestations |

### Compliance Types
- **Regulatory:** Government/industry mandated (criminal/financial penalties)
- **Contractual:** SLA/PLA between parties

---

# Domain 3: Cloud Technology and Services (34%)

## Compute Services

### Amazon EC2 (Elastic Compute Cloud)
- Virtual servers in the cloud (IaaS)
- **Instance types** determine compute capacity and cost (e.g., `t3.micro`)
- **Pricing models:** On-Demand, Reserved (1–3 yr), Spot (up to 90% off), Dedicated
- **Lifecycle:** Launch → Running → Stop → Start → Terminate
- **Key fact:** Stopped instance loses its public IP (use Elastic IP to keep it)
- **Private IP** is retained across stop/start
- **AMI** (Amazon Machine Image) defines the OS and software
- **User Data** script runs on first boot (e.g., install Apache)

### Amazon Lambda
- **Serverless** compute — no servers to manage
- **Event-driven** — triggered by S3 upload, API Gateway, CloudWatch alarm, etc.
- **Pay only for execution time** (per invocation + duration), not idle time
- Supports Python, Node.js, Java, Rust, and more
- Common triggers: S3 file upload, CloudWatch alarms, API Gateway requests

### EC2 vs Lambda
| Feature | EC2 | Lambda |
|---------|-----|--------|
| Billing | Per hour/second (even when idle) | Per invocation + duration |
| Management | You manage OS, patching | Fully managed |
| Use case | Always-on servers | Event-driven tasks |
| Scaling | Manual or Auto Scaling | Automatic |

### Amazon WorkSpaces
- **Virtual desktop** (VDI) — Windows or Linux
- Accessible from any device, anywhere
- GUI-based (not command-line like EC2)
- End users cannot resize volumes; only admins can

## Storage Services

### Amazon S3 (Simple Storage Service)
- Object storage; stores files (objects) in buckets
- Can trigger Lambda functions on file upload
- Storage classes for different access patterns and costs

### Amazon EBS (Elastic Block Store)
- Block storage attached to EC2 instances (like a virtual hard disk)

### Amazon EFS (Elastic File System)
- Shared file storage accessible by multiple EC2 instances

## Database Services

| Service | Type | Key Points |
|---------|------|------------|
| **Amazon RDS** | SQL (Relational) | Managed; supports MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, Aurora |
| **Amazon Aurora** | SQL (Relational) | AWS-native; MySQL/PostgreSQL compatible; 5x faster than MySQL |
| **Amazon DynamoDB** | NoSQL | Serverless; key-value/document; transactions cost extra |
| **Amazon DocumentDB** | NoSQL | MongoDB-compatible |
| **Amazon Redshift** | SQL (Analytics) | Data warehouse for analytics and reporting |

### RDS Key Concepts
- **Fully managed:** AWS handles provisioning, patching, backups, scaling, hardware
- **DB Instance Classes:** T3 (general), M/R (memory optimized), X (high performance)
- **Storage types:** Magnetic (legacy), GP2/GP3 (general), IO1/IO2 (high-throughput)
- **Zero-downtime storage scaling** — unlike EBS volumes on EC2
- **DB Subnet Group:** Defines which private subnets RDS deploys in
- **Not publicly accessible** by default (placed in private subnet)
- **Security Group = bridge** between EC2 and RDS; source must be the Web Security Group (not an IP)

### Multi-AZ vs Read Replicas (Heavily Tested)
| Feature | Multi-AZ | Read Replica |
|---------|----------|-------------|
| **Purpose** | High Availability / Failover | Scalability / Read Performance |
| **Can serve reads?** | No (standby is idle) | Yes |
| **Automatic failover?** | Yes | No |
| **Replication** | Synchronous | Asynchronous |

### RDS vs Self-Managed DB on EC2
| | Amazon RDS | EC2 + Database |
|-|-----------|----------------|
| Management | AWS manages engine, patching, backups | You manage everything |
| Setup | Click and use | Install and configure manually |
| Scaling | Easy (console/CLI), zero-downtime storage | Manual effort, may require downtime |
| Cost | Higher (pay for management) | Lower (but more work) |

### Amazon Aurora
- AWS's **proprietary, cloud-native** relational DB engine (part of RDS)
- Compatible with MySQL and PostgreSQL — existing tools work without modification
- Generally **faster** than standard MySQL/PostgreSQL; slightly more expensive
- **Aurora Clusters:** primary instance (read/write) + Aurora replicas (read-only)
- **Automatic Multi-AZ replication** — don't manually create replicas
- **Writer endpoint** = read + write; **Reader endpoint** = read-only
- Use cases: enterprise applications, SaaS platforms, online/mobile gaming

### Database Migration
| Service | Purpose |
|---------|---------|
| **AWS DMS** | Migrate existing on-prem databases to AWS; continuous replication |
| **AWS MGN** | Migrate full infrastructure (servers, apps) to AWS |
| **mysqldump + S3** | Manual method for small databases: export → upload to S3 → import to RDS |

### SQL JOINs
| Join Type | Description |
|-----------|-------------|
| **INNER JOIN** | Only matching rows from both tables |
| **LEFT JOIN** | All rows from left table + matching right |
| **RIGHT JOIN** | All rows from right table + matching left |
| **FULL OUTER JOIN** | All rows from both tables |
| **CROSS JOIN** | Every possible combination (Cartesian product) |

### Database Normalization
- Separate tables eliminate redundant data
- Prevents data anomalies (update one record, reflects everywhere)
- Saves storage and maintains data integrity
- Store `country_id` instead of duplicating full country data

### Amazon DynamoDB
- Fully managed **NoSQL** database service
- **Key-value store**; no fixed schema — items in same table can have different attributes
- **Primary Key:** simple (partition key only) or composite (partition key + sort key)
- **Partition Key** determines storage location; **Sort Key** orders items within partition
- **Global Tables:** multi-region replication for low latency and disaster recovery
- **DAX (DynamoDB Accelerator):** in-memory cache for DynamoDB (like Redis, DynamoDB-specific)
- Automatic encryption at rest; automatic backups; built-in scalability and fault tolerance

### DynamoDB Terminology
| DynamoDB Term | SQL Equivalent |
|---------------|---------------|
| Table | Table |
| Item | Row / Record |
| Attribute | Column / Field |
| Primary Key | Primary Key |

### SQL vs NoSQL
| Feature | SQL (RDS/Aurora) | NoSQL (DynamoDB) |
|---------|-----------------|------------------|
| Schema | Fixed, predefined | Flexible, schema-less |
| Scaling | Vertical | Horizontal |
| ACID | Full native support | Limited (costs extra) |
| Best for | Transactions, CRM, ERP | Real-time apps, big data |

## Networking Services

### Amazon VPC (Virtual Private Cloud)
- **Logically isolated** virtual network in AWS
- **Regional** service; **spans multiple AZs** within a region
- Each AWS account has a **default VPC**

### VPC Components
| Component | Purpose |
|-----------|---------|
| **CIDR Block** | IP address range for VPC (e.g., `10.0.0.0/16`) |
| **Subnet** | Subdivision of VPC in one AZ; **public** or **private** |
| **Internet Gateway (IGW)** | Allows internet access for public subnets |
| **NAT Gateway** | Outbound-only internet for private subnets; requires Elastic IP |
| **Route Table** | Rules directing traffic (`0.0.0.0/0 → IGW` = public) |
| **Security Group** | Instance-level, **stateful** firewall (default: deny inbound) |
| **Network ACL** | Subnet-level, **stateless** firewall (default: allow all) |
| **VPC Endpoint** | Private connection to AWS services without internet |
| **VPC Peering** | Connect two VPCs privately |

### Subnets
| | Public Subnet | Private Subnet |
|-|--------------|----------------|
| Internet access | Yes (via IGW) | No (or outbound only via NAT) |
| Use case | Web servers, load balancers | Databases, internal services |
| Route table | Has `0.0.0.0/0 → IGW` | No internet route (or → NAT) |

### Security Group vs NACL (Know This Cold)
| Feature | Security Group | Network ACL |
|---------|---------------|-------------|
| Level | **Instance** | **Subnet** |
| State | **Stateful** | **Stateless** |
| Default inbound | **Deny all** | **Allow all** |
| Rules | **Allow only** | **Allow and Deny** |
| Rule evaluation | All rules evaluated | Rules evaluated in order |

### IP Addressing
| Concept | Details |
|---------|---------|
| **Public IP** | Globally unique; required for internet access |
| **Private IP** | Only within VPC; retained when instance stops |
| **Elastic IP** | Static public IP; persists across stop/start; charged when unused |
| **Private IP ranges** | `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16` |
| **AWS reserves** | 5 IPs per subnet (network, router, DNS, future, broadcast) |

### Port Numbers (Memorise These)
| Port | Service | Use |
|------|---------|-----|
| **22** | SSH / SFTP | Connect to Linux EC2 |
| **80** | HTTP | Unencrypted web traffic |
| **443** | HTTPS | Encrypted web traffic |
| **53** | DNS | Domain name resolution |
| **20/21** | FTP | File transfer |
| **3389** | RDP | Windows Remote Desktop |
| **3306** | MySQL | Database connections |

### Network Protocols
| Protocol | Layer | Reliable? | Use Case |
|----------|-------|-----------|----------|
| **TCP** | 4 (Transport) | Yes (3-way handshake) | SSH, HTTPS, email, file transfer |
| **UDP** | 4 (Transport) | No | Streaming, gaming, VoIP, DNS |
| **HTTP** | 7 (Application) | — | Web (unencrypted, port 80) |
| **HTTPS** | 7 (Application) | — | Web (encrypted via TLS, port 443) |

### OSI Model (Key Layers Only)
| Layer | Name | Key Protocols |
|-------|------|---------------|
| 7 | Application | HTTP, HTTPS, FTP, SSH, DNS |
| 4 | Transport | TCP, UDP |
| 3 | Network | IP (Internet Protocol) |

## Management & Developer Tools

| Service | Purpose |
|---------|---------|
| **AWS CloudWatch** | Monitoring metrics (CPU, network), logs, alarms |
| **AWS CloudTrail** | Audit logging of all API calls |
| **AWS Systems Manager** | Manage EC2 instances; **Session Manager** for secure SSH-less access |
| **AWS Cloud9** | Browser-based IDE running on EC2 |
| **AWS CodeCommit** | Managed Git repository |
| **AWS CodeBuild** | Managed build/test service |
| **AWS CodeDeploy** | Automated deployment to EC2, Lambda, etc. |
| **AWS CodePipeline** | End-to-end CI/CD orchestration |
| **AWS CloudFormation** | Infrastructure as Code (IaC) |

## IoT & Other Services

| Service | Purpose |
|---------|---------|
| **AWS IoT Core** | Managed IoT platform; supports HTTPS, MQTT, WSS, LoRaWAN |
| **Amazon Cognito** | User authentication for web/mobile apps |
| **Amazon SageMaker** | ML platform (can detect/redact PII) |

## DevOps & CI/CD Concepts
- **DevOps:** Culture unifying development and operations (CALMS: Culture, Automation, Lean, Measurement, Sharing)
- **Continuous Integration (CI):** Auto-test code on every push
- **Continuous Delivery/Deployment (CD):** Auto-deploy to staging/production after CI passes
- **Pipeline:** Push → Test → Build → Deploy → Restart
- **Deployment environments:** Staging → Pre-production → Production

---

# Domain 4: Billing, Pricing, and Support (12%)

## AWS Pricing Models
| Model | Description |
|-------|-------------|
| **Pay-as-you-go** | Pay only for what you use (EC2 hourly, Lambda per invocation) |
| **Save when you commit** | Reserved Instances (1–3 year), Savings Plans |
| **Pay less by using more** | Volume-based discounts (S3 storage tiers) |
| **Free Tier** | Limited free usage for 12 months (e.g., 750 hrs t2.micro EC2) |

## Key Pricing Concepts
| Service | Pricing Model |
|---------|--------------|
| **EC2** | Per hour/second; varies by instance type, region, OS |
| **Lambda** | Per request + duration (GB-seconds); free tier: 1M requests/month |
| **S3** | Per GB stored; tiered pricing (more = cheaper per GB) |
| **RDS** | Per hour for DB instance + storage + data transfer |
| **Elastic IP** | Free when associated; **charged when allocated but NOT associated** |

## AWS Support Plans

| Feature | Developer | Business | Enterprise |
|---------|-----------|----------|------------|
| **Target** | Testing/dev | Business | Mission-critical |
| **Contact** | Email (business hours) | 24/7 phone, chat, email | 24/7 phone, chat, email |
| **General guidance** | ≤ 24 hrs | ≤ 24 hrs | ≤ 24 hrs |
| **Production impaired** | — | ≤ 4 hrs | ≤ 4 hrs |
| **Production down** | — | ≤ 1 hr | ≤ 1 hr |
| **Business-critical down** | — | — | **≤ 15 min** |
| **TAM (Technical Account Manager)** | No | No | **Yes** |
| **Trusted Advisor** | Limited checks | Full checks | Full checks |

## AWS Support & Resources

| Resource | Purpose |
|----------|---------|
| **AWS Trusted Advisor** | Best practice recommendations (security, cost, performance, fault tolerance) |
| **AWS Personal Health Dashboard** | Personalised alerts about AWS service issues affecting your account |
| **AWS Artifact** | Portal for compliance reports and audit documentation |
| **AWS Advisories & Bulletins** | Latest info on vulnerabilities and security issues; report discovered vulnerabilities here |
| **AWS Professional Services** | AWS experts help with implementation |
| **AWS Partner Network** | Third-party companies that help implement/manage AWS |
| **AWS Account Teams** | First point of contact; guide toward right resources |
| **AWS Auditor Learning Path** | Training for auditing/compliance/legal roles |

---

# Quick Reference Tables

## Instance States
| State | Public IP | Private IP | Billing |
|-------|-----------|------------|---------|
| Running | Assigned (dynamic) | Assigned | Yes |
| Stopped | **Released** | Retained | **No** |
| Restarted | **New IP assigned** | Same | Yes |
| With Elastic IP | **Same IP** | Same | Yes (free when associated) |

## VPC Architecture Summary
```
Internet
    │
Internet Gateway
    │
Route Table (0.0.0.0/0 → IGW)
    │
Public Subnet ─── EC2 Web Server ─── Security Group (22, 80, 443)
    │
NAT Gateway (outbound only)
    │
Private Subnet ─── RDS Database ─── DB Security Group (3306 from web SG)
```

## Traditional Networking → AWS Equivalents
| Traditional | AWS |
|-------------|-----|
| Data Centre | VPC |
| Router | Route Tables |
| Switch / Subnet | Subnet |
| Firewall | Security Groups & NACLs |
| Modem | Internet Gateway |

---

# Common Exam Gotchas

1. **Stopped EC2 loses its public IP** — use Elastic IP for persistence
2. **Private IPs are retained** when instance stops
3. **Security Group** = stateful, instance-level, deny-all default (whitelist)
4. **NACL** = stateless, subnet-level, allow-all default (blacklist)
5. **Explicit Deny always wins** over Explicit Allow in IAM
6. **IAM is global** — not region-specific
7. **IAM is free**
8. **Root account** should only be used for initial admin user creation; enable MFA
9. **Never store credentials in EC2** — use IAM Roles
10. **Groups cannot contain other groups** — only users
11. **CloudTrail** = audit logging (who did what); **CloudWatch** = performance monitoring (metrics)
12. **AWS Config** = compliance monitoring (is my config correct?)
13. **Inspector** scans vulnerabilities; **GuardDuty** detects threats continuously
14. **Trusted Advisor** recommends best practices
15. **Lambda** = pay per execution; **EC2** = pay per hour (even when idle)
16. **Multi-AZ** = high availability (not performance); **Read Replica** = performance (not HA)
17. **VPC cannot span regions** but can span AZs
18. **Subnets are AZ-specific** (one subnet = one AZ)
19. **NAT Gateway** requires Elastic IP and must be in a public subnet
26. **RDS in private subnet** = not directly accessible from internet
27. **Multi-AZ** = standby is idle (not used for reads); only activates on failover
28. **Read Replica** = can serve reads but has no automatic failover
29. **Aurora** is part of RDS — it's an RDS engine, not a separate service
30. **DAX** is for DynamoDB only — not a general-purpose cache like Redis
31. **DynamoDB Global Tables** = multi-region replication (latency + disaster recovery)
32. **CAF** = planning tool (6 perspectives: 3 business + 3 technical)
33. **WAF** = design/operational tool (6 pillars: Ops Excellence, Security, Reliability, Perf Efficiency, Cost Optimization, Sustainability)
34. **Reliability** = works as expected (MTBF); **Availability** = is running (% uptime "nines")
35. **High Availability** = Fault Tolerance + Scalability + Recoverability — know all 3
36. **Auto Scaling** = stop guessing capacity (well-architected principle)
37. **RDS Security Group** = bridge between EC2 and RDS; source = Web SG, not IP
38. **Aurora** has automatic Multi-AZ — do NOT manually create replicas
39. **DMS** = Database Migration Service (on-prem → AWS); **mysqldump + S3** = manual method for small DBs
40. **SSM Session Manager** = browser-based EC2 access without SSH; no port 22/key pairs needed

### Quick Memory Aids
```
Multi-AZ     → Availability (failover, resilience)
Read Replica → Scalability (read performance, load distribution)

RDS          → SQL / Relational databases (MySQL, PostgreSQL, Aurora, etc.)
Aurora       → AWS's own engine, faster than MySQL/PG, still part of RDS
DynamoDB     → NoSQL / Key-value (flexible schema, massive scale)

DAX          → DynamoDB's built-in cache (like Redis, but only for DynamoDB)
Global Tables → DynamoDB across multiple regions
```

---

*Consolidated from daily lecture notes, Weeks 3–10 | AWS re/Start Cohort 3: Project CloudIgnite*
*Last updated: June 6, 2026 (includes June 6 notes)*
