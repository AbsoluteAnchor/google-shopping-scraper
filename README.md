[Google Shopping Scraper](https://apify.com/khadinakbar/google-shopping-scraper?fpr=data)

# 🛍️ Google Shopping Scraper

Extract product listings, prices, sellers, ratings, discounts, and shipping info from Google Shopping in real time. Supports 28 countries, price range filters, sort by price or reviews, and new/used/refurbished condition filters.

---

## When to use this actor

Use this actor when asked to:

- Find prices for a product on Google Shopping
- Compare prices across multiple sellers or merchants
- Monitor or track product pricing over time
- Research competitor pricing for a product category
- Find the cheapest place to buy a specific product
- Get product ratings and review counts from Google Shopping
- Scrape Google Shopping results for a keyword or product name
- Get localized prices in a specific country (UK, Germany, Japan, etc.)
- Filter results by condition (new, used, refurbished) or price range

---

## Quick Start (Minimal Input)

```
{
  "searchQueries": ["wireless headphones"],
  "maxResults": 20
}
```

`searchQueries` is the only required field. All other fields have sensible defaults.

---

## Input

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| `searchQueries` | string[] | **required** | Product keywords to search. Multiple queries run independently. |
| `maxResults` | integer | `20` | Max products per query (1–200). Triggers auto-pagination for higher values. |
| `countryCode` | string | `"us"` | Target country for localized prices. E.g. `"gb"` for UK, `"de"` for Germany. |
| `languageCode` | string | `"en"` | Language for results. E.g. `"fr"` for French. |
| `sortBy` | string | `"relevance"` | Sort order: `relevance`, `price_low`, `price_high`, `review_score`. |
| `condition` | string | `"any"` | Product condition: `any`, `new`, `used`, `refurbished`. |
| `minPrice` | integer | — | Minimum price filter in the local currency (e.g. `50` = $50 in US). |
| `maxPrice` | integer | — | Maximum price filter in the local currency (e.g. `500` = $500 in US). |
| `proxyConfiguration` | object | GOOGLE_SERP | Leave as default — GOOGLE_SERP proxy is required for reliable Google access. |

### Example: Price comparison with filters

```
{
  "searchQueries": ["Sony WH-1000XM5", "Bose QuietComfort 45"],
  "maxResults": 10,
  "sortBy": "price_low",
  "condition": "new",
  "countryCode": "us"
}
```

### Example: UK price monitoring

```
{
  "searchQueries": ["iPad Pro 13 inch"],
  "maxResults": 20,
  "countryCode": "gb",
  "languageCode": "en"
}
```

### Example: Budget product research

```
{
  "searchQueries": ["gaming keyboard"],
  "maxResults": 40,
  "sortBy": "price_low",
  "minPrice": 30,
  "maxPrice": 150
}
```

---

## Output

Each item in the dataset represents one product listing.

| Field | Type | Description |
| --- | --- | --- |
| `title` | string | Full product name as shown on Google Shopping |
| `price` | number|null | Numeric price in local currency |
| `price_raw` | string|null | Raw price string with currency symbol (e.g. `"$39.99"`) |
| `currency` | string|null | Currency symbol (e.g. `"$"`, `"£"`, `"€"`) |
| `original_price` | number|null | Pre-discount price if a sale is shown |
| `discount_percent` | number|null | Calculated discount % when original price is available |
| `merchant` | string|null | Seller name (e.g. `"Best Buy"`, `"Amazon"`) |
| `rating` | number|null | Star rating out of 5.0 |
| `reviews_count` | integer|null | Number of user reviews |
| `product_url` | null | Always null — Google Shopping uses JS navigation (no static href) |
| `image_url` | null | Always null — images are lazy-loaded via JS (not in static HTML) |
| `shipping` | string|null | Shipping info (e.g. `"Free delivery by Wed"`) |
| `condition` | string|null | Product condition if shown (`new`, `used`, `refurbished`) |
| `position` | integer | 1-based rank in search results |
| `search_query` | string | The original search query that returned this product |
| `country` | string | Country code used for the search |
| `scraped_at` | string | ISO 8601 timestamp |
| `source_url` | string | The Google Shopping URL that was scraped |

### Example output item

```
{
  "title": "Sony WH-CH720N Noise Canceling Wireless Headphones",
  "price": 179.99,
  "price_raw": "$179.99",
  "currency": "$",
  "original_price": null,
  "discount_percent": null,
  "merchant": "Walmart",
  "rating": 4.6,
  "reviews_count": 14000,
  "product_url": null,
  "image_url": null,
  "shipping": "Free delivery by Tue",
  "condition": null,
  "position": 1,
  "search_query": "wireless headphones",
  "country": "us",
  "scraped_at": "2026-04-13T10:30:00.000Z",
  "source_url": "http://www.google.com/search?q=wireless+headphones&tbm=shop&gl=us&hl=en&num=40"
}
```

---

## Supported Countries

`us` `gb` `ca` `au` `de` `fr` `es` `it` `br` `mx` `in` `jp` `nl` `pl` `se` `no` `dk` `fi` `be` `at` `ch` `pt` `ie` `nz` `za` `sg` `ae` `sa`

---

## Known Limitations

- **`product_url` is always null** — Google Shopping renders product links via JavaScript. No static href is present in the HTML.
- **`image_url` is always null** — Product images are lazy-loaded by JavaScript. The static HTML only contains placeholder GIFs.
- **Price filters are approximate** — Google Shopping occasionally returns results slightly outside the min/max range.
- **GOOGLE_SERP proxy is required** — Do not change the proxy configuration or the actor will fail.

---

## Pricing

Pay-Per-Result at **$0.002 per product** extracted.

| Products scraped | Estimated cost |
| --- | --- |
| 100 | ~$0.20 |
| 1,000 | ~$2.00 |
| 10,000 | ~$20.00 |

---

## Legal

This actor scrapes publicly available data from Google Shopping. Users are responsible for ensuring their use complies with Google's Terms of Service and applicable laws.