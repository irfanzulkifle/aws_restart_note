# Week 8 Summary — May 18–24, 2026
**AWS re/Start Cohort 3: Project CloudIgnite**

---

## What We Learned

### Python Modules, File Handling & Git (Mon May 18)
- **Code organization:** Functions → Modules → Libraries; `import module` or `from module import function`
- **Creating modules:** Write functions in a `.py` file, import from another script
- **Packages:** Folders with `__init__.py`; import with `from package.module import function`
- **File handling:** `open()` with modes `"r"`, `"w"`, `"a"`; always `close()` or use `with open()`
- **Exception handling:** `try/except` with specific exception types (FileNotFoundError, ZeroDivisionError, ValueError)
- **OS module:** `os.system()`, `os.listdir()`, `os.mkdir()`, `os.getcwd()`
- **JSON module:** `json.dumps()` (Python→JSON), `json.loads()` (JSON→Python), `json.dump()/load()` for files
- **PIP:** Package manager; `pip install`, `pip list`
- **GitHub & Git Lab:** `clone`, `add`, `commit`, `push`, `pull`, branches, merge, Personal Access Token

### Python for Bioinformatics (Tue May 19)
- **Lab 118:** Reading insulin sequence from NCBI; cleaning text files; splitting sequences with string slicing
- **Lab 120:** Counting amino acid occurrences (`.count()`); building dictionaries; calculating molecular weight
- **Lab 122:** Calculating net charge using PKa values and Henderson-Hasselbalch formula; while loop over pH range
- **Key concepts:** Variable scope (declare outside `with` block), f-string formatting (`.2f`), dictionary comprehension, `sum(d.values())`

### System Administration with Python (Wed May 20)
- **File handler module:** Reusable JSON file reader with `try/except`
- **SysAdmin with Python:** `os.system()` (deprecated) vs `subprocess.run()` (preferred)
- **User management:** `adduser`, `userdel`, `usermod -aG` (add to groups)
- **Package management:** `apt install`, `yum install`
- **Command-line arguments:** `sys.argv[1]` for script arguments
- **`subprocess.run()`:** Run shell commands; `capture_output=True` for piping; Python equivalent of `ls | grep`
- **VS Code debugging:** Breakpoints (red dots), Watch panel for variable inspection

### Debugging & Testing (Thu May 21)
- **Error types:** Syntax (easy), Runtime (medium — read traceback), Logical (hard — no crash)
- **Static vs Dynamic analysis:** Code review without running vs debugging while running
- **Debugging tools:** `pdb` command-line debugger, VS Code debugger with breakpoints and watchers
- **Assertion & logging:** Unit test assertions; Python `logging` library
- **Testing levels:** Unit → Integration → System → Acceptance (UAT)
- **Code quality:** SOLID, DRY, KISS principles
- **Lab 130:** Debugging Caesar Cipher — Type error (str vs int), logic error (lowercase not handled), wrong parameter passed to decrypt

### DevOps & CI/CD (Thu May 21 — continued)
- **DevOps:** Culture uniting development and operations; CALMS framework
- **Methodologies:** Waterfall (sequential) vs Agile (sprint-based iterations)
- **Automation types:** Build, Test, Deployment
- **CI/CD:** Continuous Integration (auto-test on push) → Continuous Delivery/Deployment (auto-deploy to staging/production)
- **Pipeline:** Push → GitHub Action → Tests → Build → Deploy to EC2 → Restart
- **IaC:** Infrastructure as Code (Terraform) — define infrastructure as code

### Automation & Orchestration (Fri May 22)
- **Automation vs Orchestration:** Single task automatically vs coordinating multiple automated tasks
- **Monolithic vs Microservices:** One repo/server vs independent services (Netflix example)
- **Naming conventions:** camelCase, PascalCase, snake_case, kebab-case, UPPER_CASE
- **PyLint:** Code style checker; **PyTest:** Unit testing framework
- **Version control:** Git workflow; merge conflicts; semantic versioning (MAJOR.MINOR.PATCH)
- **CI/CD tools:** Jenkins, GitHub Actions, GitLab CI/CD, AWS CodeDeploy

### Python Practice & Problem Solving (Sat May 24)
- **Lab 14:** Prime number algorithms — basic (O(n/2)), optimized (skip evens), efficient (check up to √n)
- **Palindrome checker:** Clean string → reverse with `[::-1]` → compare
- **Highest frequency character:** Build count dictionary; iterate alphabetically for tie-breaking
- **LeetCode Two Sum:** Nested loop approach (O(n²))
- **Nested loops:** Right-angled triangle and pyramid pattern printing
- **Python tips:** Ternary operator, chained comparisons, `map()`, `zip()`, multiple assignment, list slicing, type hints

### Key CLF-C02 Connections
- AWS Lambda, Cloud9, EC2, CodeCommit, CodeBuild, CodeDeploy, CodePipeline, CloudFormation
- DevOps culture, CI/CD pipelines, IaC, microservices (ECS, EKS, Lambda)

---

## Daily Notes
- [May 18](./2026-05-18.md) — Python Modules, File Handlers, JSON, PIP, GitHub & Git Basics
- [May 19](./2026-05-19.md) — Bioinformatics Labs (Insulin Analysis), String Handling, Dictionaries
- [May 20](./2026-05-20.md) — SysAdmin with Python, subprocess, VS Code Debugging
- [May 21](./2026-05-21.md) — Debugging & Testing, Caesar Cipher Debug Lab, DevOps & CI/CD
- [May 22](./2026-05-22.md) — Automation vs Orchestration, Microservices, PyLint/PyTest, Version Control
- [May 24](./2026-05-24.md) — Prime Numbers, Palindrome, LeetCode, Nested Loops, Python Tips
