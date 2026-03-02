# AppDiscoverability Architecture v4
## "Profound for AI Tooling"

---

## The Insight

Profound tells brands: *"Here's how AI talks about you."*
We tell tool builders: *"Here's how AI chooses you — and we'll fix it for you."*

---

## Architecture: The Continuous Loop

This isn't a stack. It's a flywheel. Agents collect → test → diagnose → act → verify → repeat.

```
                    ┌──────────────────────┐
                    │    ANALYTICS LAYER    │
                    │  Dashboard + Score    │
                    │  (What you see)       │
                    └──────────┬───────────┘
                               │ surfaces insights
                               │
    ┌──────────────────────────▼──────────────────────────┐
    │                                                      │
    │                 THE CONTINUOUS LOOP                   │
    │                                                      │
    │   ┌──────────┐    ┌──────────┐    ┌──────────┐      │
    │   │          │    │          │    │          │      │
    │   │ COLLECT  │───▶│  TEST    │───▶│ DIAGNOSE │      │
    │   │          │    │          │    │          │      │
    │   └──────────┘    └──────────┘    └─────┬────┘      │
    │        ▲                                 │           │
    │        │                                 ▼           │
    │   ┌──────────┐                    ┌──────────┐      │
    │   │          │                    │          │      │
    │   │ VERIFY   │◀───────────────────│   ACT    │      │
    │   │          │                    │          │      │
    │   └──────────┘                    └──────────┘      │
    │                                                      │
    └──────────────────────────────────────────────────────┘
    
    Powered by specialized agents across two data channels:
    🏪 App Store Discovery    💬 Organic/Prompt Discovery
```

---

## The 5 Stages of the Loop

### 1. COLLECT — Data Gathering Agents
*What exists and what's happening across both channels*

**App Store Agents:**
- Crawl ChatGPT, Claude, MCP directories
- Track rankings, search positions, category placements
- Monitor competitor listing changes
- Capture metadata, schemas, tool definitions
- Detect new entrants and market shifts

**Organic/Prompt Agents:**
- Run synthetic prompts at scale (1,000+ per tool)
- Probe which tools AI selects for which intents
- Measure prompt volumes and coverage
- Track competitor selection rates
- Map intent-to-tool relationships

→ Data flows into the Testing stage

---

### 2. TEST — Intelligence Engine
*How tools actually perform when AI tries to use them*

**Simulator-to-Host Gap Detection**
- Run identical prompts through API and real ChatGPT client
- Measure behavioral differences
- Score the "reality gap"

**Persona-Based Testing at Scale**
- 1,000+ synthetic prompts per tool
- Controlled variables: memory, history, user maturity, platform
- Segment performance by persona type

**Multi-Turn Conversation Analysis**
- Simulate extended dialogues
- Track when tools lose context or get abandoned
- Measure tool switching behavior

**Tool Drift Monitoring**
- Continuous performance baselines
- Detect regressions in selection rate, success rate
- Flag when platform changes break things

→ Test results flow into Diagnosis

---

### 3. DIAGNOSE — Analysis Agents
*What's wrong, why, and what to do about it*

Diagnosis agents analyze test results and generate **specific, actionable findings:**

- "Your tool description says 'property search' but 54% of rental-intent prompts are going to SpareRoom because you don't mention 'rental' or 'rent' anywhere"
- "Selection drops from 89% → 42% after turn 3 because your tool doesn't carry forward search filters from previous turns"
- "Zillow captures 94% of 'how much is my house worth' prompts (22.4K/mo) because they expose a valuation action — you don't have one"
- "Your sim-to-host gap is 8.2% because memory-dependent prompts work on the client but fail in API testing"

Each diagnosis includes:
- **Root cause** — Why it's happening
- **Impact estimate** — Score points and prompt volume at stake
- **Recommended action** — What specifically to change
- **Which channel** — Store, Organic, or both

→ Diagnoses flow into Action

---

### 4. ACT — Optimization Agents ⚡
*Agents that take direct action on your behalf*

**This is the key differentiator.** Not just recommendations — agents that actually do things:

#### App Store Actions (with user approval):
- **Rewrite tool descriptions** — Optimize for keywords identified by testing
- **Update tool schemas** — Add missing actions, fix parameter definitions
- **Modify metadata** — Categories, images, feature descriptions
- **Adjust category positioning** — Target categories with highest opportunity

#### Organic/Selection Actions:
- **Optimize tool descriptions for LLM comprehension** — Rewrite so AI understands capabilities better
- **Schema restructuring** — Reorganize parameters so AI invokes more cleanly
- **Context hints** — Add conversation-context handling to improve multi-turn performance
- **Prompt matching optimization** — Align tool capabilities with high-volume intent patterns

#### Autonomous Actions (always-on):
- **A/B testing** — Automatically test description variants and measure selection rate impact
- **Competitive response** — When a competitor updates their listing, analyze and suggest counter-adjustments
- **Drift remediation** — When a platform change breaks something, generate and propose a fix

**Approval modes:**
- 🟢 **Auto-apply** — Low-risk changes (metadata tweaks, A/B test variants)
- 🟡 **Suggest & approve** — Medium changes (description rewrites, schema additions)
- 🔴 **Manual only** — High-impact changes (full schema restructuring)

→ Actions flow into Verification

---

### 5. VERIFY — Validation Agents
*Did it work? Close the loop.*

After every action, verification agents:
- Re-run the same test suite that identified the issue
- Measure before/after selection rates
- Confirm the fix didn't break anything else (regression testing)
- Update the Discoverability Score
- If improvement confirmed → log success, move to next priority
- If no improvement → roll back, try different approach
- If regression detected → immediate rollback + alert

**This is what makes it a loop, not a pipeline.** Every action feeds back into collection → testing → diagnosis.

→ Verification results feed back into Collection (loop restarts)

---

## The Discoverability Score

One number. Continuously updated by the loop.

**Score = App Store Visibility + Organic Selection + Reliability = 0-100**

| Component | Points | Measured by |
|---|---|---|
| App Store Visibility | /30 | Collection agents (rankings, keywords, metadata) |
| Organic Selection Rate | /40 | Testing agents (prompt selection across personas) |
| Tool Reliability | /30 | Testing agents (drift, sim-host gap, multi-turn) |

**Score updates automatically** as agents complete loop cycles. Not a daily snapshot — a living metric.

---

## Analytics Layer

The dashboard sits on top of the loop, surfacing:

**Real-time loop visibility:**
- Current loop stage for each active optimization
- Agent activity — what's being collected, tested, diagnosed, acted on, verified
- Score changes as actions take effect

**Two-channel view:**
- 🏪 App Store: keyword rankings, category positions, metadata quality, listing changes
- 💬 Organic: prompt appearances, selection rates, persona coverage, missed opportunities

**Action history:**
- What agents changed, when, and the measured impact
- A/B test results
- Rollback history
- Before/after comparisons

---

## Agent Inventory

### Collection Agents
| Agent | Channel | What it does |
|---|---|---|
| Store Scraper | 🏪 | Crawls directories for rankings, metadata, new apps |
| Keyword Tracker | 🏪 | Monitors search positions for tracked keywords |
| Competitor Watcher | 🏪 | Detects when competitors update listings |
| Cross-Platform Mapper | 🏪 | Links same tools across ChatGPT, Claude, MCP |
| Prompt Tester | 💬 | Runs 1,000+ synthetic prompts per tool |
| Selection Monitor | 💬 | Probes which tools AI chooses per intent |
| Drift Detector | 💬 | Continuous behavioral testing for regressions |
| Sim-to-Host Prober | 💬 | Compares API vs real client behavior |

### Diagnosis Agents
| Agent | What it does |
|---|---|
| Gap Analyzer | Identifies why selection rate is low for specific personas/prompts |
| Competitive Analyzer | Explains why competitors win for specific intents |
| Schema Auditor | Finds missing capabilities, poorly defined parameters |
| Description Auditor | Identifies keyword gaps, unclear language, missing features |

### Action Agents
| Agent | Channel | What it does |
|---|---|---|
| Description Optimizer | 🏪 + 💬 | Rewrites tool descriptions for both store keywords and LLM comprehension |
| Schema Optimizer | 💬 | Restructures tool schemas for better AI invocation |
| Metadata Updater | 🏪 | Updates categories, images, feature listings |
| A/B Test Runner | 🏪 + 💬 | Creates and manages description/schema variants |
| Competitive Responder | 🏪 + 💬 | Generates counter-adjustments when competitors change |

### Verification Agents
| Agent | What it does |
|---|---|
| Regression Tester | Re-runs full test suite after changes |
| Impact Measurer | Calculates before/after score deltas |
| Rollback Agent | Reverts changes that didn't improve or caused regression |

---

## What Makes This Different

| | Profound | Other ASO tools | AppDiscoverability |
|---|---|---|---|
| **Collect** | ✅ Passive monitoring | ✅ Store scraping | ✅ Both channels + active probing |
| **Test** | ❌ No behavioral testing | ❌ No testing | ✅ 1,000+ prompt testing, sim-host, drift |
| **Diagnose** | ✅ Content gaps | ⚠️ Basic keyword gaps | ✅ Root cause analysis across both channels |
| **Act** | ❌ Manual only | ⚠️ Suggestions only | ✅ Agents take direct action |
| **Verify** | ❌ No verification loop | ❌ No verification | ✅ Automated before/after + rollback |

**Key difference:** Everyone else stops at "here's what's wrong." We close the loop: test → diagnose → fix → verify it worked.

---

## Build Sequence

### Phase 1: Loop Foundation (Now)
- Collection agents (both channels)
- Testing engine (personas, sim-host, drift, multi-turn)
- Diagnosis agents
- Discoverability Score v2
- Dashboard with dual-channel view

### Phase 2: Action Layer (Next)
- Description optimizer agent
- Schema optimizer agent
- A/B testing framework
- Approval workflow (auto/suggest/manual)
- Verification agents + rollback

### Phase 3: Autonomous Flywheel (Later)
- Competitive response agents
- Always-on drift remediation
- Predictive optimization (act before issues appear)
- Enterprise multi-app portfolio optimization
- Self-improving test generation

---

## Patent Considerations

The novel combination:
1. **Continuous closed-loop optimization** for AI tool discoverability
2. **Autonomous action agents** that directly modify tool listings/schemas based on behavioral test results
3. **Dual-channel scoring** combining app store visibility with organic AI selection
4. **Verification-and-rollback** cycle ensuring changes actually improve performance
5. **Persona-based synthetic testing at scale** for AI tool selection
6. **Simulator-to-host behavioral gap detection** for AI tools
