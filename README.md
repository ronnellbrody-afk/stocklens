# StockLens — GitHub Pages MVP

A responsive, dependency-free stock research dashboard. **All company names and metrics are fictional demonstration data.** No live feeds or trading recommendations.

## Deploy to GitHub Pages
1. Create a **public** GitHub repository named `stocklens` (or any name).
2. Upload `index.html` to the repository root and commit.
3. Go to **Settings → Pages → Build and deployment**.
4. Select **Deploy from a branch**, branch **main**, folder **/(root)**, then Save.
5. Open `https://YOUR-USERNAME.github.io/stocklens/` after deployment completes.

No npm install, backend or build process is needed for this demonstration.

## Features
- Discover and filter a synthetic stock universe by market, sector, score, leverage and FCF sign.
- Individual financial scorecard with a hard risk gate (high leverage, low interest cover or negative FCF).
- Compare up to four companies.
- Custom weights (must sum to 100%).
- Browser-local watchlist, JSON export/import.
- Mobile-first dark design.

## Data integration plan
See `DATA_INTEGRATION.md`. Do not add secret API tokens to this static HTML or commit them to GitHub.

## Limitations
The financial figures and companies are fabricated for interface testing. Competitive moat and recession resilience scores require qualitative methodology and analyst review. No predictive accuracy is claimed. localStorage is per browser and can be cleared. Banks, insurers, REITs and early-stage companies require separate scoring methodologies.
