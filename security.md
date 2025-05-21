# Security Guide

## Who Should Read This
- All developers
- Anyone who discovers a security issue

## Purpose
- Protect users and data
- Provide a clear path to report problems
- Set simple rules that lower risk

## DO
- **ENV or DIE.** Put every secret in `.env`; include `.env.example`; exit if a required env var is missing.
- **Use secure channels.** Email security issues to `security@tmrw.it`.
- **Sanitize all inputs** from CLI, API, or config files.
- **Validate config files** before use.
- **Use local-only access in Alpha.** Add basic auth when the app is exposed; add JWT/OAuth in Beta or later.

## DO NOT
- Do not hard-code secrets—ever, even in development.
- Do not commit real `.env` files.
- Do not build complex auth flows unless needed.
- Do not ignore linter warnings related to security.

### Reporting a Security Issue
Send a private email with:
- A clear description of the issue
- Steps to reproduce it
- Any proof or screenshots

**Response time:** We answer within 72 hours.

## Who Maintains This File
The **Security Lead**. Reviewed every three months or after any security incident.
