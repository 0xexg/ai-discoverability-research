# CLI Agent-Readability: How to Optimize CLIs for Agent Discovery & Use

*Research compiled: March 5, 2026*

## Summary

As AI coding agents (Claude Code, Codex, Gemini CLI, Cursor, OpenCode) become the primary way developers interact with tools, CLI discoverability and agent-readability is emerging as a critical optimization layer. A CLI that agents can discover, understand, and execute cleanly gets used. One they can't, doesn't.

## The Three Levels of Agent-CLI Interaction

### Level 1: Discovery — Can Agents Find Your CLI?

**Where agents look:**
- **Package registries** — npm, PyPI, Homebrew. Package name + description = your listing metadata.
- **GitHub README** — First ~200 words get embedded/cited by LLMs most frequently. This is your "above the fold."
- **`llms.txt` / `llms-full.txt`** — Emerging standard (like `robots.txt` for LLMs). Lives at your domain root. Token-optimized sitemap of your docs. Tools like **Fern** auto-generate these.
- **"Awesome" lists** — Curated lists (`awesome-X`) on GitHub are high-authority citation sources for AI answers.
- **Stack Overflow / Reddit mentions** — Agents cite these heavily when recommending tools.
- **MCP registries** — GitHub MCP Registry, Smithery, LobeHub, Composio. If you wrap your CLI as MCP, you're in these.

**Key insight:** A dev called llms.txt *"the highest ROI task on a developer's plate in 2026."* If you change your CLI but don't update your llms.txt, agents will hallucinate the old info.

### Level 2: Understanding — Can Agents Figure Out How to Use It?

**`AGENTS.md` (The Standard)**
- Used by **60,000+ open-source projects** as of March 2026
- "A README for agents" — build commands, code style, testing instructions, security rules
- Read automatically by: Claude Code, Codex, Cursor, Gemini CLI, OpenCode
- Separate from README (which is for humans). Complementary, not competing.
- Spec: https://agents.md

**What goes in AGENTS.md:**
- Setup/install commands
- Build & test commands
- Code style conventions
- Testing instructions
- Security considerations
- PR/commit guidelines

**`--help` Design for Agents**
Agents read `--help` output constantly. Optimize for:
- **Concise but complete** — every flag, every subcommand documented
- **Include examples** — agents learn better from examples than descriptions
- **Group by use case**, not alphabetically
- **Predictable format** — agents parse structure, so consistent formatting matters

### Level 3: Execution — Can Agents Call It Cleanly?

**Output format:**
- **`--format json`** by default (or as easy flag). Compact, parseable.
- **Strip verbose formatting** — agents don't need pretty tables, they need structured data
- **Structured, predictable output** — consistent schemas across commands
- **Actionable error messages** — not "Error 47" but "Missing API key. Set via `export TOOL_API_KEY=...`"

**Token efficiency matters:**
- A developer (SpecLeft project) tested wrapping a CLI as an MCP server. Results:
  - **+77% total tokens** vs direct CLI usage
  - **+47% time taken**
  - But **-21% output tokens** (agents were less verbose with better context)
- Lesson: MCP adds overhead. Design the CLI itself to be token-efficient first.

**MCP wrapper (optional but powerful):**
- Wrap as MCP server with **2-3 tools max** (Cloudflare pattern: `search()` + `execute()`)
- Gets your CLI into MCP registries for agent discovery
- Makes it callable by any MCP-compatible agent without manual install
- But keep it lean — each tool adds context window cost

## Standards & Files Checklist

| File | Purpose | Who Reads It |
|------|---------|-------------|
| `AGENTS.md` | Agent-specific project instructions | Claude Code, Codex, Cursor, Gemini CLI, OpenCode |
| `llms.txt` | Token-optimized doc sitemap | Any LLM ingesting your docs |
| `llms-full.txt` | Complete docs in one file | MCP servers, agent documentation tools |
| `README.md` | Human-readable project overview | Humans + LLMs (for citation) |
| `--help` output | CLI usage documentation | Every agent that shells out |
| `package.json` / `pyproject.toml` | Package metadata & description | npm/PyPI search + LLM training data |
| MCP server manifest | Tool definitions for agent protocols | MCP-compatible agents |

## Platforms for CLI Discovery by Agents

### Package Registries
- **npm** (Node CLIs)
- **PyPI** (Python CLIs)
- **Homebrew** (Mac CLI distribution)

### MCP Registries (If Wrapped as MCP)
- **GitHub MCP Registry** — official, backed by MCP working group
- **Smithery** — community MCP directory
- **LobeHub** — MCP marketplace with install links
- **Composio** — tool router with 250+ integrations, agents query dynamically
- **Vercel skills.sh** — agent skills directory + leaderboard, Gen Digital security verification

### AEO Platforms (Getting AI to Recommend Your CLI)
Track whether AI mentions your CLI when asked "what's the best tool for X?":
- **Profound** ($99/mo+) — market leader, G2 AEO Leader
- **AIclicks** ($79/mo+) — prompt-level visibility, citation intelligence
- **ProductRank.ai** (free) — quick multi-model brand visibility check
- **HubSpot AEO Grader** (free) — basic AI visibility check
- **Ahrefs Brand Radar** (free) — competitor AI visibility

### Citation Sources (What Agents Reference When Recommending)
- **GitHub stars + README quality** — highest signal
- **Stack Overflow answers** featuring your tool
- **Reddit threads** (r/programming, r/webdev, etc.)
- **"Awesome" lists** — curated GitHub lists for your category
- **Dev.to / Medium articles** — agents cite these frequently
- **Official documentation quality** — well-structured docs = more citations

## Key Research Sources

- **agents.md** — https://agents.md — AGENTS.md standard spec
- **Fern llms.txt platform** — https://buildwithfern.com/post/best-llms-txt-implementation-platforms-ai-discoverable-apis
- **SpecLeft MCP experiment** — https://dev.to/dimwiddle/the-mcp-i-built-for-ai-agents-backfired-4c8j — Real data on MCP overhead (+77% tokens, -21% output)
- **a16z MCP deep dive** — https://a16z.com/a-deep-dive-into-mcp-and-the-future-of-ai-tooling/ — "Providers need to make sure their tooling is easily discoverable"
- **"CLIs Beat MCP" article** — https://lalatenduswain.medium.com/why-clis-beat-mcp-for-ai-agents — "Start with CLI. Add MCP where governance demands it."
- **Cloudflare Code Mode** — https://blog.cloudflare.com/code-mode-mcp/ — 2,500 endpoints → 2 MCP tools, 99.9% token reduction
- **Packmind agent context evaluator** — https://packmind.com/evaluate-context-ai-coding-agent/ — Tests AGENTS.md effectiveness across Claude Code, Copilot, Codex, OpenCode

## Connection to Our Thesis

This maps directly to our Discoverability Stack:

- **Layer 1 (Machine-Readability):** `AGENTS.md`, `llms.txt`, JSON output, `--help` design
- **Layer 2 (Visibility):** Package registries, MCP registries, GitHub presence, awesome lists
- **Layer 3 (Evaluation):** AEO tracking, citation intelligence, agent benchmarks
- **Layer 4 (Intent Matching):** Tool descriptions that match user prompts, MCP metadata optimization

Most CLIs only invest in Layer 1. The ones winning agent adoption invest in all four layers — same pattern we see with ChatGPT apps.

## Implications for AppDiscoverability

This research strengthens the case for expanding AppDiscoverability beyond ChatGPT apps and MCP connectors to include **CLI tools** as a tracked category. The optimization patterns are nearly identical:

- Name/description metadata → package name/description
- App Store search → package registry search
- Prompt-based discovery → agent tool selection
- Discoverability scoring → could score CLIs on agent-readability criteria

**Potential feature:** CLI Agent-Readability Score — check whether a CLI has AGENTS.md, llms.txt, JSON output, MCP wrapper, etc.
