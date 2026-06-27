[Google Shopping Scraper](https://apify.com/scrape.badger/google-shopping-scraper?fpr=data)

## What does Google Shopping Scraper do?

Scrape [Google Shopping](https://shopping.google.com) product tiles at scale — title, price, rating, review count, merchant, thumbnail, direct link — with full filter support (price range, free shipping, on sale, condition).

## Why use Google Shopping Scraper?

- **Full Google Shopping filter set.** Price range, free shipping, on sale, used/new, sort order.
- **Per-product enrichment path.** Pipe each `gpcid` through `google-products-scraper` for deep product detail.
- **200+ country domains.** `gl` + `hl` for local pricing and merchants.
- **Pagination.** Up to 10 pages per run, stops early when Google runs out.
- **Each tile as its own record.** Stream-friendly output — one product per dataset row.

## What data can Google Shopping Scraper extract?

| Field | Type | Description |
| --- | --- | --- |
| title | string | Product title |
| price | object | `{value, currency, extracted}` |
| rating | number | Star rating (when available) |
| reviews | number | Review count |
| merchant | string | Store name |
| thumbnail | string | Image URL |
| link | string | Direct product URL |
| gpcid | string | Google Shopping's product ID (for `google-products-scraper`) |
| position | number | Rank within the page |

## How to scrape Google Shopping

1. Click **Try for free**.
2. Enter your search query in `q`.
3. Optional: set `min_price` / `max_price`, `sort_by`, `free_shipping`, `on_sale`.
4. Set `gl` for the country (default `us`).
5. Set `max_pages` — each page is ≈ 40 tiles.
6. Click **Start** — each product tile streams into the dataset.

## How much will it cost?

**$3 per 1,000 pages (≈ $0.075 per 1,000 product tiles).** One API call per page. A 3-page run returns ≈ 120 tiles for $0.009.

### Competitor benchmark

| Actor | Author | Price | Notes |
| --- | --- | --- | --- |
| emastra/google-shopping-scraper | emastra | $30/mo subscription + CUs | Subscription floor |
| apify/google-search-scraper | Apify | ~$4 / 1k tiles | SERP actor with Shopping block |
| compass/crawler-google-shopping | Compass | ~$5 / 1k | Search-only |
| **scrape-badger/google-shopping-scraper** | **ScrapeBadger** | **$3 / 1k pages** | **Pay-per-use, full filter set** |

## Input

Configure the run in the **Input** tab above, or pass a JSON object matching the fields below when calling the Actor via the Apify API.

| Field | Required | Description |
| --- | --- | --- |
| q | ✅ | Product query. |
| gl | — | Country (default `us`). |
| hl | — | Language (default `en`). |
| min_price / max_price | — | Price range in local currency. |
| sort_by | — | Google's sort modes. |
| free_shipping / on_sale | — | Boolean filters. |
| max_pages | — | 1-10, default 3. |

## Output

Every successful run streams records into the run's dataset. Download as JSON, CSV, XML, Excel, or HTML from the **Dataset** tab; consume programmatically via the Apify API or webhooks.

Example record:

```
{
  "title": "Nike Air Max 90",
  "price": {
    "value": "$119.99",
    "currency": "USD",
    "extracted": 119.99
  },
  "rating": 4.5,
  "reviews": 2341,
  "merchant": "Nike.com",
  "thumbnail": "https://encrypted-tbn0.gstatic.com/shopping?q=\u2026",
  "link": "https://www.nike.com/t/\u2026",
  "gpcid": "1234567890123456789",
  "position": 1
}
```

## Tips / Advanced options

- **Enrich with `google-products-scraper`.** Pipe each `gpcid` for specs, offers, variants — full immersive product detail.
- **Use `on_sale: true` for deal tracking.** Pair with a daily scheduler for price-drop alerts.
- **Sort by `review_score` for quality.** Avoid tiles with few reviews — Google's sort controls help.
- **Country matters for pricing.** `gl: uk` returns GBP and UK merchants; `gl: de` returns EUR and DE merchants.

## FAQ, Disclaimers, Support

### What's `gpcid`?

Google Shopping's product ID. It's the input for `google-products-scraper` to get full product details (specs, offers, variants).

### Does this include sponsored tiles?

Yes — the output includes organic and sponsored tiles together. Filter by `ad: true` downstream if you need to separate.

### Why is the price an object?

`extracted` is the numeric value (cents-safe), `value` is the original formatted string, `currency` is the ISO code. The numeric field is what you want for filtering/analysis.

### Can I search by product image?

No — Google Shopping is text-search only. For visual search use `google-lens-scraper`.

### Disclaimer

This Actor scrapes public Google data only. You're responsible for compliance with Google's Terms of Service and any applicable data-protection laws (GDPR, CCPA, etc.) in your jurisdiction. ScrapeBadger does not store the scraped results — they are delivered directly to your Apify dataset.

### Support

Something not working? Open a ticket in the **Issues** tab above — we triage within one business day. Full API reference: [docs.scrapebadger.com](https://docs.scrapebadger.com).

### Related Actors

- [`google-products-scraper`](https://apify.com/scrape-badger/google-products-scraper) — Deep product detail per `gpcid`
- [`google-search-scraper`](https://apify.com/scrape-badger/google-search-scraper) — SERP with inline Shopping block

### Powered by

[ScrapeBadger](https://scrapebadger.com) — Google-optimised residential proxy pool + browser-farm fallback, 99.7% uptime, unmetered bandwidth. No CAPTCHAs reach you.