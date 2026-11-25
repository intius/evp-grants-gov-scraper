# Grants.gov Scraper & Unofficial API (Python, Node.js, MCP)

[Run Grants.gov Scraper - Federal Grant Opportunities on Apify](https://apify.com/evpp/grants-gov) to export Grants.gov data as clean JSON, CSV, Excel, or an API feed. This repository is a developer quick-start kit with working Python and Node.js clients, an MCP configuration, a real sample dataset, and an n8n automation template.

[![Run on Apify](https://img.shields.io/badge/Run%20on-Apify-orange)](https://apify.com/evpp/grants-gov)

[Open the documentation and crawlable sample explorer](https://intius.github.io/evp-labs-data-extractors/actors/grants-gov/) for quick inputs, integration links, real sample rows, and ready-made task examples.

## Why use this Grants.gov scraper?

- Export Grants.gov data without building or maintaining a custom scraper
- Get flat, schema documented JSON ready for analytics, lead generation, market research, and AI agents
- Run manually, on a schedule, through the Apify API, or through MCP compatible AI tools
- Use the included 25+ row sample dataset to prototype before running the live Actor

Built for Grant writers/consultants, nonprofits, universities, SBIR applicants monitoring federal funding.

## Quick start on Apify

Open [https://apify.com/evpp/grants-gov](https://apify.com/evpp/grants-gov) and use this input:

```json
{
  "keyword": "infrastructure",
  "oppStatuses": [
    "posted"
  ],
  "includeDetails": true,
  "maxItems": 10
}
```

## Python

```bash
pip install -r requirements.txt
export APIFY_TOKEN=your_apify_token
python python/run.py
```

On Windows PowerShell, use `$env:APIFY_TOKEN="your_apify_token"` instead of `export`.

## Node.js

```bash
npm install
export APIFY_TOKEN=your_apify_token
node node/run.mjs
```

## MCP and AI agents

Add the hosted Apify MCP server from `mcp-config.json` to your MCP client:

```json
{
  "mcpServers": {
    "apify": {
      "type": "http",
      "url": "https://mcp.apify.com/?tools=evpp/grants-gov"
    }
  }
}
```

Then ask your agent to run `evpp/grants-gov`, inspect the output schema, or export the latest dataset. The direct MCP URL is `https://mcp.apify.com/?tools=evpp/grants-gov`.

For multi-source public data agents, use the [EVP Public Data MCP server](https://github.com/intius/evp-public-data-mcp). It is published in the Official MCP Registry as `io.github.intius/evp-public-data-mcp` and is also available as a one-click Claude Desktop MCPB release.

## n8n automation

Import `n8n-workflow.json` into n8n, select your Apify credential, replace the webhook placeholder, and activate the schedule. The workflow runs the Actor every morning and posts fresh dataset items to your webhook.

## Output schema

| Field | Type | Description |
|---|---|---|
| `opportunityId` | number | Grants.gov internal opportunity ID |
| `opportunityNumber` | string | Public funding opportunity number (FOA/NOFO number) |
| `title` | string | Opportunity title |
| `agency` | string | Grant-making agency or sub-agency name |
| `agencyCode` | string | Grants.gov agency code of the owning agency |
| `status` | string | Opportunity status (posted, forecasted, closed, archived) |
| `docType` | string | Document type on Grants.gov (synopsis, forecast, modification, package) |
| `postDate` | string | Date the synopsis was posted (YYYY-MM-DD) |
| `openDate` | string | Date the opportunity opened for applications (YYYY-MM-DD) |
| `closeDate` | string | Application due date (YYYY-MM-DD) |
| `closeDateText` | string | Free-text description of the deadline when the agency provides one (e.g. rolling submissions) |
| `awardCeiling` | number | Maximum award amount in USD |
| `awardFloor` | number | Minimum award amount in USD |
| `estimatedTotalFunding` | number | Estimated total program funding in USD |
| `numberOfAwards` | number | Expected number of awards |
| `cfdaList` | string[] | Assistance Listing (CFDA) numbers associated with the opportunity |
| `fundingInstrument` | string | Funding instrument types, joined when several apply (e.g. Grant; Cooperative Agreement) |
| `fundingCategory` | string | Funding activity categories, joined when several apply |
| `eligibilities` | string[] | Applicant types eligible to apply |
| `description` | string | Plain-text synopsis of the opportunity, trimmed to about 500 characters |
| `fundingLink` | string | Agency-provided link to the full funding announcement |
| `contactEmail` | string | Agency contact email for questions |
| `url` | string | Grants.gov opportunity detail page |

## Real sample output

The first sanitized row from the included sample dataset:

```json
{
  "opportunityId": 359325,
  "opportunityNumber": "23-589",
  "title": "Community Infrastructure for Research in Computer and Information Science and Engineering (CIRC)",
  "agency": "U.S. National Science Foundation",
  "agencyCode": "NSF",
  "status": "posted",
  "docType": "synopsis",
  "postDate": "2025-06-06",
  "openDate": "2025-06-06",
  "closeDate": "2027-09-10",
  "awardCeiling": 5000000,
  "awardFloor": 50000,
  "estimatedTotalFunding": 24000000,
  "numberOfAwards": 25,
  "cfdaList": [
    "47.075"
  ],
  "fundingInstrument": "Grant",
  "fundingCategory": "Science and Technology and other Research and Development",
  "eligibilities": [
    "Others (see text field entitled \"Additional Information on Eligibility\" for clarification)"
  ],
  "description": "The Community Infrastructure for Research in Computer and Information Science and Engineering (CIRC) program drives discovery and learning in the core disciplines of the three participating CISE divisions [Computing and Communication Foundations (CCF), Computer and Network Systems (CNS), and Information and Intelligent Systems (IIS)] of the Directorate for Computer and Information Science and Engineering (CISE) by funding the creation and enhancement of world-class research infrastructure. This...",
  "fundingLink": "http://www.nsf.gov/publications/pub_summ.jsp?ods_key=nsf23589",
  "url": "https://www.grants.gov/search-results-detail/359325"
}
```

## Files in this kit

| File | Purpose |
|---|---|
| `python/run.py` | Working Python Apify API example |
| `node/run.mjs` | Working Node.js Apify API example |
| `mcp-config.json` | MCP server configuration for AI agents |
| `sample-output.json` | First five sanitized sample rows |
| `dataset-snapshot.csv` | 25+ row evaluation snapshot |
| `DATASET_CARD.md` | Dataset documentation and provenance |
| `n8n-workflow.json` | Scheduled n8n automation template |

## Fresh data

This repository contains a static evaluation sample. For current data, run the live Actor: https://apify.com/evpp/grants-gov

## Responsible use

The Actor reads public data from `grants.gov`. Review the source site's terms and applicable privacy rules before production use.
