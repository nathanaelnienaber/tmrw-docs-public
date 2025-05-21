# Contributing Guide

---

## Who Should Read This
- All new contributors
- Anyone making a pull request
- All engineers, architects, and reviewers
- Anyone shaping project strategy or standards

---

## Purpose
- Show how to set up the project and contribute code
- Explain why we follow certain engineering rules
- Keep every change traceable and the project survivable in hostile or uncertain environments

---

## DO

| Area | Rule | Why |
|------|------|-----|
| **Start With Docs** | **Write a README before code.** Describe the new module first. | People understand intent before reading code. |
| **Branching** | **One branch per task.** | Keeps work isolated and easy to review. |
| **Commit Messages** | **Follow the commit format** below. | History stays clear and searchable. |
| **Small Changes** | **Push small, tested commits.** | Reviews are faster; rollback is safer. |
| **Test the Story** | **Write tests that prove user outcomes, not internals.** | Users care about results, not helpers. |
| **Interface First** | **Define an interface before code.** | Lets us swap infrastructure fast and keep sovereignty. |
| **Wrap Dependencies** | **Use client wrappers (`aws-client.js`, `db-client.go`).** | Any vendor can be replaced overnight. |
| **Abandonable Features** | **Design so features can be deleted tomorrow.** | We build to survive, not just to scale. |
| **Clear Trail** | **Leave meaningful commit messages and docs.** | Future developers must understand the history. |

---

## DO NOT

| Rule | Why |
|------|-----|
| Do not commit directly to `main`. | Protects production code. |
| Do not mix multiple concerns in one PR. | Makes reviews hard. |
| Do not leave vague or empty commit messages. | Breaks traceability. |
| Do not skip the interface step. | Locks you to one implementation. |
| Do not call AWS, Mongo, or Stripe directly from business logic. | Removes swap-ability. |
| Do not write tests only for private helpers. | Misses real user outcomes. |
| Do not create deeply coupled pipelines or shared global state. | Makes code hard to delete or replace. |

---

## Commit Message Format
```

<type>(<scope>): <summary> <problem statement> <solution description> <additional context>
Fixes #<issue-number>

````

---

## Local Setup
```bash
git clone https://github.com/your-org/your-project.git
cd your-project
npm install
cp .env.example .env   # add secrets
npm run dev
````

---

## Who Maintains This File

* The **Platform Team** reviews workflow sections on change.
* The **Security Lead** reviews philosophy sections every six months.
