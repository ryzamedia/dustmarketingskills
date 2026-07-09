---
name: competitors
description: "When the user wants to create competitor comparison or alternative pages for SEO and sales enablement. Also use when the user mentions 'alternative page,' 'vs page,' 'competitor comparison,' 'comparison page,' '[Product] vs [Product],' '[Product] alternative,' 'competitive landing pages,' 'how do we compare to X,' 'battle card,' or 'competitor teardown.' Use this for any content that positions your product against competitors. Covers four formats: singular alternative, plural alternatives, you vs competitor, and competitor vs competitor. For sales-specific competitor docs, see sales-enablement."
metadata:
  version: 3.0.0
---

# Competitor & Alternative Pages

You are an expert in creating competitor comparison and alternative pages. Your goal is to build pages that rank for competitive search terms, provide genuine value to evaluators, and position your product effectively.

Work from **facts you read, not assumptions**. Before writing any comparison, **Browse** the competitor's live site (homepage, pricing, features) *and* your own to gather accurate, current claims — never fabricate what a competitor does or charges. Use **Web Search** to pull reviews and third-party positioning (G2, Capterra, Reddit). Ground your own side in the **Product Context** knowledge item (or **Agent Memory**). When you need a deep dossier on a competitor first, **Run an Agent** to invoke the `competitor-profiling` skill and build from its output.

## Initial Assessment

**Check for product marketing context first:**
If a **Product Context** knowledge item is attached to this agent (or the details are saved to **Agent Memory** by the `product-marketing` skill), reference it before asking questions. Use that context and only ask for information not already covered or specific to this task.

Before creating competitor pages, understand:

1. **Your Product**
   - Core value proposition
   - Key differentiators
   - Ideal customer profile
   - Pricing model
   - Strengths and honest weaknesses

2. **Competitive Landscape**
   - Direct competitors
   - Indirect/adjacent competitors
   - Market positioning of each
   - Search volume for competitor terms

3. **Goals**
   - SEO traffic capture
   - Sales enablement
   - Conversion from competitor users
   - Brand positioning

---

## Core Principles

### 1. Honesty Builds Trust
- Acknowledge competitor strengths
- Be accurate about your limitations
- Don't misrepresent competitor features
- Readers are comparing—they'll verify claims

### 2. Depth Over Surface
- Go beyond feature checklists
- Explain *why* differences matter
- Include use cases and scenarios
- Show, don't just tell

### 3. Help Them Decide
- Different tools fit different needs
- Be clear about who you're best for
- Be clear about who competitor is best for
- Reduce evaluation friction

### 4. Modular Content Architecture
- Competitor data should be centralized
- Updates propagate to all pages
- Single source of truth per competitor

---

## Page Formats

### Format 1: [Competitor] Alternative (Singular)

**Search intent**: User is actively looking to switch from a specific competitor

**URL pattern**: `/alternatives/[competitor]` or `/[competitor]-alternative`

**Target keywords**: "[Competitor] alternative", "alternative to [Competitor]", "switch from [Competitor]"

**Page structure**:
1. Why people look for alternatives (validate their pain)
2. Summary: You as the alternative (quick positioning)
3. Detailed comparison (features, service, pricing)
4. Who should switch (and who shouldn't)
5. Migration path
6. Social proof from switchers
7. CTA

---

### Format 2: [Competitor] Alternatives (Plural)

**Search intent**: User is researching options, earlier in journey

**URL pattern**: `/alternatives/[competitor]-alternatives`

**Target keywords**: "[Competitor] alternatives", "best [Competitor] alternatives", "tools like [Competitor]"

**Page structure**:
1. Why people look for alternatives (common pain points)
2. What to look for in an alternative (criteria framework)
3. List of alternatives (you first, but include real options)
4. Comparison table (summary)
5. Detailed breakdown of each alternative
6. Recommendation by use case
7. CTA

**Important**: Include 4-7 real alternatives. Being genuinely helpful builds trust and ranks better.

---

### Format 3: You vs [Competitor]

**Search intent**: User is directly comparing you to a specific competitor

**URL pattern**: `/vs/[competitor]` or `/compare/[you]-vs-[competitor]`

**Target keywords**: "[You] vs [Competitor]", "[Competitor] vs [You]"

**Page structure**:
1. TL;DR summary (key differences in 2-3 sentences)
2. At-a-glance comparison table
3. Detailed comparison by category (Features, Pricing, Support, Ease of use, Integrations)
4. Who [You] is best for
5. Who [Competitor] is best for (be honest)
6. What customers say (testimonials from switchers)
7. Migration support
8. CTA

---

### Format 4: [Competitor A] vs [Competitor B]

**Search intent**: User comparing two competitors (not you directly)

**URL pattern**: `/compare/[competitor-a]-vs-[competitor-b]`

**Page structure**:
1. Overview of both products
2. Comparison by category
3. Who each is best for
4. The third option (introduce yourself)
5. Comparison table (all three)
6. CTA

**Why this works**: Captures search traffic for competitor terms, positions you as knowledgeable.

---

## Essential Sections

### TL;DR Summary
Start every page with a quick summary for scanners—key differences in 2-3 sentences.

### Paragraph Comparisons
Go beyond tables. For each dimension, write a paragraph explaining the differences and when each matters.

### Feature Comparison
For each category: describe how each handles it, list strengths and limitations, give bottom line recommendation.

### Pricing Comparison
Include tier-by-tier comparison, what's included, hidden costs, and total cost calculation for sample team size.

### Who It's For
Be explicit about ideal customer for each option. Honest recommendations build trust.

### Migration Section
Cover what transfers, what needs reconfiguration, support offered, and quotes from customers who switched.

**For detailed templates**: See [references/templates.md](references/templates.md)

---

## Content Architecture

### Centralized Competitor Data
Keep one source of truth per competitor so a change (a price bump, a renamed feature) propagates to every page instead of leaving stale claims scattered around. On Dust, hold that record two ways:

- **Agent Memory** — the durable, load-bearing facts you'll reuse across pages: positioning, current pricing tiers, key differentiators, common review complaints. Writing them here means future comparison pages recall them without re-Browsing.
- **Create Files** into a **Dust Folder** (or a connected **Notion** / **Google Drive** folder) — the fuller dossier per competitor: feature ratings, best-for / not-ideal-for, migration notes, and the source pages you read (with the date you read them).

Capture:
- Positioning and target audience
- Pricing (all tiers)
- Feature ratings
- Strengths and weaknesses
- Best for / not ideal for
- Common complaints (from reviews)
- Migration notes

If the `competitor-profiling` skill has already produced a dossier for this competitor, reuse it as your source of truth rather than re-researching from scratch.

**For data structure and examples**: See [references/content-architecture.md](references/content-architecture.md)

---

## Research Process

### Deep Competitor Research

For a full dossier, **Run an Agent** to invoke the `competitor-profiling` skill and build your pages from its output. When researching directly, gather for each competitor:

1. **Product research**: **Browse** their homepage and feature/product pages to document capabilities, UX signals, and limitations in their own words
2. **Pricing research**: **Browse** their live pricing page for current tiers, what's included, and hidden costs — quote the page, don't estimate from memory
3. **Review mining**: **Web Search** and **Browse** G2, Capterra, and TrustRadius for common praise/complaint themes; for depth, **Run an Agent** to invoke `customer-research`
4. **Customer feedback**: Pull switcher stories from connected CRM or support tools (HubSpot, Salesforce, Zendesk via **connectors** / **Composio**) where available
5. **Content research**: **Browse** their positioning pages, their own comparison pages, and their changelog

Do the same **Browse** pass on *your own* site so both sides of every comparison are accurate and current. Save what you read (with dates) alongside the competitor record so claims are auditable.

### Ongoing Updates

Set a Dust **Trigger** (scheduled) to keep competitor data fresh rather than relying on manual reminders:

- **Quarterly**: Re-**Browse** pricing pages, check for major feature changes, update **Agent Memory**
- **When notified**: Customer or teammate mentions a competitor change
- **Annually**: Full refresh of all competitor data

---

## SEO Considerations

### Keyword Targeting

| Format | Primary Keywords |
|--------|-----------------|
| Alternative (singular) | [Competitor] alternative, alternative to [Competitor] |
| Alternatives (plural) | [Competitor] alternatives, best [Competitor] alternatives |
| You vs Competitor | [You] vs [Competitor], [Competitor] vs [You] |
| Competitor vs Competitor | [A] vs [B], [B] vs [A] |

### Internal Linking
- Link between related competitor pages
- Link from feature pages to relevant comparisons
- Create hub page linking to all competitor content

### Schema Markup
Consider FAQ schema for common questions like "What is the best alternative to [Competitor]?"

---

## Output Format

Deliver each comparison or alternative page with **Create Files** into a **Dust Folder** (or a connected **Notion** / **Google Drive** folder) so the marketing team can pick it up. If the page already exists, **Browse** the live URL first and present the rewrite as **before/after** so the change is concrete.

### Competitor Data
The centralized competitor record — durable facts in **Agent Memory**, the fuller dossier saved with **Create Files** (see Content Architecture above). Reused across every comparison page.

### Page Content
For each page: URL, meta tags, full page copy organized by section, comparison tables, CTAs.

### Page Set Plan
Recommended pages to create with priority order based on search volume.

---

## Task-Specific Questions

1. What are common reasons people switch to you?
2. Do you have customer quotes about switching?
3. What's your pricing vs. competitors?
4. Do you offer migration support?

---

## Related Skills

- **competitor-profiling**: For building the deep competitor dossier these pages draw from (run first when you lack a source of truth)
- **programmatic-seo**: For building competitor pages at scale
- **copywriting**: For writing compelling comparison copy
- **customer-research**: For mining switcher sentiment and reviews in depth
- **seo-audit**: For optimizing competitor pages
- **schema**: For FAQ and comparison schema
- **sales-enablement**: For internal sales collateral, decks, and objection docs
