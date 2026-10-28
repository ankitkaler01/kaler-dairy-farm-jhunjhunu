# Kaler Dairy Farm — Ultimate Website Starter

A responsive customer storefront, product catalogue, cart/checkout, order IDs and tracking timeline, owner dashboard, employee portal, limited product assistant, reviews and optional Razorpay/WhatsApp integration points.

## Important truth before going live

This is a **starter project**, not a fully configured production service. It does not make third-party payment, email, WhatsApp, OTP, or carrier APIs work without your own provider accounts and credentials. Do not advertise international delivery as confirmed until a carrier has confirmed food/product eligibility, customs requirements, packaging and shipping cost. Sample prices, stock counts, photo URLs and product descriptions must be verified by the farm. The product photos are remote illustrative stock images, not verified photos of Kaler Dairy Farm's actual products. Do not publish fabricated customer reviews.

The current starter persists orders and products to a JSON file. This is suitable for local testing or a single-instance demo, **not a robust production database**. For a real public store, migrate to PostgreSQL/managed database, use persistent backups, HTTPS, production secrets, proper provider webhooks with raw-body signature validation, audit/security review and error monitoring before accepting payments.

## Run locally (Node.js 20+)

1. Extract this folder.
2. Install Node.js 20 or newer.
3. Open a terminal in this folder and run `npm install`.
4. Copy `.env.example` to `.env`.
5. Generate a password hash in the terminal (replace the example with your own unique password locally):

   ```bash
   node -e "require('bcryptjs').hash('CHOOSE-A-STRONG-UNIQUE-PASSWORD',12).then(console.log)"
   ```

6. Paste the generated hash into `.env` as `OWNER_PASSWORD_HASH=...`.
7. Set `JWT_SECRET` to a random secret of at least 32 characters. For example, generate a secret locally with `node -e "console.log(require('crypto').randomBytes(48).toString('hex'))"` and paste it into `.env`.
8. Run `npm start`.
9. Open `http://localhost:3000` for the store, `http://localhost:3000/admin.html` for owner dashboard and `http://localhost:3000/employee.html` for employee login.

**Never commit `.env`, real credentials, payment keys or customer data to GitHub.** The `.gitignore` excludes `.env` and `data/store.json`.

## Features in this starter

- Customer catalogue with search, category filter, discounts, product detail modal, multiple image slots and related products.
- Cart, address form, estimated delivery fees, generated order ID and tracking number.
- Tracking timeline, owner status updates and HTTPS courier tracking URL field.
- Owner login using bcrypt password hash and JWT, owner-only product/order/settings/employee routes.
- Employee accounts with bcrypt hashes and limited order-view route.
- Seasonal price rules stored per product (summer / monsoon / winter) and editable from owner dashboard.
- Owner-configurable delivery fee estimates and free-delivery threshold.
- Customer review submission and a limited product-information assistant; the assistant has no private order access.
- Optional Razorpay order creation and payment signature verification when merchant credentials are configured.
- Optional WhatsApp Cloud API notification to the store owner when credentials are configured.

## Not yet production-ready / needs real provider setup

- **Payments:** create your own Razorpay merchant account, configure live/test keys, domain, webhooks and provider settlement bank account. The provided UPI ID is not proof of payment. Orders stay pending until a trusted provider verifies payment. Test in test mode first.
- **Webhook:** production Razorpay webhooks require raw-body signature verification; this starter's webhook endpoint intentionally returns 501 instead of pretending it is verified. Configure this before production.
- **Email:** SMTP credentials and actual email delivery templates are not wired in this starter yet.
- **WhatsApp to customers:** customer notification templates and opt-in/compliant WhatsApp Business Cloud API messaging are not wired; only an optional owner notification is attempted.
- **OTP/MFA:** employee login here uses email/password only. A genuine email OTP or authenticator MFA provider must be integrated before production use.
- **Courier live tracking:** the dashboard accepts a carrier tracking link but does not call a carrier API or invent scan events. Contract/API access from your chosen carrier is required.
- **International orders:** address capture and delivery-fee estimate only; not an assurance that perishable dairy goods can be shipped internationally.
- **Photo uploads:** dashboard currently accepts HTTPS photo URLs, not direct uploads. Use object storage (e.g. S3-compatible storage) for production uploads.
- **Storage:** replace JSON file storage with a transactional database before public production use.
- **Rate accuracy:** prices auto-switch only when the owner enables season pricing and supplies values. The site does not claim to know live market rates.

## Hosting / GitHub

GitHub stores source code; it is not a production backend host by itself. Choose a Node.js host plus a managed database, configure environment variables in the host's secret settings, connect a domain, and enable HTTPS. Do not commit secrets. If you deploy this starter without those steps, online checkout and notifications will not be fully live.

## Security scope

Server-side owner routes check role permissions, passwords are stored as bcrypt hashes and API requests are rate-limited. No front-end can be made completely invisible to browser inspection. Security means secrets and private records stay server-side and are protected by authorization. This starter still needs a professional production security review, database isolation, webhook hardening, backup/restore testing, abuse monitoring and formal privacy/terms pages before handling real customer payments or sensitive data.
