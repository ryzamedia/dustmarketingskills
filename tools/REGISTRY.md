# Marketing Tools Registry

Quick reference for reaching marketing platforms from a **Dust agent** — so a skill can pull real data or take action, not just describe what to do.

## How to reach a tool from Dust

In priority order:

1. **Native Dust connector** — many tools (Slack, Notion, Google Drive, GitHub, GA4, Stripe, and more) connect directly in Dust as data sources / tools. Prefer these.
2. **Remote MCP server** — tools with an **MCP** ✓ below can be added to Dust as a remote MCP server, exposing their actions as agent tools. See **[tools/mcp/README.md](mcp/README.md)** for each server's URL, auth, and exposed tools — and for whether it's an *official remote* server (addable in Dust) or a *community/local* one (reach via native connector or Composio).
3. **Composio** — for OAuth-heavy tools without a native Dust server (HubSpot, Salesforce, Meta Ads, LinkedIn Ads, Google Sheets, Slack, Notion, and more), [Composio](integrations/composio.md) exposes them to Dust through a single MCP server.
4. **Browse / Computer** — when a tool has no API, connector, or MCP server, the agent can read its pages with **Browse** or operate its UI with **Computer**.

The columns below show what each tool supports. **MCP** ✓ means an MCP server exists; a **†** marks a community/local-only server a Dust cloud agent can't add directly (reach it via a native connector or Composio). See **[tools/mcp/README.md](mcp/README.md)** for the official / community / Composio breakdown, server URLs, and auth. The **CLI** column links to a zero-dependency reference script that documents the tool's API surface — a handy spec when configuring a connector or MCP. The `integrations/{tool}.md` guides cover endpoints, auth, and common operations.

---

## Tool Index

| Tool | Category | API | MCP | CLI | SDK | Guide |
|------|----------|:---:|:---:|:---:|:---:|-------|
| ga4 | Analytics | ✓ | ✓ | [✓](clis/ga4.js) | ✓ | [ga4.md](integrations/ga4.md) |
| mixpanel | Analytics | ✓ | ✓ | [✓](clis/mixpanel.js) | ✓ | [mixpanel.md](integrations/mixpanel.md) |
| amplitude | Analytics | ✓ | ✓ | [✓](clis/amplitude.js) | ✓ | [amplitude.md](integrations/amplitude.md) |
| posthog | Analytics | ✓ | ✓ | ✓ | ✓ | [posthog.md](integrations/posthog.md) |
| segment | Analytics | ✓ | - | [✓](clis/segment.js) | ✓ | [segment.md](integrations/segment.md) |
| adobe-analytics | Analytics | ✓ | - | [✓](clis/adobe-analytics.js) | ✓ | [adobe-analytics.md](integrations/adobe-analytics.md) |
| plausible | Analytics | ✓ | - | [✓](clis/plausible.js) | - | [plausible.md](integrations/plausible.md) |
| google-search-console | SEO | ✓ | - | [✓](clis/google-search-console.js) | ✓ | [google-search-console.md](integrations/google-search-console.md) |
| semrush | SEO | ✓ | ✓ | [✓](clis/semrush.js) | - | [semrush.md](integrations/semrush.md) |
| ahrefs | SEO | ✓ | ✓ | [✓](clis/ahrefs.js) | - | [ahrefs.md](integrations/ahrefs.md) |
| dataforseo | SEO | ✓ | ✓ | [✓](clis/dataforseo.js) | ✓ | [dataforseo.md](integrations/dataforseo.md) |
| keywords-everywhere | SEO | ✓ | - | [✓](clis/keywords-everywhere.js) | - | [keywords-everywhere.md](integrations/keywords-everywhere.md) |
| rankparse | SEO | ✓ | ✓ | [✓](clis/rankparse.js) | - | [rankparse.md](integrations/rankparse.md) |
| clearbit | Data Enrichment | ✓ | - | [✓](clis/clearbit.js) | ✓ | [clearbit.md](integrations/clearbit.md) |
| apollo | Data Enrichment | ✓ | ✓ | [✓](clis/apollo.js) | - | [apollo.md](integrations/apollo.md) |
| zoominfo | Data Enrichment | ✓ | ✓ | [✓](clis/zoominfo.js) | - | [zoominfo.md](integrations/zoominfo.md) |
| clay | Data Enrichment | ✓ | ✓† | [✓](clis/clay.js) | - | [clay.md](integrations/clay.md) |
| supermetrics | Data Aggregation | ✓ | ✓ | [✓](clis/supermetrics.js) | - | [supermetrics.md](integrations/supermetrics.md) |
| coupler | Data Aggregation | ✓ | ✓ | [✓](clis/coupler.js) | - | [coupler.md](integrations/coupler.md) |
| hubspot | CRM | ✓ | ✓ | ✓ | ✓ | [hubspot.md](integrations/hubspot.md) |
| salesforce | CRM | ✓ | ✓ | ✓ | ✓ | [salesforce.md](integrations/salesforce.md) |
| close | CRM | ✓ | - | [✓](clis/close.js) | - | [close.md](integrations/close.md) |
| stripe | Payments | ✓ | ✓ | ✓ | ✓ | [stripe.md](integrations/stripe.md) |
| paddle | Payments | ✓ | - | [✓](clis/paddle.js) | ✓ | [paddle.md](integrations/paddle.md) |
| rewardful | Referral | ✓ | - | [✓](clis/rewardful.js) | - | [rewardful.md](integrations/rewardful.md) |
| tolt | Referral | ✓ | - | [✓](clis/tolt.js) | - | [tolt.md](integrations/tolt.md) |
| dub-co | Links | ✓ | - | [✓](clis/dub.js) | ✓ | [dub-co.md](integrations/dub-co.md) |
| mention-me | Referral | ✓ | - | [✓](clis/mention-me.js) | - | [mention-me.md](integrations/mention-me.md) |
| partnerstack | Affiliate | ✓ | - | [✓](clis/partnerstack.js) | - | [partnerstack.md](integrations/partnerstack.md) |
| mailchimp | Email | ✓ | ✓† | [✓](clis/mailchimp.js) | ✓ | [mailchimp.md](integrations/mailchimp.md) |
| customer-io | Email | ✓ | ✓ | [✓](clis/customer-io.js) | ✓ | [customer-io.md](integrations/customer-io.md) |
| sendgrid | Email | ✓ | - | [✓](clis/sendgrid.js) | ✓ | [sendgrid.md](integrations/sendgrid.md) |
| resend | Email | ✓ | ✓ | [✓](clis/resend.js) | ✓ | [resend.md](integrations/resend.md) |
| sequenzy | Email | ✓ | ✓ | ✓ | - | [sequenzy.md](integrations/sequenzy.md) |
| nitrosend | Email | ✓ | ✓ | - | - | [nitrosend.md](integrations/nitrosend.md) |
| kit | Email | ✓ | - | [✓](clis/kit.js) | ✓ | [kit.md](integrations/kit.md) |
| beehiiv | Newsletter | ✓ | - | [✓](clis/beehiiv.js) | - | [beehiiv.md](integrations/beehiiv.md) |
| klaviyo | Email/SMS | ✓ | ✓ | [✓](clis/klaviyo.js) | ✓ | [klaviyo.md](integrations/klaviyo.md) |
| postmark | Email | ✓ | - | [✓](clis/postmark.js) | ✓ | [postmark.md](integrations/postmark.md) |
| brevo | Email/SMS | ✓ | - | [✓](clis/brevo.js) | ✓ | [brevo.md](integrations/brevo.md) |
| activecampaign | Email/CRM | ✓ | - | [✓](clis/activecampaign.js) | ✓ | [activecampaign.md](integrations/activecampaign.md) |
| twilio | SMS/Voice | ✓ | - | ✓ | ✓ | [twilio.md](integrations/twilio.md) |
| plivo | SMS/Voice | ✓ | - | - | ✓ | [plivo.md](integrations/plivo.md) |
| postscript | SMS | ✓ | - | - | - | [postscript.md](integrations/postscript.md) |
| attentive | SMS | ✓ | - | - | - | [attentive.md](integrations/attentive.md) |
| audiencetap | SMS/Email | ✓ | - | - | - | [audiencetap.md](integrations/audiencetap.md) |
| hunter | Email Outreach | ✓ | - | [✓](clis/hunter.js) | - | [hunter.md](integrations/hunter.md) |
| snov | Email Outreach | ✓ | - | [✓](clis/snov.js) | - | [snov.md](integrations/snov.md) |
| truelist | Email Verification | ✓ | ✓ | - | ✓ | [truelist.md](integrations/truelist.md) |
| github | Developer Intent | ✓ | - | [✓](clis/github-prospects.js) | ✓ | [github.md](integrations/github.md) |
| firecrawl | Site Scraping | ✓ | ✓ | - | ✓ | [firecrawl.md](integrations/firecrawl.md) |
| browserbase | Site Scraping | ✓ | ✓ | - | ✓ | [browserbase.md](integrations/browserbase.md) |
| lemlist | Email Outreach | ✓ | - | [✓](clis/lemlist.js) | - | [lemlist.md](integrations/lemlist.md) |
| instantly | Email Outreach | ✓ | - | [✓](clis/instantly.js) | - | [instantly.md](integrations/instantly.md) |
| google-ads | Ads | ✓ | ✓† | [✓](clis/google-ads.js) | ✓ | [google-ads.md](integrations/google-ads.md) |
| meta-ads | Ads | ✓ | ✓ | [✓](clis/meta-ads.js) | ✓ | [meta-ads.md](integrations/meta-ads.md) |
| linkedin-ads | Ads | ✓ | - | [✓](clis/linkedin-ads.js) | - | [linkedin-ads.md](integrations/linkedin-ads.md) |
| tiktok-ads | Ads | ✓ | - | [✓](clis/tiktok-ads.js) | ✓ | [tiktok-ads.md](integrations/tiktok-ads.md) |
| zapier | Automation | ✓ | ✓ | [✓](clis/zapier.js) | ✓ | [zapier.md](integrations/zapier.md) |
| hotjar | CRO | ✓ | - | [✓](clis/hotjar.js) | - | [hotjar.md](integrations/hotjar.md) |
| optimizely | A/B Testing | ✓ | - | [✓](clis/optimizely.js) | ✓ | [optimizely.md](integrations/optimizely.md) |
| calendly | Scheduling | ✓ | - | [✓](clis/calendly.js) | - | [calendly.md](integrations/calendly.md) |
| savvycal | Scheduling | ✓ | - | [✓](clis/savvycal.js) | - | [savvycal.md](integrations/savvycal.md) |
| typeform | Forms | ✓ | - | [✓](clis/typeform.js) | ✓ | [typeform.md](integrations/typeform.md) |
| intercom | Messaging | ✓ | - | [✓](clis/intercom.js) | ✓ | [intercom.md](integrations/intercom.md) |
| outreach | Sales Engagement | ✓ | ✓ | [✓](clis/outreach.js) | - | [outreach.md](integrations/outreach.md) |
| crossbeam | Partner Ecosystem | ✓ | ✓ | [✓](clis/crossbeam.js) | - | [crossbeam.md](integrations/crossbeam.md) |
| introw | Partner Ecosystem | - | ✓† | - | - | [introw.md](integrations/introw.md) |
| pendo | Product Analytics | ✓ | - | [✓](clis/pendo.js) | - | [pendo.md](integrations/pendo.md) |
| similarweb | Competitive Intelligence | ✓ | - | [✓](clis/similarweb.js) | - | [similarweb.md](integrations/similarweb.md) |
| exa | AI Search | ✓ | ✓ | [✓](clis/exa.js) | ✓ | [exa.md](integrations/exa.md) |
| firehose | Competitive Intelligence | ✓ | - | - | - | [firehose.md](integrations/firehose.md) |
| sparktoro | Audience Research | - | - | - | - | [sparktoro.md](integrations/sparktoro.md) |
| rb2b | Visitor Identification | ✓ | - | - | - | [rb2b.md](integrations/rb2b.md) |
| gong | Revenue Intelligence | ✓ | - | - | - | [gong.md](integrations/gong.md) |
| airops | AI Content | ✓ | - | [✓](clis/airops.js) | - | [airops.md](integrations/airops.md) |
| buffer | Social | ✓ | - | [✓](clis/buffer.js) | - | [buffer.md](integrations/buffer.md) |
| wistia | Video | ✓ | - | [✓](clis/wistia.js) | - | [wistia.md](integrations/wistia.md) |
| heygen | Video | ✓ | ✓ | - | ✓ | [heygen.md](integrations/heygen.md) |
| hyperframes | Video | - | - | ✓ | ✓ | [hyperframes.md](integrations/hyperframes.md) |
| trustpilot | Reviews | ✓ | - | [✓](clis/trustpilot.js) | - | [trustpilot.md](integrations/trustpilot.md) |
| g2 | Reviews | ✓ | - | [✓](clis/g2.js) | - | [g2.md](integrations/g2.md) |
| onesignal | Push | ✓ | - | [✓](clis/onesignal.js) | ✓ | [onesignal.md](integrations/onesignal.md) |
| demio | Webinar | ✓ | - | [✓](clis/demio.js) | - | [demio.md](integrations/demio.md) |
| livestorm | Webinar | ✓ | - | [✓](clis/livestorm.js) | - | [livestorm.md](integrations/livestorm.md) |
| shopify | Commerce | ✓ | - | ✓ | ✓ | [shopify.md](integrations/shopify.md) |
| wordpress | CMS | ✓ | - | ✓ | ✓ | [wordpress.md](integrations/wordpress.md) |
| webflow | CMS | ✓ | - | ✓ | ✓ | [webflow.md](integrations/webflow.md) |
| sanity | Headless CMS | ✓ | - | ✓ | ✓ | [sanity.md](integrations/sanity.md) |
| contentful | Headless CMS | ✓ | - | ✓ | ✓ | [contentful.md](integrations/contentful.md) |
| strapi | Headless CMS | ✓ | - | ✓ | ✓ | [strapi.md](integrations/strapi.md) |
| composio | Integration Layer | ✓ | ✓ | ✓ | ✓ | [composio.md](integrations/composio.md) |
| cogny | Integration Layer | - | ✓ | - | - | [cogny.md](integrations/cogny.md) |
| profound | AI Visibility | ✓ | ✓ | - | ✓ | [mcp](mcp/README.md) |
| otterly | AI Visibility | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| peec | AI Visibility | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| scrunch | AI Visibility | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| rankscale | AI Visibility | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| llmrefs | AI Visibility | ✓ | - | - | - | — |
| ideogram | Image Generation | ✓ | - | - | ✓ | — |
| flux | Image Generation | ✓ | - | - | ✓ | — |
| recraft | Image Generation | ✓ | - | - | ✓ | — |
| gpt-image | Image Generation | ✓ | - | - | ✓ | — |
| gemini-image | Image Generation | ✓ | - | - | ✓ | — |
| midjourney | Image Generation | - | - | - | - | — |
| canva | Design | ✓ | - | - | ✓ | — |
| figma | Design | ✓ | - | - | ✓ | — |
| discord | Community | ✓ | - | - | ✓ | — |
| circle | Community | ✓ | - | - | - | — |
| discourse | Community | ✓ | - | - | - | — |
| reddit | Community | ✓ | - | - | - | — |
| common-room | Community Analytics | ✓ | - | - | - | — |
| apptweak | ASO | ✓ | - | - | - | — |
| sensortower | ASO | ✓ | - | - | - | — |
| appfollow | ASO | ✓ | - | - | - | — |
| app-store-connect | ASO | ✓ | - | - | ✓ | — |
| google-play-console | ASO | ✓ | - | - | ✓ | — |
| revenuecat | Mobile Paywalls | ✓ | - | - | ✓ | — |
| superwall | Mobile Paywalls | ✓ | - | - | ✓ | — |
| optinmonster | Popups | ✓ | - | - | - | — |
| privy | Popups | ✓ | - | - | - | — |
| optimonk | Popups | ✓ | - | - | - | — |
| vwo | A/B Testing | ✓ | - | - | ✓ | — |
| launchdarkly | Feature Flags | ✓ | - | - | ✓ | — |
| statsig | Experimentation | ✓ | - | - | ✓ | — |
| microsoft-clarity | CRO | ✓ | - | - | - | — |
| zendesk | Support | ✓ | - | - | ✓ | — |
| capterra | Reviews | - | - | - | - | — |
| trustradius | Reviews | - | - | - | - | — |
| muckrack | PR | ✓ | - | - | - | — |
| prowly | PR | ✓ | - | - | - | — |
| qwoted | PR | - | - | - | - | — |
| featured | PR | - | - | - | - | — |
| crunchbase | Data | ✓ | - | - | ✓ | — |
| builtwith | Technographics | ✓ | - | - | - | — |
| wappalyzer | Technographics | ✓ | - | - | - | — |
| linkedin-sales-navigator | Prospecting | - | - | - | - | — |
| smartlead | Email Outreach | ✓ | - | - | - | — |
| profitwell | Subscription Analytics | ✓ | - | - | - | — |
| baremetrics | Subscription Analytics | ✓ | - | - | - | — |
| churnkey | Retention | ✓ | - | - | - | — |
| prosperstack | Retention | ✓ | - | - | - | — |
| chargebee | Billing | ✓ | - | - | ✓ | — |
| recurly | Billing | ✓ | - | - | ✓ | — |
| marketo | Marketing Automation | ✓ | - | - | ✓ | — |
| pardot | Marketing Automation | ✓ | - | - | ✓ | — |
| brand24 | Social Listening | ✓ | - | - | - | — |
| mention | Social Listening | ✓ | - | - | - | — |
| producthunt | Directories | ✓ | - | - | - | — |
| twitter-ads | Ads | ✓ | - | - | ✓ | — |
| bright-data | Web Data / LinkedIn | ✓ | ✓ | - | ✓ | [mcp](mcp/README.md) |
| apify | Web Scraping | ✓ | ✓ | - | ✓ | [mcp](mcp/README.md) |
| horizondatawave | LinkedIn Data | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| phantombuster | LinkedIn Automation | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| nimble | Web Data | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| quickseo | AI Visibility | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| tavily | Web Research | ✓ | ✓ | - | ✓ | [mcp](mcp/README.md) |
| sistrix | SEO | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| se-ranking | SEO | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| contentsquare | Analytics | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| windsor-ai | Ads | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| optmyzr | Ads | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| two-minute-reports | Ads | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| attio | CRM | ✓ | ✓ | - | ✓ | [mcp](mcp/README.md) |
| lusha | Data Enrichment | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| warmly | Visitor Identification | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| amplemarket | Sales Engagement | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| fireflies | Revenue Intelligence | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| mailerlite | Email | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| omnisend | Email/SMS | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| cloudinary | DAM | ✓ | ✓ | - | ✓ | [mcp](mcp/README.md) |
| runway | Video | ✓ | ✓ | - | ✓ | [mcp](mcp/README.md) |
| fal-ai | Image/Video/Audio | ✓ | ✓ | - | ✓ | [mcp](mcp/README.md) |
| birdeye | Reviews | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| airtable | Marketing Ops | ✓ | ✓ | - | ✓ | [mcp](mcp/README.md) |
| cal-com | Scheduling | ✓ | ✓ | - | ✓ | [mcp](mcp/README.md) |
| make | Automation | ✓ | ✓ | - | - | [mcp](mcp/README.md) |
| wix | CMS | ✓ | ✓ | - | ✓ | [mcp](mcp/README.md) |
| linear | Marketing Ops | ✓ | ✓ | - | ✓ | [mcp](mcp/README.md) |
| asana | Marketing Ops | ✓ | ✓ | - | ✓ | [mcp](mcp/README.md) |

**†** = an MCP server exists but is **not a plain remote server you can add in Dust** — it's local/stdio, self-host-only, or marketplace/connector-directory-only (e.g. **Google Ads** = stdio/self-host, read-only; **Clay** and **Introw** = Claude connector-directory). Reach these via a native connector or Composio. Rows marked **—** in the Guide column don't have a dedicated integration guide yet; reach them by the priority order above (native connector → MCP → Composio → Browse/Computer). See [tools/mcp/README.md](mcp/README.md) for the full MCP breakdown — including whether each server is official-remote (addable) vs. local/marketplace-only.

---

## By Category

### Analytics

Track user behavior, measure conversions, and analyze marketing performance.

| Tool | Best For | MCP Available |
|------|----------|:-------------:|
| **ga4** | Web analytics, Google ecosystem | ✓ |
| **mixpanel** | Product analytics, event tracking | - |
| **amplitude** | Product analytics, cohort analysis | - |
| **posthog** | Open-source analytics, session replay | - |
| **segment** | Customer data platform, routing | - |
| **adobe-analytics** | Enterprise analytics | - |
| **plausible** | Privacy-focused analytics | - |

**Agent recommendation**: Start with GA4 if using Google ecosystem. Use Mixpanel or Amplitude for deeper product analytics. Plausible for privacy-focused sites.

### SEO

Search engine optimization tools for keyword research, rank tracking, and site audits.

| Tool | Best For | Notes |
|------|----------|-------|
| **google-search-console** | Free, authoritative search data | Direct from Google |
| **semrush** | Competitive analysis, keyword research | Comprehensive |
| **ahrefs** | Backlink analysis, content research | Best for links |
| **dataforseo** | SERP tracking, backlinks, on-page audits | Comprehensive API |
| **keywords-everywhere** | Quick keyword research, traffic estimates | Credit-based |
| **rankparse** | Cheap, agent-friendly backlinks + domain data | Credit-based, MCP available |

**Agent recommendation**: Google Search Console is essential (free). Add Semrush or Ahrefs for competitive research. DataForSEO for programmatic SERP data. Keywords Everywhere for quick keyword lookups. RankParse for agent workflows where per-call cost matters — backlinks, domain authority, and tech stack at a fraction of enterprise pricing.

### CRM

Customer relationship management and sales tools.

| Tool | Best For | CLI Available |
|------|----------|:-------------:|
| **hubspot** | SMB, marketing + sales alignment | ✓ |
| **salesforce** | Enterprise, complex sales processes | ✓ |
| **close** | SMB, high-velocity sales | [✓](clis/close.js) |

**Agent recommendation**: HubSpot for startups/SMBs. Close for high-velocity inside sales. Salesforce for enterprise.

### Payments

Payment processing and subscription management.

| Tool | Best For | MCP Available |
|------|----------|:-------------:|
| **stripe** | SaaS subscriptions, developer-friendly | ✓ |
| **paddle** | SaaS billing with tax handling | - |

**Agent recommendation**: Stripe is the default for SaaS. Paddle for built-in tax compliance.

### Referral & Affiliate

Tools for referral programs, affiliate tracking, and partner management.

| Tool | Best For | Stripe Integration |
|------|----------|:------------------:|
| **rewardful** | Stripe-native affiliate programs | ✓ |
| **tolt** | SaaS affiliate programs | ✓ |
| **mention-me** | Enterprise referral programs | ✓ |
| **dub-co** | Link tracking, attribution | - |
| **partnerstack** | Enterprise partner programs | ✓ |

**Agent recommendation**: Rewardful or Tolt for Stripe-based SaaS. PartnerStack for enterprise partner programs. Dub.co for link attribution.

### Email

Email marketing, transactional email, and automation platforms.

| Tool | Best For | MCP Available |
|------|----------|:-------------:|
| **mailchimp** | SMB email marketing | ✓ |
| **customer-io** | Behavior-based messaging | - |
| **sendgrid** | Transactional email at scale | - |
| **resend** | Developer-friendly transactional | ✓ |
| **sequenzy** | Lifecycle email, sequences, transactional email | ✓ |
| **kit** | Creator/newsletter focused | - |
| **beehiiv** | Newsletter platform | - |
| **klaviyo** | E-commerce email + SMS | - |
| **postmark** | Deliverability-focused transactional | - |
| **brevo** | Email + SMS, popular in EU | - |
| **activecampaign** | Email automation + CRM | - |

**Agent recommendation**: Resend for transactional (dev-friendly). Sequenzy for lifecycle email, sequences, and agent-driven email marketing. Postmark for deliverability. Customer.io for advanced automation. Kit for creators. Beehiiv for newsletters. Klaviyo for e-commerce email/SMS. ActiveCampaign for email + CRM combo.

### SMS / Messaging

SMS and MMS marketing platforms and programmable messaging APIs.

| Tool | Best For | MCP Available |
|------|----------|:-------------:|
| **klaviyo** | DTC ecom already on Klaviyo email | - |
| **postscript** | Shopify DTC, SMS-first depth | - |
| **attentive** | Mid-market+ DTC, full-service | - |
| **twilio** | Custom API builds, transactional, dev-first | - |
| **plivo** | Twilio alternative, lower per-send cost | - |
| **audiencetap** | DTC with AI-forward creative + on-pack QR opt-in | - |
| **brevo** | EU SMB email + SMS combo | - |
| **customer-io** | Behavior-based SMS automation | - |

**Agent recommendation**: Klaviyo SMS for ecom already on Klaviyo email. Postscript for Shopify-first depth. Attentive for mid-market+ wanting concierge support. Twilio (or Plivo for lower cost) for custom builds and transactional/auth. AudienceTap when AI creative or on-pack QR opt-in matters.

### Advertising

Paid advertising platforms and campaign management.

| Tool | Best For | MCP Available |
|------|----------|:-------------:|
| **google-ads** | Search intent, high-intent traffic | ✓ |
| **meta-ads** | Demand gen, visual products, B2C | - |
| **linkedin-ads** | B2B, job title targeting | - |
| **tiktok-ads** | Younger demographics, video | - |

**Agent recommendation**: Google Ads for search intent. Meta for demand generation. LinkedIn for B2B.

### Automation

Workflow automation and integration platforms.

| Tool | Best For | MCP Available |
|------|----------|:-------------:|
| **zapier** | No-code integrations + SDK for 8,000+ apps | ✓ |

**Agent recommendation**: Zapier SDK for agents that need to interact with any app directly. Zaps for always-on automations.

### CRO & A/B Testing

Conversion rate optimization, heatmaps, and experimentation.

| Tool | Best For | Notes |
|------|----------|-------|
| **hotjar** | Heatmaps, recordings, surveys | Visual behavior data |
| **optimizely** | A/B testing, feature flags | Enterprise experimentation |

**Agent recommendation**: Hotjar for understanding user behavior. Optimizely for running experiments.

### Scheduling

Booking and appointment scheduling tools.

| Tool | Best For | Notes |
|------|----------|-------|
| **calendly** | Meeting scheduling, lead gen | Most popular |
| **savvycal** | Personalized scheduling | Developer-friendly |

**Agent recommendation**: Calendly for general use. SavvyCal for personalized booking experiences.

### Forms & Surveys

Form builders and survey platforms.

| Tool | Best For | Notes |
|------|----------|-------|
| **typeform** | Interactive forms, surveys | Conversational UX |

**Agent recommendation**: Typeform for engaging forms and surveys.

### Messaging

In-app messaging, chat, and customer communication.

| Tool | Best For | Notes |
|------|----------|-------|
| **intercom** | In-app messaging, support, product tours | Full customer platform |

**Agent recommendation**: Intercom for in-app messaging and customer support.

### Social Media

Social media scheduling, management, and analytics.

| Tool | Best For | Notes |
|------|----------|-------|
| **buffer** | Social scheduling, analytics | Multi-platform |

**Agent recommendation**: Buffer for scheduling and analytics across social platforms.

### Video

Video hosting, creation, and AI generation.

| Tool | Best For | Notes |
|------|----------|-------|
| **wistia** | Video hosting, marketing analytics | Best for marketing video hosting |
| **heygen** | AI avatars, talking-head videos | MCP server available |
| **hyperframes** | Programmatic video from HTML/CSS | Open source, agent-native |

**Agent recommendation**: HeyGen for AI avatar videos (MCP-enabled). Hyperframes for templated, data-driven video from code. Wistia for hosting and analytics.

### Data Enrichment

Company and person data enrichment for sales and marketing.

| Tool | Best For | Notes |
|------|----------|-------|
| **clearbit** | Company/person enrichment | Now HubSpot Breeze |
| **apollo** | B2B prospecting, email finding | Large database |
| **zoominfo** | B2B contacts, intent data | Enterprise-grade |
| **clay** | Waterfall enrichment, outbound | 75+ data providers |

**Agent recommendation**: Clearbit for enrichment. Apollo for prospecting and outbound. ZoomInfo for enterprise B2B data with intent signals. Clay for waterfall enrichment across multiple providers.

### Email Verification

Pre-outreach email deliverability validation.

| Tool | Best For | Notes |
|------|----------|-------|
| **truelist** | Bulk + single email deliverability validation | Returns `email_state` (ok / email_invalid / risky / unknown / accept_all) + `email_sub_state`. MCP server + 7-language SDKs available. |

**Agent recommendation**: Truelist for any prospect list before outreach — Apollo/ZoomInfo/Hunter data accuracy is typically 60–80%, validation is non-negotiable to keep sender reputation healthy.

### Developer Intent / GitHub

Discovery channel for dev-tool SaaS prospecting via GitHub stargazers, forkers, and watchers.

| Tool | Best For | Notes |
|------|----------|-------|
| **github** | Stargazers / forks / watchers of competitor or adjacent repos | Public API; pair with Apollo/Clay/Hunter for email enrichment |

**Agent recommendation**: Use `github-prospects.js` CLI to pull stargazers/forks of 3–5 anchor repos (competitors, category leaders, complementary tools). Filter to users with `company` field set, then enrich missing emails via Apollo or Hunter, then validate via Truelist before outreach.

### Site Scraping (single-target only)

Programmatic page extraction for **individual public business sites** — not for the platforms hosting prospects (Google Maps, LinkedIn, Yelp, Apollo, etc.).

| Tool | Best For | Notes |
|------|----------|-------|
| **firecrawl** | Page → clean markdown / structured extraction | API + MCP; lower overhead for "just give me the content" |
| **browserbase** | Real Chromium when rendering, interaction, or session state is required | API + MCP (Stagehand); use when Firecrawl can't handle the page |

**Agent recommendation**: Default to Firecrawl for static-ish pages and structured extraction. Use Browserbase when the site requires JS rendering, form interaction, cookie consent, or auth — and when you want session recordings for debugging. **For both: discovery happens on platforms (manual browser); extraction happens on the prospect's own website URL.** For platform data like LinkedIn, use the purpose-built providers below instead.

### Web Data & LinkedIn Prospecting

Structured web, SERP, and LinkedIn data at scale, via official MCP servers with managed proxies — the right tools for platform data that Firecrawl/Browserbase shouldn't touch. **LinkedIn itself ships no official MCP; these are third-party providers — respect each platform's ToS and local scraping law.**

| Tool | Best For | Agent Reach |
|------|----------|-------------|
| **bright-data** | LinkedIn people/company/jobs datasets, SERP, page unlocking at scale | **Official MCP** + API; 5k free credits/mo |
| **apify** | LinkedIn + thousands of scraper actors through one MCP | **Official MCP** + API |
| **horizondatawave** | LinkedIn search + profile + email lookup | **Official MCP** + API |
| **phantombuster** | LinkedIn automation + lead-list building (action, not just data) | **Official MCP**; paid plan |
| **nimble** | General multi-engine web search / extract / crawl | **Official MCP** + API |

**Agent recommendation**: For LinkedIn prospecting from a Dust agent, default to **Bright Data** (scale + generous free tier), then **HorizonDataWave** (richest LinkedIn search + email), **Apify** (actor flexibility), or **PhantomBuster** (to *act* on LinkedIn). Validate emails with **Truelist** before outreach. **Proxycurl is dead** (LinkedIn injunction, 2025) — don't use it. See [tools/mcp/README.md](mcp/README.md).

### Reviews

Review management and social proof platforms.

| Tool | Best For | Notes |
|------|----------|-------|
| **trustpilot** | Consumer business reviews | Most recognized |
| **g2** | Software/B2B reviews | Best for SaaS |

**Agent recommendation**: Trustpilot for consumer products. G2 for B2B software.

### Push Notifications

Push notification delivery platforms.

| Tool | Best For | Notes |
|------|----------|-------|
| **onesignal** | Multi-channel push notifications | Web + mobile |

**Agent recommendation**: OneSignal for web and mobile push notifications.

### Webinar

Webinar and virtual event platforms.

| Tool | Best For | Notes |
|------|----------|-------|
| **demio** | Marketing webinars | Simple, focused |
| **livestorm** | Video engagement, webinars | Full event platform |

**Agent recommendation**: Demio for marketing-focused webinars. Livestorm for full event engagement.

### Sales Engagement

Sales engagement and outreach automation platforms.

| Tool | Best For | Notes |
|------|----------|-------|
| **outreach** | Enterprise sales engagement | Sequences, tasks, analytics |

**Agent recommendation**: Outreach for enterprise sales teams managing multi-touch sequences at scale.

### Product Analytics

Product analytics, feature adoption tracking, and in-app guidance.

| Tool | Best For | Notes |
|------|----------|-------|
| **pendo** | Feature adoption, in-app guides | Product-led growth |

**Agent recommendation**: Pendo for tracking feature adoption and delivering targeted in-app guidance.

### Competitive Intelligence

Traffic analytics, competitor benchmarking, and market research.

| Tool | Best For | Notes |
|------|----------|-------|
| **similarweb** | Website traffic, competitor analysis | Traffic sources, keywords |

**Agent recommendation**: Similarweb for competitor traffic analysis and market benchmarking.

### Audience Research

Audience intelligence and behavioral research tools.

| Tool | Best For | Notes |
|------|----------|-------|
| **sparktoro** | Audience affinities, behavioral data | Clickstream + social data |

**Agent recommendation**: SparkToro for discovering where your ICP spends time — what they read, watch, listen to, follow, and search for. Essential for customer research, content strategy, and media buying decisions.

### Visitor Identification

Website visitor de-anonymization for B2B sales and marketing.

| Tool | Best For | Notes |
|------|----------|-------|
| **rb2b** | Person-level visitor ID, intent signals | LinkedIn profiles, emails, page-level data |

**Agent recommendation**: RB2B for identifying anonymous B2B website visitors and routing high-intent visitors to outreach tools. Pairs well with Clay for enrichment and Instantly/Lemlist for cold email.

### Revenue Intelligence

Sales conversation analytics, call recording, and deal intelligence.

| Tool | Best For | Notes |
|------|----------|-------|
| **gong** | Call recording, transcript analysis, deal insights | REST API, 10k API calls/day |

**Agent recommendation**: Gong for mining sales call transcripts for customer research, competitive intelligence, and coaching insights. Essential for revenue attribution and win/loss analysis.

### AI Content

AI-powered content generation and optimization platforms.

| Tool | Best For | Notes |
|------|----------|-------|
| **airops** | AI content workflows, SEO content | Flow-based automation |

**Agent recommendation**: AirOps for building AI content workflows that generate SEO-optimized content at scale.

### AI Search

AI-powered web search APIs built for LLMs and agents. Return structured results with on-demand text, highlights, and summaries.

| Tool | Best For | Notes |
|------|----------|-------|
| **exa** | Neural/semantic web search, content research, competitor discovery | Search + findSimilar + Contents; MCP and SDKs available |

**Agent recommendation**: Exa for neural search over the open web — content research, competitor/similar-page discovery, link prospecting, news monitoring, and audience research. Pairs well with seo-audit, content-strategy, and competitor-profiling skills.

### Partner Ecosystem

Partner data sharing, co-sell, and ecosystem management.

| Tool | Best For | Notes |
|------|----------|-------|
| **crossbeam** | Account overlaps, co-sell | Now part of Reveal |
| **introw** | Partner management, deal registration, QBRs | MCP-enabled PRM |

**Agent recommendation**: Crossbeam for identifying partner account overlaps and co-sell opportunities. Introw for full partner relationship management — partner pipeline, commissions, tasks, and automated business review prep.

### Email Outreach

Cold email outreach and email finding tools for link building and sales prospecting.

| Tool | Best For | Notes |
|------|----------|-------|
| **hunter** | Email finding, domain search | Largest email database |
| **snov** | Email finding, drip campaigns | Built-in sequences |
| **lemlist** | Cold email campaigns | Personalization features |
| **instantly** | Cold email at scale | Email warmup built-in |

**Agent recommendation**: Hunter for finding emails. Lemlist or Instantly for sending cold email campaigns. Snov for combined finding + outreach.

### Data Aggregation

Marketing data pipeline tools that connect multiple platforms for unified reporting.

| Tool | Best For | Notes |
|------|----------|-------|
| **supermetrics** | Cross-platform data pulling | 200+ connectors |
| **coupler** | Automated data flows to sheets/BI | Scheduled pipelines |

**Agent recommendation**: Supermetrics for pulling data from multiple marketing platforms into unified reports. Coupler.io for automated data flows to spreadsheets and BI tools.

### Commerce & CMS

E-commerce platforms and content management systems.

| Tool | Best For | CLI Available |
|------|----------|:-------------:|
| **shopify** | E-commerce, product sales | ✓ |
| **wordpress** | Blogs, content sites | ✓ |
| **webflow** | Design-focused marketing sites | ✓ |
| **sanity** | Headless CMS, structured content | ✓ |
| **contentful** | Enterprise headless CMS, multi-locale | ✓ |
| **strapi** | Open-source headless CMS, self-hosted | ✓ |

**Agent recommendation**: Shopify for e-commerce. Webflow for marketing sites. WordPress for blogs. For headless CMS: Sanity for developer-flexible content, Contentful for enterprise multi-locale, Strapi for self-hosted/budget-conscious. See [headless CMS guide](../skills/content-strategy/references/headless-cms.md) for selection criteria.

### AI Visibility / GEO

Track whether your brand is cited in AI answers — ChatGPT, Perplexity, Gemini, Claude, Copilot, and Google AI Overviews. Feeds the **ai-seo** skill.

| Tool | Best For | Agent Reach |
|------|----------|-------------|
| **profound** | Enterprise; also tracks which AI bots crawl your site | REST API + **official MCP** + SDKs |
| **otterly** | SMB / agent-native default | **Official MCP** + public API (+ a published Claude Skill) |
| **peec** | Popular monitoring UI (the one teams ask for by name) | **Official MCP** `api.peec.ai/mcp` + API, all paid plans |
| **quickseo** | GEO + Google Search Console in one MCP | **Official MCP** + API; from $99/mo |
| **scrunch** | AI-search monitoring + optimization | **Official MCP** + API |
| **rankscale** | Affordable, MCP-first citation tracking | **Official MCP** |
| **llmrefs** | Broad engine list at low cost | API only, no MCP |

**Agent recommendation**: For a Dust agent that needs to *pull* AI-visibility data, default to **Otterly** (SMB, from ~$29/$189) or **Profound** (enterprise) — both official MCP + API. **Peec** (the best-known UI) also has an official MCP (`api.peec.ai/mcp`) on all paid plans, and **QuickSEO** bundles GEO + Google Search Console in one MCP. If the team already pays for **Semrush** (its MCP now serves the AI Visibility Toolkit) or **Ahrefs** (Brand Radar), pull AI-visibility data there first. See [tools/mcp/README.md](mcp/README.md).

### Image Generation & Design

AI image models and design tools. In Dust, the primary path is the native **Create Images** capability; reach a specific model when it's connected as a remote MCP or via Composio, otherwise generate with Create Images.

| Tool | Best For | Agent Reach |
|------|----------|-------------|
| **ideogram** | Text-in-image, typography, logos | API / Composio |
| **flux** | Photorealism, brand-consistent generation | API (BFL / Replicate / fal) |
| **recraft** | Vector/brand asset sets, style control | API / Composio |
| **gpt-image** | General-purpose, instruction-following edits | OpenAI API |
| **gemini-image** | Conversational editing ("Nano Banana") | Gemini API |
| **midjourney** | Highest-aesthetic stills | No official API — Browse/Discord |
| **canva** | Templated brand assets, Magic Resize | API / Composio |
| **figma** | Design source of truth, frames → assets | API (Dev Mode MCP is local) |

**Agent recommendation**: Default to Dust **Create Images**. Route by job when a model is connected: text-heavy graphics → **Ideogram**, brand-consistent photography → **Flux**, vector/brand sets → **Recraft**. Use **Canva/Figma** for templated brand assets. Feeds the **image** and **ad-creative** skills.

### Community Platforms

Where communities live and how to measure them. Feeds the **community-marketing** skill.

| Tool | Best For | Agent Reach |
|------|----------|-------------|
| **slack** | B2B communities | **Native Dust connector** / official MCP / Composio |
| **discord** | Product & creator communities | API / Browse + Computer |
| **circle** | Paid/course communities | API / Browse |
| **discourse** | Public forums | API / Browse |
| **reddit** | Public subreddit monitoring + listening | API / Browse / Web Search |
| **common-room** | Cross-platform community analytics & scoring | API |

**Agent recommendation**: Pull health metrics (active members, post/reply rates, sentiment) from whichever platform is connected — **Slack** via the native connector, **Discord/Circle/Discourse** via API or Browse+Computer, **Reddit** via Web Search/Browse. Use **Common Room** when the community spans multiple platforms and you need unified scoring.

### App Store Optimization (ASO)

Keyword volume, rankings, and listing data for mobile apps. Feeds the **aso** skill.

| Tool | Best For | Agent Reach |
|------|----------|-------------|
| **apptweak** | ASO keyword + competitor data | API / Browse |
| **sensortower** | Market intelligence, download/revenue estimates | API / Browse |
| **appfollow** | Reviews, rankings, ASO monitoring | API / Browse |
| **app-store-connect** | First-party iOS impressions/conversion/keywords | Apple API (auth'd) / export |
| **google-play-console** | First-party Android acquisition data | Google API (auth'd) / export |

**Agent recommendation**: The public listing is reachable with **WebFetch/Browse/Computer** (core to the skill). For keyword *volume* and exact *rank*, connect an ASO tool (**AppTweak / Sensor Tower / AppFollow**) or use a **App Store Connect / Play Console** export; otherwise run the qualitative audit and flag that volume/rank are unavailable.

### Subscription, Retention & Billing

Revenue and churn data beyond Stripe/Paddle. Feeds **pricing**, **churn-prevention**, and **paywalls**.

| Tool | Best For | Agent Reach |
|------|----------|-------------|
| **profitwell** | Subscription analytics, price-sensitivity, retention metrics | API |
| **baremetrics** | SaaS metrics dashboards (MRR, churn, LTV) | API |
| **churnkey** | Cancel-flow save offers + dunning | API / Browse |
| **prosperstack** | Cancellation flows + retention offers | API / Browse |
| **chargebee** | Subscription billing (alt to Stripe/Paddle) | API / SDK |
| **recurly** | Subscription billing + dunning | API / SDK |
| **revenuecat** | **Mobile** app subscriptions + paywall analytics | API / SDK |
| **superwall** | Mobile paywall experimentation | API / SDK |

**Agent recommendation**: For web billing, **Stripe** (native/MCP) or **Paddle** is the primary source; layer **ProfitWell/Baremetrics** for deeper retention/price metrics and **Churnkey/ProsperStack** for cancel-flow tooling. For mobile apps, **RevenueCat** is the default subscription + paywall data source (Stripe/Paddle don't cover in-app purchases).

### More Categories

Additional tools referenced by skills, reached by the priority order above (most are Composio or Browse today):

- **Popups**: optinmonster, privy, optimonk — popup/opt-in builders (API / Browse). Klaviyo covers popups for ecom.
- **Experimentation / flags**: vwo, launchdarkly, statsig (API/SDK); microsoft-clarity for free heatmaps + rage-click data (Browse).
- **Support**: zendesk — tickets for VOC and switching pain (Composio).
- **Reviews**: capterra, trustradius — Browse-only (no public API); complement G2/Trustpilot.
- **PR / journalist discovery**: muckrack, prowly (journalist databases, API); qwoted, featured (inbound press requests, Browse-only — HARO/Connectively was discontinued in 2024).
- **Prospecting / firmographics**: crunchbase (funding, API), builtwith / wappalyzer (technographics, API), linkedin-sales-navigator (Browse/Computer only), smartlead (cold-email sending/warmup, API).
- **Marketing automation**: marketo, pardot — enterprise MAP for RevOps lifecycle (API, Composio).
- **Social listening**: brand24, mention — brand mention monitoring (API); feeds the social-listening marketing loop.
- **Directories / launch**: producthunt — GraphQL API for listing data; the launch event itself is Browse/Computer.

---

## CLI Tools

Zero-dependency, single-file Node.js CLIs for tools that don't ship their own. See [`clis/README.md`](clis/README.md) for install instructions and usage.

All CLIs follow a consistent pattern:
- **No dependencies** — Node 18+ only, uses native `fetch`
- **JSON output** — pipe to `jq`, save to file, or use in scripts
- **Env var auth** — set `{TOOL}_API_KEY` and go
- **Consistent commands** — `{tool} <resource> <action> [options]`

---

## MCP-Enabled Tools

The **full categorized catalog (~160 verified servers)** lives in **[tools/mcp/README.md](mcp/README.md)** — server URLs, auth, exposed tools, and the remote-vs-local distinction. Quick index of official-remote servers (addable directly in Dust) by function:

- **SEO & search**: semrush, ahrefs, dataforseo, sistrix, se-ranking, serpstat, mangools, serpapi, similarweb, oncrawl, diffbot, tavily, linkup, jina
- **AI visibility / GEO**: profound, otterly, peec, quickseo, scrunch, rankscale, writesonic
- **Analytics & BI**: ga4 *(local — use the native connector)*, posthog, mixpanel, amplitude, contentsquare *(Heap/Hotjar)*, statsig, pendo, fullstory, snowplow, matomo, airtable, bigquery, snowflake, databricks, clickhouse, motherduck, metabase, power-bi, looker, airbyte, hightouch
- **Ads**: meta-ads, windsor-ai, two-minute-reports, polar-analytics, optmyzr, improvado, tiktok-ads ⚠, amazon-ads ⚠
- **CRM & sales**: hubspot, salesforce, attio, close, pipedrive ⚠, monday, outreach *(Amplify)*, apollo ⚠, zoominfo, amplemarket, lemlist, reply, instantly, smartlead
- **Enrichment / intent**: lusha, fullenrich, surfe, prospeo, hunter, warmly, truelist; **LinkedIn/web data**: bright-data, apify, horizondatawave, phantombuster, nimble
- **Email / SMS / lifecycle**: klaviyo, customer-io, resend, brevo, moengage, kit, mailerlite, omnisend, marketo, activecampaign, beehiiv, courier, novu, knock, intercom
- **Payments / billing**: stripe, paddle, revenuecat, polar, square, paypal, ramp, mercury, brex
- **CMS & commerce**: wordpress-com, webflow, wix, contentful, sanity, datocms, storyblok, hygraph, builder-io, shopify-storefront, bigcommerce, saleor, cloudinary, frontify, optimizely-cms, aem
- **Social & creative**: buffer, postiz, typefully, blotato, canva, runway, fal-ai, replicate, ideogram, heygen, invideo, figma
- **Marketing ops**: asana, linear, atlassian, clickup, smartsheet, todoist, coda, box, dropbox, cal-com, calendly, typeform, tally, make, pipedream, miro, front; notion + slack + google-drive *(native Dust connectors)*
- **Reviews / experimentation / events**: vwo, optimizely-experimentation, launchdarkly, birdeye, zoom, livestorm, press-ranger ⚠, g2 ⚠
- **Web scraping / browser**: firecrawl, exa, scrapingbee, scrapegraphai, scrapeless, olostep, zenrows, browserless, anchor-browser
- **Data / automation glue**: supermetrics, coupler, outreach *(Amplify)*, crossbeam *(Limited Availability)*, zapier, fireflies

**⚠** = official but access-gated (paid tier, waitlist, or per-account provisioning) — see the catalog for details.

**Community / local / marketplace-only** (no plain remote server to add in Dust — reach via native connector or Composio): **google-ads** (stdio/self-host, read-only), **clay** (Claude connector-directory), **introw** (Claude connector-directory), **mailchimp** (Marketing API community-only; the official MCP is transactional/Mandrill), **google-search-console** (community/local), **linkedin-ads** (third-party only).

To use a remote MCP tool, add its server in the Dust workspace (URL + auth) and attach it to the agent.

### Composio Integration

[Composio](integrations/composio.md) provides managed OAuth and pre-built connectors for 500+ tools via a single MCP server. It adds MCP access to tools that don't have native MCP servers, including HubSpot, Salesforce, Meta Ads, LinkedIn Ads, Google Sheets, Slack, Notion, and more.

- **Setup**: `npx @composio/mcp@latest setup`
- **Quick start**: See [tools/composio/README.md](composio/README.md)
- **Marketing tool mapping**: See [tools/composio/marketing-tools.md](composio/marketing-tools.md)

Use Composio when you need MCP access to OAuth-heavy tools. Prefer native MCP servers (GA4, Stripe, Mailchimp, etc.) when available — they have deeper coverage.

### Cogny Integration

[Cogny](integrations/cogny.md) is a hosted MCP gateway focused on marketing channels — one federated MCP URL with managed OAuth across every channel you've connected. Narrower than Composio (marketing-only) and useful when you want SEO, paid social, and privacy-friendly analytics behind a single MCP login.

- **Setup**: connect channels at [cogny.com](https://cogny.com), then in Claude.ai go to Settings → Connectors → Add custom connector and paste `https://app.cogny.com/mcp`
- **Channels**: Search Console, Bing Webmaster, Semrush, LinkedIn Ads, Reddit Ads, TikTok Ads, Plausible, Fathom
- **Pricing**: Solo plan starts at $9/mo (7-day trial)

Use Cogny when you only need marketing channels and want to avoid running your own OAuth proxy. Prefer native APIs when you need deep, custom control of a single tool.

---

## Quick Start by Use Case

### Setting up analytics tracking
1. Read [ga4.md](integrations/ga4.md) for web analytics
2. Read [segment.md](integrations/segment.md) if routing to multiple tools

### Launching a referral program
1. Read [rewardful.md](integrations/rewardful.md) or [tolt.md](integrations/tolt.md) for Stripe-based programs
2. Read [dub-co.md](integrations/dub-co.md) for link tracking

### Setting up email automation
1. Read [customer-io.md](integrations/customer-io.md) for behavior-based automation
2. Read [resend.md](integrations/resend.md) for transactional email

### Running email outreach for backlinks
1. Read [hunter.md](integrations/hunter.md) for finding emails
2. Read [lemlist.md](integrations/lemlist.md) or [instantly.md](integrations/instantly.md) for sending campaigns

### Running paid ads
1. Read [google-ads.md](integrations/google-ads.md) for search campaigns
2. Read [meta-ads.md](integrations/meta-ads.md) for social campaigns
