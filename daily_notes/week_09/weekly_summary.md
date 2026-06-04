# Week 9 Summary — May 25–30, 2026
**AWS re/Start Cohort 3: Project CloudIgnite**

---

## What We Learned

### Database Fundamentals (Mon May 25)
- **Data & Database:** Data = piece of information; Database = organized collection of data in tables
- **Data models:** Relational (SQL), Semi-structured (CSV/XML), Entity-Relationship, Object-Based (JSON)
- **Relational database:** Tables with rows and columns; fixed schema; primary keys and foreign keys
- **Relationships:** One-to-One, One-to-Many, Many-to-Many
- **Schema:** Blueprint defining column names, data types, relationships; modifiable with `ALTER TABLE`
- **SQL categories:** DDL (CREATE, ALTER, DROP), DML (INSERT, UPDATE, DELETE), DQL (SELECT), DCL (GRANT, REVOKE), TCL (COMMIT, ROLLBACK)
- **Data types:** CHAR(n) vs VARCHAR(n), SMALLINT/INT/BIGINT, DECIMAL vs FLOAT/REAL, DATE/TIME/TIMESTAMP
- **Constraints:** NOT NULL, UNIQUE, DEFAULT, PRIMARY KEY, FOREIGN KEY
- **Transactions:** BEGIN → ACTIVE → COMMITTED/ABORTED; ACID properties (Atomicity, Consistency, Isolation, Durability)
- **Relational vs NoSQL:** Fixed schema + ACID vs Flexible schema + Horizontal scaling
- **AWS database services:** Amazon RDS, Aurora (SQL), DynamoDB, DocumentDB (NoSQL)
- **Data interaction models:** Client-Server vs 3-Tier Web Application

### SQL Fundamentals — DDL & DML (Tue May 26)
- **SQL tools:** SQLite (beginner), MySQL/PostgreSQL (production), DB Browser for SQLite (GUI)
- **DDL commands:** `CREATE DATABASE/TABLE`, `ALTER TABLE`, `DROP TABLE`, `SHOW`, `DESCRIBE`
- **DML commands:** `INSERT INTO` (with/without column names), `SELECT`, `UPDATE SET`, `DELETE FROM`
- **CSV import/export:** `LOAD DATA INFILE`, `SELECT INTO OUTFILE`
- **Data cleaning:** Common errors (data entry, wrong type, duplicates, missing data); SQL string functions (TRIM, CONCAT, UPPER, LOWER, LEFT, RIGHT)
- **EC2 + SSM Session Manager:** Connecting to instances without SSH keys
- **Labs 268–269:** Creating databases/tables, inserting/updating/deleting data, loading from SQL files

### SQL Queries — NULL, SELECT, Filtering (Thu May 28)
- **NULL values:** Absence of value; `NULL = NULL` is FALSE; `IS NULL` / `IS NOT NULL` syntax
- **SELECT structure:** `SELECT → FROM → WHERE → GROUP BY → HAVING → ORDER BY → LIMIT`
- **WHERE filtering:** Comparison operators (`=`, `<>`, `>`, `<`), logical operators (`AND`, `OR`), `IN`, `BETWEEN`, `LIKE`
- **LIKE wildcards:** `%` = zero or more chars; `_` = exactly one char
- **GROUP BY:** Groups rows for aggregate calculations; **HAVING:** Filters groups after GROUP BY
- **ORDER BY:** ASC (default) / DESC; **LIMIT:** Cap returned rows
- **Aliases:** `AS` for temporary column display names
- **Lab 270:** WHERE, LIKE, IN, BETWEEN, aggregate queries on world database

### SQL Advanced Queries (Fri May 29)
- **Operator precedence:** Parentheses > Arithmetic > Comparison > NOT > AND > OR
- **NULL behavior:** Any arithmetic with NULL returns NULL; use `IS NULL` not `= NULL`
- **Aggregate functions:** `SUM()`, `AVG()`, `COUNT()`, `MAX()`, `MIN()`
- **DISTINCT:** Removes duplicate values; `COUNT(DISTINCT col)` (MySQL only)
- **String functions:** `LOWER`, `UPPER`, `TRIM`, `CHAR_LENGTH`, `SUBSTRING_INDEX`, `INSERT`
- **Date functions:** `CURRENT_DATE`, `DATE_ADD` (MySQL only, not SQLite)
- **Case sensitivity:** Keywords/colnames = case-insensitive; string values = case-sensitive
- **Labs 271–272:** Conditional queries, aggregate functions, string functions, customer table filtering

### MySQL Labs & Database Practice (Sat May 30)
- **Labs 268–271:** Full hands-on MySQL practice
- **Lab 268:** CREATE DATABASE/TABLE, DESCRIBE, ALTER TABLE, DROP
- **Lab 269:** INSERT (positional and named), UPDATE (unconditional and conditional), DELETE, foreign key constraints, loading from `.sql` files
- **Lab 270:** SELECT, WHERE, ORDER BY, IS NULL, IN, LIMIT
- **Lab 271:** BETWEEN, LIKE, aggregate functions (COUNT, SUM, AVG, MIN, MAX)
- **Common mistakes:** Using `==` instead of `=`, forgetting WHERE on UPDATE/DELETE, parent-child delete order

### Key CLF-C02 Connections
- Amazon RDS (managed relational DB), Aurora (AWS-native, high performance), DynamoDB (NoSQL), DocumentDB, Redshift
- EC2 for lab environments, SSM Session Manager (secure keyless access), Security Groups
- Shared Responsibility Model (self-managed DB on EC2 vs managed RDS)

---

## Daily Notes
- [May 25](./2026-05-25.md) — Database Fundamentals, Data Models, SQL Overview, Constraints, ACID, DBaaS
- [May 26](./2026-05-26.md) — SQL Data Types, DDL & DML, CSV Import/Export, Data Cleaning
- [May 28](./2026-05-28.md) — NULL Values, SELECT Statement, WHERE/LIKE/IN/BETWEEN, GROUP BY/HAVING
- [May 29](./2026-05-29.md) — Operator Precedence, NULL Behavior, Aggregate Functions, String Functions
- [May 30](./2026-05-30.md) — MySQL Labs 268–271, Full Hands-on Practice
