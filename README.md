# Git Security Investigation & Audit

This repository contains security documentation, configuration templates, and best practices for managing sensitive data in version control systems. It serves as a guide to prevent credential leaks and establish secure coding environments.

---

## Repository Structure

*   [**SECURITY.md**](./SECURITY.md): A comprehensive security audit detailing what information must never be committed, risks and vulnerabilities from credential leaks, a comparison between public and private repositories, and credentials management workflows.
*   [**.gitignore**](./.gitignore): A production-ready template to prevent tracking of local environment files (`.env`), private cryptographic keys (`.pem`, `.key`), system logs, caches, and IDE/editor workspace files.
*   [**.env.example**](./.env.example): A template environment file illustrating the naming and placeholder formatting for application configurations (e.g., database connection strings, API integration keys) without exposing live credentials.

---

## Getting Started

### 1. Applying the Protection Configuration
To secure a new project using these templates, copy the files into your project's root folder:
```bash
cp .gitignore /path/to/your/project/
cp .env.example /path/to/your/project/
```

### 2. Creating Local Environment Variables
Create your local `.env` configuration using the template:
```bash
cp .env.example .env
```
Open `.env` and configure your actual credentials locally. Git will automatically ignore this file based on the `.gitignore` rules.

### 3. Verification Check
Before committing, you can run the following command to check if any secrets or sensitive keys are accidentally staged in Git:
```bash
git diff --cached | grep -iE "key|password|secret|token"
```
*(On Windows PowerShell, use `Select-String`):*
```powershell
git diff --cached | Select-String -Pattern "API_KEY|secret|password|token|private" -CaseSensitive:$false
```
