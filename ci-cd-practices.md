# CI/CD Practices

## Who Should Read This
- All developers who push code to the repository
- Anyone writing tests, workflows, or deployment scripts

## Purpose
- Help you write code that passes automated checks
- Reduce errors in production
- Make deployments faster and safer

---

## Pipeline Overview
1. **Build** – Code is checked and bundled.  
2. **Test** – Automated tests run.  
3. **Lint** – Code style and errors are checked.  
4. **Deploy** – Code goes to staging or production.

---

## DO

| Area | Rule | Why |
|------|------|-----|
| **Small Changes** | Push small, tested commits. | Easier reviews and quick rollbacks. |
| **Testing** | Write or update tests for new code. | Keeps quality high. |
| **CI Checks** | Ensure your branch passes all CI steps before opening a pull request. | Prevents broken builds on `main`. |
| **Secrets** | Use environment variables for secrets and config. | Protects sensitive data. |
| **Workflow Files** | Keep GitHub Actions and other pipeline configs version-controlled. | Changes are tracked and reviewed. |

### Common Tools

| Tool | Purpose |
|------|---------|
| GitHub Actions | Run workflows on push and PR |
| Docker | Build and run containers |
| Vercel / Fly.io | Deploy frontend and backend |
| Biome / ESLint | Lint code before deployment |

---

## DO NOT

| Rule | Why |
|------|-----|
| Do not push directly to `main`. | Protects production code. |
| Do not merge if CI fails. | Prevents broken builds. |
| Do not hard-code secrets in workflow files. | Keeps credentials safe. |
| Do not disable failing tests instead of fixing them. | Hides real problems. |
| Do not ignore linter or security warnings. | Small issues become big issues later. |

---

## Who Maintains This File
The **DevOps Team** (or **Platform Team**) maintains this file.  
Review happens every three months or after any pipeline change.