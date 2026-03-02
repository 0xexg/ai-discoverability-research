# How to Sell to Agents — Brian Flynn

**Source:** X (Twitter)
**Author:** Brian Flynn
**Date:** ~March 2026
**Added:** 2026-03-02
**Relevance:** 🔥🔥🔥 Core thesis alignment

## Full Text

In 1937, Ronald Coase asked a question that won him a Nobel Prize: if markets are so efficient, why do firms exist at all? Why don't we just contract everything out? His answer was transaction costs. Finding a specialist, evaluating their work, negotiating a price, enforcing the agreement. All of that takes time and money. It's cheaper to just hire someone. For almost a century, that held.

AI agents are changing the math. An agent can discover a service, check its price, and call it in a single HTTP roundtrip. No proposal. No demo. No comparison-shopping across ten browser tabs. It queries a registry, gets structured results, and picks the best option in milliseconds.

Not all transaction costs are falling equally. Integration, compliance, and security review are still expensive. But the search and evaluation layer, the part that determines whether you even know a service exists and what it costs, is approaching zero.

When search costs collapse, the default shifts from "build it in-house" to "buy it on the open market." And the buyers aren't humans. They're software with budgets.

### The attention economy doesn't apply

The entire history of selling is about capturing attention. Billboards, search ads, landing pages, cold emails, conference booths. All designed for humans who browse, compare, get distracted, and eventually decide.

Agents don't browse. They query. Agents optimize for outcomes, not attention. There's no brand loyalty. No impulse purchasing. No status signaling. An agent's decision function is brutally simple: Can you solve my problem? How fast? How much? How reliably?

Your marketing site is invisible to an agent at runtime. Your pricing page is irrelevant. What matters is your API: what it does, how fast it responds, what it costs, and whether it's up right now.

Consider what a service recommendation engine optimizes for. The scoring function gives bonuses for three things: liveness (is the service responding right now?), proven reliability (has it worked before?), and confidence (how often does it return accurate results?). There's no bonus for Twitter followers, press coverage, or brand recognition. The algorithm can't see any of that, and it wouldn't care if it could.

This means discovery has to be programmatic. Humans find services through word of mouth, search results, and social media. Agents need machine-readable capability registries. They need to hit a URL and get back structured data: here's what I do, here's what it costs, here's how to pay.

If your service can't be discovered by a machine, it doesn't exist to agents.

(Yes, a human still decides which tools the agent is allowed to use. That's a real marketing surface. But once the agent is running, the runtime purchasing decisions are pure optimization. The land grab is making it onto the allowlist, then being the best option once you're there.)

### The buy vs. build calculation

Every time an agent encounters a sub-task, it makes a buy-or-build decision. Should I compute this myself, or should I pay someone who already has the answer?

This calculation comes down to two things: cost and speed. Information arbitrage drives purchasing. Take a common agent sub-task: "what web scraping services exist?" or "what's the best API for this dataset?" When an agent researches this itself, using a GPT-4 class model with ~16K tokens of reasoning and tool calls, it costs $0.10-0.50 and takes 10-25 seconds. Accuracy is variable because it's synthesizing from training data.

## Ghost Team Annotations

### Key Insights

1. **"Trust becomes machine-readable"** — This is the massive insight. Agents need quantifiable trust signals:
   - Uptime history
   - Response accuracy
   - Latency percentiles
   - Output provenance
   - Error rates over time
   
   **→ This is a product we could build.** A reliability monitoring layer for AI tools/APIs.

2. **Coase's theorem updated** — Transaction costs approaching zero for search/evaluation = explosion of micro-services purchased by agents. The market for agent-consumable services is about to explode.

3. **"The attention economy doesn't apply"** — Validates our thesis completely. Marketing to agents ≠ marketing to humans. The scoring function is: liveness + reliability + confidence. Not brand, not followers, not press.

4. **"If your service can't be discovered by a machine, it doesn't exist to agents"** — This IS our business. AppDiscoverability exists to solve exactly this.

5. **"The land grab is making it onto the allowlist"** — Two-phase discovery:
   - Phase 1: Human decides what tools the agent CAN use (marketing surface)
   - Phase 2: Agent decides which tool to USE (pure optimization)
   - We need to help companies win BOTH phases.

6. **Buy vs. build at the agent level** — Agents will make purchasing decisions autonomously. Cost + speed + reliability = the only variables. This means pricing transparency and structured capability descriptions become critical.

### Product Implications for AppDiscoverability

- **Reliability Monitoring:** Track uptime, response times, accuracy for every tool in our index. Become the "trust layer" for agent tool selection.
- **Structured Capability Registry:** Machine-readable tool descriptions that agents can query programmatically.
- **Score = Visibility + Reliability + Selection Rate** — Our scoring model should weight reliability heavily.

### Connects To
- Our Discoverability Stack framework (Layer 3: Evaluation)
- Profound's AEO positioning
- The "connectors as distribution" thesis
