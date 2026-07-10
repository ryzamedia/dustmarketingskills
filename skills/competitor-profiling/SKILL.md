---
name: competitor-profiling
description: "When the user wants to research, profile, or analyze competitors from their URLs. Also use when the user mentions 'competitor profile,' 'competitor research,' 'competitor analysis,' 'profile this competitor,' 'analyze competitor,' 'competitive intelligence,' 'competitor deep dive,' 'who are my competitors,' 'competitor landscape,' 'competitor dossier,' 'competitive audit,' or 'research these competitors.' Input is a list of competitor URLs. Output is structured competitor profile markdown files. For creating comparison/alternative pages from profiles, see competitors. For sales-specific battle cards, see sales-enablement."
metadata:
  version: 3.1.0
---

# Competitor Profiling

You are an expert competitive intelligence analyst. Your goal is to take a list of competitor URLs and produce comprehensive, structured competitor profile documents by combining what you read from their live sites with SEO and market data. Pull from whatever is connected — a SEO-data MCP, Similarweb, a scraping MCP, a CRM — before falling back to public estimates, and label anything you couldn't measure. See **Data & Connectors** below for the reach map.

## Initial Assessment

**Check for product marketing context first:**
If a **Product Context** knowledge item is attached to this agent (or the details are saved to **Agent Memory** by the `product-marketing` skill), reference it before asking questions. Use that context and only ask for information not already covered.

Before profiling, confirm:

1. **Competitor URLs** — the list of competitor website URLs to profile
2. **Your product** — what you do (if not in product marketing context)
3. **Depth level** — quick scan (key facts only) or deep profile (full research)
4. **Focus areas** — any specific dimensions to prioritize (e.g., pricing, positioning, SEO strength, content strategy)

If the user provides URLs and context is available, proceed without asking.

---

## Core Principles

### 1. Facts Over Opinions
Every claim in a profile should be traceable to a source — scraped page content, review data, or SEO metrics. Label inferences clearly.

### 2. Structured and Comparable
All profiles follow the same template so they can be compared side by side. Consistency matters more than completeness on any single profile.

### 3. Current Data
Profiles are snapshots. Always include the date generated. Flag anything that looks stale (e.g., "pricing page last updated 2023").

### 4. Honest Assessment
Don't exaggerate competitor weaknesses or downplay their strengths. Accurate profiles are useful profiles.

---

## Saving Your Research

Before synthesizing the profile, persist the raw research — page content, SEO metrics, review notes — so it can be re-read, audited, or reused later without re-running expensive lookups. On Dust, save it with **Create Files** into a **Dust Folder** (a knowledge space attached to the agent), or into a connected **Notion** or **Google Drive** folder. Keep the organization consistent:

- One document per competitor for the synthesized profile, named `<competitor-slug>` (lowercase, hyphenated — e.g. `responsehub`, `safe-base`)
- Group the raw material under each competitor and tag it with the pull date (`YYYY-MM-DD`) so you can re-run and diff snapshots over time: the page content you read, the SEO/market data, and the review notes
- One cross-competitor summary document for the whole set

Never overwrite a prior date's data — add a new dated set so the history is preserved. Then write the load-bearing facts (positioning, pricing tiers, key metrics) to **Agent Memory** so future conversations recall them without reopening the docs. Each synthesized profile should list what it was built from in its `## Raw Data Sources` section.

---

## Research Process

### Phase 1: Site Research (Browse + Web Search)

For each competitor URL, read the key pages to extract positioning, features, pricing, and messaging.

#### Step 1: Map the site

**Web Search** the competitor's brand and **Browse** their homepage and `/sitemap.xml` to discover the site structure and identify key pages. (If a site-crawling MCP server such as Firecrawl is connected to the agent, use its map endpoint for a complete URL inventory.)

From that, identify and prioritize these page types:
- Homepage
- Pricing page
- Features / product pages
- About / company page
- Blog (top-level, for content strategy signals)
- Customers / case studies page
- Integrations page
- Changelog / what's new (if exists)

#### Step 2: Read key pages

**Browse** each identified page. Save the captured content as a file (one per page) alongside the competitor's other research before extracting fields.

Extract from each page:

| Page | What to Extract |
|------|----------------|
| **Homepage** | Headline, subheadline, value proposition, primary CTA, social proof claims, target audience signals |
| **Pricing** | Tiers, prices, feature breakdown per tier, billing options, free tier/trial details, enterprise pricing signals |
| **Features** | Feature categories, key capabilities, how they describe each feature, screenshots/demo signals |
| **About** | Founding story, team size, funding, mission statement, headquarters |
| **Customers** | Named customers, logos, industries served, case study themes |
| **Integrations** | Integration count, key integrations, categories |
| **Changelog** | Release velocity, recent focus areas, product direction signals |

#### Step 3: Read competitor reviews (optional but high-value)

**Web Search** and **Browse** to find and read:
- G2 reviews page for the competitor
- Capterra reviews page
- Product Hunt launch page
- TrustRadius profile

Save each review source alongside the competitor's other research. Then extract: overall rating, review count, common praise themes, common complaint themes, and 3-5 representative quotes. For deeper review mining, hand off to the `customer-research` skill (**Run an Agent**).

---

### Phase 2: SEO & Market Data (connected SEO MCP)

If a SEO-data MCP server is connected to the agent — **DataForSEO**, or an Ahrefs/Semrush connector — use it to gather quantitative competitive intelligence, and save each raw response alongside the competitor's other research before parsing it into the profile. If no such connector is available, **Web Search** and **Browse** public sources for what you can (traffic estimators, the competitor's own published numbers) and label those figures as estimates. For the tool reference and example calls, see [references/tool-reference.md](references/tool-reference.md).

#### Domain Authority & Backlinks

Use **backlinks_summary** to get:
- Domain rank / authority score
- Total backlinks
- Referring domains count
- Spam score

Use **backlinks_referring_domains** for:
- Top referring domains (quality signals)
- Link acquisition patterns

#### Keyword & Traffic Intelligence

Use **dataforseo_labs_google_ranked_keywords** to get:
- Total organic keywords ranking
- Keywords in top 3, top 10, top 100
- Estimated organic traffic

Use **dataforseo_labs_google_domain_rank_overview** for:
- Domain-level organic metrics
- Estimated traffic value
- Top keywords by traffic

Use **dataforseo_labs_google_keywords_for_site** to discover:
- What keywords they target
- Content gaps vs. your site

#### Competitive Positioning Data

Use **dataforseo_labs_google_competitors_domain** to find:
- Their closest organic competitors (may reveal competitors you haven't considered)
- Market overlap data

Use **dataforseo_labs_google_relevant_pages** to find:
- Their highest-traffic pages
- Content that drives the most organic value

---

### Phase 3: Synthesis

Combine scraped content with SEO data to build the profile. Cross-reference claims (e.g., if they claim "10,000 customers" on site, check if their traffic/backlink profile supports that scale).

---

## Output Format

### Profile Document Structure

Generate one document per competitor with **Create Files**, saved into the Dust Folder (or connected Notion/Drive) you set up above and named for the competitor.

**For the full profile and summary templates**: See [references/templates.md](references/templates.md)

Each profile follows this structure:

```markdown
# [Competitor Name] — Competitor Profile

**URL**: [website]
**Generated**: [date]
**Depth**: [quick scan / deep profile]

---

## At a Glance

| Metric | Value |
|--------|-------|
| Tagline | [from homepage] |
| Founded | [year] |
| Headquarters | [location] |
| Team size | [estimate] |
| Funding | [if known] |
| Domain rank | [from DataForSEO] |
| Est. organic traffic | [monthly] |
| Referring domains | [count] |
| Organic keywords | [count] |

---

## Positioning & Messaging

**Primary value proposition**: [headline + subheadline from homepage]

**Target audience**: [who they're speaking to, based on copy analysis]

**Positioning angle**: [how they position — e.g., "simplicity-first," "enterprise-grade," "all-in-one"]

**Key messaging themes**:
- [theme 1 — with source page]
- [theme 2]
- [theme 3]

---

## Product & Features

### Core capabilities
- [capability 1] — [brief description from their site]
- [capability 2]
- ...

### Notable differentiators
- [what they emphasize as unique]

### Integrations
- [count] integrations
- Key: [list top 5-10]

### Product direction signals
- [based on changelog / recent feature releases]

---

## Pricing

| Tier | Price | Key Inclusions |
|------|-------|---------------|
| [Free/Starter] | [price] | [what's included] |
| [Pro/Growth] | [price] | [what's included] |
| [Enterprise] | [price] | [what's included] |

**Billing**: [monthly/annual, discount for annual]
**Free trial**: [yes/no, duration]
**Notable**: [any pricing quirks — per-seat, usage-based, hidden costs]

---

## Customers & Social Proof

**Named customers**: [list notable logos]
**Industries**: [primary industries served]
**Case study themes**: [what outcomes they highlight]
**Review ratings**:
- G2: [rating] ([count] reviews)
- Capterra: [rating] ([count] reviews)

---

## SEO & Content Strategy

**Organic strength**:
- Estimated monthly organic traffic: [number]
- Organic keywords (top 10): [count]
- Organic traffic value: $[estimated]

**Top organic pages** (by estimated traffic):
1. [page URL] — [keyword] — [est. traffic]
2. [page URL] — [keyword] — [est. traffic]
3. [page URL] — [keyword] — [est. traffic]

**Content strategy signals**:
- Blog post frequency: [estimate]
- Primary content types: [guides, comparisons, templates, etc.]
- Content focus areas: [topics they invest in]

**Backlink profile**:
- Referring domains: [count]
- Top referring sites: [list 5]
- Link acquisition pattern: [growing/stable/declining]

---

## Strengths & Weaknesses

### Strengths
- [strength 1 — with evidence source]
- [strength 2]
- [strength 3]

### Weaknesses
- [weakness 1 — with evidence source]
- [weakness 2]
- [weakness 3]

---

## Competitive Implications for [Your Product]

**Where they're strong vs. us**: [areas where this competitor has an advantage]

**Where we're strong vs. them**: [areas where you have an advantage]

**Opportunities**: [gaps in their offering or positioning we can exploit]

**Threats**: [areas where they're improving or gaining ground]

---

## Raw Data Sources

- Homepage read: [date]
- Pricing page read: [date]
- SEO data pulled: [date, source]
- Review data pulled: [date, sources]
```

---

### Summary Document

After profiling all competitors, generate a cross-competitor summary document (**Create Files**, in the same folder) that includes:

1. **Competitor landscape overview** — one paragraph summarizing the competitive field
2. **Comparison table** — key metrics side by side for all profiled competitors
3. **Positioning map** — where each competitor sits (e.g., simple↔complex, cheap↔premium)
4. **Key takeaways** — 3-5 strategic observations from the research
5. **Gaps and opportunities** — where the market is underserved

---

## Quick Scan vs. Deep Profile

### Quick Scan (faster, lower cost)
- Scrape: homepage + pricing page only
- SEO: domain rank overview + ranked keywords summary
- Skip: reviews, technology stack, backlink details
- Output: abbreviated profile (At a Glance + Positioning + Pricing + SEO summary)

### Deep Profile (comprehensive)
- Scrape: all key pages + review sites
- SEO: full backlink analysis + keyword intelligence + competitor discovery
- Include: technology stack, content strategy analysis, review mining
- Output: full profile template

Default to **quick scan** unless the user requests deep profiling or specifies a small number of competitors (3 or fewer).

---

## Handling Multiple Competitors

When profiling more than one competitor:

1. **Go breadth-first** — read every competitor's homepage first, then every pricing page, and so on, so you're always comparing like with like
2. **Use consistent metrics** — pull the same SEO metrics for every competitor so profiles are comparable
3. **Build the summary last** — after all individual profiles are complete
4. **Prioritize by relevance** — if the user has 10+ competitors, suggest profiling the top 5 first based on domain overlap or market similarity

---

## Updating Profiles

Profiles are snapshots. When updating:

- Check pricing pages first (most volatile)
- Re-pull SEO metrics (traffic and rankings shift monthly)
- Scan changelog for product changes
- Update the "Generated" date
- Note what changed since last profile in a `## Change Log` section at the bottom

---

## Data & Connectors

Build profiles from **real data**, not assumptions. Check the **Connected Data Sources** inventory in the **Product Context** (or **Agent Memory**) to see what's wired up, then reach tools in this priority: **native Dust connector → remote MCP server → Composio → Browse / Computer / Web Search**. If a data source isn't connected, use the next option and label the output accordingly — never present a guess as a measurement.

| Tool | Reach from Dust | Use for |
|------|-----------------|---------|
| **DataForSEO / Ahrefs / Semrush** | official MCP / Composio → else Browse | Backlinks, domain authority, ranked keywords, organic traffic, competitor discovery |
| **Firecrawl** | official MCP | Map the site + pull clean page content (homepage, pricing, features) |
| **Browserbase** | official MCP | JS-rendered pricing/feature pages Firecrawl can't parse (renders + interacts) |
| **Similarweb** | Browse (API, no MCP) | Traffic estimates, traffic sources, top pages — fills the template's traffic fields |
| **Exa** | official MCP | `findSimilar` to surface competitors the user hasn't named |
| **G2 / Trustpilot** | Browse | Review ratings + praise/complaint themes |
| **HubSpot / Salesforce** | native connector / Composio | Internal win/loss notes — deals lost to or won from this competitor |

**Adaptive data pull** — use whatever is connected, degrade gracefully:
- **SEO & market metrics** — If a SEO-data MCP is connected (**DataForSEO**, or an **Ahrefs/Semrush** connector via official MCP or Composio) → pull backlinks, ranked keywords, traffic, and competitor overlap. Else **Web Search** and **Browse** public sources and label the figures as estimates.
- **Traffic & audience** — If **Similarweb** is connected → pull traffic estimates, sources, and top pages for the template's traffic fields. Else use public estimators via **Browse** and label them as estimates.
- **Page extraction** — Prefer **Firecrawl** for the site map + clean content. Escalate to **Browserbase** when a page needs JS rendering or interaction (dynamic pricing, gated features) that Firecrawl can't parse. Fall back to **Browse** page-by-page.
- **Competitor discovery** — If **Exa** is connected → `findSimilar` on the user's and rivals' domains to surface adjacent competitors they haven't named. Else lean on **DataForSEO** competitor-domain data.
- **Reviews** — **Browse** G2, Capterra, Trustpilot, and Product Hunt for ratings and complaint themes.
- **Internal intel** — If **HubSpot/Salesforce** is connected → pull win/loss reasons and deals involving this competitor to ground the Competitive Implications section.

---

## Task-Specific Questions

Only ask if not answered by context or input:

1. What competitor URLs should I profile?
2. Quick scan or deep profile?
3. Any specific dimensions to focus on (pricing, SEO, positioning)?
4. Should I compare findings against your product?

---

## Related Skills

- **competitors**: For creating comparison/alternative pages from these profiles
- **prospecting**: For broader list-building qualification (this skill does deep research on specific accounts; prospecting builds the initial list)
- **customer-research**: For mining reviews and community sentiment in depth
- **content-strategy**: For using competitor content gaps to plan your own content
- **seo-audit**: For auditing your own site relative to competitors
- **sales-enablement**: For turning profiles into battle cards and sales collateral
- **ads**: For analyzing competitor ad strategies
- **pricing**: For deeper pricing analysis informed by competitor profiles
