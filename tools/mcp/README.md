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

## Full catalog by marketing function

The table above is the quick-start essentials. The sections below add **many more official-remote servers** (addable directly in Dust), grouped by what a marketing agent uses them for. All verified against vendor docs on **2026-07-10** — endpoints move fast, so confirm before wiring up. A **⚠** marks servers that are official but access-gated (paid tier, waitlist, or provisioned per-account) — real, but not always freely addable. Each section ends with a note on notable **self-host / community / marketplace** options that a Dust *cloud* agent can't add directly.

### Analytics, product analytics & BI
Serves `analytics`, `cro`, `ab-testing`, `marketing-plan`, `revops`.

| Tool | Server URL | Auth | Use for |
|------|------------|------|---------|
| **Contentsquare** (Heap + Hotjar) | `api.contentsquare.com/mcp` | OAuth2 | Behavior/experience analytics, heatmaps, funnels — the MCP path for Hotjar/Heap users |
| **Statsig** | `api.statsig.com/v1/mcp` | OAuth | Experiments + feature gates end-to-end — best fit for `ab-testing` |
| **Pendo** | `app.pendo.io/mcp/visitor/shttp` (+ regional) | OAuth | Product-adoption + churn-signal analytics |
| **Fullstory** | `api.fullstory.com/mcp/fullstory` | OAuth | Session/behavior analysis for funnel friction |
| **Snowplow** | `console.snowplowanalytics.com/api/agent/mcp` | OAuth / key | Design + validate a tracking plan conversationally |
| **Matomo** | per-instance (Admin → Export → MCP) | token / OAuth | Privacy-first web analytics |
| **Airtable** | `mcp.airtable.com/mcp` | OAuth / PAT | Marketing-ops databases, editorial calendars |
| **Google BigQuery** | `bigquery.googleapis.com/mcp` | OAuth / IAM | Query the marketing warehouse (GA4 exports, spend, revenue) |
| **Snowflake** (Cortex) | per-account managed server | PAT / OAuth | Governed NL analytics over warehouse data |
| **Databricks** (Genie) | `<workspace>/api/2.0/mcp/genie/{space}` | OAuth / PAT | Lakehouse conversational analytics |
| **ClickHouse Cloud** | `mcp.clickhouse.cloud/mcp` | OAuth | Fast queries over event/clickstream data |
| **MotherDuck** / DuckDB | `api.motherduck.com/mcp` | token / OAuth | Lightweight warehouse + ad-hoc analysis |
| **Metabase** | `<your-metabase>/api/metabase-mcp` | user perms | Query + maintain existing dashboards |
| **Power BI** | `api.fabric.microsoft.com/v1/mcp/powerbi` | Entra OAuth | Query semantic models (preview) |
| **Looker** | per-instance managed | OAuth | Governed BI over the semantic model (preview) |
| **ThoughtSpot** | per-instance | OAuth | Agentic NL analytics + forecasting |
| **Cube** | per-deployment | OAuth | Consistent, governed KPI definitions |
| **Sigma** | per-org | OAuth | Search + query governed workbooks |
| **Hex** | per-workspace | OAuth | Notebook-style analyses on marketing data |
| **Airbyte** | `mcp.airbyte.ai/mcp` | OAuth | One gateway to 600+ connected data sources |
| **Hightouch** | vendor-hosted | OAuth | Reverse-ETL activation + agentic audience building |
| **RudderStack** | vendor-hosted | OAuth | Keep the CDP/event pipeline healthy |
| **Adobe CJA / Analytics** | Adobe-hosted | IMS OAuth | Enterprise cross-channel analytics |

*Self-host / community: Plausible, Umami, Fathom (usefathom), Segment, Fivetran, Google Sheets — official-or-community but local/stdio.*

### SEO & search data
Serves `seo-audit`, `programmatic-seo`, `content-strategy`, `competitor-profiling`, `ai-seo`.

| Tool | Server URL | Auth | Use for |
|------|------------|------|---------|
| **SISTRIX** | `api.sistrix.com/mcp/` | OAuth | Visibility Index + rankings + **AI-visibility** — no API key, no credit spend |
| **SE Ranking** | `api.seranking.com/mcp` | OAuth 2.1 | 160+ tools: keywords, backlinks, audits, AI search visibility |
| **Serpstat** | `serpstat.com/api/mcp/` | OAuth | SEO research + **AI Overview** monitoring |
| **Mangools** | `mcp.mangools.com/mcp` | token (`x-access-token`) | Affordable keyword/rank/backlink data |
| **SerpApi** | `mcp.serpapi.com/{API_KEY}/mcp` | API key | Raw multi-engine SERP data |
| **Similarweb** | `mcp.similarweb.com` | API key | Competitor traffic + market intelligence |
| **Oncrawl** | `mcp.oncrawl.com/mcp` | OAuth | Deep technical crawl audits (orphans, crawl diffs) |
| **Diffbot** | `mcp.diffbot.com/mcp?token=…` | token | Knowledge-graph enrichment + content extraction |
| **Google Trends** | `api.trendsmcp.ai/mcp` | Bearer | Demand/trend research (community-hosted; no official Trends API) |

*Self-host / community: Serper, Bing Webmaster Tools, AlsoAsked, Moz, Perplexity Sonar, Kagi, Frase, Screaming Frog (v24 built-in), seoClarity (⚠ enterprise-provisioned).*

### Advertising & ad analytics
Serves `ads`, `ad-creative`, `marketing-plan`. (Google Ads = stdio/self-host; Meta Ads is in the essentials table.)

| Tool | Server URL | Auth | Use for |
|------|------------|------|---------|
| **Windsor.ai** | `mcp.windsor.ai` | OAuth | Report **and write** (budgets/bids/campaigns) across Meta, Google, TikTok, LinkedIn, Microsoft Ads — one endpoint |
| **Two Minute Reports** | `mcp.twominutereports.com/mcp` | OAuth | Low-friction cross-channel ad **reporting** (30+ connectors incl. TikTok, Snapchat, X, Pinterest, Amazon) |
| **Polar Analytics** | `app.polaranalytics.com/mcp` | OAuth | Governed, citation-backed ecommerce cross-channel ROAS |
| **Optmyzr** | hosted (Settings → MCP Integration) | API key | Google + Microsoft Ads reporting **and** executable Rule-Engine optimizations |
| **Improvado** | `report.improvado.io/experimental/agent/api/mcp-customer/v1/invoke` | OAuth | Enterprise governed multi-source ad + attribution analysis |
| **TikTok Ads** ⚠ | TikTok-hosted (Agentic Hub, zero-code) | managed OAuth | First-party TikTok campaign management |
| **Amazon Ads** ⚠ | partner-provisioned | OAuth | First-party, write-capable Sponsored Ads (open beta, needs API partner creds) |
| **Omneky** ⚠ | announced (REST at `api.omneky.com`) | `X-API-Key` | Autonomous ad-creative (image + video) generation → `ad-creative` |

*Note: **Microsoft Advertising** and **Pinterest Ads** shipped official MCPs but both are read-only + waitlist/named-partner gated as of July 2026. **LinkedIn / Reddit / Snapchat / X Ads** have no first-party MCP — reach via Two Minute Reports, CData, or Zapier.*

### CRM, sales engagement & B2B enrichment
Serves `revops`, `prospecting`, `cold-email`, `sales-enablement`, `customer-research`. (HubSpot, Salesforce, Apollo, ZoomInfo, Outreach are in the essentials table.)

| Tool | Server URL | Auth | Use for |
|------|------------|------|---------|
| **Attio** | `mcp.attio.com/mcp` | OAuth | Modern CRM read/write + call-transcript/meeting search |
| **Close** | `mcp.close.com/mcp` | OAuth / key | SMB sales CRM + call-transcript mining |
| **Pipedrive** ⚠ | `mcp.pipedrive.ai/mcp` | OAuth | Pipedrive CRM read/write (beta) |
| **monday** | `mcp.monday.com/mcp` | OAuth | monday CRM + campaign/project boards |
| **Zoho CRM** ⚠ | provisioned at `zoho.com/mcp` | OAuth | Zoho CRM data + automation |
| **Amplemarket** | `mcp.amplemarket.com/mcp` | OAuth | Full outbound: prospect DB + enrich + sequences in one server |
| **lemlist** | `app.lemlist.com/mcp` | OAuth / key | Sequences + 450M-record prospecting DB + email find/verify |
| **Reply.io** | `mcp.reply.io` | key / OAuth | Multichannel outbound + AI-SDR ops |
| **La Growth Machine** | `mcp.lagrowthmachine.com/mcp` | OAuth / key | LinkedIn + email multichannel outreach |
| **Instantly** | `mcp.instantly.ai/mcp` | API key | Cold-email campaigns + deliverability + analytics |
| **Smartlead** | `mcp.smartlead.ai/sse?user_api_key=…` | key (in URL) | Cold-email campaign monitoring + deliverability (SSE) |
| **Lusha** | `mcp.lusha.com` | API key (`x-api-key`) | 100M+ contacts: enrichment + buyer-intent |
| **FullEnrich** | `mcp.fullenrich.com/mcp` | OAuth | Waterfall email/phone enrichment (20+ providers) |
| **Surfe** | `mcp.eu.surfe.com/mcp` | API key | Contact/company enrichment |
| **Prospeo** | `mcp.prospeo.io` | OAuth / key | Work-email + mobile finding, LinkedIn enrichment |
| **Hunter** | connect URL at `hunter.io/api-documentation#mcp` | API key | Email finding + verification + enrichment |
| **Warmly** | `opps-api.getwarmly.com/api/mcp` | OAuth / key | Website-visitor de-anonymization + third-party intent signals |
| **Seamless.ai** ⚠ | `mcp.seamless.ai/mcp` | OAuth / key | Sales-intelligence prospecting (MCP must be enabled on the account) |
| **Fireflies** | `api.fireflies.ai/mcp` | OAuth / key | Mine customer-interview & sales-call transcripts |

*⚠ Official but directory/enterprise-provisioned (no public paste-URL — same class as Apollo): **Gong** (per-workspace, Company Settings → Ecosystem → API), **Salesloft/Clari** (Claude connector directory). Self-host/community: RB2B, People Data Labs, Freshsales, Copper, Snov, Cognism (aggregator-only).*

### Email, SMS & lifecycle messaging
Serves `emails`, `sms`, `onboarding`, `churn-prevention`, `lead-magnets`, `launch`. (Klaviyo, Customer.io, Resend are in the essentials table.)

| Tool | Server URL | Auth | Use for |
|------|------------|------|---------|
| **Brevo** | `mcp.brevo.com/v1/brevo/mcp` | Bearer token | All-in-one email + SMS + WhatsApp + CRM (easiest headless auth) |
| **MoEngage** | `mcp.moengage.com` | OAuth | Enterprise cross-channel lifecycle (push/email/SMS/WhatsApp + flows) |
| **Kit** (ConvertKit) | `app.kit.com/mcp` | OAuth | Creator/newsletter email: subscribers, sequences, broadcasts |
| **MailerLite** | `mcp.mailerlite.com/mcp` | OAuth | SMB email marketing + automation building |
| **Omnisend** | `mcp.omnisend.com/mcp` | OAuth | Ecommerce email + SMS with revenue attribution |
| **Marketo** (Adobe) | `marketo-mcp.adobe.io/mcp` | client creds / IMS | Enterprise B2B automation + nurture (100+ ops) |
| **ActiveCampaign** | per-account remote URL | OAuth | Email + automation with CRM context |
| **beehiiv** | `mcp.beehiiv.com/mcp` | OAuth | Newsletter content, audience growth, monetization |
| **Courier** | `mcp.courier.com` | API key | Multi-channel messaging + templates (109 tools) |
| **Novu** | `mcp.novu.co` (EU: `eu.mcp.novu.co`) | OAuth / key | Notification/lifecycle infrastructure |
| **Knock** | `mcp.knock.app/mcp` | OAuth | Build multi-channel notification workflows |
| **Intercom** | `mcp.intercom.com/mcp` | OAuth | Mine support/lifecycle signals (US workspaces) |
| **Bloomreach** ⚠ | per-account `…/mcp` | OAuth | Enterprise CDP campaigns + personalization (gated) |
| **OneSignal** ⚠ | via Smithery bridge | App ID + key | Push/email/SMS + segments (interactive first-connect) |

*Note: **Twilio**'s remote MCP (`mcp.twilio.com/docs`) is docs/search only — it can't send. **Postmark**, **Mailgun**, **Iterable**, **Braze**, **SendGrid** are transactional and/or self-host/local. Aggregator-only: Drip, Attentive, Sendlane, Constant Contact, GetResponse. **Loops** MCP is "coming soon."*

### Payments, billing & subscriptions
Serves `pricing`, `paywalls`, `churn-prevention`, `offers`, `revops`. (Stripe is in the essentials table.)

| Tool | Server URL | Auth | Use for |
|------|------------|------|---------|
| **Paddle** | `mcp.paddle.com/mcp` (sandbox `sandbox-mcp.paddle.com/mcp`) | API key (Bearer) | Merchant-of-record billing: pricing models, revenue/refund reports, failed payments |
| **RevenueCat** | `mcp.revenuecat.ai/mcp` | key / OAuth | **Mobile-app** subscriptions + paywalls (Stripe/Paddle don't cover in-app) |
| **Polar.sh** | `mcp.polar.sh/mcp/polar-mcp` | token / OAuth | Developer-first MoR billing: products, subscriptions, checkouts |
| **Square** | `mcp.squareup.com/sse` | OAuth | Commerce: orders, customers, invoices, subscriptions |
| **PayPal** | `mcp.paypal.com` (`/sse` or `/http`) | OAuth | Invoices, transactions, orders, subscriptions, disputes |
| **Ramp** | `mcp.ramp.com/mcp` | OAuth | Marketing-spend + finance analytics (permission-aware, audit-logged) |
| **Mercury** | `mcp.mercury.com/mcp` | OAuth (read) | Cash/revenue-inflow lookups + reconciliation |
| **Brex** | `api.brex.com/mcp` | OAuth 2.1 / token | Expense + card-spend analysis |

*Self-host / local: Chargebee, Orb, Metronome, Lago, Stigg, ChartMogul, Baremetrics, Churnkey (best for `churn-prevention`), Recurly, Lemon Squeezy, QuickBooks, Xero. ⚠ Gated/undisclosed-endpoint: Maxio, Zuora.*

### CMS, commerce & content
Serves `programmatic-seo`, `seo-audit`, `schema`, `content-strategy`, `site-architecture`, `copywriting`, `image`.

| Tool | Server URL | Auth | Use for |
|------|------------|------|---------|
| **WordPress.com** | `public-api.wordpress.com/wpcom/v2/mcp/v1` | OAuth 2.1 | Run a WordPress content site by prompt (posts, pages, media) |
| **Webflow** | `mcp.webflow.com/mcp` | OAuth | CMS collections + on-page elements/styles |
| **Wix** | `mcp.wix.com/mcp` | OAuth | Site copy + CMS collections |
| **Contentful** | `mcp.contentful.com/mcp` | OAuth | Headless CMS content ops + AI Actions |
| **Sanity** | `mcp.sanity.io` | OAuth / token | GROQ queries + schema-aware content edits |
| **DatoCMS** | `mcp.datocms.com` | OAuth | Bulk content modeling + entry edits |
| **Storyblok** | `mcp.labs.storyblok.com/mcp` | token (PAT) | Component-based CMS management |
| **Hygraph** | `mcp-{region}.hygraph.com/{project}/{env}/mcp` | token | Query/publish GraphQL-native content |
| **Builder.io** | `mcp.builder.io/mcp/publish` | OAuth | Visual-CMS content + landing pages |
| **Shopify Storefront** | `{shop}.myshopify.com/api/mcp` | none (guest) | Live product/catalog + policy data for commerce copy & PDP SEO |
| **BigCommerce** | per-store (Settings → Early Access) | guest | Product catalog for storefront copy/SEO (beta) |
| **Saleor** | `mcp.saleor.app/mcp` | token | Read products, customers, orders |
| **Cloudinary** | `asset-management.mcp.cloudinary.com/mcp` (+ metadata/analysis) | OAuth2 | Media DAM: generate, transform, compress (WebP/OG), organize |
| **Frontify** | `mcp.frontify-integrations.com/mcp` | OAuth | Ground image/copy generation in approved brand assets + guidelines |
| **Optimizely CMS** | `cms.mcp.opal.optimizely.com/mcp` | OAuth | Manage CMS content (pairs with its Experimentation server) |
| **Adobe Experience Manager** | `mcp.adobeaemcloud.com/adobe/mcp/…` | Adobe OAuth | Enterprise content ops + DAM + brand governance |

*Self-host / local: Strapi, Directus, Contentstack, Kontent.ai, Payload, commercetools, WooCommerce, Prismic, Ghost, Sitecore. No MCP: Framer, Squarespace, Bynder.*

### Social, community & creative
Serves `social`, `community-marketing`, `image`, `video`, `ad-creative`. (In Dust, native **Create Images** covers basic raster generation — the model servers below add text-in-image, brand/vector, video, and audio.)

| Tool | Server URL | Auth | Use for |
|------|------------|------|---------|
| **Buffer** | `mcp.buffer.com/mcp` | OAuth | Cross-channel scheduling/publishing (LinkedIn, X, IG, TikTok, …) |
| **Postiz** | `api.postiz.com/mcp/{API_KEY}` | key | Scheduling across 30+ channels incl. Reddit/Discord/Bluesky/Mastodon |
| **Typefully** | `mcp.typefully.com/mcp?TYPEFULLY_API_KEY=…` | key | Thread/long-form drafting + scheduling |
| **Blotato** | `mcp.blotato.com/mcp` | OAuth / key | Agent-driven posting/repurposing across platforms |
| **Canva** | `mcp.canva.com/mcp` | OAuth | Editable, brand-consistent designs + template autofill |
| **Runway** | `mcp.runwayml.com/mcp` | OAuth | Marketing **image + video** (proxies Kling/Veo/Nano Banana) |
| **fal.ai** | `mcp.fal.ai/mcp` | API key | 1,000+ image/video/audio/speech models behind one key |
| **Replicate** | `mcp.replicate.com/sse` | token | Broad model catalog (FLUX, upscalers, video, transcription) |
| **Ideogram** | `mcp.ideogram.ai/mcp` | OAuth | Best-in-class **text-in-image** (posters, social/ad graphics) + brand training |
| **HeyGen** | `mcp.heygen.com/mcp/v1/` | OAuth | Avatar spokesperson / explainer / UGC-style video |
| **invideo** | `mcp.invideo.io/sse` | OAuth | Prompt → full video with script, stock, voiceover, subtitles |
| **Figma** | `mcp.figma.com/mcp` | OAuth | Design specs/assets for landing pages + creative |

*Self-host / community: Discord, Reddit, Bluesky, Mastodon, YouTube (all community); ElevenLabs (audio/voiceover), Recraft (vector/brand), Freepik, Shotstack (templated video), Pexels/Unsplash — official-or-community but local. Marketplace-only: Synthesia, Creatomate (via Zapier).*

### Marketing ops — project mgmt, forms, scheduling, storage, support
Serves delivery/planning across `marketing-plan`, `launch`, `customer-research`, `onboarding`, `content-strategy`. (Notion, Slack, Google Drive are native Dust connectors — prefer those.)

| Tool | Server URL | Auth | Use for |
|------|------------|------|---------|
| **Asana** | `mcp.asana.com/v2/mcp` | OAuth | GTM plans + cross-functional launch checklists |
| **Linear** | `mcp.linear.app/mcp` | OAuth | Campaign delivery + content pipeline as issues/projects |
| **Atlassian** (Jira/Confluence) | `mcp.atlassian.com/v1/mcp` | OAuth 2.1 | Campaign tickets + marketing knowledge base/briefs |
| **ClickUp** | `mcp.clickup.com/mcp` | OAuth | Content calendars + campaign task tracking |
| **Smartsheet** | `mcp.smartsheet.com` (EU/AU variants) | token | Campaign/budget/rollout trackers in grids |
| **Todoist** | `ai.todoist.net/mcp` | OAuth | Lightweight task capture for an operator |
| **Coda** | `coda.io/apis/mcp` | token | Living marketing docs/wikis + planning tables |
| **Box** | `mcp.box.com` | OAuth | Retrieve brand/creative assets from enterprise storage |
| **Dropbox** | `mcp.dropbox.com/mcp` | OAuth | Pull creative files + research docs |
| **Cal.com** | `mcp.cal.com/mcp` | OAuth 2.1 | Book demos + webinar slots |
| **Calendly** | `mcp.calendly.com` | OAuth | Availability + booking management |
| **Typeform** | `api.typeform.com/mcp` | OAuth | Pull survey responses for VOC; spin up research forms |
| **Tally** | `api.tally.so/mcp` | OAuth / key | Build lead-capture + research forms (free) |
| **Make.com** | `mcp.make.com/sse` | token / OAuth | Trigger cross-tool marketing automations |
| **Pipedream** | `mcp.pipedream.com/{user}/{app}` | OAuth | Reach 2,800+ long-tail SaaS apps |
| **Miro** | `mcp.miro.com` | OAuth | Campaign brainstorms + customer-journey maps |
| **Front** | `mcp.frontapp.com/mcp` | OAuth | Analyze shared-inbox conversations for research |
| **Help Scout** ⚠ | `mcp-beta.helpscout.net` | OAuth / PAT | Support-ticket + VOC analysis (beta) |

*Self-host / community: Trello, Basecamp, n8n (per-instance), Zendesk, Discourse, SurveyMonkey, Google Workspace Docs/Sheets. **Microsoft 365 / Dataverse** = preview, per-org.*

### Reviews, experimentation & events
Serves `cro`, `ab-testing`, `referrals`, `public-relations`, `customer-research`, `launch`, webinars.

| Tool | Server URL | Auth | Use for |
|------|------------|------|---------|
| **VWO** | `mcp.vwo.io/mcp` (EU/AS variants) | OAuth 2.0 | Read live CRO data **and create** A/B tests + heatmaps/recordings |
| **Optimizely Experimentation** | `exp.mcp.opal.optimizely.com/mcp` | OAuth | Query + manage Web/Feature experiments |
| **LaunchDarkly** | `mcp.launchdarkly.com/mcp/launchdarkly` | OAuth | Feature-flagged rollouts + experiment gating |
| **Birdeye** | hosted (in-product connect URL) | OAuth 2.0 | Reviews, ratings trends, NPS/CSAT survey data |
| **Zoom** | `mcp.zoom.us/mcp/zoom/streamable` | OAuth 2.1 | Webinar/event transcripts, recordings, recap docs |
| **Livestorm** | `mcp.livestorm.co/mcp/livestorm-mcp` | API key header | Webinar events, sessions, registrant data |
| **Press Ranger** ⚠ | hosted (one-click OAuth) | OAuth | Draft + distribute AI-optimized press releases (first PR-distribution MCP) |
| **G2** ⚠ | Claude connector directory | OAuth | Review + buyer-intent intelligence (connector-gallery only) |

*Self-host / community: Microsoft Clarity (free heatmaps), Yelp, Product Hunt, Sensor Tower + AppTweak (ASO), Refgrow (referrals), Everflow (⚠ private beta). No MCP found: Trustpilot, Capterra, Google Business Profile, PartnerStack, Refersion, Impact.com, Muck Rack, Prowly, Cision, Demio, AppFollow.*

### Web scraping, search & browser automation
Serves `competitor-profiling`, `customer-research`, `prospecting`, `content-strategy`, `ai-seo`. (Firecrawl, Exa, Bright Data, Apify are already cataloged above.)

| Tool | Server URL | Auth | Use for |
|------|------------|------|---------|
| **Tavily** | `mcp.tavily.com/mcp/` | OAuth / key | Best all-round AI web research (search + extract + crawl) |
| **Linkup** | `mcp.linkup.so/mcp` | API key | Sourced web answers with citations |
| **Jina AI** | `mcp.jina.ai/v1` (`/sse`) | API key | URL → clean markdown + web search + rerank |
| **ScrapingBee** | `mcp.scrapingbee.com/mcp` | API key (in URL) | Hosted proxy/CAPTCHA/JS scraping + retail extractors |
| **ScrapeGraphAI** | `mcp.scrapegraphai.com/mcp` | API key (`X-API-Key`) | AI-prompted structured extraction |
| **Scrapeless** | `api.scrapeless.com/mcp` | token | SERP + Google Trends + JS-heavy scraping + cloud browser |
| **Olostep** | `mcp.olostep.com/mcp` | API key | High-volume batch scraping (2–10k URLs) + search |
| **ZenRows** | `mcp.zenrows.com/mcp` | key / OAuth | Scrape or **drive** protected/JS-heavy sites (30+ browser tools) |
| **Browserless** | `mcp.browserless.io/mcp` | token / OAuth | Agentic browsing + **Lighthouse audits** + crawl |
| **Anchor Browser** | `api.anchorbrowser.io/mcp` | API key | Full cloud browser for multi-step tasks on gated sites |

*Self-host / local: Oxylabs, Crawlbase, Spider.cloud, AgentQL, Hyperbrowser, Steel.dev, Notte, Dumpling AI (YouTube transcripts + Google reviews), Perplexity, Kagi. Review-site data (G2/Trustpilot/Capterra) has no native MCP — reach via Apify or a scraping server against the review URL.*

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