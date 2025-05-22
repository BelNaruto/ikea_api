# IKEA Data API Documentation (Unofficial)

## Overview

To use this API you have to Subscribe to the [API on RapidAPI](https://rapidapi.com/belchiorarkad-FqvHs2EDOtP/api/ikea-data-api) and include your API key in the X-RapidAPI-Key header.

The IKEA Data API provides comprehensive access to IKEA's product catalog, search functionality, and store information. This API allows developers to integrate IKEA's extensive furniture and home goods database into their applications, enabling users to search for products, browse categories, check availability, and access detailed product information.



**Perfect for:** E-commerce applications, price comparison tools, interior design apps, inventory management systems, and any application that needs access to IKEA's product data.

## Key Features

- **Product Search**: Search through thousands of IKEA products with advanced filtering
- **Category Browsing**: Access IKEA's complete category hierarchy
- **Product Details**: Get comprehensive product information including descriptions, prices, and specifications
- **Availability Checking**: Real-time product availability across IKEA stores
- **Multi-language Support**: Access data in multiple locales and languages
- **Smart Features**: Autocomplete search, trending searches, and similar product recommendations
- **High Performance**: Built-in caching system ensures fast response times


## Base Url
- https://ikea-data-api.p.rapidapi.com

## API Endpoints

### 🔍 Search Endpoints

#### Search Products
```
GET /search
```
Search for IKEA products with customizable parameters and advanced filtering options.

**Parameters:**
- `query` (required): Search term (e.g., "sofa", "bookshelf")
- `page` (optional): Page number, default: 1
- `perPage` (optional): Results per page, default: 24
- `sortBy` (optional): Sort order, default: "RELEVANCE"
- `filters` (optional): Filter object with the following supported filters:
  - `colors`: Comma-separated color IDs (e.g., "10156,10139" for white,black)
  - `priceRange`: Comma-separated price bucket IDs (e.g., "PRICE_0_2000,PRICE_2000_4000")
  - `size`: Comma-separated size IDs (e.g., "WIDTH_20_40,HEIGHT_20_40")
  - `materials`: Comma-separated material IDs (e.g., "47349,47350" for wood,metal)
  - `type`: Comma-separated product type IDs (e.g., "Desk,Table")
  - `brand`: Comma-separated brand IDs
  - `category`: Comma-separated category IDs
  - `availability`: Comma-separated availability status IDs
  - `room`: Comma-separated room type IDs
  - `features`: Comma-separated product feature IDs
- `localeCode` (optional): Language/region code, default: "en_PT"

**Filter Examples:**
```javascript
// Single filter - White products only
filters = {
  "colors": "10156"
}

// Multiple filters - White/Black wood or metal products under €40
filters = {
  "colors": "10156,10139",
  "materials": "47349,47350",
  "priceRange": "PRICE_0_2000,PRICE_2000_4000"
}

// Size filters - Products with specific width ranges
filters = {
  "size": "WIDTH_20_40,WIDTH_40_60"
}

// Type filters - Desks and tables only
filters = {
  "type": "Desk,Table"
}
```

**Important:** Filter values must use the specific IDs returned by the `/search/filters` endpoint, not human-readable names. Common filter IDs include:
- **Colors**: 10156 (white), 10139 (black), 10019 (brown), 10003 (beige), 10028 (grey)
- **Materials**: 47349 (Wood), 47350 (Metal), 50788 (Solid wood), 38828 (Fabric)
- **Price**: PRICE_0_2000 (€0-19), PRICE_2000_4000 (€20-39), PRICE_4000_6000 (€40-59)
- **Size**: WIDTH_20_40 (20-39cm width), HEIGHT_20_40 (20-39cm height)

#### Get Search Filters
```
GET /search/filters
```
Retrieve available filters for a specific search query.

**Parameters:**
- `query` (required): Search term
- `localeCode` (optional): Language/region code, default: "en_PT"

#### Autocomplete Search
```
GET /search/autocomplete
```
Get search suggestions as users type.

**Parameters:**
- `query` (required): Partial search term
- `localeCode` (optional): Language/region code, default: "en_PT"

#### Trending Searches
```
GET /search/trending
```
Get currently popular search terms.

**Parameters:**
- `localeCode` (optional): Language/region code, default: "en_PT"

### 📂 Category Endpoints

#### Get All Categories
```
GET /categories
```
Retrieve IKEA's complete category structure.

**Parameters:**
- `localeCode` (optional): Language/region code, default: "en_PT"

#### Get Available Languages
```
GET /locale/codes
```
Get list of supported language and region codes.

**No parameters required**

### 🛋️ Product Endpoints

#### Get Products by Category
```
GET /product/bycategory
```
Browse products within a specific category.

**Parameters:**
- `categoryId` (required): IKEA category identifier
- `page` (optional): Page number, default: 1
- `perPage` (optional): Results per page, default: 24
- `sortBy` (optional): Sort order, default: "RELEVANCE"
- `localeCode` (optional): Language/region code, default: "en_PT"

#### Get Product Description (V1)
```
GET /product/description/v1
```
Get detailed product information by product ID.

**Parameters:**
- `productId` (required): IKEA product identifier
- `localeCode` (optional): Language/region code, default: "en_PT"

#### Get Product Description by URL
```
GET /product/description/byurl
```
Get product information using IKEA product URL.

**Parameters:**
- `productUrl` (required): Full IKEA product URL

#### Get Similar Products
```
GET /product/similar
```
Find products similar to a given product.

**Parameters:**
- `productId` (required): IKEA product identifier
- `localeCode` (optional): Language/region code, default: "en_PT"

#### Check Product Availability
```
GET /product/availability
```
Check real-time product availability in stores.

**Parameters:**
- `productId` (required): IKEA product identifier

## Getting Started

### 1. Authentication
Subscribe to the [API on RapidAPI](https://rapidapi.com/belchiorarkad-FqvHs2EDOtP/api/ikea-data-api) and include your API key in the `X-RapidAPI-Key` header.

### 2. Basic Example
```javascript
// Simple search for sofas
const response = await fetch('https://ikea-data-api.p.rapidapi.com/search?query=sofa&page=1&perPage=12', {
  headers: {
    'X-RapidAPI-Key': 'your-api-key',
    'X-RapidAPI-Host': 'ikea-data-api.p.rapidapi.com'
  }
});
const data = await response.json();

// Get available filters for a search query
const filtersResponse = await fetch('https://ikea-data-api.p.rapidapi.com/search/filters?query=table', {
  headers: {
    'X-RapidAPI-Key': 'your-api-key',
    'X-RapidAPI-Host': 'ikea-data-api.p.rapidapi.com'
  }
});
const availableFilters = await filtersResponse.json();

// Advanced search with specific filter IDs
const filtersExample = {
  colors: "10156,10139",      // white, black
  materials: "47349,47350",   // wood, metal
  priceRange: "PRICE_0_2000,PRICE_2000_4000", // €0-19, €20-39
  type: "Desk,Table"          // desks and tables
};

const advancedResponse = await fetch(`https://ikea-data-api.p.rapidapi.com/search?query=furniture&filters=${JSON.stringify(filtersExample)}`, {
  headers: {
    'X-RapidAPI-Key': 'your-api-key',
    'X-RapidAPI-Host': 'ikea-data-api.p.rapidapi.com'
  }
});
const advancedData = await advancedResponse.json();
```

### 3. Locale Codes
The API supports multiple regions and languages. Common locale codes include:
- `en_US` - English (United States)
- `en_GB` - English (United Kingdom)
- `en_PT` - English (Portugal) - Default
- `de_DE` - German (Germany)
- `fr_FR` - French (France)
- `sv_SE` - Swedish (Sweden)

## Performance & Caching

The API includes intelligent caching to ensure fast response times:
- **Search Results**: Cached for 5 minutes
- **Product Descriptions**: Cached for 15 minutes
- **Categories**: Cached for 30 minutes
- **Available Languages**: Cached for 1 hour
- **Product Availability**: Cached for 30 seconds (real-time data)

## Error Handling

The API returns standard HTTP status codes:
- `200` - Success
- `400` - Bad Request (missing or invalid parameters)
- `404` - Not Found
- `500` - Internal Server Error

Error responses include helpful messages to guide proper usage.

## Frequently Asked Questions

### API Questions

**Q: How many requests can I make per day?**  
A: Rate limits depend on your RapidAPI subscription plan. Check your plan details on RapidAPI for specific limits.

**Q: Is the product data real-time?**  
A: Product information and availability are updated regularly. Availability data is cached for only 30 seconds to provide near real-time accuracy.

**Q: Can I get product prices through the API?**  
A: Yes, product pricing information is included in the product description endpoints, when available for the specified locale.

**Q: Which countries/regions are supported?**  
A: The API supports all regions where IKEA operates. Use the `/locale/codes` endpoint to get the complete list of supported locale codes.

**Q: How do filter parameters work?**  
A: Filters use specific IDs rather than human-readable names. You must first call the `/search/filters` endpoint to get available filter IDs for your search query, then use these IDs in your filter parameters:

**Filter Structure from API Response:**
```json
{
  "titleInEnglish": "Colour",
  "values": [
    {"id": "10156", "title": "white", "count": 297},
    {"id": "10139", "title": "black", "count": 167},
    {"id": "10019", "title": "brown", "count": 219}
  ]
}
```

**Common Filter IDs:**
- **Colors**: `10156` (white), `10139` (black), `10019` (brown), `10003` (beige), `10028` (grey)
- **Materials**: `47349` (Wood), `47350` (Metal), `50788` (Solid wood), `38828` (Fabric), `47675` (Plastic)
- **Price**: `PRICE_0_2000` (€0-19), `PRICE_2000_4000` (€20-39), `PRICE_4000_6000` (€40-59)
- **Size**: `WIDTH_20_40` (20-39cm width), `HEIGHT_20_40` (20-39cm height), `WIDTH_60_80` (60-79cm width)
- **Type**: `Desk`, `Table`, `Coffee table`, `Bedside table`

**Usage Example:**
```javascript
// Use specific IDs, not names
filters = {
  "colors": "10156,10139",        // white, black
  "materials": "47349,47350",     // wood, metal
  "priceRange": "PRICE_0_2000"    // €0-19
}
```

**Q: Can I filter search results?**  
A: Yes, both the `/search` and `/product/bycategory` endpoints support advanced filtering. Always use the `/search/filters` endpoint first to discover the exact filter IDs available for your search query, then apply them using the `filters` parameter with the specific IDs returned.

**Q: How do I handle pagination?**  
A: Use the `page` and `perPage` parameters. Start with `page=1` and increment to get subsequent pages. The API will return information about total results and available pages.

### IKEA Questions

**Q: What is IKEA?**  
A: IKEA is a Swedish multinational conglomerate that designs and sells ready-to-assemble furniture, kitchen appliances, decoration, home accessories, and various other useful goods and home services.

**Q: When was IKEA founded?**  
A: IKEA was founded in 1943 by Ingvar Kamprad in Sweden. The name IKEA comes from the founder's initials (I.K.) plus the first letters of Elmtaryd and Agunnaryd, the farm and village where he grew up.

**Q: How many IKEA stores are there worldwide?**  
A: As of 2024, IKEA operates over 460 stores in more than 60 countries around the world, making it one of the world's largest furniture retailers.

**Q: What does "flat-pack" furniture mean?**  
A: Flat-pack furniture is IKEA's signature approach where furniture is sold unassembled in flat packages. This reduces shipping costs and storage space, making furniture more affordable for customers.

**Q: Are IKEA product names real words?**  
A: Yes! IKEA uses a unique naming system where products are named after Swedish places, people, or words. For example, beds are named after Norwegian places, chairs after men's names, and fabrics after women's names.

**Q: Can I return IKEA products?**  
A: IKEA has a generous return policy allowing returns within 365 days of purchase with receipt. Some restrictions apply to certain products.

**Q: Does IKEA offer assembly services?**  
A: Yes, IKEA offers assembly services in most locations for an additional fee. You can also find assembly instructions and videos on their website.

**Q: Is IKEA environmentally conscious?**  
A: IKEA has committed to becoming climate positive by 2030 and uses sustainable materials whenever possible. They focus on renewable energy, sustainable sourcing, and circular business practices.

## Support


For technical support with the API, please reach out via one of the following channels:

* **RapidAPI Messaging System**
* **Telegram:** [@pintoflow](https://t.me/pintoflow)  (preferred for fast reply)
* **Email:** [pintoflowpt@gmail.com](mailto:pintoflowpt@gmail.com)



---

*This API provides access to IKEA's product data for development purposes. It is not officially affiliated with IKEA Group.*
