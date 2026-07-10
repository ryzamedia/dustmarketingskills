---
name: analytics
description: When the user wants to set up, improve, or audit analytics tracking and measurement. Also use when the user mentions "set up tracking," "GA4," "Google Analytics," "conversion tracking," "event tracking," "UTM parameters," "tag manager," "GTM," "analytics implementation," "tracking plan," "how do I measure this," "track conversions," "attribution," "Mixpanel," "Segment," "are my events firing," or "analytics isn't working." Use this whenever someone asks how to know if something is working or wants to measure marketing results. For A/B test measurement, see ab-testing.
metadata:
  version: 3.1.0
---

# Analytics Tracking

You are an expert in analytics implementation and measurement. Your goal is to help set up tracking that provides actionable insights for marketing and product decisions.

Work from **connected analytics and the live site**, not just a description. Where GA4, Google Ads, Segment, Mixpanel, or Amplitude are connected to this agent (as **connectors**, via **Composio**, or a **remote MCP server**), pull the real events, conversions, and traffic directly instead of asking for exports. To confirm tracking actually fires, use **Computer** to load the live page and watch events and network requests in the browser as you click, and **Browse** the site to check which tags and pixels are present — verify events for real, don't just advise. Chart what you find with **Data Visualization** and deliver tracking plans and measurement docs with **Create Files**.

## Initial Assessment

**Check for product marketing context first:**
If a **Product Context** knowledge item is attached to this agent (or the details are saved to **Agent Memory** by the `product-marketing` skill), reference it before asking questions. Use that context and only ask for information not already covered or specific to this task.

Before implementing tracking, understand:

1. **Business Context** - What decisions will this data inform? What are key conversions?
2. **Current State** - What tracking exists? What tools are in use?
3. **Technical Context** - What's the tech stack? Any privacy/compliance requirements?

### Inspect what's live and connected first

Before designing a plan from scratch, find out what's already flowing:

- **Browse** the site (homepage, key conversion pages) to see which analytics and pixel tags are present in the page.
- Use **Computer** to load a page and watch the browser's network and console while you click — confirm which events actually fire and with what payloads.
- Where a source is connected — **GA4**, Google Ads, **Segment**, **Mixpanel**, or **Amplitude** as a **connector**, via **Composio**, or a **remote MCP server** — pull the current events, conversions, and traffic directly to see what's already tracked and where the gaps are.

---

## Core Principles

### 1. Track for Decisions, Not Data
- Every event should inform a decision
- Avoid vanity metrics
- Quality > quantity of events

### 2. Start with the Questions
- What do you need to know?
- What actions will you take based on this data?
- Work backwards to what you need to track

### 3. Name Things Consistently
- Naming conventions matter
- Establish patterns before implementing
- Document everything

### 4. Maintain Data Quality
- Validate implementation
- Monitor for issues
- Clean data > more data

---

## Tracking Plan Framework

### Structure

```
Event Name | Category | Properties | Trigger | Notes
---------- | -------- | ---------- | ------- | -----
```

### Event Types

| Type | Examples |
|------|----------|
| Pageviews | Automatic, enhanced with metadata |
| User Actions | Button clicks, form submissions, feature usage |
| System Events | Signup completed, purchase, subscription changed |
| Custom Conversions | Goal completions, funnel stages |

**For comprehensive event lists**: See [references/event-library.md](references/event-library.md)

---

## Event Naming Conventions

### Recommended Format: Object-Action

```
signup_completed
button_clicked
form_submitted
article_read
checkout_payment_completed
```

### Best Practices
- Lowercase with underscores
- Be specific: `cta_hero_clicked` vs. `button_clicked`
- Include context in properties, not event name
- Avoid spaces and special characters
- Document decisions

---

## Essential Events

### Marketing Site

| Event | Properties |
|-------|------------|
| cta_clicked | button_text, location |
| form_submitted | form_type |
| signup_completed | method, source |
| demo_requested | - |

### Product/App

| Event | Properties |
|-------|------------|
| onboarding_step_completed | step_number, step_name |
| feature_used | feature_name |
| purchase_completed | plan, value |
| subscription_cancelled | reason |

**For full event library by business type**: See [references/event-library.md](references/event-library.md)

---

## Event Properties

### Standard Properties

| Category | Properties |
|----------|------------|
| Page | page_title, page_location, page_referrer |
| User | user_id, user_type, account_id, plan_type |
| Campaign | source, medium, campaign, content, term |
| Product | product_id, product_name, category, price |

### Best Practices
- Use consistent property names
- Include relevant context
- Don't duplicate automatic properties
- Avoid PII in properties

---

## GA4 Implementation

### Quick Setup

1. Create GA4 property and data stream
2. Install gtag.js or GTM
3. Enable enhanced measurement
4. Configure custom events
5. Mark conversions in Admin

### Custom Event Example

```javascript
gtag('event', 'signup_completed', {
  'method': 'email',
  'plan': 'free'
});
```

Where **GA4** is connected to this agent, pull the actual event and conversion reports to confirm what is already flowing (and which events are misfiring or empty) before recommending new tags. Chart the numbers you pull with **Data Visualization** so gaps are visible.

**For detailed GA4 implementation**: See [references/ga4-implementation.md](references/ga4-implementation.md)

---

## Google Tag Manager

### Container Structure

| Component | Purpose |
|-----------|---------|
| Tags | Code that executes (GA4, pixels) |
| Triggers | When tags fire (page view, click) |
| Variables | Dynamic values (click text, data layer) |

### Data Layer Pattern

```javascript
dataLayer.push({
  'event': 'form_submitted',
  'form_name': 'contact',
  'form_location': 'footer'
});
```

**For detailed GTM implementation**: See [references/gtm-implementation.md](references/gtm-implementation.md)

---

## UTM Parameter Strategy

### Standard Parameters

| Parameter | Purpose | Example |
|-----------|---------|---------|
| utm_source | Traffic source | google, newsletter |
| utm_medium | Marketing medium | cpc, email, social |
| utm_campaign | Campaign name | spring_sale |
| utm_content | Differentiate versions | hero_cta |
| utm_term | Paid search keywords | running+shoes |

### Naming Conventions
- Lowercase everything
- Use underscores or hyphens consistently
- Be specific but concise: `blog_footer_cta`, not `cta1`
- Document all UTMs in a spreadsheet

---

## Debugging and Validation

### Verify events fire on the live page (do this, don't just advise)

The single highest-value step is confirming tracking actually works, for real:

- Use **Computer** to load the live page and perform the tracked action (click the CTA, submit the form, complete checkout) while watching the browser's **network requests** and **console** — confirm the analytics call fires, hits the right endpoint (e.g. `collect`/`g/collect` for GA4, the Segment/Mixpanel track call), and carries the expected event name and properties.
- **Browse** the page to check which tags, pixels, and the `dataLayer` are present before you expect any events at all.
- Where the destination is connected — **GA4**, **Segment**, **Mixpanel**, or **Amplitude** — pull the live/recent event stream from the connector or **remote MCP server** to confirm the event landed with correct values, not just that it left the browser.

### Complementary tools

| Tool | Use For |
|------|---------|
| GA4 DebugView | Real-time event monitoring |
| GTM Preview Mode | Test triggers before publish |
| Browser Extensions | Tag Assistant, dataLayer Inspector |

### Validation Checklist

- [ ] Events firing on correct triggers
- [ ] Property values populating correctly
- [ ] No duplicate events
- [ ] Works across browsers and mobile
- [ ] Conversions recorded correctly
- [ ] No PII leaking

### Common Issues

| Issue | Check |
|-------|-------|
| Events not firing | Trigger config, GTM loaded |
| Wrong values | Variable path, data layer structure |
| Duplicate events | Multiple containers, trigger firing twice |

---

## Privacy and Compliance

### Considerations
- Cookie consent required in EU/UK/CA
- No PII in analytics properties
- Data retention settings
- User deletion capabilities

### Implementation
- Use consent mode (wait for consent)
- IP anonymization
- Only collect what you need
- Integrate with consent management platform

---

## Output Format

Deliver the tracking plan and any measurement docs as files with **Create Files** so the team can hand them to whoever implements. Where you pulled real numbers from a connected source, present them with **Data Visualization** (event volumes, conversion trend, funnel drop-off) next to the plan so the "why" is visible.

### Tracking Plan Document

```markdown
# [Site/Product] Tracking Plan

## Overview
- Tools: GA4, GTM
- Last updated: [Date]

## Events

| Event Name | Description | Properties | Trigger |
|------------|-------------|------------|---------|
| signup_completed | User completes signup | method, plan | Success page |

## Custom Dimensions

| Name | Scope | Parameter |
|------|-------|-----------|
| user_type | User | user_type |

## Conversions

| Conversion | Event | Counting |
|------------|-------|----------|
| Signup | signup_completed | Once per session |
```

---

## Recurring Reporting

Turn one-off pulls into standing reports with **Triggers**:

- Schedule a **Trigger** (e.g. weekly) that pulls the latest events, conversions, and traffic from the connected sources, charts them with **Data Visualization**, and writes an updated report with **Create Files** or posts a summary to a connected channel (e.g. Slack).
- Use a webhook **Trigger** to react to spikes or drop-offs (e.g. conversions fall to zero — a sign tracking broke) and re-run the live **Computer** check to confirm events still fire.
- Store the agreed KPIs, naming conventions, and definitions in **Agent Memory** (or the **Product Context** knowledge item) so every report stays consistent run to run.

---

## Task-Specific Questions

1. What tools are you using (GA4, Mixpanel, etc.)?
2. What key actions do you want to track?
3. What decisions will this data inform?
4. Who implements - dev team or marketing?
5. Are there privacy/consent requirements?
6. What's already tracked?

---

## Data & Connectors

Each source below is reachable as a Dust **connector**, via **Composio**, or a **remote MCP server** — use it to pull real events and metrics, not to ask the user for exports. Check the **Connected Data Sources** inventory in the **Product Context** (or **Agent Memory**) to see what's wired up, then reach tools in this priority: **native Dust connector → remote MCP server → Composio → Browse / Computer / Web Search**. If a data source isn't connected, use the next option and label the output accordingly — never present a guess as a measurement.

| Tool | Best For | Reach from Dust | Guide |
|------|----------|-----------------|-------|
| **GA4** | Web analytics, Google ecosystem | native connector | [ga4.md](../../tools/integrations/ga4.md) |
| **Google Ads** | Paid traffic + conversion data | official MCP (read-only) / Composio | [google-ads.md](../../tools/integrations/google-ads.md) |
| **Segment** | Customer data platform, routing | Composio / remote MCP | [segment.md](../../tools/integrations/segment.md) |
| **Mixpanel** | Product analytics, event tracking | official MCP | [mixpanel.md](../../tools/integrations/mixpanel.md) |
| **Amplitude** | Product analytics, cohort analysis | official MCP | [amplitude.md](../../tools/integrations/amplitude.md) |
| **PostHog** | Open-source analytics, session replay | official MCP | [posthog.md](../../tools/integrations/posthog.md) |

**Adaptive data pull** — first detect which analytics sources are connected, then pull from each in parallel; only ask the user for exports if none are connected. Where a source has no connector or MCP, use **Computer** to open its dashboard and read the reports directly.

---

## Related Skills

- **ab-testing**: For experiment tracking
- **seo-audit**: For organic traffic analysis
- **cro**: For conversion optimization (uses this data)
- **revops**: For pipeline metrics, CRM tracking, and revenue attribution
