# Week 10 Summary — June 3, 2026
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

### Key CLF-C02 Connections
- **Amazon RDS:** Core database service — fully managed, multiple engines, automatic patching/backups
- **Amazon Aurora:** AWS-native high-performance relational DB
- **Multi-AZ:** High availability and fault tolerance (key cloud concepts)
- **VPC architecture:** Private subnet for databases, Security Groups, DB Subnet Groups
- **Shared Responsibility:** AWS manages RDS engine; you manage data and access control
- **Amazon DynamoDB:** NoSQL managed database (covered in upcoming sessions)

---

## Daily Notes
- [June 3](./2026-06-03.md) — SQL Advanced (ORDER BY, GROUP BY, HAVING, UNION, JOIN, Window Functions), Amazon RDS Lab 160
