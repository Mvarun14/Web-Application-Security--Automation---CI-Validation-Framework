

## WebSecAppAuto — Web Application Security, Automation & CI Validation Framework

WebSecAppAuto is a hands-on application security project that demonstrates common web application vulnerabilities, their secure remediations, and continuous security validation through automated exploitation and CI pipelines. The project models real-world AppSec workflows by combining insecure implementations, hardened fixes, automated attacks, testing, and CI enforcement.

---

## Project Highlights

* Designed a deliberately vulnerable web application showcasing **SQL Injection, Stored XSS, CSRF, Path Traversal, and IDOR**, alongside a **secure implementation** applying industry-standard mitigations.

* Built **side-by-side vulnerable and secure applications**, enabling direct comparison between insecure coding patterns and secure engineering practices.

* Developed an **automated exploitation framework** that programmatically attacks vulnerable endpoints and validates exploit failure against secured counterparts.

* Integrated a **CI pipeline** that automatically:

  * Initializes application databases
  * Executes automated exploit scripts
  * Runs `pytest`-based security tests
  * Fails builds if vulnerabilities are exploitable or security regressions are introduced

* Modeled **shift-left application security**, ensuring vulnerabilities are detected early during code changes rather than post-deployment.

---

## System Architecture

The project follows a modular, security-focused architecture:

* **Vulnerable Application Layer** – Intentionally insecure services demonstrating real attack vectors
* **Secure Application Layer** – Hardened implementations enforcing validation, authorization, and defense-in-depth
* **Automation & Exploitation Layer** – Scripts simulating attacker workflows
* **Testing & CI Layer** – Automated security validation executed on every commit

---

## Project Structure

```
WebSecAppAuto/
├── vulnerable_app/        # Intentionally vulnerable web application
│   ├── app.py
│   ├── routes/
│   └── utils/
├── secure_app/            # Secure implementation of the same functionality
│   ├── app.py
│   ├── routes/
│   └── utils/
├── auto_exploit.py        # Automated vulnerability exploitation
├── init_dbs.py            # Database initialization for CI and local runs
├── tests/                 # Pytest-based security tests
├── .github/workflows/     # CI pipeline configuration
│   └── ci.yml
├── requirements.txt
└── README.md
```

---

## Core Components

### Vulnerable Application

Located in `vulnerable_app/`, this module intentionally violates secure coding principles to demonstrate real-world exploitability:

* SQL Injection via unsanitized queries
* Stored XSS from improper output encoding
* CSRF due to missing request validation
* Path Traversal through unsafe file handling
* IDOR from missing authorization checks

---

### Secure Application

Located in `secure_app/`, this module implements security best practices:

* Parameterized queries and ORM protections
* Context-aware output encoding
* CSRF tokens and request verification
* Safe file path normalization and allowlisting
* Object-level authorization enforcement

---

### Automated Exploitation

The `auto_exploit.py` script simulates attacker behavior:

* Executes proof-of-concept attacks against vulnerable endpoints
* Demonstrates exploit feasibility and impact
* Confirms exploit failure against secure endpoints

---

### Continuous Integration (CI)

The CI pipeline enforces security on every code change:

* Sets up isolated Python environments
* Installs dependencies and initializes databases
* Runs automated exploit scripts
* Executes security-focused `pytest` test cases
* Fails the pipeline if vulnerabilities are exploitable or protections regress

This ensures **security controls are continuously validated**, not just manually tested.

---

### Testing & Validation

* Pytest-based tests assert:

  * Successful exploitation of the vulnerable app
  * Effective prevention in the secure app
* Prevents accidental reintroduction of vulnerabilities during refactors

---

## Setup & Execution (Local)

### Environment Setup

```bash
python3 -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

### Initialize Databases

```bash
python init_dbs.py
```

### Run Applications

```bash
python -m vulnerable_app.app
python -m secure_app.app
```

### Run Automated Exploits

```bash
python auto_exploit.py
```

### Run Tests

```bash
pytest -q
```

---

## CI Workflow Overview

On every push or pull request:

1. Dependencies are installed
2. Databases are initialized
3. Automated exploits are executed
4. Security tests are run
5. Build fails if any exploit succeeds unexpectedly


