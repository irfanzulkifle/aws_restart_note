# Week 7 Summary — May 11–15, 2026
**AWS re/Start Cohort 3: Project CloudIgnite**

---

## What We Learned

### Security Compliance & AWS Support (Mon May 11)
- **Compliance types:** Regulatory (government/industry) vs Contractual (SLA, PLA)
- **Standards:** PCI DSS (payment cards), HIPAA (healthcare), GDPR (EU data protection), PIPEDA (Canada)
- **AWS Risk & Compliance:** Business Risk Management, Control Environment & Automation, Certification & Attestations
- **AWS Artifact:** Portal for accessing AWS security/compliance documentation
- **AWS Support Plans:** Developer (business hours) → Business (24/7, ≤4hr production) → Enterprise (24/7, ≤15min critical, TAM)
- **AWS resources:** Trusted Advisor, Personal Health Dashboard, Advisories & Bulletins, Professional Services, Partner Network

### Python Introduction (Mon May 11 — continued)
- **Why programming:** Automation; Python is interpreted, dynamically typed, cross-platform
- **Interpreted vs Compiled:** Python = line-by-line; C/Java = whole file at once
- **Data types:** `int`, `float`, `bool`, `str`; Python infers types automatically
- **Variables:** `=` assignment vs `==` comparison
- **Python setup:** Install from python.org, add to PATH, VS Code + Python extension

### Python Basics & Data Types (Tue May 12)
- **Primitive types:** `int`, `float`, `complex`, `bool`, `str`
- **Composite types:** Combinations of primitives (e.g., Person with name, age, email)
- **Functions:** Input → Process → Output; reusable code blocks
- **Collections:** List (ordered, mutable), Set (unordered, no duplicates), Queue (FIFO), Dictionary (key-value pairs)
- **Static vs Dynamic typing:** Python allows variable type changes at runtime
- **Control flow:** `if/elif/else`, loops (`for`, `while`)
- **Python syntax:** Indentation is mandatory (4 spaces), `#` for comments
- **String operations:** Concatenation (`+`), f-strings (`f"Age: {age}"`)
- **Version control:** Git (local) vs GitHub (remote); clone, commit, push, pull, branch, merge
- **AWS Cloud9:** Browser-based IDE running on EC2; integrated terminal; auto-saves
- **AWS CodeCommit:** AWS-managed Git repository service
- **Labs 1–3:** Hello World, numeric types, string operations in Cloud9

### Python Data Types & Operators (Wed May 13)
- **Mutable vs Immutable:** Immutable: `int`, `float`, `str`, `tuple`; Mutable: `list`, `dict`, `set`
- **Type conversion:** `int()`, `float()`, `str()`; `input()` always returns string
- **Operators:** Arithmetic (`+`, `-`, `*`, `/`, `//`, `%`, `**`), comparison, logical (`and`, `or`, `not`), assignment shortcuts
- **User input:** `input()`, f-strings, `.format()` method
- **Lists:** Zero-indexed, negative indexing, `append()`, `insert()`, `pop()`, `remove()`
- **Tuples:** Ordered, immutable; created with `()`
- **Dictionaries:** Key-value pairs; created with `{}`; access by key
- **For loops & `range()`:** `range(stop)`, `range(start, stop)`, `range(start, stop, step)`
- **AWS Lambda:** Serverless compute; pay per execution; event-driven (S3 upload → Lambda trigger)
- **Labs 110–112:** Strings, lists, tuples, dictionaries

### Python Exceptions & Control Flow (Thu May 14)
- **Exceptions:** Runtime errors (IndexError, ZeroDivisionError, TypeError, RecursionError)
- **Why handle:** Prevent crashes, improve user experience
- **if/elif/else:** Colon syntax, indentation-based blocks, case-insensitive comparison with `.lower()`
- **While loop:** Runs while condition is true; `break` exits, `continue` skips iteration
- **For loop with `range()`:** `range(start, stop, step)` — upper bound is always exclusive
- **List comprehension:** `[i for i in range(1, 10)]`
- **String formatting:** `.format()`, f-strings, `.join()` method
- **CSV file reading (Lab 113):** `import csv`, `csv.reader()`, `with open()`

### Python Functions & Exception Handling (Fri May 15)
- **Functions:** `def function_name(params): ... return value`; four types (with/without args and return)
- **Exception handling:** `try/except` block; catch specific exceptions; user-friendly error messages
- **Conditionals (Lab 114):** Case-insensitive comparison, recursive input validation
- **Loops & Random (Lab 115):** `random.randint()`, `range()` with step, binary search strategy
- **Caesar Cipher:** Encrypt by shifting characters; decrypt by reversing shift
- **SCP command:** Upload files to EC2: `scp -i key.pem file.py ec2-user@ip:/path/`
- **Security Group issue:** Port 22 blocked → edit inbound rules

### Key CLF-C02 Connections
- Compliance standards (PCI DSS, HIPAA, GDPR), AWS Artifact, Support Plans, Trusted Advisor
- AWS Lambda (serverless), Cloud9, CodeCommit, EC2, S3 event triggers

---

## Daily Notes
- [May 11](./2026-05-11.md) — Security Compliance, AWS Support Plans, Python Introduction & Setup
- [May 12](./2026-05-12.md) — Data Types, Functions, Collections, Static/Dynamic Typing, Git & GitHub, Cloud9
- [May 13](./2026-05-13.md) — Python Operators, Lists, Tuples, Dictionaries, For Loops, AWS Lambda
- [May 14](./2026-05-14.md) — Exceptions, if/elif/else, While/For Loops, CSV File Reading
- [May 15](./2026-05-15.md) — Functions, Exception Handling, Caesar Cipher, SCP Upload to EC2
