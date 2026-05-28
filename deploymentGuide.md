Step-by-Step Guide to Deploy Your Next.js + Prisma + Neon App on Vercel

You already have:

Next.js
Prisma ORM
Neon

So deployment is straightforward.

1. Push Project to GitHub

GitHub is the easiest way to deploy on Vercel.

Initialize Git (if not already)

Inside project:

git init
Create .gitignore

Make sure .env is NOT uploaded.

Example:

node_modules
.next
.env


Commit Code
git add .
git commit -m "initial commit"
Create GitHub Repo

Go to:

Create GitHub Repository

Create repository.

Push Code

GitHub gives commands like:

git remote add origin YOUR_REPO_URL
git branch -M main
git push -u origin main


2. Prepare Prisma for Production
Ensure Prisma Client Exists

Run:
npx prisma generate


Add Build Script (Important)

Open package.json.

Add:

"postinstall": "prisma generate"

Example:

"scripts": {
  "dev": "next dev",
  "build": "next build",
  "start": "next start",
  "lint": "eslint",
  "postinstall": "prisma generate"
}

This ensures Vercel generates Prisma Client during build.

3. Ensure Neon DB Is Ready

Since you already migrated:

npx prisma migrate dev

your Neon DB already contains tables.

Good.

4. Deploy to Vercel

Go to:

Vercel Dashboard

5. Import GitHub Repository
Login with GitHub
Select your repo
Click Import

Vercel auto-detects Next.js.

6. Add Environment Variables

VERY IMPORTANT.

In Vercel project setup:

Open:

Environment Variables

Add:

Key	Value
DATABASE_URL	your Neon connection string

Example:

DATABASE_URL=postgresql://user:password@host/db?sslmode=require
7. Deploy

Click:

Deploy

Vercel will:

Install packages
Run prisma generate
Build Next.js app
Deploy globally
8. Common Prisma + Vercel Fix

Sometimes Vercel needs Prisma client generation during build.

If deployment fails with Prisma errors, add this to package.json:

"scripts": {
  "build": "prisma generate && next build"
}
Recommended Final Scripts
"scripts": {
  "dev": "next dev",
  "build": "prisma generate && next build",
  "start": "next start",
  "lint": "eslint",
  "postinstall": "prisma generate"
}
9. Production Prisma Setup

Your current Prisma singleton setup is correct:

import { PrismaClient } from "@prisma/client";

const globalForPrisma = globalThis as {
  prisma?: PrismaClient;
};

export const prisma =
  globalForPrisma.prisma ??
  new PrismaClient();

if (process.env.NODE_ENV !== "production") {
  globalForPrisma.prisma = prisma;
}

Keep it.

10. If Build Fails on Vercel

Most common fixes:

Missing Environment Variable

Error:

Environment variable not found: DATABASE_URL

Fix:

Add DATABASE_URL in Vercel dashboard.

Prisma Client Not Generated

Error:

PrismaClientInitializationError

Fix:

"build": "prisma generate && next build"
Edge Runtime Error

If using Prisma in Edge runtime:

Prisma is not supported in Edge Runtime

Fix:

Use Node.js runtime.

Add:

export const runtime = "nodejs";

in route/page if needed.

11. After Deployment

Vercel gives URL like:

https://your-app.vercel.app

Your app is live globally.

12. Updating App Later

Whenever you push to GitHub:

git add .
git commit -m "update"
git push

Vercel automatically redeploys.

Recommended Production Workflow
Local Development
↓
GitHub Push
↓
Vercel Auto Deploy
↓
Neon PostgreSQL
Optional Next Steps

After deployment, you can later add:

authentication
image uploads
server actions
caching
middleware
domains
analytics
CI/CD

to your app.