### Airbnb JavaScript Style Guide
https://airbnb.io/projects/javascript/

### 1. **File Naming Conventions**

- **Use `camelCase` for JavaScript files**: For component files in React or other JavaScript modules, use `camelCase`. For example:
    - `myComponent.js`
    - `userProfile.js`
- **Use `PascalCase` for React components**: When the file contains a React component, use `PascalCase` for the filename to distinguish it. For example:
    - `UserProfile.js`
    - `HeaderNav.js`
- **Avoid special characters and spaces**: Use only letters, numbers, hyphens, or underscores as needed (e.g., `HeaderNav.js` instead of `header nav.js`).
- **Use Descriptive, Single-Purpose Names**: Make file names descriptive of their contents or function. Avoid abbreviations that might not be widely recognized.

### 2. **Folder Naming Conventions**

- **Use `kebab-case` for folder names**: This format (e.g., `user-profile`) is lowercase with hyphens, improving readability and consistency, especially in URLs.
    - Examples:
        - `user-profile`
        - `components`
        - `utils`
- **Group by Feature, Not File Type**: Organize by feature or module rather than by file type. For instance:
    
    ```
    ├── user-profile
    │   ├── UserProfile.js
    │   ├── userProfile.test.js
    │   └── styles.css
    ├── auth
    │   ├── AuthForm.js
    │   ├── authUtils.js
    │   └── authStyles.css
    
    ```
    

### 3. **Component Folder Structure**

For complex components, keep all related files within a single folder:

```
└── user-profile
    ├── UserProfile.js         # Component file
    ├── UserProfile.styles.js  # Styled components (if using CSS-in-JS)
    ├── UserProfile.test.js    # Unit tests
    └── index.js               # Barrel file to simplify imports

```

### 4. **Numbers, Dates, and Versions in File Names**

- **Use Numbers Meaningfully**: Only use numbers if they’re meaningful to the file’s purpose. For example:
    - `module_part2.js` (second part of a module)
    - `report_v1.js` (version 1 of a report file)
- **Use ISO Date Format (YYYY-MM-DD)**: This format is universally accepted, easy to parse, and sorts well. For example:
    - `2024-10-30_meeting-notes.md` (created on October 30, 2024)
    - `sales-report_2024-10-30.js`
- **Use Semantic Versioning for Files with Versions**: For example, `v2.1.0` indicates the second major version, the first minor update, and no patches.
    - **Examples**:
        - `project_overview_v1.0.0.md`
        - `api_spec_v2.3.1.json`
    - Place version numbers consistently at the end for easy sorting and clarity.
- **Order by Importance**: Begin with a meaningful name, followed by dates or versions.
- **Hyphens or Underscores for Readability**: Use hyphens (``) or underscores (`_`) to separate numbers, dates, or versions, e.g., `project_v2_2024-10-30.js`.
- **Avoid Spaces**: Spaces can cause issues on some systems or in command-line applications.

### 5. **Barrel Files (`index.js`)**

- Use `index.js` files as “barrel files” to re-export modules within a folder. This allows cleaner importing. For instance:
    
    ```jsx
    // src/components/user-profile/index.js
    export { default } from './UserProfile';
    
    ```
    
- Importing this way is more concise:
    
    ```jsx
    import UserProfile from 'components/user-profile';
    
    ```
    

### 6. **Additional Tips**

- **Avoid Deep Nesting**: Keep nesting to three levels or fewer to reduce complexity.
- **Separate Logic and View Files**: Separate utility functions into their own folders to keep components clean.

Following these practices helps maintain a clean, intuitive, and scalable project structure.
