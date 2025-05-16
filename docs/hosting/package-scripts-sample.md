I notice you have three different type-checking scripts in your `package.json`:

```json
{
  "scripts": {
    "type-check": "vue-tsc --build",        // Used in build script
    "typecheck": "vue-tsc --noEmit",        // Used in PR checks
    "build": "run-p type-check \"build-only {@}\" --"  // Uses type-check
  }
}
```

And in your PR checks:
```yaml
test_and_types:
    # ...
    steps:
      # ...
      - name: Type check
        run: npm run typecheck  # Using the --noEmit version
```

Let's optimize this:

1. **Understanding the Differences**:
   - `vue-tsc --build`: Creates type declaration files (`.d.ts`) and checks types
   - `vue-tsc --noEmit`: Only checks types without generating files
   - Your build uses parallel execution with `run-p`

2. **Recommended Optimization**:

```json:package.json
{
  "scripts": {
    // Remove duplicate scripts
    "type-check": "vue-tsc --noEmit",  // Single type-checking script
    "type-check:build": "vue-tsc --build",  // Only for declaration file generation
    "build": "run-p type-check:build \"build-only {@}\" --",  // Use build version
    // ... other scripts ...
    // Remove "typecheck" as it's redundant
  }
}
```

```yaml:.github/workflows/pr-checks.yml
test_and_types:
    name: "Test & Type Check"
    runs-on: ubuntu-latest
    steps:
      # ... other steps ...
      
      # TypeScript validation
      - name: Type check
        run: npm run type-check  # Use the same script name consistently
```

3. **Why This is Better**:

- **Clarity**: 
  - `type-check` for general type checking (CI, development)
  - `type-check:build` specifically for build process
- **Efficiency**: 
  - PR checks only need type checking (`--noEmit`)
  - Build process gets declaration files when needed
- **Consistency**: 
  - Single naming convention (`type-check` instead of mixing with `typecheck`)
  - Clear purpose for each command

4. **Final Package.json Scripts Section**:
```json
{
  "scripts": {
    "dev": "vite",
    "build": "run-p type-check:build \"build-only {@}\" --",
    "preview": "vite preview",
    "test:unit": "vitest",
    "test:e2e": "playwright test",
    "build-only": "vite build",
    "type-check": "vue-tsc --noEmit",
    "type-check:build": "vue-tsc --build",
    "lint": "eslint . --ext .vue,.js,.jsx,.cjs,.mjs,.ts,.tsx,.cts,.mts --fix --ignore-path .gitignore",
    "format": "prettier --write \"**/*.{js,ts,vue,json,css,scss,md}\"",
    "format:check": "prettier --check \"**/*.{js,ts,vue,json,css,scss,md}\"",
    "test:ci": "vitest run"
  }
}
```

This optimization:
1. Removes redundant script (`typecheck`)
2. Uses consistent naming (`type-check` based)
3. Separates build and check concerns
4. Maintains your efficient parallel build process
5. Makes the purpose of each type-checking script clear

The PR checks will run faster because they don't generate declaration files, while the build process still gets the files it needs for production.
