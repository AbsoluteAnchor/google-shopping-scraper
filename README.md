[Google Shopping Scraper](https://apify.com/burbn/google-shopping-scraper?fpr=data)

# Google Shopping Scraper 🛒

Search and scrape **Google Shopping products** by keyword and export clean, structured data (product details, prices, ratings, reviews, store info, offers, shipping details).

This actor is built for:

- Price monitoring & tracking 💰
- Competitor analysis 🧠
- Market research 📊
- E-commerce intelligence 🛍️

---

## 📌 Table of Contents

- ✨ Features
- 🎯 Use Cases
- ⚡ Quick Start
- 🧾 Input Parameters
- 📤 Output
- 🧩 Dataset Views (Table View)
- ❓ FAQ
- 🔎 Tags

---

## ✨ Features

| Feature | Description |
| --- | --- |
| 🔍 **Keyword Search** | Search products by name, brand, or keywords |
| 🌍 **Multi-Country Support** | Get localized results from any country |
| 🗣️ **Multi-Language** | Results in your preferred language |
| 📊 **Flexible Sorting** | Sort by best match, price (low/high), or rating |
| 💰 **Complete Pricing** | Current price, original price, discounts, price ranges |
| ⭐ **Ratings & Reviews** | Product ratings and review counts |
| 🏪 **Store Information** | Store name, rating, reviews, shipping, returns |
| 📦 **Pagination Support** | Scrape multiple pages of results |
| 🧼 **Clean Dataset** | Organized data ready for analysis |

---

## 🎯 Use Cases

| Use Case | What You Can Do | Why It Helps |
| --- | --- | --- |
| 💰 **Price Monitoring** | Track product prices across stores | Find best deals & price drops |
| 🧠 **Competitor Analysis** | Compare competitor product pricing | Optimize your pricing strategy |
| 📊 **Market Research** | Analyze product trends & availability | Make data-driven decisions |
| 🛍️ **E-commerce Intelligence** | Monitor product listings & offers | Stay ahead of competition |
| 📈 **Price Comparison** | Compare prices from multiple sellers | Find the best value |
| 🏷️ **Deal Hunting** | Find products on sale with discounts | Save money on purchases |

---

## ⚡ Quick Start

### 1️⃣ Basic Run

Use this input to search for products:

```
{
  "searchQuery": "nike running shoes",
  "country": "us",
  "language": "en",
  "sortBy": "BEST_MATCH",
  "limit": 20
}
```

### 2️⃣ Advanced Search

Search with custom sorting and pagination:

```
{
  "searchQuery": "iPhone 15 Pro",
  "country": "us",
  "language": "en",
  "sortBy": "LOWEST_PRICE",
  "limit": 50
}
```

### 3️⃣ Tips for Better Results

- Use specific product names for accurate results
- Try different `sortBy` options to find deals
- Increase `limit` for comprehensive data
- Use appropriate `country` code for local pricing

---

## 🧾 Input Parameters

| Parameter | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| `searchQuery` | String | ✅ | - | Product name, brand, or keywords to search |
| `country` | String | ❌ | `us` | Country code (ISO 3166-1 alpha-2) |
| `language` | String | ❌ | `en` | Language code (ISO 639-1) |
| `sortBy` | Enum | ❌ | `BEST_MATCH` | Sort order: `BEST_MATCH`, `LOWEST_PRICE`, `HIGHEST_PRICE`, `TOP_RATED` |
| `limit` | Number | ❌ | `20` | Products per page (1-100) |

### Supported Countries

| Code | Country | Code | Country |
| --- | --- | --- | --- |
| `us` | United States | `gb` | United Kingdom |
| `de` | Germany | `fr` | France |
| `in` | India | `ca` | Canada |
| `au` | Australia | `jp` | Japan |

*See [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) for all country codes.*

---

## 📤 Output

Each dataset item represents **one Google Shopping product**.

### 🧾 Output Fields

| Category | Fields |
| --- | --- |
| 🏷️ **Product Info** | `productId`, `productTitle`, `productDescription`, `productPageUrl` |
| 💰 **Pricing** | `price`, `originalPrice`, `onSale`, `percentOff`, `typicalPriceRange` |
| ⭐ **Ratings** | `productRating`, `productNumReviews`, `productNumOffers` |
| 🏪 **Store Info** | `storeName`, `storeRating`, `storeReviewCount`, `storeFavicon` |
| 🚚 **Shipping** | `shipping`, `returns`, `paymentMethods`, `productCondition` |
| 🖼️ **Media** | `productPhotos`, `productVideos` |
| 🔧 **Variants** | `currentVariantProperties`, `productVariants`, `productAttributes` |

### Sample Output

```
{
  "productId": "12345678901234567890",
  "productTitle": "Sony WH-1000XM5 Wireless Headphones",
  "productDescription": "Industry-leading noise cancellation...",
  "price": "$348.00",
  "originalPrice": "$399.99",
  "onSale": true,
  "percentOff": "13% off",
  "productRating": 4.7,
  "productNumReviews": 2543,
  "storeName": "Amazon",
  "storeRating": "4.5/5",
  "shipping": "Free delivery",
  "returns": "Free 30-day returns"
}
```

---

## 🧩 Dataset Views (Table View)

This actor includes clean, organized dataset table views:

| View | Description |
| --- | --- |
| 📊 **Products Overview** | Product title, price, rating, reviews, store, buy link |
| 💰 **Pricing Details** | Current price, original price, discounts, price ranges |
| 🏪 **Store Information** | Store name, rating, reviews, shipping, returns |
| 📦 **Product Details** | Description, condition, ratings, product URLs |

---

## ❓ FAQ

### **Q1: How many products can I scrape?**

Each page can return up to 100 products. With `limit`, you can scrape thousands of products. Start small and increase as needed.

### **Q2: Why do I get fewer results than expected?**

Some searches may have limited products available. Try:

- A broader search query
- Different country/language settings
- Different sorting options

### **Q3: Are all fields always available?**

Not always. Some products may not have descriptions, ratings, or sale information. The actor returns `null` for unavailable fields.

### **Q4: Can I search in different countries?**

Yes! Use the `country` parameter with ISO 3166-1 alpha-2 codes (e.g., `us`, `gb`, `de`, `fr`, `in`).

### **Q5: How often is the data updated?**

The actor fetches real-time data from Google Shopping. Prices and availability are current at the time of scraping.

### **Q6: Can I use this for price monitoring?**

Yes! Schedule the actor to run periodically and track price changes over time using Apify's scheduling feature.

---

## 🔎 Tags

Google Shopping scraper, Google Shopping API, scrape Google Shopping, Google Shopping data extractor, Google Shopping price scraper, product price scraper, e-commerce scraper, price monitoring tool, competitor price analysis, Google Shopping product search, product data extraction, shopping comparison scraper, retail price tracker, Google product scraper, Apify Google Shopping, price comparison tool, e-commerce data extraction, product research tool, market research scraper, online shopping scraper