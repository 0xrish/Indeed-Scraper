# Indeed Jobs Scraper – Fastest & Cheapest Indeed Scraper on Apify 🚀

Extract structured job listings from Indeed with **150+ data fields per job**, support for **54 countries**, and pricing starting at **$0.05 per 1,000 jobs**. Built for recruiters, HR teams, lead-gen agencies, and data analysts who need high-quality Indeed job data at scale — without the high compute costs.

[![Apify Store](https://img.shields.io/badge/Apify-Store-blue)](https://apify.com/mikolabs/indeed-scraper)
[![Website](https://img.shields.io/badge/Website-mikolabs.xyz-green)](https://mikolabs.xyz)

🔗 **Try it now:** [apify.com/mikolabs/indeed-scraper](https://apify.com/mikolabs/indeed-scraper)
🌐 **Website:** [mikolabs.xyz](https://mikolabs.xyz)

---

## Table of Contents

- [Overview](#overview)
- [Pricing](#pricing)
- [Why Use This Scraper](#why-use-this-scraper)
- [Use Cases](#use-cases)
- [How to Use (JSON Examples)](#how-to-use-json-examples)
- [Input Parameters](#input-parameters)
- [Search Modes Explained](#search-modes-explained)
- [Sample Output Data (150+ Fields)](#sample-output-data-150-fields)
- [Limitations](#limitations)
- [Integrations](#integrations)
- [Support & Customization](#support--customization)
- [Keywords](#keywords)

---

## Overview

**Indeed Jobs Scraper** by MikoLabs is the most complete Indeed scraper on Apify, providing **150+ fields per job** — more than any comparable actor. Get pre-parsed salaries (down to cents), employer-provided attributes, CEO names, company social links, click-tracking URLs, hiring insights, GPS coordinates, company financials, and much more — all in clean, nested JSON.

---

## Pricing

| Plan | Price per 1,000 Jobs |
|------|----------------------|
| 👑 Paying Apify Users | **$0.05** |
| 👤 Normal Users | **$0.06** |

Extract millions of job listings without worrying about massive compute bills.

---

## Why Use This Scraper

- ⚡ **Blazing Fast Extraction** — scrapes hundreds of jobs in seconds, not minutes
- 💰 **Minimal Compute Usage** — low execution costs keep platform fees tiny
- 📦 **150+ Fields Per Job** — pre-parsed salary, GPS coordinates, full company dossier, normalized titles, employer tier, feed metadata, hiring insights, and more
- 🧠 **Exclusion-Based Skill Extraction** — automatically classifies ~5,000+ skills by filtering out non-skill categories (benefits, certifications, education, etc.)
- 🔍 **Three Search Modes** — Basic (fastest), Detailed (more data per job), or Rich (extra fields)
- 📄 **Full Pagination** — automatically scrapes every matching job page
- 🌍 **Smart Geo-Targeting** — supports 54 countries, with distance in miles or kilometers
- 🏢 **Company Search** — use `company:Name` to return all jobs from a specific employer
- 🔑 **Direct Job Lookup** — look up jobs by `jobKey`, including expired-status checks
- 🧩 **Clean Nested Output** — `title{}`, `urls{}`, `classification{}`, `workArrangement{}`, `salary{}`, `apply{}`, `company{}`, `dates{}`, `signals{}`, `requirements{}`, `meta{}`

---

## Use Cases

- **Analyze Hiring Trends** — track salary ranges and demand by role or location
- **Benchmark Compensation** — compare salaries across companies, roles, and regions
- **Monitor Competitors** — keep tabs on competitor hiring activity and open roles
- **Lead Generation** — build databases of hiring companies with industry, size, revenue, and CEO data
- **Job Board Aggregators** — feed structured job data into your own job board or app
- **Market Research** — track job-type distribution, benefits offered, and in-demand skills

---

## How to Use (JSON Examples)

Configure inputs on the Apify Console, or pass JSON directly via the API.

**Search by keyword + location**
```json
{
  "keyword": "Data Analyst",
  "location": "New York, NY",
  "country": "US",
  "maxItems": 200,
  "sort": "date",
  "fromDays": "7"
}
```

**Search by zip code & radius**
```json
{
  "keyword": "software engineer",
  "location": "10001",
  "country": "US",
  "radius": "25",
  "radiusUnit": "miles",
  "maxItems": 50
}
```

**Search by company**
```json
{
  "keyword": "company:Google",
  "location": "San Francisco, CA",
  "maxItems": 100
}
```

**Filter by job type and remote**
```json
{
  "keyword": "Software Engineer",
  "location": "Austin, TX",
  "jobType": "fulltime",
  "remote": "remote",
  "radius": "50"
}
```

**Detailed search mode** (hiring insights, benefits, requirements)
```json
{
  "keyword": "nurse",
  "location": "New York",
  "searchMode": "detailed",
  "maxItems": 100
}
```

**Look up specific jobs by key** (check if still active)
```json
{
  "jobKeys": ["5e5dafc2a80c214d", "550a48652b44bb83"],
  "country": "US"
}
```

---

## Input Parameters

### Search mode (keyword + location)

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `keyword` | string | – | Job title, skill, or `company:Name` |
| `location` | string | – | City, state, or ZIP code |
| `country` | select | US | 54 localized countries supported |
| `maxItems` | number | 20 | Max number of job listings to scrape (0 = no limit) |
| `radius` | select | 35 | Search distance: 0–100 |
| `radiusUnit` | select | miles | `miles` or `km` |
| `sort` | select | relevance | `relevance` or `date` |
| `fromDays` | select | any | Posted within 1, 3, 7, or 14 days |
| `jobType` | select | any | Full-time, Part-time, Contract, Temporary, Internship |
| `remote` | select | any | Remote or Hybrid |

> **Note:** the date filter cannot be combined with Job Type or Remote in the same search.

### Lookup mode (job keys)

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `jobKeys` | string[] | – | Indeed job keys to look up. Returns full data, including expired status |
| `country` | select | US | Country for the job lookup |

> When `jobKeys` is provided, regular search parameters are ignored.

### Advanced

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `searchMode` | select | basic | `basic`: fastest (1000+) · `detailed`: more data per job (1000+, slower) · `rich`: extra fields (~450 max) |
| `proxyConfig` | object | Apify datacenter | Residential proxies recommended to reduce blocking |

---

## Search Modes Explained

| Feature | Basic (default) | Detailed | Rich |
|---|---|---|---|
| Results | 1000+ | 1000+ | ~450 max |
| Speed | Fastest | Slower | Moderate |
| Hiring insights | No | Yes | No |
| Benefits & requirements | Pre-classified | Detailed (with strictness) | Pre-classified |
| Sponsored detection | No | No | Yes |
| Working hours | No | No | Yes |
| Salary source | Yes | Yes | Yes |
| Company branding | No | No | Yes |
| Employer-provided attributes | Yes | Yes | Yes |
| Click tracking URL | Yes | Yes | Yes |
| Employer responsiveness | Yes | Yes | Yes |
| Apply count | No | No | Yes |
| **Best for** | Maximum speed & coverage | In-depth job analysis | Competitive analysis |

---

## Sample Output Data (150+ Fields)

Every job listing is returned in clean, nested JSON.

**Classification & Skills**
```json
{
  "classification": {
    "jobType": ["Full-time"],
    "occupations": {
      "5NN53": "Software Development Occupations",
      "EHPW9": "Technology Occupations"
    },
    "skills": [
      { "key": "UJF52", "label": "AI" },
      { "key": "8PA9N", "label": "Full-stack development" },
      { "key": "XRFGF", "label": "Software architecture" },
      { "key": "7X6EH", "label": "MCP" },
      { "key": "Y72YJ", "label": "Debugging" }
    ]
  }
}
```

**Salary & Benefits**
```json
{
  "salary": {
    "text": "₹20,000.00 - ₹400,000.00 per month",
    "min": 20000,
    "max": 400000,
    "minCents": "2000000",
    "maxCents": "40000000",
    "currency": "INR",
    "period": "monthly",
    "source": "EXTRACTION",
    "estimated": false
  },
  "benefits": ["Paid time off", "Flexible schedule"]
}
```

**Location (with GPS)**
```json
{
  "location": {
    "formatted": "Sanpada, Navi Mumbai, Maharashtra",
    "fullAddress": "Sanpada, Navi Mumbai, Maharashtra",
    "city": "Navi Mumbai",
    "state": "Maharashtra",
    "stateName": "Maharashtra",
    "admin2Name": "Raigad District",
    "latitude": 19.06062,
    "longitude": 73.01396,
    "country": "IN"
  }
}
```

**Company Profile**
```json
{
  "company": {
    "name": "Infiny Webcom Pvt Ltd.",
    "key": "aa4afaf5982cb2d9",
    "tier": "FREE",
    "urls": {
      "indeed": "https://in.indeed.com/cmp/Infiny-Webcom-Pvt-Ltd.-1"
    },
    "ratings": {
      "overall": 4.2,
      "count": 15,
      "reviewCount": 8
    }
  }
}
```

---

## Limitations

- The date filter cannot be combined with Job Type or Remote filter in the same search (Indeed limitation).
- Company `ratings.count` is the number of star ratings; `ratings.reviewCount` is the number of written reviews — they often differ.
- Rich mode returns ~450 results max (Indeed's search limit).
- `isSponsored`, `applyCount`, and `employerResponsive` signals are only available in Rich mode.
- Hiring insights, detailed benefits, and requirements with strictness levels are only available in Detailed mode.

---

## Integrations

Works seamlessly with:

- Apify API
- Python
- JavaScript / Node.js
- Make (Integromat)
- Zapier
- n8n
- REST APIs
- Custom automation pipelines

---

## Support & Customization

Looking for a custom scraping solution, enterprise integration, or support with this actor? Reach out to us or explore more tools by MikoLabs:

👉 **[mikolabs.xyz](https://mikolabs.xyz)**
👉 **[Apify Store – mikolabs/indeed-scraper](https://apify.com/mikolabs/indeed-scraper)**

If you find this actor useful, consider ⭐ starring it and sharing it with others in the recruitment & data community.

---

## Keywords

Indeed Scraper, Indeed Jobs Scraper, Indeed API, Indeed Job API, Job Scraper, Job Data Extraction, Recruitment Data, HR Analytics, Salary Data, Lead Generation, Company Data, Hiring Intelligence, Job Board API, Job Market Analytics, Recruitment Automation, Apify Indeed Scraper, Indeed Jobs API, Employment Data, Hiring Trends, Job Listings API, GPS Job Data, Pre-Parsed Salary Scraper.

---

<p align="center">Built with ❤️ by <a href="https://mikolabs.xyz">MikoLabs</a></p>
