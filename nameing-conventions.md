# Naming Conventions

This file explains how to name files, folders, variables, and other parts of the code.  
Clear naming makes the code easier to read and maintain.

## Who Should Read This

- All developers writing or reviewing code
- Anyone creating new files, functions, or APIs

## Purpose

Using consistent names:

- Makes the project easier to navigate
- Helps new developers understand the code faster
- Avoids confusion and mistakes

## File and Folder Names

| Thing             | Format         | Example                   |
|------------------|----------------|---------------------------|
| Folders           | kebab-case     | `auth-routes/`, `user-model/` |
| JS/TS files       | kebab-case.js  | `db-client.js`, `email-service.js` |
| Components (React)| PascalCase.jsx | `LoginForm.jsx`           |
| Hooks             | useXxx.js      | `useAuth.js`              |
| Interfaces/Types  | PascalCase.ts  | `User.ts`, `AuthPayload.ts` |
| ENV variables     | SCREAMING_SNAKE_CASE | `JWT_SECRET`, `MONGO_URI` |

## Naming by Responsibility

Use names that describe what the file or function does.

**Examples:**

- ✅ `upload-file.js` (clear)  
- ❌ `utils.js` (too generic)

Avoid abbreviations unless they are well known.

- ✅ `authentication/`  
- ❌ `auth/`

## Function and Variable Names

- Use camelCase
- Name functions after what they do
- Do not use short or unclear names

**Examples:**

```js
function fetchUserData() {}
const isVerified = true;
```

## Who Maintains This File

The **Platform Team** maintains this file.  
Review happens every three months or after major refactors.
