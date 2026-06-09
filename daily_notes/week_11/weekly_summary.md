# Week 11 Summary — June 8–9, 2026
**AWS re/Start Cohort 3: Project CloudIgnite**

---

## What We Learned

### System Operations (SysOps) & Automation (Mon Jun 8)

#### System Operations Overview
- **SysOps** = deployment, administration, monitoring, maintenance, security of cloud infrastructure
- Core responsibilities: Build, Test, Deploy, Monitor, Maintain, Safeguard
- **Automation tools:** Bash/Shell, Python (recommended), C#/Ruby, CloudFormation, Terraform
- Key distinction: **CloudFormation** creates reusable infrastructure templates; **IAM** manages permissions only

#### Troubleshooting Knowledge Base
- Structured document (Excel/CSV) recording known issues, symptoms, root causes, resolution steps
- Fields: Issue Number, Category, Description, Symptoms, Root Cause Analysis, Resolution, Helpful Tools
- Categories: Storage & Data Management, Networking, Security & Compliance, Compute
- Enables consistent response and institutional memory

#### AWS Identity and Access Management (IAM) — Recap
- **Three access methods:** Management Console (GUI), AWS CLI, AWS SDK
- **Identity types:** User, Group, Role
- **Policy types:** Identity-based, Resource-based, SCP (org-level), ACL (legacy)
- **IAM policy JSON:** Effect (Allow/Deny), Action, Resource, Condition (optional)
- **Best practices:** Least privilege, use IAM Roles, enable MFA, never use root
- **SSO/Federated access:** single credentials for multiple services; cross-account access via roles

#### AWS Command Line Interface (CLI)
- Terminal-based AWS management
- Installation: download zip → unzip → `sudo ./aws/install`
- Configuration: `aws configure` (stores keys in `~/.aws/credentials` and `~/.aws/config`)
- Output formats: `json`, `table`, `text`
- Common commands: `aws ec2 describe-instances`, `aws s3 ls`, `aws iam list-users`
- **Dry run:** `--dry-run` simulates command to check permissions without execution
- CLI is **instance-specific** — configure on each EC2 separately

#### AWS Systems Manager (SSM)
- Centralized management of many EC2/on-prem servers without SSH
- **Capabilities:**
  - Fleet Manager — inventory of managed instances
  - Run Command — execute scripts across instances simultaneously
  - Session Manager — browser-based terminal, no port 22 needed
  - Patch Manager — centralized OS patching
  - Maintenance Window — schedule tasks
  - State Manager — enforce desired state
  - Parameter Store — store secrets/config values securely
- **SSM Documents:** instruction files (Bash-like) used by Run Command, State Manager
- **Parameter Store:** EC2 reads parameters at runtime; enables dynamic configuration

#### Labs: AWS CLI & Systems Manager
- **Lab 168:** Installed AWS CLI on EC2, configured with IAM credentials, retrieved IAM policy using CLI
- **SSM Lab:** Used Fleet Manager for inventory, Run Command to install dashboard app, Parameter Store to toggle beta feature, Session Manager for browser-based SSH-less access

### Amazon S3 Static Website Hosting & EC2 Deep Dive (Tue Jun 9)

#### Amazon S3 Static Website Hosting
- **Static website** = HTML, CSS, client-side JS only (no server-side scripting, no database)
- **Why S3:** No infrastructure to manage, cost-effective (storage + transfer only), automatic scalability, high availability
- **Setup:** Create bucket (globally unique name) → upload files → enable Static Website Hosting → disable Block Public Access → enable ACLs
- **Endpoint format:** `http://<bucket-name>.s3-website-<region>.amazonaws.com`
- **Custom domain:** Use Route 53 to map domain to S3 endpoint
- **Automation:** Use AWS CLI with bash scripts; `aws s3 sync` (only changed files) vs `aws s3 cp --recursive` (re-uploads everything)
- **Bash script pitfall:** `#!/bin/bash` must be on its own line; make executable with `chmod +x`

#### EC2 Deep Dive
- **EC2 architecture:** Virtual machines on hypervisor; CPU, RAM, ephemeral instance store (not persistent — use EBS for persistence)
- **AMI (Amazon Machine Image):** Pre-configured template for launching instances; contains boot volume, block device mapping, launch permissions; sources: AWS-provided, community, custom
- **Instance types:** General Purpose (T), Compute Optimized (C), Memory Optimized (R/X), Storage Optimized (I/D), Accelerated Computing (P/G), HPC (Hpc)
- **Key pairs:** Public key (stored on instance), private key (.pem file, keep safe); used for SSH on port 22
- **IP addressing:**
  - **Private IP:** static within VPC, retained on stop/start
  - **Public IP:** dynamic, changes on every stop/start
  - **Elastic IP:** static public IP, persists across stop/start
- **Security Groups:** Virtual firewall at instance level; control inbound/outbound traffic by port/protocol/source; can reference another SG as source
- **Instance Profile:** Attaches IAM Role to EC2; enables EC2 to access AWS services without storing credentials
- **User Data:** Bash script that runs once at first boot; used for software installation, configuration tasks
- **Instance Metadata Service:** `http://169.254.169.254/latest/meta-data/` — accessible only from within EC2; returns instance info (ID, type, hostname, AMI ID, etc.)
- **Connection methods ranked by security:** SSM Session Manager (no ports, no keys, fully logged) > EC2 Instance Connect (port 22, browser) > SSH (port 22, .pem key)

#### Lab: Static Website on S3 using AWS CLI
- Built static website for Sophia's Café using S3
- Created S3 bucket → created IAM user → attached S3FullAccess policy → enabled public access & ACLs → configured static website hosting
- Uploaded files using `aws s3 cp --recursive --acl public-read`
- Created automation script using `aws s3 sync` (only uploads changed files)

### Key CLF-C02 Connections
- **IAM:** Users/Groups/Roles; identity-based vs resource-based policies; SCPs; MFA; Least Privilege
- **AWS CLI & SDK:** three access methods for AWS (Console, CLI, SDK)
- **AWS Systems Manager:** central management; Run Command, Session Manager, Parameter Store, Fleet Manager
- **CloudFormation:** Infrastructure-as-Code for reusable templates (contrast with IAM)
- **Automation philosophy:** automate repetitive tasks; use Python/CloudFormation/Terraform
- **Shared Responsibility:** You manage IAM users and policies; AWS manages the underlying service infrastructure
- **S3:** static website hosting, bucket naming (globally unique), endpoint URL format, storage classes (automation via CLI)
- **EC2:** instance types (T/C/R/X/P/G/Hpc), AMI, key pairs, security groups (stateful), instance store vs EBS, public IP vs Elastic IP, instance profile, user data, metadata service
- **VPC flow:** EC2 in public subnet can access internet via IGW; RDS typically placed in private subnet; security groups bridge between tiers

---

## Daily Notes
- [June 8](./2026-06-08.md) — System Operations, AWS CLI, AWS Systems Manager, IAM Recap, Troubleshooting Knowledge Base
- [June 9](./2026-06-09.md) — S3 Static Website Hosting, EC2 Deep Dive (AMI, Instance Types, Key Pairs, Security Groups, IP Types, Instance Profile, User Data, Metadata), Lab Walkthrough
