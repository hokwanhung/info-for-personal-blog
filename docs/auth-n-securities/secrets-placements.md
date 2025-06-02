You're absolutely right to be concerned about this! When you put sensitive configuration like Firebase keys in `.env` files and exclude them from Git (which you should), GitHub Actions won't have access to those files during the build process. However, there's a proper solution for this.

## The Problem
You're right - if you put Firebase config in `.env` files and exclude them from Git, GitHub Actions won't have access to them during the build process.

## The Solution: GitHub Secrets + Environment Variables

Here's how to properly handle this:

### 1. First, add `.env` files to your `.gitignore`

Your `.gitignore` doesn't currently exclude `.env` files. You should add:

```gitignore
# Environment variables
.env
.env.local
.env.production
.env.*.local
```

### 2. Create a `.env` file locally with your Firebase config

Create a `.env` file in your project root:

```env
VITE_FIREBASE_API_KEY=your-actual-api-key
VITE_FIREBASE_AUTH_DOMAIN=personal-blog-18d7c.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=personal-blog-18d7c
VITE_FIREBASE_STORAGE_BUCKET=personal-blog-18d7c.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=your-actual-sender-id
VITE_FIREBASE_APP_ID=your-actual-app-id
```

**Note**: The `VITE_` prefix is important for Vite to expose these variables to your client-side code.

### 3. Update your Firebase config to use environment variables

Update `src/firebase/config.ts`:

```typescript:src/firebase/config.ts
import { initializeApp } from 'firebase/app'
import { getAuth } from 'firebase/auth'
import { getFirestore } from 'firebase/firestore'

const firebaseConfig = {
  apiKey: import.meta.env.VITE_FIREBASE_API_KEY,
  authDomain: import.meta.env.VITE_FIREBASE_AUTH_DOMAIN,
  projectId: import.meta.env.VITE_FIREBASE_PROJECT_ID,
  storageBucket: import.meta.env.VITE_FIREBASE_STORAGE_BUCKET,
  messagingSenderId: import.meta.env.VITE_FIREBASE_MESSAGING_SENDER_ID,
  appId: import.meta.env.VITE_FIREBASE_APP_ID,
}

// Initialize Firebase
const app = initializeApp(firebaseConfig)

// Initialize Firebase Authentication and get a reference to the service
export const auth = getAuth(app)

// Initialize Cloud Firestore and get a reference to the service
export const db = getFirestore(app)

export default app
```

### 4. Add GitHub Secrets

In your GitHub repository:
1. Go to **Settings** → **Secrets and variables** → **Actions**
2. Add these secrets:
   - `VITE_FIREBASE_API_KEY`
   - `VITE_FIREBASE_AUTH_DOMAIN`
   - `VITE_FIREBASE_PROJECT_ID`
   - `VITE_FIREBASE_STORAGE_BUCKET`
   - `VITE_FIREBASE_MESSAGING_SENDER_ID`
   - `VITE_FIREBASE_APP_ID`

### 5. Update your GitHub Actions workflow

Update `.github/workflows/firebase-hosting-merge.yml`:

```yaml
name: Deploy to Firebase Hosting on merge
on:
  push:
    branches:
      - main
jobs:
  build_and_deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm ci && npm run build
        env:
          VITE_FIREBASE_API_KEY: ${{ secrets.VITE_FIREBASE_API_KEY }}
          VITE_FIREBASE_AUTH_DOMAIN: ${{ secrets.VITE_FIREBASE_AUTH_DOMAIN }}
          VITE_FIREBASE_PROJECT_ID: ${{ secrets.VITE_FIREBASE_PROJECT_ID }}
          VITE_FIREBASE_STORAGE_BUCKET: ${{ secrets.VITE_FIREBASE_STORAGE_BUCKET }}
          VITE_FIREBASE_MESSAGING_SENDER_ID: ${{ secrets.VITE_FIREBASE_MESSAGING_SENDER_ID }}
          VITE_FIREBASE_APP_ID: ${{ secrets.VITE_FIREBASE_APP_ID }}
      - uses: FirebaseExtended/action-hosting-deploy@v0
        with:
          repoToken: ${{ secrets.GITHUB_TOKEN }}
          firebaseServiceAccount: ${{ secrets.FIREBASE_SERVICE_ACCOUNT_PERSONAL_BLOG_18D7C }}
          channelId: live
          projectId: personal-blog-18d7c
```

### 6. Update your TypeScript environment types

Update `env.d.ts` to include type definitions for your environment variables:

```typescript:env.d.ts
/// <reference types="vite/client" />

interface ImportMetaEnv {
  readonly VITE_FIREBASE_API_KEY: string
  readonly VITE_FIREBASE_AUTH_DOMAIN: string
  readonly VITE_FIREBASE_PROJECT_ID: string
  readonly VITE_FIREBASE_STORAGE_BUCKET: string
  readonly VITE_FIREBASE_MESSAGING_SENDER_ID: string
  readonly VITE_FIREBASE_APP_ID: string
}

interface ImportMeta {
  readonly env: ImportMetaEnv
}
```

## Security Note

For Firebase client-side configuration, these values are **not actually secret** - they're exposed in your built JavaScript anyway. However, using environment variables is still a good practice for:

1. **Different environments** (dev, staging, prod)
2. **Consistency** with truly secret values (like service account keys)
3. **Easy configuration management**

The real security comes from Firebase Security Rules, not hiding these config values.

This approach ensures that:
- Your sensitive config isn't committed to Git
- GitHub Actions can access the values during build
- You can easily manage different environments
- Your build process works consistently across local and CI/CD environments
