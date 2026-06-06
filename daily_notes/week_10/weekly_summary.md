# Week 10 Summary — June 3–5, 2026
**AWS re/Start Cohort 3: Project CloudIgnite**

---

## What We Learned

### SQL Advanced Queries & Amazon RDS (Tue Jun 3)

#### SQL Advanced Topics
- **ORDER BY:** Sort ascending (default) or descending; multiple columns (priority left to right); can reference column numbers
- **GROUP BY:** Groups rows sharing same value; used with aggregate functions (`COUNT`, `SUM`, `AVG`)
- **HAVING:** Filters groups after `GROUP BY` (like `WHERE` but for grouped results); cannot use aggregate functions in `WHERE`
- **Set Operations:** `UNION` (combine, dedupe), `UNION ALL` (combine, keep dupes), `INTERSECT` (common rows), `MINUS`/`EXCEPT` (rows in A not in B)
- **JOIN Operations:**
  - `INNER JOIN` — matching rows in both tables
  - `LEFT JOIN` — all left table + matching right
  - `RIGHT JOIN` — all right table + matching left
  - `FULL JOIN` — all rows from both tables
  - Table aliases (`ci`, `co`) for readability; `ON` clause defines join condition
- **Window Functions:**
  - `OVER()` with `PARTITION BY` — aggregate across related rows without collapsing them (unlike GROUP BY)
  - `RANK()` — assigns rank number within each partition

#### Amazon RDS (Lab 160)
- **What is RDS:** Fully managed relational database service; supports MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, Aurora
- **RDS vs EC2 + DB:** RDS = AWS manages provisioning, patching, backups; EC2 = you manage everything
- **Security Group for DB:** Inbound MySQL/Aurora (port 3306) from Web Security Group only — not from internet
- **DB Subnet Group:** RDS deployed in private subnets across two AZs; not publicly accessible
- **Multi-AZ Deployment:** Primary + standby replica in different AZs; automatic failover for high availability
- **3-tier architecture:** Internet → EC2 (Public Subnet) → RDS (Private Subnet)
- **Lab steps:** Create DB Security Group → Create DB Subnet Group → Launch RDS instance (MySQL, db.t3.medium, Multi-AZ, private subnet, no public access)

### Amazon RDS Deep Dive, Aurora & DynamoDB (Wed Jun 4)

#### Amazon RDS
- **Fully managed** relational DB; AWS handles OS, patching, backups, hardware
- Supports: MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, Aurora
- **DB Instance Classes:** T3 (general), M/R (memory optimized), X (high performance)
- **Storage types:** Magnetic (legacy), GP2/GP3 (general), IO1/IO2 (high-throughput)
- **Zero-downtime storage scaling** — unlike EBS on EC2
- **Creation methods:** Easy Create (recommended defaults) vs Standard Create (full config)

#### Multi-AZ vs Read Replicas (Highly Tested)
| | Multi-AZ | Read Replica |
|-|---------|-------------|
| Purpose | High Availability / Failover | Scalability / Read Performance |
| Can serve reads? | No (standby is idle) | Yes |
| Automatic failover? | Yes | No |
| Replication | Synchronous | Asynchronous |

#### RDS Scaling
- **Vertical:** Change instance class (e.g., T3 → M5) for more CPU/RAM
- **Storage:** Increase capacity with zero downtime

#### Amazon Aurora
- AWS's **proprietary, cloud-native** relational DB engine (part of RDS)
- Compatible with MySQL and PostgreSQL; generally faster
- Slightly more expensive but more features
- **Aurora Clusters:** primary instance (read/write) + Aurora replicas (read-only)
- Uses read endpoints and writer endpoints to route traffic

#### Amazon DynamoDB
- Fully managed **NoSQL** database service
- Key-value store; **no fixed schema** — items in same table can have different attributes
- **Primary Key:** simple (partition key only) or composite (partition key + sort key)
- **Partition Key** determines which partition stores the item; **Sort Key** orders items within partition
- **Global Tables:** multi-region replication for low latency and disaster recovery
- **DAX (DynamoDB Accelerator):** in-memory cache for DynamoDB (like Redis, DynamoDB-specific)
- Automatic encryption at rest; automatic backups; built-in scalability

#### Labs 274–275
- **Lab 274:** Aurora MySQL-compatible cluster; connected via SSM; standard MySQL syntax works
- **Lab 275:** Created DynamoDB `music` table; demonstrated flexible schema; Query (fast, uses key) vs Scan (slower, checks all items)

### AWS Cloud Adoption Framework & Well-Architected Framework (Thu Jun 5)

#### AWS Cloud Adoption Framework (CAF)
- **Planning tool** for transitioning from on-premises to cloud
- **6 Perspectives:** 3 Business (Business, People, Governance) + 3 Technical (Platform, Security, Operations)
- Key insight: Even if technology is ready, failure to train people or align governance will cause migration to fail

#### AWS Well-Architected Framework (WAF)
- **Design/operational tool** for building cloud systems efficiently, securely, cost-effectively
- **6 Pillars:**
  1. **Operational Excellence** — deliver business value, improve continuously
  2. **Security** — protect systems and data (IAM, encryption, traceability)
  3. **Reliability** — system recovers and meets demand (test recovery, auto-recover, scale horizontally)
  4. **Performance Efficiency** — use resources efficiently (right-sizing, serverless, data-driven decisions)
  5. **Cost Optimization** — eliminate waste (consumption-based model, measure efficiency)
  6. **Sustainability** — environmentally responsible cloud usage

#### Well-Architected Design Principles
- Stop guessing capacity (use Auto Scaling)
- Test systems at production scale (duplicate, test, shut down)
- Automate to ease experimentation (Terraform, Python, Bash)
- Allow for evolutionary architectures (cloud is dynamic)
- Drive architecture using data (data-driven decisions)
- Improve through game days (simulate failures, practice recovery)

#### Reliability & High Availability (Most Important for Exam)
- **Reliability:** System works as expected (MTBF = Total Time ÷ Failures)
- **Availability:** System is up and running (% uptime, measured in "nines")
- **The "nines":** 99.999% (5-nines) = ~5 minutes max downtime/year; Amazon S3 = 11 nines durability
- **High Availability prime factors:**
  - Fault tolerance (redundant components, Multi-AZ)
  - Scalability (Auto Scaling)
  - Recoverability (restore after failure)

#### Traditional → AWS Service Mapping
| Traditional | AWS |
|------------|-----|
| Physical server | EC2 |
| SAN storage | EBS |
| NAS storage | EFS |
| Tape backup | S3 |
| Active Directory | AWS Directory Service |

#### Lab 16: Aurora/RDS Challenge
- Launch Aurora (MySQL-compatible) or RDS MySQL database
- Connect from EC2 instance via SSH
- Run SQL queries against the database

### Key CLF-C02 Connections
- **Amazon RDS:** Core database service — fully managed, multiple engines, automatic patching/backups
- **Amazon Aurora:** AWS-native high-performance relational DB; MySQL/PostgreSQL compatible
- **Multi-AZ vs Read Replicas:** Availability vs scalability — heavily tested distinction
- **Amazon DynamoDB:** NoSQL; key-value; flexible schema; Global Tables for multi-region
- **DAX:** In-memory cache for DynamoDB read performance
- **AWS Cloud Adoption Framework (CAF):** 6 perspectives for planning migration
- **AWS Well-Architected Framework (WAF):** 6 pillars for designing cloud systems
- **Reliability vs Availability:** Definitions and measurements (MTBF, "nines")
- **High Availability:** Fault tolerance, scalability, recoverability — exam vocabulary
- **Traditional → AWS mapping:** EC2, EBS, EFS, S3, AWS Directory Service
- **VPC architecture:** Private subnet for databases, Security Groups, DB Subnet Groups
- **Shared Responsibility:** AWS manages RDS engine; you manage data and access control
- **3-tier architecture:** Internet → EC2 (Public Subnet) → RDS (Private Subnet)

---

## Daily Notes
- [June 3](./2026-06-03.md) — SQL Advanced (ORDER BY, GROUP BY, HAVING, UNION, JOIN, Window Functions), Amazon RDS Lab 160
- [June 5](./2026-06-05.md) — AWS Cloud Adoption Framework (CAF), Well-Architected Framework, Reliability & HA, Lab 16
