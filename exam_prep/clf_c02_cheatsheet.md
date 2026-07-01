# AWS Certified Cloud Practitioner (CLF-C02) — Exam Cheat Sheet
**Consolidated from Cohort 3: Project CloudIgnite lecture notes (Weeks 3–14)**

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
- **Instance types** determine compute capacity and cost: T (General Purpose), C (Compute Optimized), R/X (Memory Optimized), I/D (Storage Optimized), P/G (Accelerated Computing), Hpc (High Performance Compute)
- **Pricing models:** On-Demand, Reserved (1–3 yr), Spot (up to 90% off), Dedicated
- **Lifecycle:** Launch → Running → Stop → Start → Terminate
- **Key fact:** Stopped instance loses its public IP (use Elastic IP to keep it)
- **Private IP** is retained across stop/start
- **AMI** (Amazon Machine Image) defines the OS and software; sources: AWS-provided, community, custom
- **User Data** script runs once at first boot (e.g., install Apache)
- **Instance Metadata Service:** `http://169.254.169.254/latest/meta-data/` — accessible only from within EC2; returns instance info (ID, type, hostname, AMI ID, etc.)
- **Instance Profile** = IAM Role attached to EC2; enables EC2 to access AWS services without storing credentials
- **Connection methods ranked by security:** SSM Session Manager (no ports, no keys, fully logged) > EC2 Instance Connect (port 22, browser) > SSH (port 22, .pem key)

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
- **Static website hosting:** no servers, cost-effective, automatic scalability; bucket names must be globally unique; endpoint format: `http://<bucket>.s3-website-<region>.amazonaws.com`; requires disabling Block Public Access and enabling ACLs
- **S3 CLI automation:** `aws s3 sync` (only changed files) preferred over `aws s3 cp --recursive` (re-uploads everything)
- **Custom domain:** Use Route 53 to map domain to S3 endpoint

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
| **AWS Systems Manager** | Manage EC2 instances; **Fleet Manager** (inventory), **Run Command** (execute scripts across instances), **Session Manager** (SSH-less secure access), **Parameter Store** (store secrets/config), **Patch Manager**, **State Manager** |
| **AWS Cloud9** | Browser-based IDE running on EC2 |
| **AWS CodeCommit** | Managed Git repository |
| **AWS CodeBuild** | Managed build/test service |
| **AWS CodeDeploy** | Automated deployment to EC2, Lambda, etc. |
| **AWS CodePipeline** | End-to-end CI/CD orchestration |
| **AWS CloudFormation** | Infrastructure as Code (IaC) |

### AWS Command Line Interface (CLI)
- Terminal-based AWS management
- Installation: download zip → unzip → `sudo ./aws/install`
- Configuration: `aws configure` (stores keys in `~/.aws/credentials` and `~/.aws/config`)
- Output formats: `json`, `table`, `text`
- Common commands: `aws ec2 describe-instances`, `aws s3 ls`, `aws iam list-users`
- **Dry run:** `--dry-run` simulates command to check permissions without execution
- CLI is **instance-specific** — configure on each EC2 separately
- **Three access methods** for AWS: Management Console (GUI), AWS CLI, AWS SDK

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
41. **S3 static website hosting** = no servers to manage, cost-effective, automatic scaling; bucket names must be globally unique
42. **aws s3 sync** uploads only changed files (preferred for automation); `aws s3 cp --recursive` re-uploads everything
43. **EC2 instance types:** T (General Purpose), C (Compute Optimized), R/X (Memory Optimized), I/D (Storage Optimized), P/G (Accelerated Computing), Hpc (High Performance Compute)
44. **Instance store** = ephemeral (data lost on stop/terminate); **EBS** = persistent storage
45. **Elastic IP** = static public IP that persists across stop/start; **Public IP** changes on every stop/start; **Private IP** is retained
46. **Instance Profile** = IAM Role attached to EC2; enables EC2 to access AWS services without storing credentials
47. **User Data** = bash script that runs once at first boot; **Instance Metadata** = `http://169.254.169.254/latest/meta-data/` (accessible only from within EC2)
48. **AWS CLI `--dry-run`** = checks whether you have required permissions without actually executing the command
49. **Troubleshooting Knowledge Base** = structured document (Excel/CSV) tracking issues, symptoms, root causes, and resolutions for consistent incident response
50. **EC2 instance lifecycle:** pending → running → stopping → stopped → terminated; **terminated is permanent and unrecoverable**
51. **Stopped EC2 is still billed for EBS storage** (no compute charge, but EBS persists); also billed during the brief "stopping" transition
52. **Delete on Termination** setting controls whether the root EBS volume is removed when the instance terminates (default = Yes)
53. **Elastic Beanstalk** = PaaS — AWS manages OS, runtime, scaling, health; you upload code; **no additional charge** (pay only for underlying EC2/EBS/RDS); supports Java, .NET, PHP, Node.js, Python, Ruby, Go, Docker
54. **IaaS vs PaaS vs Serverless:** EC2 = IaaS (you manage OS), Elastic Beanstalk = PaaS (AWS manages OS/runtime), Lambda = Serverless (AWS manages everything)
55. **AMI deprecation:** custom AMIs deprecated **~2 years** after creation; existing instances keep running, but new launches are **blocked** (critical to refresh AMI in time for ASGs)
56. **ALB (Application Load Balancer):** Layer 7 (HTTP/HTTPS/gRPC); supports **path-based** and **host-based routing**, TLS termination, target groups, listeners, health checks, native IPv6, deletion protection
57. **NLB (Network Load Balancer):** Layer 4 (TCP/UDP/TLS); extreme performance/low latency (hundreds of thousands of req/sec); static IP per AZ; good for gaming and bursty traffic
58. **GWLB (Gateway Load Balancer):** Layer 3/4; routes traffic through third-party virtual security/inspection appliances
59. **CLB (Classic Load Balancer):** legacy — mix of ALB+NLB features; **deprecated, avoid for new designs**
60. **ASG capacity:** **Minimum** (floor — never below), **Desired** (target), **Maximum** (ceiling — never above)
61. **ASG scaling policy types:** **Target Tracking** (maintain a metric at target, e.g., CPU 50%), **Step Scaling** (reacts to size of CloudWatch alarm breach), **Simple Scaling**, **Scheduled Scaling**
62. **ASG anti-thrashing guards:** **Cooldown Period** (default 300s — no new actions after a scaling event), **Warm-Up Period** (default 300s — new instance given time to be ready), **Alarm Sustain Period** (alarm must remain in breach for a duration before triggering)
63. **ASG termination policies:** Default, Oldest Instance, **Newest Instance** (useful when a new config fails), Oldest Launch Configuration, Closest to Next Instance Hour
64. **To force ASG to launch new instances** → increase the **minimum capacity** (ASG launches to meet the new floor)
65. **If all newly launched ASG instances fail** → check the **Launch Template and AMI** (they define instance config/behavior)
66. **Route 53 routing policies:** **Simple** (single resource), **Weighted** (% split — used for blue-green), **Latency-based** (lowest response time), **Failover** (primary → secondary), **Geolocation** (user's location), **Geoproximity** (physical distance), **Multi-value** (up to 8 random healthy), **IP-based** (user IP block)
67. **Geolocation vs Geoproximity vs Latency** (commonly confused): **Geolocation** = where the user **is**; **Geoproximity** = physical **distance** to resources; **Latency** = measured **response time**
68. **Route 53 distributes traffic across REGIONS**; **ALB distributes traffic only within ONE region**
69. **CloudFront (CDN):** global network of **Edge Locations** + **Regional Edge Caches**; speeds static and dynamic content; for live streaming, the origin keeps 1 connection to the edge and the edge fans out to viewers (greatly reduces origin load)
70. **Creating an IAM user alone is not enough** — must also add a **login profile** (password) AND attach a **policy**; otherwise the user cannot sign in or do anything
71. **AWS access keys** = Access Key ID + Secret Access Key; **secret is shown ONCE at creation** and cannot be retrieved later
72. **S3 buckets are PRIVATE by default**; public access requires **disabling Block Public Access** + **enabling ACLs** (Object Ownership) + **bucket policy** allowing public read
73. **S3 static website endpoint:** `http://<bucket>.s3-website-<region>.amazonaws.com`
74. **`aws s3 sync`** uploads only **changed** files (preferred for automation); `aws s3 cp --recursive` re-uploads **everything** every run
75. **AMIs are region-specific** — an AMI ID valid in one region will NOT work in another
76. **IAM Roles / Instance Profiles** = preferred way to give EC2 AWS access (no stored credentials, temporary auto-rotated keys); **exam-favoured over long-term access keys**
77. **CloudWatch alarms** drive ASG scaling actions — when a metric (e.g., CPU > 50%) breaches the target, the alarm fires and the ASG launches more instances
78. **Decoupled / scalable architecture pattern:** `Route 53 → ALB (public subnets) → ASG/EC2 (private subnets) → RDS (shared)`; static/media content offloaded to S3 + CDN
79. **AWS Lambda** = fully managed, **event-driven serverless compute**; you only build & deploy code and monitor the application — AWS handles everything else
80. **Lambda billing = per-invocation + duration** (sub-second metering); no charge while idle, in contrast to EC2 (pay per hour even when idle)
81. **Lambda max execution time = 15 minutes per invocation** (not a daily limit); tasks exceeding this return an error
82. **Lambda Layers** = packages of shared libraries/dependencies attached separately from the function code; keeps handler clean and lets you reuse dependencies across functions
83. **Lambda execution role** = IAM role that grants the function its AWS permissions (e.g., CloudWatch Logs, VPC access); passed when creating the function
84. **Amazon Route 53** = AWS managed **DNS web service**; supports Simple, Weighted, Latency, Failover, Geolocation, Geoproximity, Multi-value, and IP-based routing policies
85. **Route 53 failover routing** = active/passive DNS routing: primary serves traffic, secondary takes over automatically when health checks fail
86. **Route 53 health check** = continuously monitors an endpoint; **failover threshold = number of failed checks** before marking unhealthy (e.g., threshold 2 = mark unhealthy after 2 consecutive failures)
87. **TTL (Time To Live)** in DNS = how long a record is cached by clients/resolvers before re-querying (e.g., 15s for fast failover testing)
88. **A record** = DNS record mapping a name to an **IPv4** address; **AAAA record** = IPv6
89. **Amazon API Gateway** = fully managed AWS service to **create, publish, and maintain APIs** (REST and others); commonly paired with Lambda for serverless APIs
90. **API Gateway integrations** = Lambda, EC2, DynamoDB, Kinesis, and VPC resources; supports an **API Gateway cache** (cache miss → forward to backend)
91. **AWS Step Functions** = **serverless orchestration** of workflows (state machine) — coordinates multiple Lambda functions/microservices with dependencies
92. **Step Functions building blocks:** **state machine** = the workflow; **state** = a step; **task** = the work performed at a state (exam-style fact: a Task does the work)
93. **Sequential vs. parallel in Step Functions:** sequential = Task 1 → Task 2 → Task 3; parallel = Task 1 and Task 2 run together, Task 3 waits for both (parallel + join)
94. **Container** = app + dependencies in a **resource-isolated process that shares the host OS kernel** (lightweight, starts in seconds, portable)
95. **Virtual Machine (VM)** = full **guest OS on a hypervisor** (heavy, several GB, slower to start); runs on top of a hypervisor
96. **VM stack:** Hardware → Host OS → Hypervisor → [Guest OS + App] × N; **Container stack:** Hardware → Host OS → Docker Engine → [Container (app + deps)] × N
97. **"Works on my machine" problem** = environment mismatch between dev and prod; containers bundle the environment so what works locally works in deployment
98. **Docker** = platform/tool to **build, manage, and run containers**; not AWS-specific (install on your laptop)
99. **Docker components:** **Dockerfile** = blueprint (base OS, apps, env vars); **Docker image** = built immutable artifact; **registry** = image store (Docker Hub, ECR); **container** = running instance of an image
100. **Amazon ECR** (Elastic Container Registry) = fully managed **Docker image registry** on AWS (like Docker Hub)
101. **Amazon ECS** (Elastic Container Service) = AWS-native **container orchestration for Docker** (create, launch, run containers)
102. **Amazon EKS** (Elastic Kubernetes Service) = managed **Kubernetes** on AWS (no control plane/cluster to operate); Kubernetes is open-source and portable
103. **AWS Fargate** = **serverless compute engine for containers** (ECS/EKS) — no EC2 to manage, AWS handles instances/scaling/patching/load balancing
104. **Container compute choices for ECS/EKS:** (1) **Fargate** = serverless, AWS manages EC2; (2) **your own EC2 cluster** = cheaper but you patch & scale
105. **Containers run on EC2 under the hood** (Fargate abstracts this; with your own cluster you see the EC2s)
106. **S3 → Lambda → SNS** = canonical **event-driven, serverless** pattern: S3 upload event invokes Lambda, Lambda publishes to SNS topic for email/notification
107. **Amazon SNS** (Simple Notification Service) = **pub/sub messaging** for notifications (email, SMS, HTTP endpoints); topic types: **Standard** (not FIFO for typical use)
108. **Amazon EventBridge** (formerly CloudWatch Events) = event bus / scheduler with **cron** support; can trigger Lambda on a schedule (e.g., daily report)
109. **AWS Systems Manager Parameter Store** = secure store for **configuration values and secrets**; EC2/Lambda read parameters at runtime — **don't hard-code credentials**
110. **ARN** = Amazon Resource Name; **unique identifier for an AWS resource** (e.g., `arn:aws:iam::123:role/MyRole`); exam gotcha: IAM role ARN ≠ SNS topic ARN ≠ SNS subscription ARN
111. **Amazon RDS as a managed database** = AWS handles **backups, patching, maintenance, availability** — textbook example of the **Shared Responsibility Model** in action (reduces operational labor vs. self-managed DB on EC2)
112. **DB Subnet Group** = a set of subnets spanning **≥2 Availability Zones** that an RDS instance can use (RDS requires a multi-AZ subnet group)
113. **mysqldump** = MySQL utility that exports a database to a backup file (schema + data); common manual migration method (mysqldump → S3 → import to RDS)
114. **Three ways to access/interact with AWS:** **Management Console** (GUI), **AWS CLI** (terminal), **AWS SDK** (programmatic, e.g., **boto3** for Python)
115. **HTTP methods (REST verbs):** **GET** = read, **POST** = create, **PUT** = update, **DELETE** = remove
116. **HTTP status code families:** **1xx** informational; **2xx** success (200 OK, 201 Created, 202 Accepted); **3xx** redirect; **4xx** client error (401 Unauthorized, 403 Forbidden, 404 Not Found); **5xx** server error (500, 502)
117. **Environment variables in Lambda** = store config (ARNs, feature flags) outside the code; **casing matters** (e.g., `topicARN`); don't hard-code secrets
118. **VPC ID vs. Security Group ID:** VPC IDs start with `vpc-`, security group IDs with `sg-` — never mix them up in CLI commands
119. **Serverless** = you run code without provisioning/managing servers; AWS manages the infrastructure. Lambda, Fargate, API Gateway, and Step Functions are AWS serverless services
120. **Lambda destinations** = on success/failure, Lambda can send result info to another target (e.g., another S3 bucket, SNS, EventBridge) — separate from the Lambda's own execution output
121. **CIDR block conflicts** = two subnets cannot have overlapping CIDR blocks; if wrong, change the block (don't necessarily delete the subnet)
122. **Lambda free tier** = **1 million requests per month** + compute time (verify current AWS docs for exact GB-seconds allowance)
123. **Amazon VPC** = a logically isolated virtual network in AWS; **Region-scoped** and can span **all AZs** in that Region, while a **subnet lives in exactly one AZ** (a subnet does not span AZs)
124. **VPC CIDR block** must be between **/16 and /28** using **RFC 1918** private ranges (10.x, 172.16–31.x, 192.168.x); AWS reserves **5 IPs per subnet** (network, VPC router, DNS, future, broadcast)
125. **Public subnet** = route table has `0.0.0.0/0 → Internet Gateway` (IGW); **private subnet** = no IGW route (uses **NAT Gateway** for outbound-only internet)
126. **NAT Gateway** = AWS-managed outbound-only gateway for private subnets; must live in a **public subnet**, requires an **Elastic IP**, supports TCP/UDP/ICMP; deploy across **multiple AZs** for high availability
127. **VPC Peering is NOT transitive** — A peered to B and B peered to C does NOT connect A and C (must peer them directly); use **Transit Gateway** for many VPCs
128. **VPC Endpoints:** **Gateway Endpoint** = private access to **only S3 and DynamoDB**, **free**; **Interface Endpoint (PrivateLink)** = private access to other AWS services, **paid**
129. **Site-to-Site VPN** = encrypted tunnel over the public internet to on-premises (use when **encryption required**); **Direct Connect** = dedicated private physical line to AWS (can be combined with VPN)
130. **Security Group vs. NACL — the exam favorite:** SG = **instance-level, stateful, allow-only** (return traffic auto-allowed); NACL = **subnet-level, stateless, allow + deny, numbered rules evaluated lowest-number-first (first match wins)**
131. **NACL default rules:** default NACL = **allow all** in/out; custom NACL = **deny all** until you add an allow rule; **a low-numbered DENY overrides a higher-numbered ALLOW** (e.g., Rule #40 DENY port 22 blocks SSH before Rule #100 ALLOW all)
132. **Bastion host** = a public-subnet EC2 used as a secure jump box to SSH into private-subnet instances; the private instance's SG should allow port 22 **only from the bastion/VPC CIDR**
133. **VPC Flow Logs** = capture accepted/rejected IP traffic metadata for a VPC, stored in **S3 or CloudWatch**; log lines include ENI, source IP, port, action (ACCEPT/REJECT); timestamps are in **Unix epoch**; **analyze with `grep REJECT`** to find blocked traffic
134. **Connectivity troubleshooting order:** instance running → Security Group allows ports → NACL allows traffic → Route Table has the right routes → IGW attached to VPC
135. **Amazon EBS (Elastic Block Store)** = persistent block storage attached to EC2; **single-AZ (zonal)** — a volume can only attach to EC2 in the **same Availability Zone**; every EC2 needs at least one EBS volume as its boot drive
136. **EBS volume types:** **SSD** = io1/io2 (highest IOPS, databases, most expensive) and gp3/gp2 (general purpose, boot volumes, virtual desktops); **HDD** = st1 (throughput-optimized, streaming/big data, NOT a boot volume) and sc1 (cold, cheapest, NOT a boot volume)
137. **IOPS vs. Throughput:** **IOPS** = read/write **operations** per second (databases); **Throughput** = amount of **data** per second (streaming); **SSD = IOPS**, **HDD = Throughput** (or cheap bulk)
138. **EBS snapshots** = point-in-time, **incremental** backups of EBS volumes stored in **S3**; can be **copied cross-Region** to create a volume in another Region; **restore = create new volume from snapshot** (keeps the file system intact)
139. **Data Lifecycle Manager (DLM)** automates EBS snapshot creation, retention, and deletion — **always set retention** (24 snapshots/day = ~720/month, surprise bill); DLM requires the **AWS Data Lifecycle Manager default role** (`aws dlm create-default-role`)
140. **Instance Store = ephemeral** block storage tied to the instance host (very fast); **data is LOST on stop or terminate** (reboot is OK); use only for **cache, buffers, scratch/temp data** — never for permanent data
141. **Amazon EFS (Elastic File System)** = shared NFS file system mounted by **many EC2s at once** (block storage like EBS is NOT shared); **Linux only**; auto-scales (no capacity management); petabyte-scale
142. **EFS vs FSx:** **EFS = Linux only, NFS protocol**; **FSx = Windows AND Linux**, multi-purpose file system
143. **Amazon S3** = **object storage** with **11 nines (99.999999999%) durability**, **strong read-after-write consistency**, effectively unlimited capacity; concepts: **bucket** (Region-scoped), **object**, **key** (unique within bucket)
144. **S3 storage classes (cost ↓ left → right, retrieval gets slower):** Standard → Intelligent-Tiering → Standard-IA → One Zone-IA → Glacier Instant Retrieval → Glacier Flexible Retrieval → **Glacier Deep Archive** (cheapest, **12–48 hr** retrieval)
145. **S3 Intelligent-Tiering** = auto-moves objects between tiers (Standard / Standard-IA / Glacier) based on access patterns — **no manual tracking required**; ideal for unknown or changing access patterns
146. **S3 One Zone-IA** = single AZ; data **lost if AZ fails**; use only for **reproducible** data
147. **S3 Standard-IA / Glacier cost caveat:** cheaper storage per GB but **retrieval fees** — **frequent access to IA/Glacier can cost MORE than Standard**; **archive tip = zip many tiny files into one** to reduce per-access cost
148. **S3 Versioning** = keeps multiple object versions; states are **Disabled / Enabled / Suspended**; deleting an object adds a **delete marker** instead of erasing it (restore by removing marker or fetching `--version-id`); **versioning must be enabled BEFORE the delete to protect the object**
149. **S3 Object Lock (WORM)** = Write Once Read Many; **retention period** = cannot delete for N days; **legal hold** = indefinite lock until removed; used for **compliance and governance** (e.g., financial, healthcare)
150. **S3 security:** objects are **private by default**; **Block Public Access** at account/bucket level; **pre-signed URLs** grant **time-limited** access to a private object; **CORS** needed when S3 hosts a **static website**
151. **S3 → Lambda → SNS** = canonical **event-driven, serverless** pattern; S3 event (e.g., suffix `.txt`) invokes Lambda, Lambda publishes to SNS topic for email/SMS/HTTP notification
152. **Three ways to access AWS:** **Management Console** (GUI), **AWS CLI** (terminal), **AWS SDK** (programmatic — `boto3` for Python); same services, three interfaces
153. **Lambda IAM execution role gotcha:** choosing "no permissions" tries to **create a new IAM role** and fails with "not authorized to perform create role…" — **fix = use an existing IAM role** that already has the required permissions
154. **S3 object keys must NOT contain spaces** — a space splits the key into two arguments and causes `NoSuchKey` errors in Linux/CLI; **escape with `\` or rename the file**
155. **DB Subnet Group** = a set of subnets spanning **≥2 Availability Zones** that an RDS instance can use; **RDS requires a multi-AZ subnet group**
156. **RDS DB Security Group source = Web-tier Security Group** (NOT an IP) — allows tier-to-tier access control so only the application tier can reach the database
157. **Amazon RDS** = managed relational database; AWS handles **backups, patching, maintenance, availability**; place in **private subnets**; **DB Subnet Group ≥2 AZs**; repoint the app to RDS via **Parameter Store** (`cafe/dbUrl` → RDS endpoint)
158. **AWS Storage Gateway** = hybrid connection between on-premises data center and AWS storage (file gateway, volume gateway, tape gateway); use cases: **disaster recovery, tiering, migration**
159. **AWS Snow Family** = physical devices AWS ships to you for **offline bulk data transfer**; use when bandwidth is insufficient (e.g., **50 TB over 100 Mbps ≈ 12.5 MB/s = weeks/months**); device size scales from Snowcone to Snowmobile (truck-scale for petabytes)
160. **Three components of cloud storage:** **client device** → **internet** → **data center**
161. **VPC troubleshoot checklist (the lab exam-favorite):** (1) EC2 instance running? (2) Security Group allows the required ports? (3) NACL allows the traffic (check numbered rules, lowest-first)? (4) Route Table has the right routes (IGW for public, NAT for private)? (5) Internet Gateway attached to VPC? Public/Elastic IP correct?
162. **S3 Glacier storage classes and retrieval times:** Instant Retrieval (ms), Flexible Retrieval (standard = 3-5 hrs, expedited = 1-5 min, bulk = 5-12 hrs), Deep Archive (up to 48 hrs); frequently tested — match use case to retrieval speed
163. **RAM/memory utilization is NOT a standard CloudWatch metric** — requires the **CloudWatch agent** as a custom metric (one of the most frequently tested details)
164. **CloudWatch basic (5-min, free) vs detailed (1-min, extra cost) monitoring**
165. **CloudWatch vs CloudTrail vs Config:** CloudWatch = resource health/monitoring; CloudTrail = API activity audit (who did what); AWS Config = resource compliance/rules
166. **AWS Organizations key components:** Root (management account), OU (account group, up to 5 levels nested), Member account, SCP (restricts services per OU); consolidated billing = one bill + per-OU cost view
167. **AWS Budgets alerts + forecasted alerts — NOTIFY only, does NOT stop resources** (frequently tested nuance)
168. **Trusted Advisor five pillars:** Cost Optimization, Performance, Security, Fault Tolerance, Service Limits; core checks = free, full checks = Business/Enterprise
169. **Support plans:** Basic (free, no tech cases), Developer (~$29/mo, business-hours email, one contact), Business (~$100/mo, 24/7 phone/chat, full Trusted Advisor), Enterprise (~$15K/mo, dedicated TAM, <15-min critical response)
170. **TAM (Technical Account Manager) = Enterprise only** (frequently tested); **24/7 phone/chat = Business+**
171. **CloudFormation = IaC service** (template = code/program, stack = running instantiation/process, change set = preview of updates); **automatic rollback on error; incremental updates via change sets**
172. **CloudFormation drift:** manual out-of-band changes detected; unresolved drift blocks further updates
173. **CloudFormation `--on-failure DO_NOTHING`** keeps failed resources for debugging (default rolls back, deleting evidence); **DependsOn** = creation order, **WaitCondition** = wait for in-instance success signal
174. **AMI = blueprint/snapshot for EC2, region-scoped** (must copy to use in another region); launch template = full recipe (AMI + instance type + subnet + key pair + SG) with versioning
175. **DynamoDB key facts:** key-value/document NoSQL, flexible schema, single-digit-ms latency, unlimited throughput/storage; **Scan** = read all items (for non-key attributes), **Query** = use primary key; **DAX** = in-memory cache for hot reads
176. **CloudFront = CDN** (delivers static content with low latency via Edge Locations); **S3 = stores** objects; **Glacier = archives** (not for active delivery)
177. **Global vs regional services:** **Global** = IAM, CloudFront, Route 53; **Regional** = EC2, AMI (region-bound)
178. **User data runs at initialization** (after instance creation, not during creation)
179. **Instance metadata IP: `169.254.169.254`** — exam trap often swaps digits
180. **CLI `--dry-run`** checks permissions without executing the action; **table** = most readable CLI output format
181. **Multi-AZ deployment = availability/fault tolerance** (exam heuristic: whenever question says availability/fault tolerance, answer = multiple AZs)
182. **EC2 pricing models:** On-Demand (flexible, no commitment), Reserved (1-3 yr, cheaper for steady workloads), Spot (up to ~90% off, reclaimable in ~1-3 min, fault-tolerant/non-critical only)

### Quick Memory Aids
```
Multi-AZ     → Availability (failover, resilience)
Read Replica → Scalability (read performance, load distribution)

RDS          → SQL / Relational databases (MySQL, PostgreSQL, Aurora, etc.)
Aurora       → AWS's own engine, faster than MySQL/PG, still part of RDS
DynamoDB     → NoSQL / Key-value (flexible schema, massive scale)

DAX          → DynamoDB's built-in cache (like Redis, but only for DynamoDB)
Global Tables → DynamoDB across multiple regions

EBS          → Block storage, single-AZ, persistent (boot volume)
Instance Store → Ephemeral block storage (lost on stop/terminate)
EFS          → Shared NFS file system, Linux-only (multi-EC2)
FSx          → Windows + Linux file system
S3           → Object storage, 11 nines durability, buckets/objects/keys

Glacier Deep Archive → Cheapest S3 tier, 12–48 hr retrieval
Intelligent-Tiering  → S3 auto-moves objects by access pattern
Object Lock          → WORM for compliance (retention + legal hold)

VPC Peering → NOT transitive (A↔B + B↔C ≠ A↔C)
Gateway Endpoint → Free, S3/DynamoDB only
Interface Endpoint (PrivateLink) → Paid, other AWS services
NAT Gateway → Public subnet + Elastic IP, outbound only
Bastion Host → Public jump box into private subnets

SG vs NACL → SG = stateful/instance/allow-only
             NACL = stateless/subnet/allow+deny/numbered/lowest-first
```

---

*Consolidated from daily lecture notes, Weeks 3–14 | AWS re/Start Cohort 3: Project CloudIgnite*
*Last updated: July 1, 2026 (includes Weeks 13–14: S3 Glacier, CloudWatch Deep Dive, CloudTrail, Organizations, Tagging, Cost Management, SageMaker, Support Plans, Trusted Advisor, AMIs, IaC, CloudFormation, and Certification Prep Assessment)*
