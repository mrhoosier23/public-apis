# Andrew's API Shortlist

A small, practical selection from the [Public APIs directory](README.md), chosen for Andrew's performer portfolio, music projects, accessible website design, and possible future experiments.

**Reviewed:** 2026-11-18  
**Status:** Research shortlist, not installed, connected, deployed, or tested against live API responses.  
**Scope:** Six recommended services. Each external API has its own terms and limits; inclusion here is not permission to integrate it into a project.

## Quick reference

| API | Best use | Access / cost | Priority |
| --- | --- | --- | --- |
| [NYC Open Data](#3-nyc-open-data) | NYC public datasets and local-data experiments | Public datasets can be queried without a token; app token recommended for higher limits | Useful for a specific project |


## NYC data

### 3. NYC Open Data

- **Documentation:** https://www.nyc.gov/opendata/get-started/user-guides/open-data-apis
- **What it provides:** Public city datasets accessed through the Socrata Open Data API (SODA), including local-government and civic data.
- **Where it might help:** A Brooklyn/NYC-focused data visualization or an explicitly scoped client project. This is a potential source, **not** an automatic feed for JARVIS operational state.
- **Authentication:** Public dataset requests can be made without an application token. A Socrata app token helps avoid sharing a smaller IP-based throttling pool; write/private access has different requirements.
- **Free / limits:** Public read access is available; requests without tokens can be throttled. NYC notes that some dataset requests return **1,000 rows by default** unless pagination or limits are specified. Check licensing and data definitions for the chosen dataset.
- **Documented dataset example (not executed):** NYC 311 Service Requests, 2020 to present, dataset ID `erm2-nwe9`.

```bash
curl 'https://data.cityofnewyork.us/resource/erm2-nwe9.json?$limit=5'
```

- **ChatGPT / Codex:** Research the dataset and schema in ChatGPT; use Codex to build a small read-only query or chart with source attribution and privacy checks, only for a defined project.
- **Check before integration:** Dataset freshness, pagination, correct column definitions, possible changes to SODA API versions, and whether public fields are suitable for the intended use.
- **Official sources:** [NYC API guide](https://www.nyc.gov/opendata/get-started/user-guides/open-data-apis) · [Application tokens and throttling](https://dev.socrata.com/docs/app-tokens) · [311 dataset](https://data.cityofnewyork.us/d/erm2-nwe9)


## How to use this shortlist safely

1. **Choose a project outcome first.** This file is a menu, not a request to implement all six.
2. **Check the original API docs again.** Source listings in [README.md](README.md) may contain outdated authentication, pricing, or endpoint fields.
3. **Start with a documented, read-only example.** The samples above were sourced from documentation and **were not live-tested**.
4. **Keep provider costs separate from OpenAI.** ChatGPT and Codex can help design or write an integration. Eligible OpenAI Pro API credits may pay for supported OpenAI API calls, **not** third-party API usage, hosting, or licensing.
5. **Protect secrets and third-party data.** Do not commit API tokens, private user records, or credentials to GitHub. Use existing authorized secret storage if integration is approved.
6. **Do not change a live site or JARVIS automatically.** A read-only discovery list is not authority to publish, deploy, install an MCP server, or change the Cloudflare-owned operational system.

## Tiny resume point

**If a portfolio design task is active:** Open [PickShade's contrast checker](https://pickshade.com/api), test one actual text/background color pair, and record the result. A useful first finish is **one tested color pair and a clear pass/fail or improvement target**. No system setup needed.
