# Git Standards

This file explains how to use Git in this project.  
It helps all developers work in the same way.

## Who Should Read This

- All developers using Git for this project

## Purpose

Using Git the same way:

- Makes commit history easy to read
- Helps other people understand your work
- Makes it easier to review and debug code

## Branching Rules

- Use one branch per task or bug
- Branch names must use kebab-case (all lowercase with hyphens)

**Examples:**

```
feature/add-login-form  
fix/user-role-bug  
chore/update-readme
```

## Commit Message Format

All commit messages must follow this style:

```
<type>(<scope>): <summary>
<problem statement>
<solution description>
<additional context>
Fixes #<issue-number>
```

**Types:**  
`feat`, `fix`, `chore`, `docs`, `refactor`, `test`, `ci`

**Example:**

```
fix(auth): incorrect role on new users
New users were always getting 'viewer' role.
Updated logic to assign role based on org ownership.
Also added test for org check.
Fixes #42
```

## Pull Request Rules

- One PR per task
- Keep PRs small and easy to review
- Link to related issue
- Add clear title and description
- Do not merge your own PR unless urgent

## Who Maintains This File

The **Platform Team** maintains this file.  
Review happens every three months or after any Git workflow changes.
