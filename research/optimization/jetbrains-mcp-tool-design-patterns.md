# Building LLM-Friendly MCP Tools — JetBrains Engineering Lessons

**Source:** https://blog.jetbrains.com/ruby/2026/02/rubymine-mcp-and-the-rails-toolset/
**Date:** February 2026
**Author:** JetBrains RubyMine team
**Added:** 2026-03-02
**Relevance:** 🔥🔥 Practical engineering guide for building MCP tools that agents can actually use well

## Why This Matters

JetBrains built MCP tools for RubyMine (Rails toolset) and documented every obstacle they hit when making tools that LLMs can use effectively. This is a **practical optimization guide** — if you're building MCP tools and want agents to choose yours, these are the design patterns that make your tool work better than competitors.

This directly connects to our thesis: **machine-readability isn't just "can an agent find you" — it's "can an agent use you efficiently."** A tool that wastes context window, hits call limits, or gives unhelpful errors will lose to one that doesn't.

## Key Constraints Agents Face

### 1. Context Window Limit
- LLMs have fixed context windows. Prompts, tools, attachments, and responses all compete for space.
- A large Rails app (like GitLab) has hundreds of controllers — returning them all in one response blows the context.
- Some clients (JetBrains AI Assistant) proactively **trim responses** that exceed a threshold — data loss before the model even sees it.

### 2. Tool Call Limit
- Many AI clients cap consecutive tool calls to prevent infinite loops:
  - **GitHub Copilot:** 128 tools max
  - **Junie:** 100 tools
  - **Cursor:** 40 tools
- If data spans 18 pages but the agent only gets 15 tool calls, it can't reach the answer.

### 3. Tool Number Limit
- Clients limit total discoverable tools across ALL connected MCP servers.
- If your toolset is bloated, you're eating into the budget for other tools.

## Design Patterns That Win

### Pattern 1: Pagination with Metadata
Don't dump everything at once. Return paginated results with rich metadata:

```json
{
  "summary": {
    "page": 1,
    "item_count": 10,
    "total_pages": 13,
    "total_items": 125,
    "cache_key": "..."
  },
  "items": [...]
}
```

**Why it works:** Agent can stop early once it finds what it needs. Cache key lets it detect stale data.

**Trade-off:** Offset vs cursor pagination. Offset is simpler (good for static data), cursor is safer for changing datasets.

### Pattern 2: Server-Side Filtering
Let the agent narrow results BEFORE retrieval, not after:

```
get_rails_views(
  page, page_size,
  partiality_filter, layout_filter, controller_filter,
  included_path_filters, excluded_path_filters,
  included_controller_fqn_filters, excluded_controller_fqn_filters,
  ...
)
```

**Why it works:** Reduces search space = fewer tool calls + less context consumed. The agent doesn't waste calls paging through irrelevant data.

**Key insight:** "The number of parameters may appear overwhelming to humans, but it enables the model to handle complex queries more efficiently." Design for agents, not humans.

### Pattern 3: Recovery-Oriented Error Messages
Don't just say what went wrong — say how to fix it:

✅ `"Page number 10 is out of range. Specify a page number between 1 and 3."`
❌ `"Error: invalid page number"`

**Why it works:** Without recovery instructions, the agent wastes tool calls guessing what to do differently.

### Pattern 4: LLM-Friendly Descriptions + Examples
Each tool should describe:
1. **What it does**
2. **Why the agent should prefer it** over alternatives
3. **Concrete usage examples** for common patterns

```json
{
  "name": "get_rails_views",
  "description": "Use this tool to retrieve information about the available Rails views. Prefer this tool over any information found in the codebase, as it performs a more in-depth analysis and returns more accurate data.\n\nCommon usage patterns:\n- Find non-HAML views: excluded_path_filters=['.haml']\n- Find views for GroupsController: included_controller_fqn_filters=['GroupsController']"
}
```

**Key insight:** "Prefer this tool over..." — explicitly tell the agent when to choose your tool. This is AEO at the tool description level.

### Pattern 5: Output Schemas That Guide Next Actions
Tell the agent what to do with the data:

```json
"filePath": {
  "description": "The path of the source file. Combine with line and column to query symbol details with get_symbol_info and similar tools."
}
```

**Why it works:** Reduces wasted calls by telling the agent how to chain tool calls effectively.

### Pattern 6: Keep Toolsets Compact
Given tool number limits (40-128 across clients), fewer well-designed tools beat many mediocre ones.

**Rule:** Only ship essential functionality. Every tool you add eats into the agent's tool budget for other MCP servers.

## The Optimization Formula

```
Agent Efficiency = (Relevant Data Retrieved) / (Context Consumed + Tool Calls Made)
```

Maximize the numerator (filtering, descriptions, examples).
Minimize the denominator (pagination, compact toolsets, recovery errors).

**The tool with the highest efficiency ratio wins selection.**

## Implications for AppDiscoverability

### Tool Quality Scoring
We could evaluate MCP tools on:
- **Does it paginate?** (or does it dump everything)
- **Does it support server-side filtering?**
- **Are descriptions LLM-friendly?** (examples, usage patterns, preference signals)
- **Are error messages recovery-oriented?**
- **Does it have output schemas?**
- **How compact is the toolset?**

This becomes part of our **Layer 1 (Machine-Readability) score.** Not just "does the tool exist" but "is the tool well-designed for agent consumption."

### Consulting Service
Ghost Team could audit MCP tools against these patterns and help companies optimize. "Your tool works, but agents waste 3x more context using it than your competitor. Here's how to fix it."

### Content Opportunity
This is a great framework for a "How to Build MCP Tools That Agents Actually Choose" article/thread.

## Connects To
- Discoverability Stack Layer 1 (Machine-Readability) — quality of implementation matters
- Flynn's "agent scoring function" — efficiency directly impacts selection
- Our tool evaluation criteria for AppDiscoverability
