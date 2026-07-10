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
| **Semrush** | SEO | `mcp.semrush.com/v1/mcp` | API key / OAuth | keyword overview, domain analytics, backlinks, traffic, trends | Paid SEO plans+ |
| **Ahrefs** | SEO | `api.ahrefs.com/mcp/mcp` | API key | backlinks, organic keywords, rank tracking, site audit (42 tools) | Lite plan+ |
| **DataForSEO** | SEO | `mcp.dataforseo.com/mcp` | API credentials | SERP, Keywords Data, Labs, OnPage, Backlinks | Pay-as-you-go; best for programmatic SERP at scale |
| **Google Ads** | Ads | official `google-ads-mcp` server | OAuth | campaign & performance reporting | **Read-only** |
| **Meta Ads** | Ads | `mcp.facebook.com/ads` | OAuth | campaigns, ad sets, ads, insights (29 tools) | Beta (launched 2026) |
| **HubSpot** | CRM | `mcp.hubspot.com` | OAuth 2.1 / PKCE | contacts, companies, deals, lists, workflows, engagements | GA 2026; replaces the old "Composio-only" guidance |
| **Salesforce** | CRM | Salesforce-hosted MCP | OAuth | records, SOQL queries, reports | Enterprise Edition+; GA 2026 |
| **Stripe** | Payments | `mcp.stripe.com` | OAuth | customers, subscriptions, charges, invoices, balances (23 tools) | |
| **Klaviyo** | Email/SMS | `mcp.klaviyo.com/mcp` | OAuth | flows, campaigns, segments, metrics, profiles | |
| **Customer.io** | Email | see `docs.customer.io/ai/mcp` | API key | journeys, segments, broadcasts, CDP (read/write) | |
| **Apollo** | Prospecting | `mcp.apollo.io/mcp` | OAuth | people & org search, enrichment, sequences, tasks | Beta; paid plans. Available in this environment as a connector. |
| **PostHog** | Analytics / CRO | `mcp.posthog.com/mcp` | API key | insights, funnels, feature flags, experiments, session replay | Free, hosted |
| **Mixpanel** | Analytics | `mcp.mixpanel.com` | OAuth | events, funnels, retention, cohorts | GA 2026 |
| **Amplitude** | Analytics | official Amplitude MCP | OAuth | cohorts, charts, session replay, behavioral graph | |
| **Notion** | Docs / CMS | `mcp.notion.com/mcp` | OAuth | pages, databases, search | Also a **native Dust connector** — prefer that |
| **Slack** | Messaging | `mcp.slack.com` | OAuth | messages, channels, search | Also a **native Dust connector** — prefer that |
| **Zapier** | Automation | Zapier MCP endpoint | OAuth | actions across 8,000+ apps | Use for the long tail of app actions |
| **Firecrawl** | Scraping | official Firecrawl MCP | API key | scrape, crawl, map, extract | Single-target site extraction |
| **Exa** | AI Search | official Exa MCP | API key | search, find similar, contents | Neural web search for research |

---

## AI visibility / GEO MCP servers

The category the SEO team flagged (tracking whether your brand is cited in ChatGPT, Perplexity, Gemini, Claude, Copilot, and Google AI Overviews). Most serious players are now agent-native. Feeds the **ai-seo** skill.

| Tool | Server URL | Auth | Also has REST API? | Notes |
|------|------------|------|:------------------:|-------|
| **Profound** | `docs.tryprofound.com/mcp` (read-only) | OAuth | ✓ (+ TS/Python SDKs) | **Enterprise default.** Strongest programmatic stack; also tracks which AI bots crawl your own site. |
| **Otterly.ai** | official Otterly MCP | OAuth | ✓ | **SMB / agent-native default.** From ~$29 (no API) / $189 (API). Ships a published Claude Skill. |
| **Scrunch AI** | official Scrunch MCP | OAuth | ✓ | AI-search monitoring + optimization; enterprise CX angle. |
| **Rankscale** | `rankscale.ai/mcp` | OAuth | ✓ | Affordable, MCP-first; brand mentions + citation sources. |
| **Goodie** | Goodie MCP | — | — | GEO monitoring + optimization, AI-Overview emphasis. |

**Not agent-ready (dashboard-first):** **Peec AI** (popular, well-regarded UI — but API is enterprise-only beta and there is **no MCP**; use Browse for its dashboard), **ZipTie**, **LLMrefs** (has an API, no MCP), **Am I on AI**. **Incumbent shortcut:** if the team already pays for **Semrush** (AI Toolkit) or **Ahrefs** (Brand Radar), pull AI-visibility data through those before buying a point tool.

---

## Tools without a remote MCP — reach via native connector or Composio

For these, there is **no** remote server to add in Dust today. Use the path in the last column.

| Tool | Category | Situation | Reach from Dust |
|------|----------|-----------|-----------------|
| **GA4** | Analytics | Official MCP is **local/stdio** — a Dust cloud agent can't reach it | Native GA4 connector, or Composio |
| **Google Search Console** | SEO | **Community** MCP only (local) | Native connector if available, or Composio / Cogny |
| **Google Drive** | Storage | — | **Native Dust connector** (default) |
| **Mailchimp** | Email | **No official** server (Intuit); community MCP only | Composio (OAuth) |
| **LinkedIn Ads** | Ads | No official server; third-party only | Composio |
| **Meta Ads / Google Ads (write)** | Ads | Official servers are read-first | Composio for write-heavy campaign ops |

> **Composio** bridges 500+ OAuth tools behind one MCP server — the right fallback for anything above and for the long tail. See `../integrations/composio.md` and `../composio/marketing-tools.md`. **Cogny** is a marketing-only MCP gateway (Search Console, Bing, Semrush, LinkedIn/Reddit/TikTok Ads, Plausible, Fathom) — see `../integrations/cogny.md`.

---

## Keeping this current

MCP is moving fast — several of the servers above went GA or migrated endpoints in 2026, and the vendor's docs are the source of truth for the live URL and auth. When you refresh this file:

1. Verify each **official** server still resolves and note if it moved (SSE → streamable-HTTP migrations are common).
2. Promote any tool that ships a new remote server out of the "no remote MCP" table.
3. Mirror the change into the `MCP` column of `../REGISTRY.md` and the `## MCP server` subsection of the tool's integration guide.

This is the authoritative three-state (**official / community / composio**) classification; the `MCP` column in `REGISTRY.md` is a quick yes/no that links back here.