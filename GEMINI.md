# Task: GitHub Security Investigation

## Step 1: Remote Repository Setup
Create a dedicated space for your security audit.
* Create a new public GitHub repository named `git_security`.
* Initialize your local project folder and clone or link it to this repository.

## Step 2: Documentation & Research
Create a document to capture your findings on sensitive data management.
* `SECURITY.md`: Create a markdown file to document what information must never be pushed (e.g., API keys, private keys, database credentials, environment variables).
* Investigation: Research common vulnerabilities caused by committed secrets and the risks involved. What is a private and public repo?

## Step 3: Implementing Protection
Learn to secure your repository proactively.
* Create a `.gitignore` file to ensure sensitive local configuration files are excluded from version control.
* Document best practices for using environment variable files (e.g., `.env`) and keeping them out of Git.

## Step 4: Initial Commit
Save your security documentation and your `.gitignore` template.

## Step 5: Verification
Run a check to ensure no sensitive patterns are staged in your local environment.

## Step 6: Finalize and Push
Publish your security guide to your repository.
