## 🚀 Helsinki Full Stack Open: Continuous Integration & Delivery (KB)

Welcome to my central knowledge base and architectural playbook for the **University of Helsinki's Full Stack Open: CI/CD** course. This repository contains my structured notes, deep dives, and core concepts learned while building production-grade deployment pipelines.

🎯 **Practical Implementations:** My hands-on assignment submissions and pipeline code can be found in my accompanying [cicd-assignments](https://github.com/raghvendrashrinet/cicd-assignments) repository.

---

## 🛠️ Tech Stack & Ecosystem Covered
* **CI/CD Platforms:** GitHub Actions
* **Testing & Quality:** Jest, Cypress (End-to-End), ESLint
* **Containerization & Hosting:** Docker, Fly.io / Render / Heroku
* **Monitoring & Notifications:** Slack/Discord Webhooks, Health Checks

---

## 🧠 Key Learnings & Core Concepts

### 1. The Core Philosophies of CI/CD
* **Continuous Integration (CI):** Automating the build, linting, and testing processes on every single commit to catch bugs early.
* **Continuous Delivery (CD) vs. Continuous Deployment:** Understanding the critical boundary between code being *ready* for production vs. being *automatically pushed* to production after passing the pipeline.

### 2. Building Robust GitHub Actions Pipelines
* **Workflow Anatomy:** Mastering triggers (`on: [push, pull_request]`), environments, runners, and steps.
* **Caching & Optimization:** Utilizing dependency caching to dramatically cut down build times.
* **Securing Secrets:** Handling deployment tokens, API keys, and environment variables securely using GitHub Secrets.

### 3. Pipeline Safety & Verification
* **Linting & Pre-commit Checks:** Ensuring code style consistency before wasting runner minutes on building.
* **Automated Testing:** Running unit/integration tests (`Jest`) and orchestrating automated end-to-end testing (`Cypress`) in headless environments before a deployment triggers.
* **Deployment Safety:** Setting up automatic rollbacks using health check endpoints if a new deployment fails to respond.

### 4. Versioning & Release Automation
* **Semantic Versioning (SemVer):** Implementing automated tag generation (`v1.0.0`) based on commit messages.
* **Conditional Steps:** Restricting deployments only to the `main` branch and filtering out pull requests or specific commit flags (e.g., `[skip ci]`).

---

## 📋 Recommended Resources
* Official Course Material: [Full Stack Open - CI/CD](https://courses.mooc.fi/org/uh-cs/courses/full-stack-open-continuous-integration/)
* My Hands-On Solutions: [cicd-assignments](https://github.com/raghvendrashrinet/cicd-assignments)

---
🔑 *Maintained by Raghvendra Shrinet. Focused on writing reliable, automated, and production-ready code.*
