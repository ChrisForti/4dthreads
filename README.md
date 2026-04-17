# 4dthreads — Print on Demand Merch Store

Custom apparel storefront built on React + TypeScript + Vite, deployed via Railway + GitHub.
Connects to a Printful backend proxy for live catalog, mockup generation, and order fulfillment.

## Tech Stack

- **React 19** — UI framework
- **TypeScript** — Type safety
- **Tailwind CSS v4** — Styling
- **Vite** — Build tool & dev server
- **React Router v7** — Client-side routing

## What's Built

| Feature                                                       | Status |
| ------------------------------------------------------------- | ------ |
| Landing page (hero, featured products, features, footer)      | ✅     |
| Product detail with size/color variant selection              | ✅     |
| Customization — boat name, logo upload, design template       | ✅     |
| Live CSS overlay preview (text + logo on product image)       | ✅     |
| Cart (add/remove/qty, localStorage persistence)               | ✅     |
| Checkout form with inline validation                          | ✅     |
| Order submission + success page                               | ✅     |
| Mock catalog + order services (swap to real API via env flag) | ✅     |
| GitHub Actions CI/CD → GitHub Pages                           | ✅     |

## Project Structure

```
src/
├── components/       # Header, Footer, Hero, FeaturedProducts, Features
├── context/          # CartContext (useReducer + localStorage)
├── data/             # mockProducts.ts
├── pages/            # LandingPage, ProductDetail, CartPage, CheckoutPage, OrderSuccessPage
├── services/         # catalogService (interface), mockCatalogService, apiCatalogService, orderService
├── types/            # models.ts — Product, Variant, CartItem, OrderDraft, ShippingAddress
├── config/           # env.ts — typed VITE_* wrappers
└── index.css         # Tailwind @theme tokens
```

## Getting Started

```bash
npm install
npm run dev
```

Set `VITE_USE_MOCK_CATALOG=true` to run on mock data without a backend.

## Environment Variables

Copy `.env.example` to `.env` when connecting to a real backend:

```bash
cp .env.example .env
```

| Variable                 | Purpose                                  |
| ------------------------ | ---------------------------------------- |
| `VITE_API_BASE_URL`      | Backend/proxy base URL                   |
| `VITE_APP_ENV`           | `development` / `staging` / `production` |
| `VITE_PRINTFUL_STORE_ID` | Printful store ID                        |
| `VITE_STRIPE_PUBLIC_KEY` | Stripe publishable key                   |

## Integration Points

Search for `// WIRE-UP:` comments across `src/` to find every backend connection point:

```bash
grep -r "WIRE-UP" src/
```

Key env flags:

- `VITE_USE_MOCK_CATALOG=false` — switches catalog to live Printful data via backend proxy
- `VITE_USE_MOCK_ORDER=false` — switches order submission to real API
- `VITE_API_BASE_URL` — Railway backend URL

## Deployment

Push to `main` — GitHub Actions typechecks, builds, and deploys to GitHub Pages automatically.

Enable Pages first: **Settings → Pages → Source → GitHub Actions**
