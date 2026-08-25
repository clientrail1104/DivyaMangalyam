# DivyaMangalyam — Stripe Checkout

This version replaces the demo payment button with Stripe-hosted Checkout.

## 1. Install

```bash
npm install
```

## 2. Configure Stripe

Create a Stripe account for your Malaysian business and use test mode first.

Copy `.env.example` to `.env` and set:

- `STRIPE_SECRET_KEY`
- `STRIPE_WEBHOOK_SECRET`
- `PUBLIC_BASE_URL`

Never expose `STRIPE_SECRET_KEY` in the browser.

## 3. Start

```bash
npm start
```

Open:

http://localhost:4242

## 4. Local webhook testing

Install the Stripe CLI, authenticate it, then run:

```bash
stripe listen --forward-to localhost:4242/api/stripe/webhook
```

Copy the displayed `whsec_...` value into `STRIPE_WEBHOOK_SECRET`.

## 5. Production requirements

Before granting a member premium access, persist the authenticated member ID and Stripe identifiers in your database and activate the 12-month entitlement only after a verified Stripe webhook confirms payment.

The browser `success_url` is not a trusted payment confirmation.

## Package mapping

- Package 1: RM 3,000 → 10 contacts
- Package 2: RM 5,000 → 25 contacts
- Package 3: RM 8,000 → 50 contacts
- Package 4: RM 10,000 → 80 contacts

The checkout creates one-time Stripe Checkout payments in MYR. The website then treats the purchased package as a 12-month entitlement; actual entitlement state should be stored in your backend database.
