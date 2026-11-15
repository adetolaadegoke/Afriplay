# Deployment

Provision PostgreSQL, an S3-compatible storage bucket, and a Paystack account. Copy `.env.example` to `.env` locally and set production secrets in the host dashboard—never in Git.

1. Install Node 20+ and run `npm install`, then `npm run db:generate` and `npm run db:migrate`.
2. Deploy `apps/api` as a long-running Node service. Set `WEB_ORIGIN`, `AUTH_SECRET`, `DATABASE_URL`, Paystack keys, and storage values.
3. Deploy `apps/web` as a static Vite build with `VITE_API_URL` pointing to the HTTPS API.
4. Configure Paystack's webhook URL as `https://api.example.com/webhooks/paystack`. Before enabling live payments, implement signature validation and use the provider's dashboard to rotate leaked keys.
5. For mobile, set `EXPO_PUBLIC_API_URL`, add real icon/splash assets, and run `npx expo prebuild`; use EAS Build for signed Android AAB and iOS archives. `com.afriplay.app` is a placeholder identifier—replace it with an identifier you own before release.

Use database backups, least-privilege storage credentials, HTTPS, and a migration run as part of each release.
