# Week 6 Summary — May 5–7, 2026
**AWS re/Start Cohort 3: Project CloudIgnite**

---

## What We Learned

### PKI, SSL/TLS & AWS KMS (Mon May 5)
- **Public Key Infrastructure (PKI):** Asymmetric encryption — public key encrypts, private key decrypts
- **SSL/TLS key exchange:** Server sends public key → client encrypts symmetric key → server decrypts → both share symmetric key
- **Digital certificates:** Electronic credentials with public key, owner info, expiry date; CA-signed vs self-signed
- **Certificate Authority (CA):** Root CA + Subordinate CA; internal (free) vs external (paid); certificates have expiry dates and can be revoked (CRL)
- **AWS Certificate Manager (ACM):** Manages SSL/TLS certificates; automates renewal
- **AWS KMS Lab (Lab 278):** Create symmetric KMS key → encrypt/decrypt files using AWS Encryption SDK CLI on EC2 via SSM

### Identity Management & IAM (Tue May 6)
- **SSO (Single Sign-On):** One login, multiple services; central server issues tokens
- **Federated users:** External identity developer grants temporary access; no permanent AWS account needed
- **JWT tokens:** JSON Web Token format; has expiry; refresh tokens extend sessions
- **Amazon Cognito:** Managed user auth for web/mobile apps
- **AWS IAM:** Free, global service; Users, Groups, Roles, Policies
- **Root account:** Full access; use only for initial setup; enable MFA
- **IAM Roles:** Temporary delegated access (e.g., EC2 → S3 access without stored credentials)
- **IAM Policies:** JSON documents; identity-based vs resource-based; Explicit Deny > Explicit Allow > Implicit Deny
- **Lab 279:** Explored IAM users, groups, permissions — tested granular access control
- **Malware types:** Virus, worm, bot, backdoor/trojan, rootkit, spyware, adware, ransomware
- **IDS:** Signature-based vs anomaly-based; Network-based (NIDS) vs Host-based (HIDS)
- **Amazon GuardDuty:** AI-powered threat detection using VPC Flow Logs, DNS logs, CloudTrail

### CloudTrail, AWS Config & Incident Response (Wed May 7)
- **AWS CloudTrail:** "CCTV for AWS" — records who, when, what, where, how for every API call; logs stored in S3; infinite loop warning
- **AWS Config:** Compliance monitoring — continuously checks resource configurations against rules; alerts via SNS on non-compliance
- **Incident Response:** Stop → Inspect → Notify → Remediate → Prevent
- **BCP/DRP:** Business Continuity Plan (keep running during disaster); Disaster Recovery Plan (recover after)
- **Recovery metrics:** RTO (max downtime), RPO (max data loss), WRT (time to restore)
- **DR strategies:** Backup & Restore (cheapest) → Pilot Light → Active-Passive → Active-Active (most expensive)
- **AWS Network Firewall (Lab 280):** Block malicious URLs using Suricata-compatible stateful rules in VPC

### Key CLF-C02 Connections
- AWS KMS, ACM, IAM (Users/Groups/Roles/Policies), SSO, Cognito, Amazon Inspector, GuardDuty, CloudTrail, AWS Config, Disaster Recovery (RTO/RPO), AWS Network Firewall

---

## Daily Notes
- [May 5](./2026-05-05.md) — PKI, SSL/TLS, Digital Certificates, AWS KMS Lab, IAM Intro
- [May 6](./2026-05-06.md) — SSO, Federated Users, JWT, Cognito, IAM Deep Dive, Malware, IDS, GuardDuty
- [May 7](./2026-05-07.md) — CloudTrail, AWS Config, Incident Response, DR Strategies, AWS Network Firewall Lab
