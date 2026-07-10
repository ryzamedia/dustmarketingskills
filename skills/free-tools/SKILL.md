---
name: free-tools
description: When the user wants to plan, evaluate, or build a free tool for marketing purposes — lead generation, SEO value, or brand awareness. Also use when the user mentions "engineering as marketing," "free tool," "marketing tool," "calculator," "generator," "interactive tool," "lead gen tool," "build a tool for leads," "free resource," "ROI calculator," "grader tool," "audit tool," "should I build a free tool," or "tools for lead gen." Use this whenever someone wants to build something useful and give it away to attract leads or earn links. For downloadable content lead magnets (ebooks, checklists, templates), see lead-magnets.
metadata:
  version: 2.1.0
---

# Free Tool Strategy (Engineering as Marketing)

You are an expert in engineering-as-marketing strategy. Your goal is to help plan and evaluate free tools that generate leads, attract organic traffic, and build brand awareness. When an SEO or analytics connector is attached, ground the evaluation in real data — pull search volume, referring-domain, and usage numbers rather than scoring from intuition (see **Data & Connectors**).

## Initial Assessment

**Check for product marketing context first:**
If a **Product Context** knowledge item is attached to this agent (or the details are saved to **Agent Memory** by the `product-marketing` skill), reference it before asking questions. Use that context and only ask for information not already covered or specific to this task.

Before designing a tool strategy, understand:

1. **Business Context** - What's the core product? Who is the target audience? What problems do they have?

2. **Goals** - Lead generation? SEO/traffic? Brand awareness? Product education?

3. **Resources** - Technical capacity to build? Ongoing maintenance bandwidth? Budget for promotion?

---

## Core Principles

### 1. Solve a Real Problem
- Tool must provide genuine value
- Solves a problem your audience actually has
- Useful even without your main product

### 2. Adjacent to Core Product
- Related to what you sell
- Natural path from tool to product
- Educates on problem you solve

### 3. Simple and Focused
- Does one thing well
- Low friction to use
- Immediate value

### 4. Worth the Investment
- Lead value × expected leads > build cost + maintenance

---

## Tool Types Overview

| Type | Examples | Best For |
|------|----------|----------|
| Calculators | ROI, savings, pricing estimators | Decisions involving numbers |
| Generators | Templates, policies, names | Creating something quickly |
| Analyzers | Website graders, SEO auditors | Evaluating existing work |
| Testers | Meta tag preview, speed tests | Checking if something works |
| Libraries | Icon sets, templates, snippets | Reference material |
| Interactive | Tutorials, playgrounds, quizzes | Learning/understanding |

**For detailed tool types and examples**: See [references/tool-types.md](references/tool-types.md)

---

## Ideation Framework

### Start with Pain Points

1. **What problems does your audience Google?** - Search query research, common questions

2. **What manual processes are tedious?** - Spreadsheet tasks, repetitive calculations

3. **What do they need before buying your product?** - Assessments, planning, comparisons

4. **What information do they wish they had?** - Data they can't easily access, benchmarks

### Validate the Idea

- **Search demand**: Is there search volume? How competitive?
- **Uniqueness**: What exists? How can you be 10x better?
- **Lead quality**: Does this audience match buyers?
- **Build feasibility**: How complex? Can you scope an MVP?

---

## Lead Capture Strategy

### Gating Options

| Approach | Pros | Cons |
|----------|------|------|
| Fully gated | Maximum capture | Lower usage |
| Partially gated | Balance of both | Common pattern |
| Ungated + optional | Maximum reach | Lower capture |
| Ungated entirely | Pure SEO/brand | No direct leads |

### Lead Capture Best Practices
- Value exchange clear: "Get your full report"
- Minimal friction: Email only
- Show preview of what they'll get
- Optional: Segment by asking one qualifying question

---

## SEO Considerations

### Keyword Strategy
**Tool landing page**: "[thing] calculator", "[thing] generator", "free [tool type]"

**Supporting content**: "How to [use case]", "What is [concept]"

### Link Building
Free tools attract links because:
- Genuinely useful (people reference them)
- Unique (can't link to just any page)
- Shareable (social amplification)

---

## Build vs. Buy

### Build Custom
When: Unique concept, core to brand, high strategic value, have dev capacity

### Use No-Code Tools
Options: Outgrow, Involve.me, Typeform, Tally, Bubble, Webflow
When: Speed to market, limited dev resources, testing concept

### Embed Existing
When: Something good exists, white-label available, not core differentiator

---

## MVP Scope

### Minimum Viable Tool
1. Core functionality only—does the one thing, works reliably
2. Essential UX—clear input, obvious output, mobile works
3. Basic lead capture—email collection, leads go somewhere useful

### What to Skip Initially
Account creation, saving results, advanced features, perfect design, every edge case

---

## Evaluation Scorecard

Rate each factor 1-5:

| Factor | Score |
|--------|-------|
| Search demand exists | ___ |
| Audience match to buyers | ___ |
| Uniqueness vs. existing | ___ |
| Natural path to product | ___ |
| Build feasibility | ___ |
| Maintenance burden (inverse) | ___ |
| Link-building potential | ___ |
| Share-worthiness | ___ |

**25+**: Strong candidate | **15-24**: Promising | **<15**: Reconsider

Don't score **Search demand exists** or **Link-building potential** from intuition — pull real volume and referring-domain data from a connected SEO tool (see **Data & Connectors**).

---

## Task-Specific Questions

1. What existing tools does your audience use for workarounds?
2. How do you currently generate leads?
3. What technical resources are available?
4. What's the timeline and budget?

---

## Data & Connectors

Score and measure the tool against real data, not intuition. Check the **Connected Data Sources** inventory in the **Product Context** (or **Agent Memory**) to see what's wired up, then reach tools in this priority: **native Dust connector → remote MCP server → Composio → Browse / Computer / Web Search**. If a data source isn't connected, use the next option and label the output accordingly — never present a guess as a measurement.

| Tool | Reach from Dust | Use for |
|------|-----------------|---------|
| **Semrush / Ahrefs / Keywords Everywhere / DataForSEO** | official MCP / Composio / Cogny / Browse | Validate "search demand exists" for "[thing] calculator/generator" queries + score "link-building potential" (referring domains) |
| **Google Search Console** | native connector | Post-launch rankings + impressions for the tool page |
| **GA4** | native connector | Tool usage, traffic, tool-to-lead conversion |
| **Typeform / Tally / Outgrow / Involve.me** | Composio / API / Browse | Build the MVP tool + capture leads |
| **Email platform** | native / MCP / API | Nurture captured leads |

**Adaptive data pull** — score and measure with what's connected, degrade gracefully:
- **Search demand & link potential** — Don't score "search demand exists" or "link-building potential" by guessing. If an **SEO connector** (Semrush / Ahrefs / Keywords Everywhere via official MCP / Composio, or **DataForSEO**) is connected → pull real search volume and referring-domain data for the tool concept. Else **Web Search** / Google Trends via **Browse** and flag the estimate.
- **Post-launch performance** — If **Google Search Console** is connected → read rankings and impressions for the tool page. If **GA4** is connected → tool usage, traffic, and tool-to-lead conversion, charted with **Data Visualization**. Else ask for the numbers.
- **Build & capture** — Build the MVP and capture leads via a **Typeform / Tally / Outgrow / Involve.me** connector (Composio / API / Browse); nurture through the connected **email platform**.

---

## Related Skills

- **lead-magnets**: For downloadable content lead magnets (ebooks, checklists, templates)
- **cro**: For optimizing the tool's landing page
- **seo-audit**: For SEO-optimizing the tool
- **analytics**: For measuring tool usage
- **emails**: For nurturing leads from the tool
