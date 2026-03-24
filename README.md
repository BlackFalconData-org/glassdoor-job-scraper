# Glassdoor Job Scraper

Extract structured job listings from Glassdoor across 21 markets with salary data, filters, compact mode, and built-in change tracking.

**[Run on Apify →](https://apify.com/blackfalcondata/glassdoor-job-scraper)**

---

## Key features

🔍 **Smart search with filters**

Search by keyword, location, and multiple filters. Smart input resolution ensures you always get results.

📄 **Detail enrichment**

Fetch full job descriptions, salary data, employer profiles, and contact information for each listing.

🔄 **Incremental mode**

Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured job listings from glassdoor on a schedule. Export to CSV, JSON, or directly to your database.

**Market research**
Monitor job listings, track trends, and analyze market dynamics with structured, deduplicated data from glassdoor.

**AI and LLM workflows**
Use compact mode and description truncation to feed data into AI agents, MCP servers, and LLM pipelines without exceeding token budgets.

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

---

## Related products by Black Falcon Data

| Product | Description |
|:--------|:------------|
| [StepStone Jobs API](https://github.com/BlackFalconData-org/stepstone-jobs-api) | Job listings from 18 European portals |
| [Company Jobs Tracker](https://github.com/BlackFalconData-org/company-jobs-tracker-api) | Track new/removed jobs per company |
| [Indeed Jobs Feed](https://github.com/BlackFalconData-org/indeed-jobs-feed) | Indeed job listings with salary data |
| [Glassdoor Jobs Feed](https://github.com/BlackFalconData-org/glassdoor-jobs-feed) | Glassdoor listings with company ratings |
| [Arbeitsagentur Jobs Feed](https://github.com/BlackFalconData-org/arbeitsagentur-jobs-feed) | Germany's federal job portal (1M+ listings) |
| [Naukri Jobs Feed](https://github.com/BlackFalconData-org/naukri-jobs-feed) | India's largest job portal |
| [Bilbasen Scraper](https://github.com/BlackFalconData-org/bilbasen-scraper) | Denmark's largest car marketplace |

---

*Last updated: 2026 03*
