# Dubai Taste — Premium Restaurant Website

A mobile-friendly React + Vite restaurant website starter with a Supabase backend.

## Included
- Luxury black-and-gold customer website
- Responsive menu and category filters
- Cart and order submission
- Table reservation requests
- WhatsApp fallback while Supabase is not connected
- Supabase Auth admin sign-in
- Admin view for orders and reservations
- Supabase SQL schema with row-level security

## 1. Run locally
Install Node.js, then in this folder run:

```bash
npm install
cp .env.example .env
npm run dev
```

Open the local URL printed by Vite.

## 2. Connect Supabase
1. Create a Supabase project.
2. Open SQL Editor and run `supabase/schema.sql`.
3. Copy the Project URL and publishable key (or legacy anon key) from Project Settings > API.
4. Copy `.env.example` to `.env` and fill in `VITE_SUPABASE_URL`, `VITE_SUPABASE_ANON_KEY`, and `VITE_WHATSAPP_NUMBER`.
5. Restart the development server after editing `.env`.

Never put the Supabase `service_role` key or secret key in this frontend project.

## 3. Make an admin account
1. In Supabase Authentication, create a user with email and password.
2. In the Supabase SQL Editor, replace the UUID below with that user's ID and run:

```sql
update auth.users
set raw_app_meta_data = coalesce(raw_app_meta_data, '{}'::jsonb) || '{"role":"admin"}'::jsonb
where id = 'PASTE-ADMIN-USER-UUID-HERE';
```

3. Sign out and sign back in so the refreshed JWT includes the admin role.
4. Open the website and use the small Admin link in the footer.

## 4. Deploy
Push the repository to GitHub and import it into Netlify.
- Build command: `npm run build`
- Publish directory: `dist`
- Add the same `VITE_SUPABASE_URL`, `VITE_SUPABASE_ANON_KEY`, and `VITE_WHATSAPP_NUMBER` values in Netlify environment variables.

## Important before real launch
This is a working starter/MVP, not a payment-certified production ordering system. It does not process card payments, calculate delivery fees, prevent duplicate/abusive public submissions, or provide full menu editing in the admin UI yet. Add server-side validation/rate limiting, order notification workflow, payment-provider integration, backups, and test all RLS policies before taking real customer orders. Replace the sample restaurant address, phone, email, opening hours, imagery and menu with the actual business details. Check image licences/availability before commercial use.
