# Agent Purchasing Economics — Brian Flynn Analysis

**Date:** 2026-03-02
**Source:** "How to Sell to Agents" by Brian Flynn (X article)
**Full article:** /external/articles/brian-flynn-how-to-sell-to-agents.md

## Core Economic Model

### Coase's Theorem, Updated
- Transaction costs historically favored firms over markets
- AI agents collapse search + evaluation costs toward zero
- Default shifts from "build in-house" to "buy on open market"
- **Buyers aren't humans — they're software with budgets**

### The Buy vs. Build Decision
Every agent sub-task triggers a calculation:

| Factor | Self-Compute | Specialized Service |
|---|---|---|
| Cost | $0.10-0.50 (GPT-4 class reasoning) | $0.01-0.02 |
| Speed | 10-25 seconds | <200ms |
| Accuracy | Variable (synthesized from training data) | Higher (maintained/curated data) |
| Ratio | Baseline | 7-50x cheaper, 50-100x faster |

**Rule:** If marginal cost of delegation < marginal cost of computation, AND faster → delegate. Always.

### What Survives Self-Computation
As models get cheaper, many services get absorbed. The survivors have:
- Proprietary datasets agents can't replicate
- Real-time feeds
- Hardware-dependent computation (image gen, web rendering)
- **"You don't sell intelligence. You sell access to things they literally cannot compute on their own."**

### Speed Compounds
- 10-step workflow × 20 sec/step = 3+ minute wait
- Replace with 200ms service calls = 2 seconds total
- Speed isn't just nice-to-have — it's the blocking resource

## The Death of Attention Economy

### What Agents Don't Care About
- Brand loyalty
- Impulse purchasing
- Status signaling
- Marketing websites
- Pricing pages
- Twitter followers
- Press coverage

### What Agents Optimize For
1. Can you solve my problem?
2. How fast?
3. How much?
4. How reliably?

### Scoring Function
- **Liveness:** Is the service responding right now?
- **Proven reliability:** Has it worked before?
- **Confidence:** How often does it return accurate results?

## Trust as Machine-Readable Value

### Brand → Reliability Score
Agents will track and publish:
- Uptime history
- Response accuracy
- Latency percentiles (P50, P95, P99)
- Output provenance
- Deterministic replays
- Confidence scores

**"If your outputs are opaque, agents will treat them as risky, and risky means expensive."**

### The Reliability Crisis
- 44 services tested → 2 fully working
- 53% direct call success rate
- 87% recommendation layer success
- **"Dead services get zero traffic, permanently"**

## Two-Phase Discovery Model

### Phase 1: The Allowlist (Human Decision)
- Human decides what tools the agent CAN use
- This is still a marketing surface
- Brand, trust, reputation matter HERE
- **"The land grab is making it onto the allowlist"**

### Phase 2: Runtime Selection (Agent Decision)
- Agent chooses which tool to USE from the allowlist
- Pure optimization: speed, cost, reliability
- No brand loyalty, no impulse
- **"Then being the best option once you're there"**

### Implication
Companies need to win BOTH phases:
- Phase 1: Market to humans (content, brand, relationships)
- Phase 2: Optimize for agents (reliability, speed, pricing, machine-readability)

## The Agent-Native Checklist

1. **Machine-readable capabilities** — JSON manifest, not marketing page
2. **Pricing in the protocol** — HTTP 402, not pricing webpage
3. **Automatable onboarding** — Programmatic auth, payment, access
4. **Provable reliability** — Published uptime, latency, accuracy metrics
5. **Faster + cheaper than self-computation** — The only value prop that matters

## Key Quotes

> "You don't sell intelligence. Agents have plenty of that. You sell access to things they literally cannot compute on their own."

> "Trust is the ultimate product feature in a market of machines."

> "Dead services get zero traffic, permanently."

> "The web was built for humans to browse. The next layer will be built for agents to buy."

> "Brand doesn't vanish. It becomes a reliability score."

> "If your service can't be discovered by a machine, it doesn't exist to agents."
