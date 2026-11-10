# Kasua MVP

A responsive first-release foundation for Kasua: a public marketplace plus a seller workspace for products, inventory, branches, sales and expenses.

## Included

- Public marketplace with category filtering, product search and an interactive cart preview
- Seller workspace with overview, products/stock, sales, expenses and branch views
- Demo workspace (sample data; changes are temporary)
- Supabase Auth integration (email/password)
- Supabase/Postgres schema with row-level security
- Atomic `record_sale` database function that validates stock and records the sale while decrementing inventory
- Seller-owned business and branch data

## Important scope notes

This is a working MVP foundation, not a deployed production service. Online payments, checkout, delivery integrations, reviews, staff roles, inventory transfers, custom domains, image upload storage, and full accounting are intentionally not included yet. The cart is an interaction preview and does not take payment. Demo data is not persisted. A storefront preview is available in the seller workspace; production public routes require deployment/routing configuration.

## 1. Create the database

1. Create a Supabase project at https://supabase.com.
2. Open **SQL Editor** in the Supabase dashboard.
3. Run the complete contents of `supabase/schema.sql`.
4. In **Project Settings → API**, copy the Project URL and anon/public key.

## 2. Connect the app

Edit `config.js`:

```js
window.KASUA_CONFIG = {
  SUPABASE_URL: 'https://YOUR-PROJECT.supabase.co',
  SUPABASE_ANON_KEY: 'YOUR_SUPABASE_ANON_PUBLIC_KEY'
};
```

Only use the anon/public key in this browser app. Never expose the `service_role` key.

## 3. Run locally

You can use any static web server. For example:

```bash
npx serve .
```

Then open the local URL shown in the terminal. You can also open `index.html` directly to explore the demo, but Supabase Auth and database features should be tested through a local web server.

## 4. First test flow

1. Choose **For business** → **Create your business**.
2. Create an account with email/password.
3. Create a business and its first branch.
4. Add a product and opening stock.
5. Record a sale; the database function updates stock atomically.
6. Add an expense and inspect the overview.
7. Add another branch and switch between branches.
8. Open **Discover** to view active marketplace products.

## Security and production checklist

- Confirm RLS policies in Supabase before inviting real sellers.
- Add email verification and password reset flows.
- Add server-side validation and rate limits for public endpoints.
- Add private image storage with safe upload policies.
- Add audit logs for stock changes and financial records.
- Implement staff roles and branch-scoped permissions before multi-user teams.
- Add tests, backups, monitoring, privacy terms and Nigerian data-protection review before launch.
- Consider whether public product prices/stock should be visible for every seller and provide seller controls.

## Stack

- HTML, CSS and vanilla JavaScript for a lightweight responsive MVP
- Supabase Auth and PostgreSQL for accounts and persistence
- Supabase Row Level Security for tenant isolation
