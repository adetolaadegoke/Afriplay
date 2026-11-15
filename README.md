# Afriplay

Afriplay is an original, African-focused streaming platform foundation: a responsive web experience, cookie-secured API, PostgreSQL/Prisma data model, artist and administrator workflows, subscription records, Paystack checkout initialization, and an Expo mobile client that uses the same API.

## Architecture

`apps/web` is the Vite/React web client; `apps/api` is Fastify + Prisma; `apps/mobile` is Expo; `docs` contains API and deployment guidance. Audio and images are intentionally URL-based: production uploads belong in configured object storage, never this repository.

## Quick start

1. Copy `.env.example` to `.env` and provide a local PostgreSQL `DATABASE_URL` and a long `AUTH_SECRET`.
2. `npm install`
3. `npm run db:generate && npm run db:migrate`
4. `npm run prisma:seed -w @afriplay/api`
5. Run `npm run dev` and, in another terminal, `npm run dev:web`.

The API runs at port 4000 and the web app normally at port 5173. Seeded demo credentials are `artist@afriplay.demo` / `DemoPassword123!`; change or remove them in any shared environment.

## Security and payments

Passwords are Argon2 hashes. API access is role-checked server-side, cookies are httpOnly, request input is validated with Zod, and rate limits/security headers are enabled. Paystack payment state is created and verified server-side; frontend success signals never activate a subscription. Webhooks require an HMAC signature and independently verify the transaction with Paystack. See [API documentation](docs/API.md) and [deployment guidance](docs/DEPLOYMENT.md).

## What must be supplied before production

Create a PostgreSQL database, Supabase Storage bucket (or S3-compatible storage), a Paystack merchant account, and an Expo/Apple/Google developer account. For Supabase, use the project URL and the server-only service-role key for upload administration; do not expose that key to the web or mobile client. Put each credential only in the corresponding environment variable from `.env.example`; do not paste credentials into source code.
