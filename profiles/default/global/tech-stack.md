# Tech Stack

## Frontend
- Next.js 15 (App Router) with TypeScript
- React 19
- Tailwind CSS v4
- shadcn/ui (Radix UI primitives)
- React Hook Form + Zod (forms)
- TanStack Query v5 (polling / reactive cache only)

## Backend
- Next.js Route Handlers + Server Actions
- Prisma ORM v6 (PostgreSQL)
- Stack Auth (`@stackframe/stack`) for authentication

## Payments
- Pagar.me v5 API (PIX + split payments)

## Infrastructure
- AWS S3 (photo storage)
- AWS Rekognition (face detection / moderation)
- Vercel KV (rate limiting / cache)
- Resend (email)

## Key conventions
- Server Actions for all mutations (`"use server"`)
- Server Components for data fetching (async/await)
- `pnpm` as package manager
- `dayjs` for all date manipulation
- `Prisma.Decimal` for all monetary values
