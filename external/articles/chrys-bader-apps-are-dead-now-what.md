# Apps Are Dead. Now What? — Chrys Bader

**Source:** X / Blog
**Author:** Chrys Bader
**Date:** ~March 2026
**Added:** 2026-03-02
**Relevance:** 🔥🔥🔥 Maps the SaaS survival landscape and what it means for discoverability

## Full Text

I've been building my AI chief of staff, Claudia, over the past couple weeks. She has access to my calendar, email, our team's Notion workspace, meeting transcripts, financial history, and more. I've built over a dozen powerful automations. And I've stopped opening half my tools.

Not because they're bad. Because my agent replaced the need to.

You've heard the diagnosis. Satya Nadella said SaaS is dead. Peter Steinberger visited YC and declared 80% of apps will become APIs or disappear. IDC predicts 70% of software vendors will abandon per-seat pricing by 2028.

What's missing is the prescription: if apps are dying, what do you build instead?

### Workflows Are Changing, Fast

My agent summarizes every meeting and drops action items into our project tracker. I haven't opened Fathom's AI notetaker dashboard in weeks.

Fathom's value to me is the transcript data and the webhook that fires when a meeting ends. Not the UI.

Notion invested heavily into their own AI. I don't use it anymore. Notion AI knows Notion deeply but nothing else. My agent knows Notion shallowly but knows everything else: calendar, email, meetings, context. Cross-system orchestration beats single-system for coordination tasks.

The pattern holds across every tool in my stack. The value is shifting from the interface to the API, and the orchestration layer belongs to the agent.

### What Dying Actually Looks Like

It won't be immediate. It looks more like this:

Your per-seat revenue starts declining because companies realize half their "users" are agents that don't need seats. They push for API pricing. You're not ready, so they negotiate bulk seat discounts that crater your ARPU.

Your product-led growth loop breaks. PLG depends on humans experiencing your UI, getting hooked, inviting teammates. When the agent is the user, there's no one to get hooked. Your viral loop goes silent.

A competitor launches with no UI at all. Just an API, a Stripe billing page, and a docs site. Their engineering team is a third your size because they don't maintain a frontend. They undercut you on price because their cost structure is fundamentally different.

And agents don't care what the dashboard looks like.

### Not All Apps Die Equal

Before the prescription, a necessary caveat: not every app is equally exposed.

**Dead on arrival:** CRUD tools, dashboards, anything that's mostly "show me data and let me edit it." Agents handle this natively. If your product is a prettier spreadsheet, you're already losing.

**Vulnerable but defensible:** Workflow tools, project management, CRMs. The data is valuable. The interface is not. These have a window to pivot.

**Trenchcoat companies:** Multiple businesses in one. LinkedIn's identity graph is a durable moat, but agents that evaluate candidates across GitHub and portfolios don't need a profile page. The eyeballs stay; the intent leaves.

**Last to fall:** Creative tools, design surfaces, strategy canvases. Anything where the seeing IS the thinking. Spatial reasoning and creative judgment are the hardest things for agents to replace. But "last" isn't "never."

### Browser Agents Are a Bridge, Not a Destination

Right now, an entire industry exists to help agents access data from services that don't offer a real API: Browserbase, Browserless, Stagehand, Anon, and more cropping up each day. Agents pay a tax to scrape UIs because there's no other door. Others like Unbrowse are starting to reverse engineer APIs via website network traffic to find more efficient paths beyond UI.

This is temporary arbitrage. Browser automation thrives in the gap between what agents need and what SaaS provides. Close the gap, and the browser becomes a fallback, not the default.

The stakes are asymmetric. Open the door and agents become distribution. They recommend you by using you. Keep it closed and agents scrape you anyway. You pay the compute; they owe you nothing. Competitors who are agent-friendly steal the workflow. You become the SaaS equivalent of "no mobile app" in 2012.

### The Cheapest Bit Wins

In a world where every interaction costs tokens, agents are ruthlessly economical. A calendar lookup via API costs fractions of a cent. The same lookup via browser automation costs 10-50x more and 100x the latency.

The hierarchy of death:
- **UIs die first.** Most expensive to navigate, least structured data.
- **Browser automation dies next.** Works but wasteful.
- **Token-hungry APIs die after that.** Too many round-trips, too much parsing.
- **Clean, efficient APIs survive.** Not because they're smartest. Because they're cheapest.

Lock-in evaporates when the cost of trying something new is a single API call. Switching costs approach zero. The only moat is being the best data source — most reliable, most complete, most efficient to query.

### Three Futures for SaaS

Every surviving SaaS company lands in one of three categories. Which one depends on what you believe your actual product is.

**1. Go Headless**

Your product is data and actions. The UI becomes optional. Maybe a debugging tool for power users, maybe gone entirely.

Plaid is heading here: pure data pipes, no end-user UI to speak of. But there's a catch: getting API access still requires enterprise onboarding, sales calls, compliance reviews. The product is headless. The front door isn't.

Instacart has the same problem. Agents that could drive thousands of transactions are stuck in an application queue designed for Fortune 500 partnerships.

To win here: Simplify authentication. OAuth flows designed for humans break agents. Make API keys easy and scoped. Collapse the call chain: every round-trip costs tokens and latency, so return rich, nested responses that anticipate the next question. Think in terms of agent developer experience, not user experience.

How this goes wrong: You go headless but your API is poorly documented, rate-limited to uselessness, or missing critical endpoints. Agents route around you to a competitor who did it right. Headless only works if the API is genuinely great.

Pricing: Shifts from seats to API calls or outcomes. This restructures your sales motion, your CAC model, your entire go-to-market. Per-seat pricing subsidized low-usage customers with high-usage ones. Usage-based pricing exposes that.

Some tools were never really apps to begin with — they're calculations or domain logic (energy bill analysis, tax optimization, options timing) that only lived inside UIs because there was no other way to reach users. Agents free them.

**2. Make the UI Irreplaceable**

Double down on interface as moat. Make the experience so good that staying in-app beats external orchestration.

This is Notion's bet. Linear's bet. It works if the interface is genuinely irreplaceable. Not just familiar, not just "beautiful".

The danger is building a really good UI for a workflow that agents are about to automate entirely.

The narrow version that survives: interfaces for decisions that require human judgment, spatial reasoning, or creative work. Design tools. Strategy canvases. Anything where the visual representation IS the cognitive process.

How this goes wrong: You invest heavily in UI while agents get good enough at the underlying task. Your beautiful interface becomes a museum piece. The test: if an agent could do this task with just an API, your UI isn't irreplaceable, it's just comfortable.

Where it gets interesting: Ship your UI inside your SDK. API client, local data sync, opinionated visualization. One package. The agent uses the API. The human opens a local interface with your design language. Your dashboard escapes your app and lives wherever the agent runs.

**3. Agent-to-Agent**

Instead of my agent calling your API directly (shallow context, raw data), what if it talked to your agent instead?

My agent tells Notion's agent what it needs. Notion's agent handles the internal complexity: traversing the workspace graph, understanding relationships, doing deep work that a raw API call can't. Each service keeps its context advantage but exposes an intelligent interface.

This solves the depth vs. breadth tradeoff. My orchestration agent speaks intent ("find all action items from last week and create tasks"). Your service agent handles the how. It's B2B, but for agents.

How this goes wrong: Trust and auditability. When my agent talks to your agent, who's accountable for the output? Agent-to-agent carries overhead that raw APIs don't: you need to verify what the other agent did, handle hallucinations on both sides, and build audit trails. The protocol layer for this doesn't exist yet.

### What to Build Monday Morning

The underground railroad of the internet, originally built for developers, is being inherited by agents. APIs were plumbing. Now they're the product.

**This week:** Audit your API. Can an agent do everything your UI does? If not, that's your roadmap. If yes, ask why anyone would open your dashboard.

**This month:** Talk to the agent builders. What do they need from you? What's broken? Where are they routing around you?

**This quarter:** Pick your path. Headless, irreplaceable UI, or agent-to-agent. Each requires different teams, different pricing, different product thinking. Straddling all three is how you end up with none.

The window is open. The companies building agent-native from day one are already here. The rest have time, but not much.

The best thing you can build right now is a front door for agents. Make yourself easy to find, hard to replace.

## Ghost Team Annotations

### Core Thesis
Apps → APIs. The value is shifting from interfaces to data pipes. The orchestration layer (the agent) wins because it has cross-system context that no single app can match.

### The Vulnerability Spectrum (Key Framework)
1. **Dead on arrival:** CRUD tools, dashboards, prettier spreadsheets
2. **Vulnerable but defensible:** Workflow tools, PMs, CRMs (data valuable, UI not)
3. **Trenchcoat companies:** Multiple businesses in one (LinkedIn — identity graph durable, profile page not)
4. **Last to fall:** Creative/design tools (seeing IS thinking)

**Implication for AppDiscoverability:** We could categorize every tool in our index by vulnerability tier. Companies in tiers 1-2 are our ideal customers — they NEED to become agent-discoverable or die.

### The Three Futures (Key Framework)
1. **Go Headless** — Become a pure API. Kill the UI. (Plaid model)
2. **Make UI Irreplaceable** — Double down on interface as moat. (Notion/Linear bet)
3. **Agent-to-Agent** — Your agent talks to their agent. (B2B for agents)

**Ghost Team opportunity across all three:**
- Path 1: We help companies build their MCP connectors (headless transition)
- Path 2: We track which UIs agents bypass anyway (prove the UI isn't the moat)
- Path 3: We become the discovery/trust layer for agent-to-agent commerce

### The "Hierarchy of Death"
UIs → Browser automation → Token-hungry APIs → Clean APIs survive

**This IS our business.** We help companies move DOWN this hierarchy — from UI-dependent to clean-API-discoverable.

### Key Quotes
> "The value is shifting from the interface to the API, and the orchestration layer belongs to the agent."

> "Cross-system orchestration beats single-system for coordination tasks."

> "Open the door and agents become distribution. They recommend you by using you."

> "You become the SaaS equivalent of 'no mobile app' in 2012."

> "Lock-in evaporates when the cost of trying something new is a single API call."

> "The only moat is being the best data source — most reliable, most complete, most efficient to query."

> "The best thing you can build right now is a front door for agents. Make yourself easy to find, hard to replace."

### Connections to Other Research
- **Flynn's "How to Sell to Agents"** — Bader describes the demand side (apps dying), Flynn describes the supply side (how to sell to agents). Together they paint the full picture.
- **JetBrains MCP patterns** — Bader says "clean, efficient APIs survive." JetBrains shows exactly what "clean and efficient" looks like at the tool level.
- **x402 protocol** — Bader mentions pricing shift from seats to API calls. x402 is the payment infrastructure for that world.
- **Our Discoverability Stack** — Bader's "make yourself easy to find, hard to replace" = our entire platform thesis.

### Content Opportunity
"The SaaS Survival Guide: Which Path Is Right for Your Company?" — Using Bader's three futures framework + our discoverability data to help companies decide.
