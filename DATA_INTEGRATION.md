# StockLens — live data integration roadmap

## Architecture
GitHub Pages (static UI) → HTTPS API endpoint (Cloudflare Worker / Netlify Function / similar) → licensed financial data vendor. Cache vendor responses server-side, protect API keys in secret storage, and enforce rate limits. Never expose vendor keys in browser JavaScript.

## Provider selection (validate before purchase)
Evaluate Financial Modeling Prep, Finnhub, EODHD, Polygon/Massive and other providers against: UK LSE and US symbol coverage, financial statement history, cash-flow fields, share counts, price freshness, fundamentals refresh timing, licence for browser display and derived screening, API quotas, uptime, currency handling, adjusted statements and costs. Provider features/pricing are not verified here.

## Minimum normalized schema
- identity: ticker, exchange, ISIN (where available), name, sector, reporting currency, fiscal year, as_of_date, source URL
- price: price, currency, price_as_of, market cap, enterprise value, shares outstanding
- financials: cash, total debt, net debt, EBITDA, EBIT, interest expense, operating cash flow, capex, free cash flow, revenue, net income, invested capital; 5 annual periods and latest interim where available
- quality: dilution, buybacks, maturity schedule, lease liabilities, one-offs, auditor flags, customer concentration, sector notes
- metadata: missing-data flags, stale-data flags, restatement/version, calculation method

## Calculation rules
- FCF = cash flow from operations − capex (standardize vendor sign conventions).
- Net debt = interest-bearing debt − cash (disclose lease treatment).
- Net debt / EBITDA only meaningful with positive, normalized EBITDA; negative EBITDA → not meaningful and red flag, not an artificially low ratio.
- Interest cover = EBIT / interest expense; handle zero interest separately.
- FCF yield = annualized normalized FCF / market cap, with explicit period and currency alignment.
- ROIC = NOPAT / average invested capital, with disclosed tax and capital adjustments.
- Valuation: sector-relative FCF yield, EV/EBIT, P/E and a sensitivity-based DCF. Avoid applying P/E to loss-makers.
- Score categories must define reproducible threshold functions and peer normalization; do not turn missing data into zero or a passing grade.
- Critical overrides: negative FCF persistence, near-term maturity coverage, interest cover <3, leverage >3, going-concern warnings, auditor qualification, material restatements. Context-specific overrides and sector exceptions are essential.

## Implementation phases
1. Build API adapter + provider evaluation, test on 10 US and 10 UK stocks with known filings.
2. Add source/date/currency labels and a transparent metric calculation drilldown.
3. Replace fictional sample universe with a licensed, paginated stock universe; provide search, sorting and caching.
4. Add configurable screening, valuation ranges, portfolio watchlist, and alert delivery via a backend scheduler.
5. Backtest screening rules out of sample, avoid survivorship and look-ahead bias, and distinguish research scores from buy/sell instructions.

## Security and operations
Server-side API key; HTTPS; input validation; API quotas; caching and retries; logs without personal portfolio data; accessible UI; data provider attribution; clear disclaimers; optional authenticated cross-device storage later.
