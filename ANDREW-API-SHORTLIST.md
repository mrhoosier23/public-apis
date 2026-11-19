# Andrew's API Shortlist

A small, practical selection from the [Public APIs directory](README.md), chosen for Andrew's performer portfolio, music projects, accessible website design, and possible future experiments.

**Reviewed:** 2026-11-18  
**Status:** Research shortlist, not installed, connected, deployed, or tested against live API responses.  
**Scope:** Six recommended services. Each external API has its own terms and limits; inclusion here is not permission to integrate it into a project.

## Quick reference

| API | Best use | Access / cost | Priority |
| --- | --- | --- | --- |
| [MusicBrainz](#1-musicbrainz) | Recording, artist, and release metadata | No key for public reads; free **noncommercial** use; commercial plan/permission required | Useful when needed |
| [Bandsintown](#2-bandsintown) | Show listings on an authorized artist's website | Artist-specific API key required; read-only and restricted to approved artist use | Conditional |
| [NYC Open Data](#3-nyc-open-data) | NYC public datasets and local-data experiments | Public datasets can be queried without a token; app token recommended for higher limits | Useful for a specific project |
| [Iconify](#4-iconify) | Icons for portfolio and client sites | Free hosted API with fair-use limits; icon-set licenses vary | **Use** |
| [PickShade](#5-pickshade) | Contrast checks, accessible palettes, design tokens | Free, no key; about 10 requests/second per IP | **Use** |
| [The Color API](#6-the-color-api) | Color conversions and palette generation | Public API, no key; precise rate limit not established | **Try** |

**Best first experiment:** Test a few existing performer-page colors with PickShade and compare a palette from The Color API. This is exploratory design QA, not a request to change the published site.

## Music and live performance

### 1. MusicBrainz

- **Documentation:** https://musicbrainz.org/doc/MusicBrainz_API
- **What it provides:** Public artist, release, recording, and relationship metadata, with JSON and XML output.
- **Where it might help:** Metadata reference or credits research for a music archive, jukebox, or discography. Do not treat community records as authoritative proof of Andrew's own performance credits.
- **Authentication:** No API key is required for public reads. Requests involving user information or submission require authentication.
- **Free / commercial terms:** The web service is free for noncommercial use. Commercial projects require checking MusicBrainz commercial access terms.
- **Rate limit:** At most **one call per second**; send a meaningful `User-Agent` with an application identifier and contact information.
- **Documented example (not executed):**

```bash
curl -H 'User-Agent: AndrewMusicResearch/0.1 (https://github.com/mrhoosier23)' \
  'https://musicbrainz.org/ws/2/artist/?query=artist%3A%22Bill%20Monroe%22&fmt=json&limit=3'
```

- **ChatGPT / Codex:** Codex can build a small, rate-limited lookup script if a project needs it. Ordinary research can also start with ChatGPT. The MusicBrainz API does not consume OpenAI API credits; any additional OpenAI calls would be billed separately.
- **Check before integration:** Attribution, data accuracy, actual project license classification, and whether the selected MusicBrainz entity resolves to the right performer or recording.
- **Official sources:** [API and access terms](https://musicbrainz.org/doc/MusicBrainz_API) · [Rate limits](https://musicbrainz.org/doc/MusicBrainz_API/Rate_Limiting)

### 2. Bandsintown

- **Documentation:** https://help.artists.bandsintown.com/en/articles/9186477-api-documentation
- **What it provides:** Artist profile information and events, including dates, venues, locations and ticket links.
- **Where it might help:** Showing future performance dates on an authorized artist's portfolio or band page, if that artist already maintains a Bandsintown profile and has authorized API access.
- **Authentication correction:** The upstream README says `No`, but **current Bandsintown documentation requires an API key linked to an artist**. The artist/team can obtain the key from Bandsintown for Artists. This does **not** grant general access to arbitrary artists.
- **Permitted scope:** Read-only. Keys generally cover one artist; multi-artist platforms must request separate approval. Bandsintown does not accept personal or educational API-key requests unrelated to authorized artist use.
- **Free / limits:** Artist API access is documented, but a general public free-access guarantee and numeric request limit were **not confirmed** during this review. Check current terms before building or publishing anything.
- **Documented request template (not executed):**

```text
GET https://rest.bandsintown.com/artists/{ARTIST_NAME}/events/?app_id={ARTIST_API_KEY}
```

- **ChatGPT / Codex:** Codex could create a read-only event-list component once artist ownership, permission, and key handling are verified. Never put an artist API key directly in public GitHub files or browser-visible code if the provider requires it to remain private.
- **Alternative:** A simple manually maintained upcoming-shows section is lower-maintenance if there's no existing Bandsintown artist account.
- **Official sources:** [Who can access the API](https://help.artists.bandsintown.com/en/articles/7053475-what-is-the-bandsintown-api) · [Examples and event fields](https://help.artists.bandsintown.com/en/articles/9186477-api-documentation)

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

## Website design and accessibility

### 4. Iconify

- **Documentation:** https://iconify.design/docs/api/
- **What it provides:** Open-source icon collections, icon search, JSON icon data, and SVG/CSS rendering.
- **Where it might help:** Consistent navigation and interface icons for the performer site and custom-coded client projects. It is an alternative or complement to a directly installed SVG icon set.
- **Authentication:** Public hosted API generally needs no key.
- **Free / limits:** Iconify provides free public servers with fair-use/anti-abuse limits. A precise public request-per-second quota was **not confirmed**. Self-hosting is possible but unnecessary for a small project.
- **Licenses:** Iconify aggregates icon packs with different licenses. Verify the chosen **icon set's** attribution and reuse obligations before publishing.
- **Documented example (not executed):**

```text
GET https://api.iconify.design/mdi/music.svg
```

- **ChatGPT / Codex:** Codex can add selected local SVG assets or an Iconify component to a custom-coded project. Prefer bundling a small stable set rather than depending on live icon requests at runtime.
- **Check before integration:** Icon-pack license, accessibility labels, visual consistency, and whether the existing site already includes an icon system.
- **Official sources:** [API](https://iconify.design/docs/api/) · [SVG rendering](https://iconify.design/docs/api/svg.html)

### 5. PickShade

- **Documentation:** https://pickshade.com/api
- **What it provides:** WCAG 2 and APCA contrast calculations, color conversion, palette audits, color-blindness checks, and design-token exports.
- **Where it might help:** Check colors on the performer portfolio, identify contrast failures, and produce consistent accessible design tokens for future site revisions.
- **Authentication:** No key or registration required for the documented API.
- **Free / limits:** Advertised as free; approximately **10 requests per second per IP** with short bursts. Exceeding limits returns HTTP 429 and `Retry-After`.
- **Documented example (not executed):**

```bash
curl 'https://pickshade.com/api/v1/check-contrast?text=%236b7280&background=%23ffffff'
```

- **ChatGPT / Codex:** Codex can call the API in a design QA script. PickShade also advertises an MCP endpoint: `https://pickshade.com/api/mcp`; configure it only in a compatible client and for an authorized workflow.
- **Check before integration:** Compare API results with actual interface states and WCAG requirements. Passing a numeric contrast test is not a substitute for keyboard, semantic, or screen-reader QA.
- **Official sources:** [API, examples, pricing and rate limit](https://pickshade.com/api) · [MCP instructions](https://pickshade.com/mcp)

### 6. The Color API

- **Documentation:** https://www.thecolorapi.com/docs
- **What it provides:** Color identification, names, format conversion, and palettes such as complementary, analogous, triadic and monochrome.
- **Where it might help:** Rapid brand color exploration and variations for a portfolio or music-release graphics. Use PickShade afterwards to check accessibility.
- **Authentication:** Public read API; no key required.
- **Free / limits:** The provider describes the API as open to all. A specific public-service rate limit or commercial SLA was **not established** here; confirm terms before high-volume production use.
- **Documented example (not executed):**

```text
GET https://www.thecolorapi.com/scheme?hex=3B82F6&mode=analogic&count=5
```

- **ChatGPT / Codex:** ChatGPT can help choose a direction; Codex can fetch and transform the palette into site CSS or design tokens after reviewing the generated colors.
- **Check before integration:** Brand fit and readability. A mathematically harmonious palette is not necessarily accessible or on-brand.
- **Official sources:** [Documentation](https://www.thecolorapi.com/docs) · [About and public access](https://www.thecolorapi.com/about)

## How to use this shortlist safely

1. **Choose a project outcome first.** This file is a menu, not a request to implement all six.
2. **Check the original API docs again.** Source listings in [README.md](README.md) may contain outdated authentication, pricing, or endpoint fields.
3. **Start with a documented, read-only example.** The samples above were sourced from documentation and **were not live-tested**.
4. **Keep provider costs separate from OpenAI.** ChatGPT and Codex can help design or write an integration. Eligible OpenAI Pro API credits may pay for supported OpenAI API calls, **not** third-party API usage, hosting, or licensing.
5. **Protect secrets and third-party data.** Do not commit API tokens, private user records, or credentials to GitHub. Use existing authorized secret storage if integration is approved.
6. **Do not change a live site or JARVIS automatically.** A read-only discovery list is not authority to publish, deploy, install an MCP server, or change the Cloudflare-owned operational system.

## Tiny resume point

**If a portfolio design task is active:** Open [PickShade's contrast checker](https://pickshade.com/api), test one actual text/background color pair, and record the result. A useful first finish is **one tested color pair and a clear pass/fail or improvement target**. No system setup needed.
