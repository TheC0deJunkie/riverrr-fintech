# Riverrr

A credit-builder fintech for South Africa: a wallet and card, a plan that reports contributions
so a member builds a credit history, and a set of community finance tools around it.

The premise is narrow. Plenty of people here have income and no credit record, which means no
record to lend against. A credit-builder plan turns a small monthly contribution into reported
repayment behaviour, and the wallet and card exist so the money has somewhere to sit while that
happens.

No longer actively maintained. The repo is kept as a reference build.

![screenshot](docs/screenshot.jpg)

## What's in it

**Marketing site** — the public pages, on the same Next.js app as the product.

**Authed product**
- Sign-in, open-account and card activation flows.
- Dashboard: cards, transactions, statements, send money, PayShap, airtime, and the
  credit-builder balance.
- Wallet with card top-up, and PDF statement export.

**App vault** — smaller finance tools inside the same shell, so a member does not leave the app
to reach them:
- **Better Stash / Stokvel** — group savings with locked returns and multi-person approval,
  modelled on how stokvels actually run rather than on a generic savings pot.
- **Better Cover / Funerals** — a funeral cover marketplace.
- **Better Merchants** — merchant payments: tap to pay, PayShap and QR.
- **Kasi4Hire, KasiShows** — local hire and events listings.

**Bureau integration** — `src/lib/bureau` wraps the credit bureau behind an interface with a
ClearScore implementation and a mock. The mock is the default in development, so nobody needs live
bureau credentials to work on the dashboard.

## Architecture

```
src/app/            Next.js App Router: /, /signin, /open-account, /activate,
                    /dashboard, /wallet, and /api for auth, credit, activation, paystack
src/components/     apps/ (the vault), dashboard/, auth/, bb/ (design primitives)
src/lib/            auth/, db/ (Drizzle), bureau/, paystack/
```

Auth is written by hand rather than delegated to a provider. For a product that touches money and
identity, I would rather own the session model and know exactly what is in the cookie.

## Stack

| | |
| --- | --- |
| Framework | Next.js 16, React 19, TypeScript |
| Styling | Tailwind CSS 4 |
| Database | Neon Postgres (serverless driver) + Drizzle ORM |
| Auth | Neon Auth, with hand-rolled session handling |
| Payments | Paystack |
| PDF | jsPDF for statements |

## Status

Archived. Nothing here is a live financial product, and none of it is regulated advice.

---

<sub>Source is private — this repo is the write-up. [Shaun Madondo](https://github.com/TheC0deJunkie) · Durban, KwaZulu-Natal.</sub>
