# Git Security Audit & Guide

This repository serves as a security guide and resource for managing sensitive data in version control. Following these principles prevents unauthorized access, resource abuse, and security breaches.

---

## 1. What Information Must Never Be Pushed to Version Control

The following categories of sensitive information must never be committed to Git:

*   **API Keys and Tokens:** Private tokens for external services (e.g., OpenAI, AWS, Google Cloud, Stripe, Slack, GitHub Personal Access Tokens).
*   **Private Cryptographic Keys:** Private SSH keys (`id_rsa`), SSL/TLS private keys (`.key`, `.pem`), and token signing keys.
*   **Database Credentials:** Database connection strings, database usernames, passwords, ports, and host addresses.
*   **Local Configuration & Environment Files:** Configuration files containing passwords or credentials (e.g., `.env`, `config.json`, `settings.py` containing hardcoded secrets).
*   **Personally Identifiable Information (PII):** Usernames, passwords, phone numbers, email addresses, or client-sensitive data.

---

## 2. Investigation: Common Vulnerabilities & Risks of Leaked Secrets

Committing credentials to version control exposes repositories to significant vulnerabilities:

*   **Credential Leaks and Automated Exploits:** Public repositories are continuously crawled by malicious bots (scrapers) that scan commits for recognizable API keys and AWS credentials within seconds of a push.
*   **Resource and Compute Theft:** Leaked cloud credentials (e.g., AWS, GCP) are commonly exploited by attackers to spin up high-performance GPU instances for cryptocurrency mining or DDoS attacks, resulting in massive financial bills.
*   **Data Breaches & Data Exfiltration:** Compromised database credentials allow attackers to read, modify, or delete sensitive user databases, resulting in data leaks and regulatory penalties (e.g., GDPR, HIPAA).
*   **Supply Chain Compromise:** Pushing access tokens to build/deployment pipelines can allow attackers to inject malicious packages or compromise software update infrastructure.

---

## 3. Public vs. Private Repositories

Understanding the scope of repository visibility is crucial for risk assessment:

| Feature | Public Repository | Private Repository |
| :--- | :--- | :--- |
| **Visibility** | Open to anyone on the internet. | Restricted to authorized users/collaborators. |
| **Scraping Risk** | Extremely high; crawled automatically in real-time. | Low; but exists if collaborator credentials are leaked. |
| **Git History Retention** | Permanent unless history is rewritten (e.g., `git-filter-repo`). | Permanent; risk of exposure if the repo is ever made public. |
| **Security Policy** | Never commit secrets under any circumstances. | Never commit secrets; treat private repos like public ones. |

---

## 4. Best Practices for Managing Local Environment Variables

To keep credentials secure while maintaining a smooth developer workflow, implement the following best practices:

### A. Use Environment Variable Files Locally
Store configuration and secrets in a local `.env` file that is kept out of Git.
```env
# Example of local .env file (DO NOT commit this)
DATABASE_URL="postgresql://db_user:super_secret_password@localhost:5432/my_db"
STRIPE_API_KEY="sk_test_51Nx..."
```

### B. Provide a Template File (`.env.example`)
To help other developers set up the project, commit a `.env.example` file that lists all required keys but contains placeholder or mock values.
```env
# Required configuration variables for this project
DATABASE_URL="postgresql://db_user:password@localhost:5432/db_name"
STRIPE_API_KEY="sk_test_placeholder"
```

### C. Implement a `.gitignore` File
Use a `.gitignore` file to ensure that local sensitive files are never staged or tracked by Git.

### D. Use Secrets Managers for Production
For staging and production environments, inject credentials dynamically using environments/secrets managers rather than files (e.g., AWS Secrets Manager, GitHub Secrets, or Vercel Environment Variables).
