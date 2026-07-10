# MCP Connection Registry

How to reach marketing tools from a **Dust agent** through the **Model Context Protocol (MCP)** — one place with the connection details a skill author or Dust admin actually needs: server URL, auth type, the key tools each server exposes, and whether Dust can add it at all.

This complements `../REGISTRY.md` (which tells you *which* tool to pick for a job) and `../integrations/{tool}.md` (endpoints and API detail). Here we answer only: **"How do I wire this up as an MCP server in Dust, and what does it give the agent?"**

---

## How Dust connects an MCP server

In Dust, you add a **remote MCP server** in the workspace (Tools / Connections → add a custom MCP server), then attach it to an agent. Adding one requires two things:

1. A **hosted server URL** (e.g. `https://mcp.hubspot.com`).
2. **Auth** — usually OAuth (you approve access in a popup) or an API key / header.

Once connected, the server's tools appear to the agent exactly like native Dust tools.

### Remote vs. local — the distinction a checkmark can't show

- **Remote / hosted MCP** — the vendor runs the server at a public URL. Dust (a cloud product) can connect it directly. ✅ **These are the ones you add in Dust.**
- **Local / stdio MCP** — the server runs as a process on your own machine (e.g. `npx some-mcp`). A Dust cloud agent **cannot** reach it. For these, use the **native Dust connector** if one exists, or **Composio** as the OAuth bridge.

When a tool only has a local/community server, the practical answer in Dust stays "native connector or Composio," not "add the MCP." Each row below says which case applies.

### Priority order when a tool has several paths

**Native Dust connector → official remote MCP → Composio → Browse / Computer.** Prefer a native connector when Dust ships one (deepest integration, managed auth). Otherwise an official remote MCP is usually the best and most current option. Fall back to Composio for the long tail and OAuth-heavy tools without a remote server, and to Browse/Computer when there's no API at all.

---

## Official remote MCP servers (add these directly in Dust)

These vendors host a public MCP endpoint. Auth is OAuth unless noted. Server URLs move as products graduate from beta — confirm against the vendor's current docs before wiring up.

| Tool | Category | Server URL | Auth | Key tools exposed | Notes |
|------|----------|------------|------|-------------------|-------|
| **Semrush** | SEO | `mcp.semrush.com/v2/mcp` | API key / OAuth | keyword, domain, backlinks, traffic, trends, **AI Visibility Toolkit** | Paid plans; ~50k API units/mo |
| **Ahrefs** | SEO | `api.ahrefs.com/mcp/mcp` | API key | backlinks, organic keywords, rank tracking, site audit (42 tools) | Lite plan+ |
| **DataForSEO** | SEO | `mcp.dataforseo.com/mcp` | API credentials | SERP, Keywords Data, Labs, OnPage, Backlinks | Pay-as-you-go; best for programmatic SERP at scale |
| **Meta Ads** | Ads | `mcp.facebook.com/ads` | OAuth | campaigns, ad sets, ads, insights (29 tools) | Beta (2026); read/write |
| **HubSpot** | CRM | `mcp.hubspot.com` | OAuth 2.1 / PKCE | contacts, companies, deals, lists, workflows, engagements | GA 2026; replaces the old "Composio-only" guidance |
| **Salesforce** | CRM | `api.salesforce.com/platform/mcp/v1/platform/<server>` | OAuth + PKCE | records, SOQL queries, reports | Enterprise Edition+; GA 2026 |
| **Stripe** | Payments | `mcp.stripe.com` | OAuth | customers, subscriptions, charges, invoices, balances (23 tools) | |
| **Klaviyo** | Email/SMS | `mcp.klaviyo.com/mcp` | OAuth | flows, campaigns, segments, metrics, profiles | |
| **Customer.io** | Email | `mcp.customer.io/mcp` (US) / `mcp-eu.customer.io/mcp` (EU) | OAuth | journeys, segments, broadcasts, CDP (read/write) | |
| **Apollo** | Prospecting | `mcp.apollo.io/mcp` | OAuth | people & org search, enrichment, sequences, tasks | ⚠️ Beta; inherits your Apollo plan's API/credit limits — full search/enrich effectively needs the **Organization tier** with API access, and it's flaky on lower plans. Prefer the REST API or Composio for reliable Dust use. |
| **PostHog** | Analytics / CRO | `mcp.posthog.com/mcp` | API key | insights, funnels, feature flags, experiments, session replay | Free, hosted |
| **Mixpanel** | Analytics | `mcp.mixpanel.com/mcp` | OAuth | events, funnels, retention, cohorts | Beta; an org admin must enable MCP first |
| **Amplitude** | Analytics | `mcp.amplitude.com/mcp` (US) / `mcp.eu.amplitude.com/mcp` (EU) | OAuth | cohorts, charts, session replay, behavioral graph | |
| **Outreach** | Sales Engagement | `api.outreach.io/mcp` | OAuth 2.1 | sequences, prospects, mailings, tasks | Requires Outreach **Amplify**; licensed users |
| **ZoomInfo** | Data Enrichment | `mcp.zoominfo.com/mcp` | OAuth | company/contact search, intent, enrichment | Requires **SalesOS or Copilot** subscription |
| **Truelist** | Email Verification | `api.truelist.io/mcp` | OAuth | bulk + single email deliverability validation | Hosted server |
| **Notion** | Docs / CMS | `mcp.notion.com/mcp` | OAuth | pages, databases, search | Also a **native Dust connector** — prefer that |
| **Slack** | Messaging | `mcp.slack.com/mcp` | OAuth + PKCE | messages, channels, search | Also a **native Dust connector** — prefer that |
| **Zapier** | Automation | `mcp.zapier.com/api/v1/connect` | OAuth | actions across 8,000+ apps | Per-user server; the long tail of app actions |
| **Firecrawl** | Scraping | `mcp.firecrawl.dev/{API_KEY}/v2/mcp` | API key (in path) | scrape, crawl, map, extract | Single-target site extraction |
| **Exa** | AI Search | `mcp.exa.ai/mcp` | API key (`x-api-key`) | search, find similar, contents | Neural web search for research |

---

## Prospecting & web-data MCP servers (incl. LinkedIn)

**LinkedIn itself ships no official MCP.** These third-party data providers do — the practical way to pull LinkedIn people/company data (and general web/SERP data) into a Dust agent. Respect each platform's ToS and local scraping law.

| Tool | Server URL | Auth | Exposes | Notes |
|------|------------|------|---------|-------|
| **Bright Data** | `mcp.brightdata.com/mcp?token=…` | API token | SERP, Web Unlocker scraping, Scraping Browser, 60+ structured datasets incl. **LinkedIn people / company / jobs / posts** | **Best default for LinkedIn prospecting at scale.** 5,000 free credits/mo, no card |
| **Apify** | `mcp.apify.com` (+ `apify.com/mcp/linkedin-mcp-server`) | OAuth / API token | thousands of Store actors incl. LinkedIn profile/company/email scrapers, SERP, maps | One MCP over the whole actor catalog |
| **HorizonDataWave (AnySite)** | `api.anysite.io/mcp/sse` | OAuth / API key | LinkedIn user search, profile lookup, email→profile, connections, light actions | Richest LinkedIn-specific search + email lookup |
| **PhantomBuster** | `mcp.phantombuster.com` | OAuth | run automations, LinkedIn visits/connection requests, lead-list building | Action-oriented (not just data pull); paid plan |
| **Nimble** | `mcp.nimbleway.com/mcp` | API key | multi-engine web search, extract, map, crawl (residential proxies) | General web data; LinkedIn only via generic scraping |

**Recommendation for LinkedIn prospecting**: **Bright Data** (data at scale, generous free tier) → **HorizonDataWave** (richest LinkedIn search + email) → **Apify** (actor flexibility) → **PhantomBuster** (when you need to *act* on LinkedIn, not just read). Pair any of these with **Truelist** to validate emails before outreach. Do **not** use **Proxycurl** — shut down in 2025 after a LinkedIn injunction.

---

## AI visibility / GEO MCP servers

The category the SEO team flagged (tracking whether your brand is cited in ChatGPT, Perplexity, Gemini, Claude, Copilot, and Google AI Overviews). Most serious players are now agent-native. Feeds the **ai-seo** skill.

| Tool | Server URL | Auth | Also has REST API? | Notes |
|------|------------|------|:------------------:|-------|
| **Profound** | `mcp.tryprofound.com/mcp` | OAuth | ✓ (+ TS/Python SDKs) | **Enterprise default.** Strongest programmatic stack; also tracks which AI bots crawl your own site. |
| **Otterly.ai** | `data.otterly.ai/mcp` | OAuth | ✓ | **SMB / agent-native default.** From ~$29 / $189 (API). Ships a published Claude Skill. |
| **Peec AI** | `api.peec.ai/mcp` | OAuth / PAT | ✓ (all paid plans) | The popular monitoring UI — it *does* have an MCP; available on every paid plan. |
| **Scrunch AI** | hosted (URL via `developers.scrunch.com/mcp/setup`) | OAuth | ✓ | AI-search monitoring + optimization; enterprise CX (Sitecore-owned). |
| **Rankscale** | connect at `rankscale.ai/mcp` | OAuth | ✓ | Affordable, MCP-first; brand mentions + citation sources. |
| **Goodie** | account-specific URL (from dashboard) | OAuth | — | GEO monitoring + optimization, AI-Overview emphasis. |
| **QuickSEO** | account setup URL | OAuth | ✓ | GEO **plus** unified Google Search Console metrics in one MCP; from $99/mo. |

**Not agent-ready (dashboard-first):** **ZipTie** (CSV export only — no API, no MCP), **LLMrefs** (API only, no MCP), **Am I on AI**. **Incumbent shortcut:** if the team already pays for **Semrush** (its MCP now serves the AI Visibility Toolkit) or **Ahrefs** (Brand Radar API + the parent Ahrefs MCP), pull AI-visibility data through those before buying a point tool.

---

## Tools without a remote MCP — reach via native connector or Composio

For these, there is **no** remote server to add in Dust today. Use the path in the last column.

| Tool | Category | Situation | Reach from Dust |
|------|----------|-----------|-----------------|
| **Google Ads** | Ads | Official MCP is **stdio/self-host-only**, read-only — Google hosts **no** remote endpoint | Self-host it and expose your own URL, or Composio |
| **GA4** | Analytics | Official MCP is **local/stdio** — a Dust cloud agent can't reach it | Native GA4 connector, or Composio |
| **Google Search Console** | SEO | **Community** MCP only (local) | Native connector if available, or Composio / Cogny |
| **Google Drive** | Storage | — | **Native Dust connector** (default) |
| **Mailchimp** | Email | No official **Marketing** MCP (campaigns/audiences) — community only. The one official MCP is **transactional-only** (Mandrill, `mandrillapp.com/mcp`) | Composio (OAuth) for the Marketing API |
| **Clay** | Enrichment | Official MCP exists (`api.clay.com/v3/mcp`) but is a **connector-directory** offering (Claude/ChatGPT/Codex) — not confirmed addable by plain URL | Clay REST API or Composio; test the URL first |
| **Introw** | Partner Ecosystem | **Marketplace-only** (Claude connector); no published addable remote URL | Reach its CRM data (HubSpot/Salesforce) via Composio |
| **LinkedIn Ads** | Ads | No official server; third-party only | Composio |

> **Composio** bridges 500+ OAuth tools behind one MCP server — the right fallback for anything above and for the long tail. See `../integrations/composio.md` and `../composio/marketing-tools.md`. **Cogny** is a marketing-only MCP gateway (Search Console, Bing, Semrush, LinkedIn/Reddit/TikTok Ads, Plausible, Fathom) — see `../integrations/cogny.md`.

---

## Keeping this current

MCP is moving fast — several of the servers above went GA or migrated endpoints in 2026, and the vendor's docs are the source of truth for the live URL and auth. When you refresh this file:

1. Verify each **official** server still resolves and note if it moved (SSE → streamable-HTTP migrations are common).
2. Promote any tool that ships a new remote server out of the "no remote MCP" table.
3. Mirror the change into the `MCP` column of `../REGISTRY.md` and the `## MCP server` subsection of the tool's integration guide.

This is the authoritative three-state (**official / community / composio**) classification; the `MCP` column in `REGISTRY.md` is a quick yes/no that links back here.