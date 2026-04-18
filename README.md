# Glassdoor Job Scraper

Extract structured job listings from Glassdoor across 21 markets with salary data, filters, compact mode, and built-in change tracking.

**[Glassdoor Job Scraper - Salary & Reviews on Apify →](https://apify.com/blackfalcondata/glassdoor-job-scraper?fpr=1h3gvi)**

---

## Key features





**Search with filters** — Search by keyword and location. Filter by country, job type, remote filter, and more.

**Detail enrichment** — Fetch full job descriptions, salary data, employer profiles, contact information for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

**Change classification** — Track unchanged, expired, cross-run repost detection across runs. Build audit trails of how listings evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per listing to control output size and cost.

**Result cap** — Stop after N listings (up to 500). Set to 0 for the full catalog.

**Proxy support** — Route traffic through Apify Proxy or your own proxy group to avoid regional blocks and rate limits.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every listing returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases





**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from glassdoor.com on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from glassdoor.com.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired listings. Perfect for price-tracking, churn analysis, and alerting pipelines.

**Compensation benchmarking**
Aggregate salary ranges across roles, industries, and locations on glassdoor.com to inform pricing decisions, hiring plans, or candidate negotiations.

**AI / LLM training data**
Structured JSON per listing is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "software engineer",
  "maxResults": 50,
  "includeDetails": true
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Job search keywords. Use JSON array for multi-query. |
| `country` | enum | `"US"` | Which Glassdoor domain to search (21 markets). |
| `location` | string | — | City, state, or region. Use JSON array for multi-location. |
| `startUrls` | array | — | Direct Glassdoor search or job detail URLs. |
| `maxResults` | integer | `50` | Maximum total job listings to return. |
| `maxPages` | integer | `5` | Maximum SERP pages to scrape per search source. |
| `postedDays` | integer | — | Only return jobs posted within this many days. Snapped to nearest valid: 1, 3, 7, or 14. |
| `jobType` | enum | — | Filter by employment type. |
| `remoteFilter` | enum | — | Filter by remote work arrangement. |
| `radius` | integer | — | Radius around the location in miles/km (5, 10, 15, 25, 35, 50, or 100). Snapped to nearest valid value. |
| `sort` | enum | `"relevance"` | Sort results by relevance or posting date. |
| `includeDetails` | boolean | `true` | Fetch each job's detail page for full description, salary data, and company info. |
| `includeCompanyProfile` | boolean | `false` | Fetch company overview pages for industry, headcount, and more. |
| `compactMode` | boolean | `false` | Output only 12 core fields (jobId, title, company, location, salary, dates, URL). Ideal for AI agents and MCP workflows to reduce token usage. |
| `descriptionMaxLength` | integer | `0` | Truncate job descriptions to this many characters. Set to 0 for full descriptions. Useful for reducing output size in AI/LLM pipelines. |
| `incrementalMode` | boolean | `false` | Compare against previous run state. Requires stateKey. |
| `stateKey` | string | — | Stable identifier for the tracked search universe (e.g. "us-software-nyc"). |
| `emitUnchanged` | boolean | `false` | When incremental, also emit records that haven't changed. |
| `emitExpired` | boolean | `false` | When incremental, also emit records no longer found. |

---

## FAQ

<!-- WRITE: 4-6 Q&A pairs relevant to this product -->

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs, only new or changed listings are emitted — saving time, compute, and storage.

---

## Known limitations

<!-- WRITE: 4-6 honest limitations -->

- <!-- WRITE: limitation 1 -->
- <!-- WRITE: limitation 2 -->


## Output fields

Every listing returns the same 61-field schema. Missing values are `null` — never omitted.

- `jobId`
- `jobKey`
- `title`
- `company`
- `companyUrl`
- `location`
- `description`
- `descriptionHtml`
- `descriptionLength`
- `salaryText`
- `salaryMin`
- `salaryMax`
- `salaryCurrency`
- `salaryType`
- `employmentType`
- `postedDate`
- `validThrough`
- `canonicalUrl`
- `applyUrl`
- `requirements`
- `benefits`
- `portalUrl`
- `sourceUrl`
- `sourceCountry`
- `sourceDomain`
- `searchQuery`
- `searchUrl`
- `isSponsored`
- `locationCity`
- `locationRegion`
- `locationCountry`
- `postalCode`
- `isRemote`
- `locationFormatted`
- `companyRating`
- `companyReviewsCount`
- `companyLogoUrl`
- `scrapedAt`
- `detailFetched`
- `contentQuality`
- `extractedEmails`
- `latitude`
- `longitude`
- `companyIndustry`
- `companyEmployeeRange`
- `companyEmployeeRangeRaw`
- `companySectorNames`
- `companyRevenue`
- `companyFoundedYear`
- `companyHeadquarters`
- `companyWebsite`
- `companyOpenJobsCount`
- `companyDescription`
- `companyCeo`
- `changeType`
- `trackedHash`
- `firstSeenAt`
- `lastSeenAt`
- `previousSeenAt`
- `expiredAt`
- `stateKey`


## Sample output

One object per listing. Here is a real example from a production run:

```json
{
  "jobId": "a3ab7c825d9e6d2e3bfaa653dfdadb1c71b569453fe20ec70e9271e962a82dc2",
  "jobKey": "1010090472882",
  "title": "AI Manager",
  "company": "Leonard Truck & Trailer",
  "companyUrl": null,
  "location": "North Jackson, OH",
  "description": "Leonard Truck & Trailer is a family-owned and operated dealership specializing in trucks and trailers, established in 1963. We pride ourselves on building trusting relationships wi…",
  "descriptionHtml": "<p>Leonard Truck &amp; Trailer is a family-owned and operated dealership specializing in trucks and trailers, established in 1963. We pride ourselves on building trusting relations…",
  "descriptionLength": 2930,
  "salaryText": "USD 25.38–30.57 HOURLY",
  "salaryMin": 25.379808,
  "salaryMax": 30.570192
}
```

*Truncated — full records contain 61 fields. See Output fields for the complete schema.*


**[Try Glassdoor Job Scraper - Salary & Reviews now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/glassdoor-job-scraper?fpr=1h3gvi)**


## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.01 |
| Result | $0.002 |

See the [actor on Apify](https://apify.com/blackfalcondata/glassdoor-job-scraper?fpr=1h3gvi) for current pricing.

---

## Related products by Black Falcon Data





- [StepStone Scraper](https://apify.com/blackfalcondata/stepstone-scraper?fpr=1h3gvi) — Job listings from 18 European portals
- [Indeed Job Scraper](https://apify.com/blackfalcondata/indeed-job-scraper?fpr=1h3gvi) — Indeed job listings with salary data
- [Arbeitsagentur Scraper](https://apify.com/blackfalcondata/arbeitsagentur-scraper?fpr=1h3gvi) — Germany's official job portal (1M+ listings)
- [SEEK Scraper](https://apify.com/blackfalcondata/seek-scraper?fpr=1h3gvi) — Australia & NZ's largest job board
- [Naukri Scraper](https://apify.com/blackfalcondata/naukri-scraper?fpr=1h3gvi) — India's largest job portal
- [Bilbasen Scraper](https://apify.com/blackfalcondata/bilbasen-scraper?fpr=1h3gvi) — Denmark's largest car marketplace


## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. [Sign up free](https://console.apify.com/sign-up?fpr=1h3gvi) — $5 credit included
2. Open the actor and paste your input
3. Click Start — results download as JSON, CSV, or Excel

Need more volume? [See pricing](https://apify.com/pricing?fpr=1h3gvi).

---


## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---
---

*Last updated: 2026 03*
