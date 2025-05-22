You've identified an important distinction between types and scopes. Let me explain the difference and optimize your scope list to avoid duplication:

```javascript
export default {
  extends: ['@commitlint/config-conventional'],
  rules: {
    'type-enum': [
      2,
      'always',
      [
        'feat', // A new feature
        'fix', // A bug fix
        'docs', // Documentation only changes
        'style', // Changes that do not affect the meaning of the code (white-space, formatting, etc)
        'refactor', // A code change that neither fixes a bug nor adds a feature
        'perf', // A code change that improves performance
        'test', // Adding missing tests or correcting existing tests
        'chore', // Changes to the build process or auxiliary tools and libraries
        'ci', // Changes to CI configuration files and scripts
        'revert', // Reverts a previous commit
        'build', // Changes that affect the build system or external dependencies
      ],
    ],
    'type-case': [2, 'always', 'lower-case'],
    'subject-case': [2, 'always', 'lower-case'],
    'subject-min-length': [2, 'always', 10], // Minimum subject length of 10 characters
    'subject-max-length': [2, 'always', 72],
    'body-max-line-length': [2, 'always', 72],
    'header-max-length': [2, 'always', 72],
    'body-leading-blank': [2, 'always'],
    'footer-leading-blank': [2, 'always'],

    // Scope rules - focused on architecture components
    'scope-case': [2, 'always', 'lower-case'],
    'scope-empty': [0, 'never'], // Don't require scopes, but allow them
    'scope-enum': [
      2,
      'always',
      [
        // ...self-defined
      ],
    ],
  },
}

```

## Types vs. Scopes: Key Differences

**Types** (what kind of change):
- Represent the *nature* of the change (feat, fix, docs, etc.)
- Answer "What kind of change is this?"
- Are standardized across projects
- Example: `feat`, `fix`, `docs`

**Scopes** (where the change occurs):
- Represent the *area/component* being changed
- Answer "Where in the codebase is this change happening?"
- Are project-specific and reflect your architecture
- Example: `auth`, `dashboard`, `api-client`

Some of the scopes I provided earlier overlap with types (like `docs`, `style`, `refactor`, `perf`), which is redundant and confusing. Let's create a more focused, architecture-based scope list:


I've completely redesigned your scope list to avoid duplication with types and align with your Vue/Quasar project's architecture. Here's how the improved scopes work:

## Improved Scope Design

### 1. Architecture-Based (Not Action-Based)
- **Before**: Scopes like `refactor`, `style`, and `perf` duplicated the types
- **After**: Scopes now describe *where* in your app the change occurs

### 2. Project-Specific Alignment
- The scopes are tailored to your personal blog project structure
- Added specific page-related scopes (`home`, `blog`, `contact`, `resources`, `sooonai`)
- Added Vue-specific architecture concepts (`router`, `store`)

### 3. Structured by Categories
- **Core application areas**: Fundamental systems (auth, router, store, api)
- **UI components and features**: Page-specific and shared UI
- **Infrastructure**: Technical foundations (config, deps, db, i18n)
- **Other**: Catch-all for project-wide changes

## Example Commit Messages

Using this new configuration, here are examples of meaningful commit messages:

```
feat(blog): implement comment system with pagination
fix(auth): resolve token refresh issue during session expiry
docs(api): update endpoint documentation with new parameters
refactor(store): improve state management organization
perf(resources): optimize resource loading for faster page rendering
style(layout): ensure consistent spacing in header component
test(auth): add comprehensive unit tests for login flow
chore(deps): update frontend dependencies to latest versions
ci(project): configure automatic deployment to staging
```

Each commit now clearly communicates:
1. **What** kind of change (type)
2. **Where** in the codebase (scope)
3. **Which** specific improvement (subject)

This approach creates a more useful and navigation-friendly commit history while avoiding redundancy between types and scopes.
