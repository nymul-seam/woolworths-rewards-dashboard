# Everyday Rewards — Loyalty Dashboard

An interactive analytics dashboard for the **Woolworths Everyday Rewards** loyalty programme, covering 10,000 customers and 105,508 transactions across 11 Sydney stores (2024–2025).

**Live dashboard:** `https://<your-username>.github.io/<repo-name>/`  *(replace after enabling Pages — see below)*

> Add a screenshot here: save it as `docs/screenshot.png` and uncomment the next line.
> <!-- ![Dashboard preview](docs/screenshot.png) -->

## What it shows

| Area | Detail |
|---|---|
| KPI cards | Customers, transactions, points earned, points redeemed, transaction amount |
| Trends | Monthly registrations (2023); earned vs redeemed points on dual axes (2024–2025) |
| Stores | Treemap of points earned; earned-vs-redeemed scatter with network redemption-rate line |
| Redemptions | Breakdown by type (Shopping, Fuel, Qantas, Donation) |
| Customers | Membership status mix; all-time top 10 redeemers |
| Insights | Four auto-generated takeaways that recalculate with every filter |

**Interactions:** Year filter, Store filter, click any store tile or scatter dot to cross-filter, Reset button, hover/keyboard tooltips on every mark.

## Headline findings

- Members redeem only **2.5%** of the points they earn (772,394 of 31.1M).
- **Shopping Discount** is ~70% of redemptions, Fuel ~20%; Qantas (~6%) and Donations (~4%) are marginal.
- Earning is evenly spread across stores, but redemption varies: Blacktown highest (73,541 pts), Hornsby lowest (65,121 pts).
- Monthly sign-ups jump from ~167 (Jan–Jun 2023) to ~1,800 (Jul–Nov 2023), roughly 11×.
- 89.9% of members are Active; 1,007 are Suspended or Inactive.

## Deploy to GitHub Pages

1. Create a new public repo and upload everything in this folder (keep the folder structure).
2. Go to **Settings → Pages → Build and deployment → Source** and choose **GitHub Actions**.
3. Push to `main` — the workflow in `.github/workflows/pages.yml` publishes the site. Your link appears in the **Actions** run and under Settings → Pages.

*Simpler alternative:* Settings → Pages → Deploy from a branch → `main` / `(root)`. The `.nojekyll` file is already included.

## Run locally

Open `index.html` in a browser. No build step, server or internet connection is needed.

## Refresh the data

```bash
pip install pandas openpyxl
python scripts/build_data.py path/to/Woolworths_Reward_Dashboard_-_Dataset.xlsx
```

This regenerates `data/dashboard-data.js` and `.json` as small aggregates (about 1,100 rows) — raw customer records are never published. `.gitignore` excludes `.xlsx` and `.pbix` files so the source workbook is not committed by accident.

## Project structure

```
index.html              page markup, metadata
css/style.css           design tokens and layout
js/dashboard.js         filters, aggregation, SVG charts (no libraries)
data/                   aggregated data (.js for the page, .json for reuse)
assets/img/             logos and background
scripts/build_data.py   workbook -> aggregates
docs/DESIGN.md          high-level design
.github/workflows/      GitHub Pages deployment
```

See [docs/DESIGN.md](docs/DESIGN.md) for architecture, data model and design decisions.

## Notes and limitations

- Registrations (Jan–Nov 2023) and transactions (2024–2025) do not overlap, so registrations and membership status ignore the Year and Store filters.
- The Top 10 Redeemers roster is fixed to the all-time top 10; it responds to Year but not Store.
- Dataset appears synthetic. If you adapt this to real customer data, replace customer names with IDs.
- Woolworths and Everyday Rewards names and logos belong to their owners; this is an independent portfolio project, not an official Woolworths product.

## Author

Built by **Nymul Islam**, Operations Data Analyst, The Data & AI Institute.

Licensed under the MIT License (code only; brand assets excluded).
