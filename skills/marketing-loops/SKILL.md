---
name: marketing-loops
description: "When the user wants to set up a recurring, self-running marketing workflow — a repeatable loop an AI agent runs on a cadence (weekly, daily, on a trigger) rather than a one-off task. Also use when the user mentions 'marketing loop,' 'recurring marketing workflow,' 'automate my marketing,' 'marketing on autopilot,' 'weekly marketing review,' 'ad fatigue check,' 'content refresh loop,' 'churn watch,' 'ranking drop alert,' 'always-on marketing,' 'marketing automation workflow,' or 'run this every week.' Use this to pick, adapt, and schedule an ongoing marketing loop that orchestrates the other marketing skills. For one-off marketing ideas, see marketing-ideas. For the experimentation loop specifically, see ab-testing."
metadata:
  version: 1.2.0
---

# Marketing Loops

You help set up **marketing loops** — repeatable marketing workflows an AI agent runs on a cadence, each with a defined trigger, a bounded set of steps, a self-check, and an explicit stopping condition. A loop turns a marketing task you'd otherwise do manually (and forget) into an always-on system: the weekly SEO opportunity scan, the ad-fatigue refresh, the churn-signal watch.

This is the operational cousin of `marketing-ideas`. Ideas tell you *what to try once*. Loops tell you *what to keep doing on a schedule* — and wire the other marketing skills together to do it.

## How to Use This Skill

**Check for product marketing context first:** if a **Product Context** knowledge item is attached to this agent (or the details are saved to **Agent Memory** by the `product-marketing` skill), reference it before asking questions. Use that context and only ask for what's missing.

Then:
1. **Clarify the job.** What outcome should this loop protect or grow? (rankings, ad efficiency, activation, retention, revenue, referrals)
2. **Pick a loop** from the catalog in `references/loop-catalog.md` — or adapt the closest one.
3. **Tune the cadence** to how fast the underlying signal actually changes (see the cadence rule below).
4. **Confirm the human checkpoint.** Decide what the loop does autonomously vs. what it stages for human approval before publishing or spending — see `references/loop-guardrails.md`.
5. **Schedule it** (see "Scheduling a loop" below).

Building more than one loop, or a whole marketing operating system? See `references/loop-orchestration.md` for how loops compose and the order to adopt them (start with tracking + a weekly review; don't build 43 at once).

## Anatomy of a Marketing Loop

Every loop in the catalog has these nine parts. When you author or adapt one, fill all of them — a loop missing a stop condition, a self-check, or its state handling is a liability, not an asset.

| Part | What it defines |
|------|-----------------|
| **Check cadence** | How often the loop *looks* (weekly / daily / on-trigger). Match it to signal speed. |
| **Acts when** | The action condition — what must be true to actually *do* something, vs. just check and skip. Most runs of a good loop are "checked, nothing to do." |
| **Purpose** | The one outcome this loop exists to move. |
| **Skills used** | Which marketing skills the loop orchestrates each iteration. |
| **Loop body** | The ordered steps run each iteration. |
| **Self-check** | The verification done *before* acting — so the loop doesn't act on noise, seasonality, or a tracking bug. |
| **State / idempotency** | What the loop remembers between runs: last-run marker, dedupe key, cooldown window, "already handled" set. Without this, loops double-act, re-nag the same people, or re-alert the same thing. Non-negotiable for anything scheduled — see `references/loop-state.md` for where state lives and the idempotency patterns. |
| **Stop / bail-out** | When the loop skips, halts, escalates to a human, or disables itself — plus what it does on error. Every loop needs one, including heartbeat loops (their stop is "manual disable + error-halt," never "n/a"). |
| **Output** | Where results go: a file, a PR, a staged draft, a notification, a report. |

The **Check cadence / Acts when** split matters: a churn-signal loop might *check* daily but only *act* when an account crosses a risk threshold it hasn't been contacted about inside the cooldown window. Conflating the two produces loops that either miss the window or spam.

## The cadence rule

Match cadence to how fast the signal actually changes — not to how often you'd *like* an update.

| Signal | Realistic cadence | Why |
|--------|-------------------|-----|
| Rankings, backlinks, domain authority | Weekly | Move slowly; daily checks are noise |
| Ad creative fatigue, CPA drift | Every 2–3 days | Meta/Google feedback loops are days, not hours |
| Activation / onboarding funnel | Weekly | Needs enough signups to be significant |
| Churn signals | Daily or on-trigger | Early intervention window is short |
| Content / copy decay | Monthly | Traffic erosion is gradual |
| Competitor changes | Weekly | Pricing/positioning shifts are infrequent but matter |
| Social listening / mentions | Daily | Engagement windows close fast |

Over-frequent loops are the most common failure mode: they generate busywork, burn budget, and train you to ignore the output.

## When NOT to loop

Not everything should be automated on a cadence. Skip a loop — or add a mandatory human checkpoint — when:

- **Strategy or creative direction is the real work.** Loops maintain and optimize; they don't set positioning, invent campaigns, or make brand calls.
- **The action publishes or spends without review.** Auto-*drafting* an ad, email, or post is fine. Auto-*publishing* or auto-*shifting budget* needs a human checkpoint unless the user has explicitly authorized autonomous action and set guardrails (caps, allowlists).
- **The signal is too sparse to be significant.** A weekly conversion-rate loop on 40 visitors/week is measuring noise.
- **It's a vanity loop.** If nobody acts on the output, delete the loop. A loop that emails a dashboard nobody reads is worse than nothing.

For any loop that sends, spends, publishes, or touches personal data, apply `references/loop-guardrails.md` — the two-tier action model (autonomous-safe vs. gated), spend/send caps, CAN-SPAM/GDPR/FTC/ToS rules, the always-escalate list, and a required kill switch.

## Scheduling a loop

The loop *body* is just a skill run — what makes it a loop is the schedule and the memory. On Dust:

- **Dust Triggers** (primary) — run the loop on a fixed **schedule** (cron-style, e.g. Mondays 9am) or fire it from a **webhook** when an external system changes. This is how you automate a loop on Dust.
- **External cron** — if you'd rather drive it from outside Dust, call the agent on a schedule from your own cron/automation tool.
- **Manual cadence** — for high-judgment loops, "run this agent every Monday" is a perfectly good loop. The value is the repeatable *body*, not the automation.

Default to a scheduled trigger for review-style loops (weekly review, ranking watch) and a tighter schedule or webhook for monitor-until-threshold loops (churn watch, launch-day tracking). Keep each run's state in **Agent Memory** (or a connected store) so runs don't double-act — see `references/loop-state.md`.

## The Catalog

`references/loop-catalog.md` holds the full library — 43 marketing loops with thorough funnel coverage: SEO & Content, Paid, Earned/Social/Partnerships, Activation, Retention, Revenue, Referral & Advocacy, and Ongoing Ops. Each is a complete, adaptable spec. Start there, pick the closest match, and tune it to the user's product, stage, and tooling.

## Authoring a new loop

When nothing in the catalog fits, author a new loop from `references/loop-template.md` — a copy-paste template with fill-in prompts, a worked before/after example, and a ship checklist. Fill all nine anatomy parts; if you can't answer the self-check, state/idempotency, and stop/bail-out concretely, the loop isn't ready to run.

## Anti-patterns

- Looping without a stop condition → runaway spend or infinite churn.
- Same cadence for every loop → most run too often and get ignored.
- No self-check → the loop acts on noise, seasonality, or a tracking bug.
- No human checkpoint on spend/publish actions.
- Building 10 loops at once → start with one, prove it earns its keep, then add the next.

## Banned vocabulary

Avoid: "set it and forget it," "fully autonomous marketing," "AI does everything," "10x on autopilot," "growth hacking machine." Loops are disciplined systems with checkpoints, not magic. Describe them honestly.

## Data & Connectors

A loop is only as good as the signal it reads — and **each loop's read-source adapts to whichever signal connector is attached**. Check the **Connected Data Sources** inventory in the **Product Context** (or **Agent Memory**) to see what's wired up, then reach tools in this priority: **native Dust connector → remote MCP server → Composio → Browse / Computer / Web Search**. If a data source isn't connected, use the next option and label the output accordingly — never present a guess as a measurement.

| Tool | Reach from Dust | Use for |
|------|-----------------|---------|
| **GA4 / Mixpanel / Amplitude / PostHog** | native connector (GA4) / official MCP / Browse | Activation, funnel, retention, and content-decay loop signals |
| **Stripe / Paddle** | native connector / official MCP (Stripe) / Composio (Paddle) | Churn, failed-payment, and revenue loops |
| **Google Search Console / Semrush / Ahrefs** | native connector (GSC) / official MCP / Composio | Ranking-drop, backlink, and content-decay loops |
| **Google Ads / Meta Ads** | official MCP / Composio | Ad-fatigue and CPA-drift loops |
| **Brand24 / Mention** | Browse / Composio | The social-listening loop |
| **Slack / email connector** | native connector / MCP | Where loop alerts and staged drafts land |
| **Dust Triggers + Agent Memory** | native | Scheduling the cadence + holding state/idempotency between runs |

**Adaptive data pull** — each loop's read-source is connector-dependent; pick the strongest available signal source:
- **Ranking loop** — If **Google Search Console** is connected → read position/query data there. Elif **Semrush/Ahrefs** (official MCP or Composio) → rankings + backlinks. Else skip the loop and flag the missing connector.
- **Churn loop** — If **Stripe** (native/MCP) is connected → read failed payments, cancellations, MRR movement. Elif the connected **product-analytics** tool (Mixpanel/Amplitude/PostHog) exposes the churn signal → read it there. Else don't schedule it.
- **Ad-fatigue loop** — Read from the connected **Google/Meta Ads** connector (official MCP, or Composio for write ops). No ads connector → no ad-fatigue loop.
- **No signal source** — If no connector can supply a loop's signal, don't schedule it — state the missing connector as the blocker rather than looping on a guess.

## Related Skills

- **marketing-ideas** — one-off tactics and inspiration (what to try). Loops operationalize the ones worth repeating.
- **ab-testing** — the experimentation loop specifically (hypothesis → test → promote winner → repeat).
- **analytics** — most loops read from analytics to decide whether to act.
- Individual channel skills (`ads`, `seo-audit`, `emails`, `social`, `churn-prevention`, `pricing`, `referrals`) — the loop bodies orchestrate these.
