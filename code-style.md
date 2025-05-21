# Code Style Guide

## Who Should Read This
- All developers writing or reviewing code

## Purpose
- Make code easy to read and review
- Reduce errors and confusion
- Keep the project consistent across all languages

---

## DO

| Area | Rule | Why |
|------|------|-----|
| **Formatting** | Use **Prettier** on save. | Keeps style the same for every file. |
| **Linting** | Use **Airbnb ESLint rules** (and `golangci-lint` for Go). | Catches mistakes early. |
| **Clarity** | Write one function per file when possible. | Each file has one clear job. |
| **Comments** | Explain **why** the code exists, not **what** the code does. | Readers understand intent. |
| **Indentation** | Use 2 spaces, never tabs. | Consistent spacing. |
| **Variables** | Use `const` or `let`; prefer `const`. | Avoids accidental mutation. |
| **Functions** | Use arrow functions when possible. | Keeps syntax short and clear. |
| **General Practices** | One file = one responsibility.<br>One function = one clear job.<br>Avoid cleverness—clarity wins.<br>Use ENV over hard-coded values.<br>Make logs traceable by default. | Improves maintainability and security. |

### Language-Specific DO Rules

| Language / Layer | DO Rules |
|------------------|----------|
| **Rust** | Follow `rustfmt` defaults.<br>Use clear module names.<br>Avoid unsafe code unless required. |
| **JavaScript** | Follow ESLint rules strictly.<br>Avoid global variables.<br>Prefer `async/await` over promise chains. |
| **React** | Use functional components.<br>Keep components small.<br>Name files with `PascalCase.jsx`. |
| **Go** | Run `gofmt` and `golangci-lint`.<br>Exported functions use `CamelCase`.<br>Files use `snake_case.go`.<br>One struct per file.<br>Keep packages small. |
| **TypeScript** | Format with Prettier.<br>Lint with Airbnb config.<br>Use `kebab-case` for files and folders.<br>Prefer named exports.<br>Use interfaces for API surfaces. |

---

## DO NOT

| Rule | Why |
|------|-----|
| Do not write clever or cryptic code. | Readability is more important than brevity. |
| Do not use `var`. | `let` and `const` are safer. |
| Do not leave unused or dead code. | Remove it instead of commenting it out. |
| Do not mix multiple responsibilities in one file. | Single-responsibility files are easier to test. |
| Do not hard-code secrets or config values. | Use environment variables. |
| Do not ignore linter or formatter errors. | Fix issues before committing. |

---

## Who Maintains This File
The **Platform Team** maintains this file.  
Review happens every three months or after major updates.
