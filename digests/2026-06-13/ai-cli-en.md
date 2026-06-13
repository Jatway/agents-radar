# AI CLI Tools Community Digest 2026-06-13

> Generated: 2026-06-13 07:10 UTC | Tools covered: 9

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [GitHub Copilot CLI](https://github.com/github/copilot-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Pi](https://github.com/badlogic/pi-mono)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [DeepSeek TUI](https://github.com/Hmbown/DeepSeek-TUI)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# AI CLI Developer Tools Ecosystem — Cross-Tool Comparison Report
**Date:** 2026-06-13

---

## 1. Ecosystem Overview

The AI CLI tools landscape is experiencing rapid iteration with significant stability trade-offs. All six major tools shipped patches or nightly releases this week, but every platform also faces critical regressions—from Claude Code's Fable 5 model outage to Copilot CLI's Linux ARM64 crash and Kimi Code's billing miscalculation. The community is increasingly vocal about production reliability, with developer pain points converging around agent stability, context management, and cross-platform compatibility. A clear architectural divergence is emerging: tools like Gemini CLI and CodeWhale push toward multi-agent fleet architectures, while Claude Code and OpenAI Codex prioritize enterprise security and credential management. The ecosystem is maturing from novelty to production-critical infrastructure, and the breakage rate is beginning to erode developer trust.

---

## 2. Activity Comparison

| Tool | Open Issues | PRs Today | Release Today | Critical Bugs | Community Engagement (Top Issue) |
|------|-------------|-----------|---------------|---------------|----------------------------------|
| **Claude Code** | High (~68K+ total) | 1 | v2.1.176, v2.1.177 | Fable 5 outage, hanging (#26224 142👍) | 116 comments on #26224 |
| **OpenAI Codex** | High (~28K+ total) | 10 | 3x rust-v0.140.0-alpha | Windows sandbox, false safety flags | 79 comments on #12564 (closed) |
| **Gemini CLI** | Moderate (~2K+) | 10 | v0.48.0-nightly | Agent hang (#21409), false success (#22323) | 8 upvotes on #21409 |
| **Copilot CLI** | Moderate (~3.8K+) | 1 | v1.0.62-1 | Terminal corruption (6 issues/48h), ARM64 crash | 17👍 on #2627 (config sys prompt) |
| **Kimi Code** | Low (~2.5K) | 6 | None | Infinite loop (#640), billing bug (#1994 7👍) | 9 comments on #640 |
| **OpenCode** | Moderate (~32K+) | 10 | None | Go access slow (#20404), schema generation (#31996) | 22👍 on #14187 (markdown preview) |
| **Pi** | Moderate (~5.7K+) | 10 | v0.79.2 | Codex connection hang (#4945 30👍) | 55 comments on #4945 |
| **Qwen Code** | Moderate (~5K+) | 10 | v0.18.0 | OAuth free tier firestorm (#3203 127 comments) | 127 comments on #3203 |
| **CodeWhale** | Low (~3.2K) | 10 | v0.8.59 (rebrand) | Image upload (#2584), TUI freeze (#3035) | 8 comments on #2584 |

**Key observations:**
- **OpenAI Codex** leads in PR throughput (10 PRs today) with rapid iteration on sandbox fixes.
- **Claude Code** has the highest community engagement but also the most severe outage (Fable 5).
- **Gemini CLI**, **Qwen Code**, and **OpenCode** all show 10 PRs today—strong maintenance velocity.
- **Kimi Code** has the lowest issue count but stagnated with no release and no resolution on its top bug (#640, open since January).
- **CodeWhale** stands out for scope of change (rebrand + multi-agent architecture planning).

---

## 3. Shared Feature Directions

### 3.1 Multi-Agent & Sub-Agent Architecture (5/9 tools)
| Tool | Specific Need |
|------|---------------|
| **Claude Code** | Sub-agent recursive spawning bug (#68110) |
| **Gemini CLI** | Generalist agent hangs, agent ignores settings (#21409, #22267) |
| **CodeWhale** | Headless worker runtime, agent fleet (#3096, fleet architecture) |
| **Qwen Code** | Fork sub-agent enablement (#4956), background agent permissions (#4928) |
| **OpenCode** | Task sub-agent hang/truncation (#32121, #32131) |

### 3.2 Context Window Management (6/9 tools)
| Tool | Specific Need |
|------|---------------|
| **Claude Code** | Auto-compaction regression at 168K (#66022) |
| **OpenAI Codex** | Context full at conversation start (#9046) |
| **Copilot CLI** | Auto-compaction loops with large instructions (#3621) |
| **Kimi Code** | Configurable token limits (#2418 direction) |
| **Qwen Code** | Oversized context warnings (#5073, ~15% threshold) |
| **Pi** | `excludeFromContext` for custom messages (#5654) |

### 3.3 Cross-Platform Compatibility (5/9 tools)
| Tool | Specific Need |
|------|---------------|
| **Claude Code** | Linux bwrap sandbox broken (#17727) |
| **OpenAI Codex** | Windows `CreateProcessAsUserW` failures (6+ reports) |
| **Gemini CLI** | Wayland browser agent crash (#21983) |
| **Copilot CLI** | Linux ARM64 Tokio panic (#3784) |
| **Kimi Code** | Windows path handling implied |
| **OpenCode** | PowerShell UTF-8 fixes (#31985) |

### 3.4 Provider & Model Flexibility (4/9 tools)
| Tool | Specific Need |
|------|---------------|
| **Qwen Code** | Multi-provider model disambiguation (#4877) |
| **Pi** | Bedrock Mantle, Anthropic Vertex (#5363, #5262) |
| **CodeWhale** | Z.ai, StepFlash, Anthropic native routes (#3191, #3054) |
| **Gemini CLI** | GATEWAY auth type regression (#27553) |

### 3.5 Terminal & TUI Rendering Quality (4/9 tools)
| Tool | Specific Need |
|------|---------------|
| **Copilot CLI** | Terminal corruption cluster (6 issues/48h) |
| **OpenCode** | Plugin loader resilience, spinner fixes (#32151, #32150) |
| **CodeWhale** | TUI freezes under sub-agent load (#3035) |
| **Pi** | Cosmetic rendering "`+` renders as `-`" bug (#5657) |

### 3.6 Billing & Usage Transparency (3/9 tools)
| Tool | Specific Need |
|------|---------------|
| **Kimi Code** | Usage miscalculation, real vs marketing (#1994) |
| **OpenAI Codex** | False rate limits on MAX PRO (#28044) |
| **Qwen Code** | OAuth free tier reduction debate (#3203) |

---

## 4. Differentiation Analysis

### 4.1 Feature Focus

| Tool | Primary Focus | Unique Strength | Weakest Area |
|------|---------------|-----------------|--------------|
| **Claude Code** | Agentic workflow, model quality | Most mature agent behavior, rich tool ecosystem | Model availability churn, web parity |
| **OpenAI Codex** | Enterprise security, cross-platform | Credential broker, Windows sandbox hardening | Windows stability paradox |
| **Gemini CLI** | Code intelligence, MCP integration | AST-aware tools, sub-agent composition | Agent hang reliability |
| **Copilot CLI** | Terminal UX, GitHub integration | YOLO mode, session-scoped canvas | Terminal rendering quality |
| **Kimi Code** | Simplicity, Chinese market | Lightweight, minimal configuration | Billing, stability |
| **OpenCode** | Full-stack TUI, multi-agent | Plugin system, `db doctor` CLI | Chinese-speaking user performance |
| **Pi** | Provider abstraction, extensibility | Wide provider support (OpenAI, Anthropic, Bedrock) | Connection reliability |
| **Qwen Code** | Daemon mode, persistence | Durable cron jobs, transport abstraction | Release CI reliability |
| **CodeWhale** | Multi-agent fleet, rebrand momentum | Headless worker architecture, workflow cards | Young ecosystem, sub-agent lock-in |

### 4.2 Target Users

| Tool | Primary Audience | Entry Barrier |
|------|------------------|---------------|
| **Claude Code** | Professional developers, teams | Medium (Anthropic ecosystem lock) |
| **OpenAI Codex** | Enterprise teams, Windows-heavy orgs | High (infrastructure setup) |
| **Gemini CLI** | Google Cloud developers, agent-heavy workflows | Medium (Google ecosystem) |
| **Copilot CLI** | GitHub ecosystem, individual devs | Low (existing GitHub account) |
| **Kimi Code** | Chinese developers, budget-conscious users | Low |
| **OpenCode** | Full-stack developers, TUI enthusiasts | Medium (plugin system complexity) |
| **Pi** | Provider-flexibility seekers, self-hosters | Medium-high (configuration) |
| **Qwen Code** | Alibaba Cloud developers, daemon-mode fans | Medium (Qwen ecosystem) |
| **CodeWhale** | Multi-agent architecture early adopters | Medium (rebrand migration friction) |

### 4.3 Technical Approach

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | CodeWhale |
|-----------|-------------|--------------|------------|-------------|-----------|
| **Architecture** | Monolithic agent | Rust CLI + credential broker | MCP-first, sub-agent composition | VS Code extension-adjacent | Headless worker fleet |
| **Model Strategy** | Anthropic-only | OpenAI-only | Multi-model | GitHub Copilot model | Multi-provider |
| **Sandbox** | Bubblewrap (Linux) | Extensive sandbox (Windows focus) | Sub-agent isolation | Server-side | TUI-process coupled |

---

## 5. Community Momentum & Maturity

### High Momentum / Rapid Iteration
| Tool | Evidence |
|------|----------|
| **CodeWhale** | Rebrand + 10 PRs + multi-agent fleet planning (8+ issues) |
| **OpenAI Codex** | 10 PRs, 3 alpha releases, proactive cross-platform fixes |
| **Qwen Code** | 10 PRs, daemon mode maturation, durable cron advancement |
| **OpenCode** | 16 issues closed, 10 PRs, `db doctor` merged |

### Stable / Mature Communities
| Tool | Evidence |
|------|----------|
| **Claude Code** | Largest community (68K issues), but signal-to-noise low (duplicate Fable 5 reports) |
| **Gemini CLI** | Structured component-level evaluations (#24353), methodical PR pipeline |
| **Pi** | Responsive maintenance (10 PRs, quick bug fixes), but top issue (#4945) unresolved for months |

### Stagnant / Concerning
| Tool | Evidence |
|------|----------|
| **Kimi Code** | No release, top bug open since January (#640), low engagement beyond billing issue (#1994) |
| **Copilot CLI** | 1 PR today (possibly placeholder), terminal corruption crisis escalating |

---

## 6. Trend Signals for Developers

### 6.1 The "Agent Complexity Cliff" is Here
The honeymoon phase is over. Every tool with multi-agent capabilities (Claude, Gemini, CodeWhale) is discovering that sub-agents introduce exponential failure modes—recursive spawning, false success reporting, configuration override bugs. **Takeaway:** If you're building on agent delegation, implement explicit depth limits, cost ceiling alerts, and a kill switch. Don't assume "GOAL" status means success.

### 6.2 Context Window Management is the New Maturity Metric
Six of nine tools have open issues about context boundaries—auto-compaction failures silent context overflows, infinite compaction loops. This is the #1 production reliability problem. **Takeaway:** Demand configurable compaction thresholds, pre-emptive warnings (like Qwen's 15% heuristic), and `excludeFromContext` controls. If your tool doesn't surface token usage per-request, your billing will surprise you.

### 6.3 Cross-Platform Quality is Deteriorating
Windows users of OpenAI Codex face systemic sandbox failures. Linux ARM64 is broken on Copilot CLI v1.0.62-1. Wayland crashes Gemini's browser agent. The "works on macOS" assumption is breaking down. **Takeaway:** Test across all three platforms before deploying any AI CLI tool. If your team uses non-mainstream setups (ARM64 Linux, Wayland, custom keyboards), budget extra friction.

### 6.4 Terminal Rendering is a Failing Capability
Copilot CLI's 6 terminal corruption issues in 48 hours and CodeWhale's TUI-freeze-under-load bugs reveal that streaming token-by-token output to terminal emulators is harder than it looks. As tools add reasoning displays and sub-agent panels, rendering complexity explodes. **Takeaway:** If you're building for terminal UX, invest heavily in rendering throttling, ANSI escape sequence testing, and platform-specific terminal testing. This will be a differentiator.

### 6.5 Provider Lock-in Creates Fragile Ecosystems
Anthropic-only Fable 5 outage broke Claude Code globally. OpenAI Codex's Windows sandbox is inseparable from OpenAI's API. Qwen's ecosystem is Alibaba-centric. **Takeaway:** Tools with multi-provider abstraction (Pi, CodeWhale) are more resilient but pay a complexity tax. For production use, prefer tools that support at least two providers and have a documented fallback strategy.

### 6.6 Billing Transparency Defines Trust
Kimi Code's 2-requests-for-2-hours vs. "300-1200 requests" marketing gap and Qwen's 90% free-tier reduction proposal show that pricing is the most emotionally charged dimension. **Takeaway:** Before adopting any tool, run it on your actual workload for one week. Monitor token consumption. Don't trust pre-sales estimates. The discrepancy between marketing and reality is the #1 source of community outrage across all tools.

### 6.7 The "Fleet Architecture" is the Next Major Paradigm
CodeWhale's multi-agent fleet planning and Qwen's background agent enablement signal a shift from single-agent assistants to persistent, concurrently-running agent pools. This is where the most ambitious innovation is happening. **Takeaway:** If your use case involves background linting, long-running builds, or monitoring, watch CodeWhale and Gemini CLI closely. If you need reliability above all, stay with Claude Code's more conservative single-agent model until fleet architectures stabilize.

---

## Final Assessment

| Tool | Recommendation For |
|------|-------------------|
| **Claude Code** | Production use with budget for context window tuning |
| **OpenAI Codex** | Windows-heavy enterprise, if sandbox reliability improves |
| **Gemini CLI** | Google Cloud developers, agent experimentation |
| **Copilot CLI** | Wait until terminal corruption crisis resolves |
| **Kimi Code** | Avoid until billing is fixed; high risk for production |
| **OpenCode** | Full-stack developers comfortable with TUI quirks |
| **Pi** | Multi-provider flexibility seekers, self-hosters |
| **Qwen Code** | Daemon-mode enthusiasts, Alibaba Cloud users |
| **CodeWhale** | Early adopters of multi-agent architectures |

The ecosystem is in an uncomfortable adolescence: immensely powerful capabilities are marred by reliability regressions that erode daily confidence. The tools that stabilize their core execution layer—context management, cross-platform sandboxing, and terminal rendering—while continuing to innovate on agent architectures will win the next six months.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

## Claude Code Skills Community Highlights Report (Data as of 2026-06-13)

### 1. Top Skills Ranking

**1. Frontend Design Skills (Multiple PRs)**
- **PR #1046** (ALMMECHANICAL) — Adds `frontend-design`, `ai-experience-consultant`, and `automation-workflows-builder` skill definitions. Combined with **PR #210** (justinwetch) which revises `frontend-design` for clarity and actionability, this domain commands the most attention. PR #210 specifically addresses ensuring every instruction is actionable within a single conversation.
- *Status:* Both open. PR #1046 created 2026-04-27, PR #210 created 2026-01-05.
- [PR #1046](https://github.com/anthropics/skills/pull/1046) | [PR #210](https://github.com/anthropics/skills/pull/210)

**2. document-typography (PR #514)**
- *Author:* PGTBoos
- *Functionality:* Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. Addresses a universal pain point: "Users rarely ask for good typography, but they notice when it's wrong."
- *Discussion highlight:* The PR identifies that every document Claude generates is affected by these issues — a strong practical value proposition.
- *Status:* Open. Created 2026-03-04.
- [PR #514](https://github.com/anthropics/skills/pull/514)

**3. ODT / OpenDocument Skill (PR #486)**
- *Author:* GitHubNewbie0
- *Functionality:* Full OpenDocument Format support — create, fill, read, and convert `.odt`/`.ods` files. Triggers on mentions of ODF, LibreOffice, or open-source document formats.
- *Discussion highlight:* Represents demand for ISO-standard document formats beyond proprietary DOCX.
- *Status:* Open. Created 2026-03-01.
- [PR #486](https://github.com/anthropics/skills/pull/486)

**4. Meta Skills: skill-quality-analyzer & skill-security-analyzer (PR #83)**
- *Author:* eovidiu
- *Functionality:* Two meta-skills for evaluating other skills — quality analysis across 5 dimensions (Structure, Documentation, Robustness, Reliability, Actionability) and security analysis.
- *Discussion highlight:* The most commented-on PR in the repository. Reflects community desire for tooling that governs the skills ecosystem itself.
- *Status:* Open. Created 2025-11-06.
- [PR #83](https://github.com/anthropics/skills/pull/83)

**5. PDF & DOCX Fixes (PR #538, #541)**
- *Authors:* Lubrsy706
- *Functionality:* PR #538 fixes case-sensitive file references breaking PDF skill on Linux; PR #541 prevents document corruption when DOCX skills add tracked changes to documents with existing bookmarks (w:id collision in OOXML).
- *Discussion highlight:* These are the most actionable, well-scoped bug fixes — high signal that existing skills need robustness hardening.
- *Status:* Both open. Created 2026-03-06.
- [PR #538](https://github.com/anthropics/skills/pull/538) | [PR #541](https://github.com/anthropics/skills/pull/541)

**6. agent-creator Meta-Skill (PR #1140)**
- *Author:* SyedaQurratAI
- *Functionality:* Creates task-specific agent sets. Also fixes multi-tool evaluation and adds Windows support.
- *Discussion highlight:* Addresses Issue #1120 and includes critical stability fixes for the evaluation pipeline.
- *Status:* Open. Created 2026-05-15.
- [PR #1140](https://github.com/anthropics/skills/pull/1140)

**7. skill-creator Windows Compatibility (Multiple PRs — #1050, #1099, #1298)**
- *Authors:* gstreet-ops, joshuawowk, MartinCajiao
- *Functionality:* Fixes `run_eval.py` and `run_loop.py` crashes on Windows — `PATHEXT` for `.cmd` files, `cp1252` encoding, `select` on pipes, and the critical `recall=0%` bug.
- *Discussion highlight:* The most active bug-fix cluster. PR #1298 reports 10+ independent reproductions of `recall=0%` — the evaluation pipeline is currently optimizing against noise.
- *Status:* All open.
- [PR #1050](https://github.com/anthropics/skills/pull/1050) | [PR #1099](https://github.com/anthropics/skills/pull/1099) | [PR #1298](https://github.com/anthropics/skills/pull/1298)

**8. color-expert (PR #1302)**
- *Author:* meodai
- *Functionality:* Self-contained color expertise — covers ISCC-NBS, Munsell, XKCD, RAL, Ridgway 1912 color naming systems; OKLCH/OKLAB/CAM16 color space guidance.
- *Discussion highlight:* A highly targeted, specialized skill with strong domain expertise from the author. Created very recently (2026-06-10) but already attracting attention.
- *Status:* Open. Created 2026-06-10.
- [PR #1302](https://github.com/anthropics/skills/pull/1302)

### 2. Community Demand Trends

From the Issues tracker, the most-anticipated new Skill directions are:

- **Org-wide Skill Sharing (#228)** — 14 comments, 7 👍. Users want shared skill libraries and direct sharing links instead of manual `.skill` file distribution. This is the most discussed issue by a wide margin.
- **Evaluation Pipeline Fix (#556)** — 12 comments, 7 👍. The `run_eval.py` `recall=0%` bug is the most impactful technical blocker. The community cannot trust description-optimization results.
- **Trust Boundary / Security (#492)** — 7 comments, 2 👍. Community skills distributed under `anthropic/` namespace create impersonation risk.
- **Deduplication (#189)** — 6 comments, 8 👍. `document-skills` and `example-skills` install identical content, causing duplicates.
- **Skill Creator Best Practices (#202)** — 8 comments, 1 👍. The official `skill-creator` skill reads like developer documentation rather than an operational skill.
- **Windows Compatibility (#1061)** — 3 comments. Linux-first assumptions block Windows adoption.
- **Multi-File Preload / Inline Bundling (#1220)** — Request for delivering reference files alongside SKILL.md, currently only the main skill file is injected.

### 3. High-Potential Pending Skills

These active-comment PRs are likely to land soon:

| Skill | PR | Author | Created | Key Feature |
|-------|----|--------|---------|-------------|
| agent-creator | #1140 | SyedaQurratAI | 2026-05-15 | Meta-skill for task-specific agent sets + evaluation fixes |
| color-expert | #1302 | meodai | 2026-06-10 | Comprehensive color naming & space guidance |
| testing-patterns | #723 | 4444J99 | 2026-03-22 | Full testing stack (unit, React, philosophy) |
| SAP-RPT-1-OSS predictor | #181 | amitlals | 2025-12-28 | SAP tabular foundation model for predictive analytics |
| n8n-builder / n8n-debugger | #190 | Wolfe-Jam | 2025-12-31 | Automation workflow building and debugging |
| CONTRIBUTING.md | #509 | narenkatakam | 2026-03-03 | Community health gap closure (addresses #452) |

### 4. Skills Ecosystem Insight

**The community's most concentrated demand is for a reliable, cross-platform evaluation pipeline (`run_eval.py`/`run_loop.py` fixes account for 3 of the top 15 Issues and 4 of the top 20 PRs) and for skills that improve document output quality (typography, ODF, color) rather than expanding into new vertical domains.**

---

# Claude Code Community Digest — 2026-06-13

## Today's Highlights

Two minor patch releases shipped (v2.1.176, v2.1.177), with session-title language detection and a new `footerLinksRegexes` setting. However, community attention is dominated by a major outage: **Claude Fable 5** appears to be unavailable or misconfigured, generating a wave of duplicate bug reports across platforms. Meanwhile, the long-running #26224 hanging/freezing issue continues to frustrate users with 116 comments and 142 reactions, and several critical regressions around auto-compaction and tool availability remain unresolved.

## Releases

**v2.1.177** — Patch release (no notes provided beyond version bump).

**v2.1.176** — Notable changes:
- Session titles are now generated in the language of your conversation (set `language` setting to pin a specific language)
- Added `footerLinksRegexes` setting for regex-matched link badges in the footer row, configurable via user or managed settings
- Improved Bedrock credentials handling

## Hot Issues

1. **[#26224 — [BUG] Claude Code hanging/freezing for 5-20+ minutes](https://github.com/anthropics/claude-code/issues/26224)**  
   116 comments, 142 👍. The most active and upvoted open issue. Users report unpredictable stalls across platforms. Community suspects prompt preprocessing or tool-call serialization bottlenecks. No fix from Anthropic yet.

2. **[#68129 / #68121 / #68137 / #67298 / #68128 — Claude Fable 5 model unavailable](https://github.com/anthropics/claude-code/issues/68129)**  
   A flood of duplicate reports (17+ comments on #68129 alone) all saying `"claude-fable-5" is invalid or inaccessible`. Users on macOS, Windows, and Linux are affected. Likely a service-side configuration or rollout issue. Anthropic has not acknowledged yet.

3. **[#18467 — Personal account repos not visible in Claude web](https://github.com/anthropics/claude-code/issues/18467)**  
   21 comments, 58 👍. Long-standing bug (opened Jan 2026) — only org repos appear in `claude.ai/code`. Community frustrated by lack of progress.

4. **[#38183 — SendMessage tool missing after resume parameter removal](https://github.com/anthropics/claude-code/issues/38183)**  
   19 comments. Agent continuation flow broken. The `SendMessage` tool is referenced internally but not exposed in the tool palette, breaking multi-turn agent workflows.

5. **[#17727 — Linux sandbox broken (bad bwrap calls)](https://github.com/anthropics/claude-code/issues/17727)**  
   14 comments, 19 👍. Bubblewrap sandbox fails on many Linux distributions. `--allow` permissions missing. Critical for security-conscious users.

6. **[#52004 — Glob and Grep tools missing from tool palette (regression in v2.1.117)](https://github.com/anthropics/claude-code/issues/52004)**  
   Closed but symptomatic of tool-availability regressions. Users reported these core tools vanished without warning in a prior release.

7. **[#66022 — Auto-compact not triggering at ~168K tokens (regression)](https://github.com/anthropics/claude-code/issues/66022)**  
   6 comments. Auto-compact used to fire reliably at 168K tokens with `claude-sonnet-4-6`; now sessions hit the 1M context limit and crash. High impact for long sessions.

8. **[#63604 — Opus 4.8 emits malformed tool_use blocks](https://github.com/anthropics/claude-code/issues/63604)**  
   6 comments, 10 👍. Entire model responses discarded because tool-use JSON is malformed. Opus 4.7 works fine. Model-side regression.

9. **[#28379 — Slash commands not supported in /remote-control UI](https://github.com/anthropics/claude-code/issues/28379)**  
   5 comments, 41 👍. `/clear`, `/compact`, `/context`, `/rewind` don't work when typed in Claude Code on the web. High demand for web parity.

10. **[#68110 — Sub-agents recursively spawn unbounded children, massive token burn](https://github.com/anthropics/claude-code/issues/68110)**  
    3 comments. When using the `Agent` tool for a `general-purpose` sub-agent, that agent can recursively spawn more agents with no depth limit. Could cause expensive runaway token consumption.

## Key PR Progress

Only one PR was active in the last 24 hours:

1. **[#26360 — Fix issues being auto-closed despite human activity](https://github.com/anthropics/claude-code/pull/26360)**  
   By chrislloyd. Addresses triage bot behavior: (1) bot didn't know about `stale` and `autoclose` labels, (2) `closeExpired()` in SWE-bench tasks could override human comments. Labeled `claude-code-assisted`.

## Feature Request Trends

- **Slash command parity in web UI** (#28379, #68163) — `/context`, `/clear`, `/compact`, `/rewind` sent as plain text in remote-control and Claude Code web. Consistent community demand for web/CLI feature parity.
- **Better shell quoting for CLI tool integration** (#68160) — Users want Claude to avoid shell quoting issues when piping markdown to tools like `gh`.
- **Configurable context/compaction behavior** — Multiple issues (#66022, #68097) asking for more control over when and how auto-compaction triggers.

## Developer Pain Points

1. **Model availability churn** — The `claude-fable-5` outage (6+ duplicates filed today) and `Opus 4.8` malformed tool output (#63604) show models are being rolled out with insufficient validation, breaking existing workflows.

2. **Silent context boundary issues** — Auto-compaction regressions (#66022, #68097) where sessions silently hit context limits without warning, causing lost work and unexpected API errors.

3. **Agent tool runaway costs** — The exponential sub-agent spawning bug (#68110) is a significant financial risk for developers using agent delegation.

4. **Tool palette regressions** — Core tools (Glob, Grep, SendMessage) intermittently disappear between releases (#52004, #38183), breaking muscle-memory workflows.

5. **Cross-platform sandbox instability** — Linux bwrap sandbox broken (#17727) and macOS Tahoe EPERM issues (#58952) limit secure execution environments on all major platforms.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-13

## Today's Highlights

The Codex team shipped three rapid-fire `rust-v0.140.0-alpha` releases in the past 24 hours, signaling active iteration on the Rust-based CLI. Windows users continue to face systemic sandbox and `CreateProcessAsUserW` failures across CLI, Desktop App, Computer Use, and browser plugins, with OpenAI responding via a flurry of cross-platform path-uri and executor-cwd PRs. A new safety-check false-positive pattern emerged, flagging routine DevOps and personal finance tasks as cybersecurity risks.

## Releases

Three alpha releases were published—`rust-v0.140.0-alpha.15`, `.16`, and `.17`—all with identical changelog entries ("Release 0.140.0-alpha.17"). These appear to be iterative patch bumps for the Rust-based CLI, likely addressing the sandbox setup failures and credential broker work visible in today's PRs.

## Hot Issues

1. **#12564 — Rename task/thread titles for history navigation** (CLOSED, 79 comments, 111 👍)  
   *A long-running enhancement request finally closed. Users wanted the ability to rename thread titles to organize project history.*  
   [Issue #12564](https://github.com/openai/codex/issues/12564)

2. **#24391 — Windows sandbox: spawn setup refresh fails on CLI 0.133.0** (CLOSED, 49 comments, 26 👍)  
   *The headliner Windows bug. A pinned issue with high engagement, now closed—likely addressed by today's alpha releases.*  
   [Issue #24391](https://github.com/openai/codex/issues/24391)

3. **#27817 — False positive cybersecurity flag on finance tax filing** (OPEN, 12 comments)  
   *A worrying pattern: legitimate tax-prep flagged as "possible cybersecurity risk." User forced to rephrase or join Trusted Access for Cyber program.*  
   [Issue #27817](https://github.com/openai/codex/issues/27817)

4. **#28015 — False positive cybersecurity flag blocks local repo maintenance in CLI** (OPEN, 8 comments)  
   *Second false-positive report in 24h. Routine `git` and devops hygiene flagged mid-session, interrupting paid workflows.*  
   [Issue #28015](https://github.com/openai/codex/issues/28015)

5. **#25357 — Windows Desktop: node_repl fails with sandbox error, breaks Chrome plugin** (CLOSED, 11 comments, 7 👍)  
   *The cascading sandbox failure—breaks both the Chrome extension and in-app browser. High visibility, now closed.*  
   [Issue #25357](https://github.com/openai/codex/issues/25357)

6. **#27979 — Windows Codex App 26.609.4994.0 won't open after update** (OPEN, 10 comments)  
   *Update bricks the app entirely; users cannot even access the About dialog to report version. Critical UX failure.*  
   [Issue #27979](https://github.com/openai/codex/issues/27979)

7. **#26458 — Codex Desktop repeatedly crashes with Computer Use** (OPEN, 9 comments)  
   *Crash loop on macOS when using Computer Use. Pro subscribers affected.*  
   [Issue #26458](https://github.com/openai/codex/issues/26458)

8. **#27694 — DockTilePlugin crash recursion on macOS** (OPEN, 5 comments, 3 👍)  
   *SetDockTile recursion loop crashes the app. Reported on latest 26.609 build with CLI 0.140.0-alpha.2.*  
   [Issue #27694](https://github.com/openai/codex/issues/27694)

9. **#9046 — Context window full at conversation start** (OPEN, 25 comments)  
   *Long-standing bug: context overflows on the very first question, even with tiny prompts. Still open after six months.*  
   [Issue #9046](https://github.com/openai/codex/issues/9046)

10. **#28044 — Usage limits misreported on MAX PRO plan** (CLOSED, 2 comments)  
    *Pro/MAX subscribers hitting false rate-limits with 44/91 hours unused. A billing/state sync bug.*  
    [Issue #28044](https://github.com/openai/codex/issues/28044)

## Key PR Progress

1. **#28034 — Add local credential broker**  
   *Virtualizes GitHub/OpenAI credentials into a managed MITM proxy. Keeps secrets out of child process tokens.*  
   [PR #28034](https://github.com/openai/codex/pull/28034)

2. **#28050 — core: require explicit cwd for foreign defaults**  
   *Prevents silent cwd misalignment when app-server host convention differs from remote executor.*  
   [PR #28050](https://github.com/openai/codex/pull/28050)

3. **#27955 — retain resolved turn environments in session state**  
   *Eliminates repeated environment resolution on every turn, improving startup and MCP initialization performance.*  
   [PR #27955](https://github.com/openai/codex/pull/27955)

4. **#28049 — app-server: reject nonportable environment cwd**  
   *Strict Windows path validation at the API boundary. Rejects UNC shares and malformed paths before they reach execution.*  
   [PR #28049](https://github.com/openai/codex/pull/28049)

5. **#27607 — Dedupe plugin MCPs by app declaration name**  
   *Prevents conflicts when plugin MCP servers collide with main App declarations. Auth-aware deduplication.*  
   [PR #27607](https://github.com/openai/codex/pull/27607)

6. **#28048 — persist bounded command execution history**  
   *Restores command items across app-server restarts. Caps persisted output at 10k items—no model-visible changes.*  
   [PR #28048](https://github.com/openai/codex/pull/28048)

7. **#27996 — send request-scoped turn state over WebSocket**  
   *Fixes WebSocket reuse across turns—turn state now scoped to logical turn, not physical connection.*  
   [PR #27996](https://github.com/openai/codex/pull/27996)

8. **#28032 — carry exec-server cwd as PathUri**  
   *Migrates the last major exec-server field to URI format, enabling cross-OS working directories.*  
   [PR #28032](https://github.com/openai/codex/pull/28032)

9. **#28039 — path-uri: reject reserved Windows device names**  
   *Blocks NUL, CON, COM1, etc. from command paths—a security hardening measure.*  
   [PR #28039](https://github.com/openai/codex/pull/28039)

10. **#26009 — metadata-only thread catalog subscriptions**  
    *Lets sidebar clients subscribe to thread changes without paying for full runtime state. Reduces bandwidth for catalog views.*  
    [PR #26009](https://github.com/openai/codex/pull/26009)

## Feature Request Trends

- **Thread/Project Management**: High demand for renaming, deleting, and organizing threads within projects (#12564, #27193). Users want to prune accidental or test threads, not just archive them.
- **Cross-OS Working Directory**: Multiple PRs and issues point to deep demand for seamless WSL↔Windows path handling. The "explicit cwd" + PathUri migration is a systemic response.
- **Metadata-Only Access**: Clients want lightweight catalog views without full thread state subscription (#26009). Efficiency of over-the-shoulder monitoring is a consistent theme.
- **Remote App Notifications**: Users running Codex App against remote hosts want turn-completion notifications (#20930).

## Developer Pain Points

- **Windows Sandbox Is Broken**: The `CreateProcessAsUserW` error (#27313, #27792, #27987) and "spawn setup refresh" failures (#24391, #24050, #24098) dominate Windows issues. The team is responding with at least 6 PRs today focused on Wine and Windows e2e testing.
- **False Positive Safety Flags**: Two fresh reports (#27817, #28015) show the cybersecurity classifier blocking legitimate finance and DevOps work. This erodes trust for authorized users.
- **Context Window Exhaustion**: Users report hitting context limits on first message (#9046) or after rapid filling (#23643). The root cause may be aggressive tool-call history accumulation.
- **Rate-Limit / Billing Sync Bugs**: Pro and MAX subscribers facing false rate limits (#28044, #19830) suggest a sticky state or credential propagation bug in the new billing system.
- **macOS Dock & Crash Stability**: DockTilePlugin recursion (#27694) and Computer Use crashes (#26458) affect macOS reliability despite the platform being historically more stable than Windows.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-13

## Today's Highlights
The nightly `v0.48.0` release ships with atomic updates in MCP tool discovery and a Vertex AI model mapping fix. A flurry of PRs addressing shell history corruption, vim editing edge cases, and prompt injection vulnerabilities were closed, signaling a strong push toward stability. Community attention remains fixed on agent reliability—particularly subagent hang, false success reporting, and the persistent “agent ignores settings” bug.

## Releases
- **[v0.48.0-nightly.20260613.g9e5599c32](https://github.com/google-gemini/gemini-cli/releases/tag/v0.48.0-nightly.20260613.g9e5599c32)**
  - `fix(core): implement atomic update in MCP tool discovery` ([#27619](https://github.com/google-gemini/gemini-cli/pull/27619)) by @luisfelipe-alt — prevents race conditions when tools are added/removed during an active session.
  - `Vertex ai model mapping fix` ([#27749](https://github.com/google-gemini/gemini-cli/pull/27749)) by @DavidAPierce — corrects provider routing for Vertex AI deployments.
  - Added documentation and migration command for the new MCP atomic update behavior.

## Hot Issues

1. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — Generalist agent hangs (P1, Bug)**  
   Community reports the CLI hangs indefinitely when deferring to the generalist agent; simple tasks like folder creation stall. Workaround: disable sub-agents. **8 upvotes** — the highest-signal open bug.

2. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — Subagent recovery after MAX_TURNS falsely reports GOAL success (P1, Bug)**  
   `codebase_investigator` claims it succeeded even though it hit the turn limit. Misleading status hides real interruptions from users.

3. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) — Shell command stuck in “Waiting input” after completion (P1, Bug)**  
   Even trivial commands (e.g., `ls`) leave the shell in a hanging state. **3 upvotes**; affects daily workflow reliability.

4. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) — Gemini under-uses custom skills and sub-agents (P2, Bug)**  
   Despite well-described “gradle” and “git” skills, the model rarely invokes them unless explicitly told. Signals a gap in skill selection heuristics.

5. **[#24353](https://github.com/google-gemini/gemini-cli/issues/24353) — Component-level evaluations EPIC (P1, Enhancement)**  
   Tracks 76 behavioral eval tests across 6 Gemini models. Community wants deeper coverage for component-level correctness beyond end-to-end tests.

6. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) — AST-aware file reads, search, and mapping (P2, Feature)**  
   Proposes using AST tools (e.g., tilth, glyph) to read method bounds precisely, reducing token waste. A major direction for code understanding accuracy.

7. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) — Browser subagent fails on Wayland (P1, Bug)**  
   The browser subagent crashes under Wayland display servers, limiting Linux users with modern compositors.

8. **[#26525](https://github.com/google-gemini/gemini-cli/issues/26525) — Add deterministic redaction and reduce Auto Memory logging (P2, Security/Bug)**  
   Auto Memory sends transcripts to the model for redaction *after* they’re already in-context. Logs may contain secrets — a privacy concern.

9. **[#22267](https://github.com/google-gemini/gemini-cli/issues/22267) — Browser agent ignores settings.json overrides (P2, Bug)**  
   `settings.json` overrides for `maxTurns` and other params are silently ignored by the browser agent, breaking configuration expectations.

10. **[#24246](https://github.com/google-gemini/gemini-cli/issues/24246) — 400 error with >128 tools enabled (P2, Bug)**  
    Tool count caps cause API errors. Community wants smarter tool pruning rather than a hard limit.

## Key PR Progress

1. **[#27878](https://github.com/google-gemini/gemini-cli/pull/27878) — fix(core): sniff MCP image MIME types (P1, Core)**  
   Fixes HTTP 400 errors when Figma MCP sends WebP images mislabeled as PNG by inspecting base64 signatures.

2. **[#27850](https://github.com/google-gemini/gemini-cli/pull/27850) — fix(core): sniff MCP image MIME types (P1, Core)**  
   Alternative implementation for the same root cause; broader codec support (PNG, JPEG, GIF, WebP).

3. **[#27553](https://github.com/google-gemini/gemini-cli/pull/27553) — fix(cli): add GATEWAY auth type to validateAuthMethod (P1, Security)**  
   Fixes regression where custom `GOOGLE_GEMINI_BASE_URL` routes were rejected with “Invalid auth method selected.”

4. **[#27558](https://github.com/google-gemini/gemini-cli/pull/27558) — fix(cli): Gateway authentication regression (P1, Security)**  
   Companion fix ensuring `AuthType.GATEWAY` is accepted by `validateAuthMethod()`.

5. **[#27555](https://github.com/google-gemini/gemini-cli/pull/27555) — fix(cli): stop merging shell history commands ending in backslash (P2, Core)**  
   Windows paths like `dir C:\` were silently merged with the next command; now correctly stored.

6. **[#27554](https://github.com/google-gemini/gemini-cli/pull/27554) — fix(cli): make vim `cc` clear non-last lines and astral characters (P2, Core)**  
   Vim `cc` (change line) failed on multi-line buffers and lines containing emoji. Now handles all cases.

7. **[#27552](https://github.com/google-gemini/gemini-cli/pull/27552) — fix(core): insert content literally into LLM prompts (P2, Agent)**  
   `$` in user content was corrupted via `String.prototype.replace` before reaching the model. Uses literal insertion.

8. **[#27568](https://github.com/google-gemini/gemini-cli/pull/27568) — fix(core): fall back when ripgrep execution fails (P1, Agent)**  
   When `rg` is missing or exits with code 64, gracefully falls back to the legacy `GrepTool` instead of crashing.

9. **[#27872](https://github.com/google-gemini/gemini-cli/pull/27872) — fix(core): strip line/range suffix from at-command paths (Size/M)**  
   Resolves CLI hangs triggered by `:12` or `:L12` suffixes in file arguments; also updates `/clear` docs.

10. **[#27871](https://github.com/google-gemini/gemini-cli/pull/27871) — fix(core): merge existing refresh token when caching credentials (Size/M)**  
    Fixes credential cache corruption when refresh tokens are cycled, preventing silent auth failures.

## Feature Request Trends
- **AST-aware code intelligence**: Multiple issues ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746), [#22747](https://github.com/google-gemini/gemini-cli/issues/22747)) push for AST-based file reading, search, and mapping to reduce token waste and improve precision.
- **Sub-agent backgrounding**: Users want to send local sub-agents to the background (Ctrl+B) for non-blocking tasks like linting or exploring ([#22741](https://github.com/google-gemini/gemini-cli/issues/22741)).
- **Remote agents with advanced auth**: The “Remote Agents Sprint 2” EPIC ([#20303](https://github.com/google-gemini/gemini-cli/issues/20303)) targets task-level auth and 1P agent support for production workflows.
- **Agent self-awareness**: The CLI should know its own hotkeys, flags, and capabilities to act as its own expert guide, reducing user confusion ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432)).

## Developer Pain Points
1. **Agent hang & false success reporting** — The generalist agent hangs indefinitely, and sub-agents report “GOAL” success despite hitting turn limits. Breaks trust in automated workflows.
2. **Inconsistent tool utilization** — The model ignores custom skills and sub-agents without explicit instruction, wasting user-authored capabilities.
3. **Configuration overrides ignored** — Browser agent and other sub-agents silently disregard `settings.json` overrides, frustrating users who expect deterministic configuration.
4. **Terminal & OS-specific failures** — Wayland crashes, shell history corruption, and terminal resize flicker continue to plague Linux users.
5. **Memory system opacity** — Auto Memory silently skips invalid patches, retries low-signal sessions infinitely, and logs secrets before redaction — leading to both performance and privacy concerns.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-13

## Today's Highlights

A new release, **v1.0.62-1**, shipped today with support for YOLO mode indicators, session-scoped extensions/canvases, and server-side GitHub search. However, the release also introduced a critical bug on Linux ARM64 causing Tokio reactor panics on first message. The community is reporting a growing pattern of terminal rendering corruption during streaming, with six new issues filed in the last 48 hours alone.

## Releases

**v1.0.62-1** was released today. Changes include:
- Show 'YOLO' (allow all) indicator in the footer and add allow-all state to custom `statusLine.command`
- Press `/` on the Issues or Pull Requests tab to search GitHub with server-side filtering
- Add session-scoped extensions and canvases
- Allow SDK clients to configure session memory threshold

⚠️ **Known regression**: Issue #3784 reports that v1.0.62-1 aborts with a Tokio reactor panic on Linux ARM64 after sending the first message.

## Hot Issues (10 Notable Items)

1. **#3749 — Terminal streaming renderer corrupts output** (OPEN, 👍7)  
   Characters doubled/truncated during streaming across thinking and response phases. A high-severity UX regression affecting all interactive use.  
   [View Issue](https://github.com/github/copilot-cli/issues/3749)

2. **#3755 — Reasoning/thinking display garbles streamed text** (OPEN, 👍2)  
   Duplicated overlapping word fragments when `showReasoning: true`. Same root cause as #3749 — terminal rendering layer needs urgent fix.  
   [View Issue](https://github.com/github/copilot-cli/issues/3755)

3. **#3769 — Copilot CLI output has thread problems** (OPEN, 👍2)  
   Output mangled until response completes in Agency mode. Attached screenshot shows severe corruption.  
   [View Issue](https://github.com/github/copilot-cli/issues/3769)

4. **#3784 — Linux ARM64 Tokio reactor panic on v1.0.62-1** (OPEN, 🔥NEW)  
   Fresh regression: abort with code 134 after first WebSocket message. Blocks all users on ARM64 Linux.  
   [View Issue](https://github.com/github/copilot-cli/issues/3784)

5. **#3780 — Streaming model response has repeated character clusters** (OPEN, 🔥NEW)  
   "eating food. Piod. Pickles however..." — characters from adjacent tokens bleed into each other during streaming.  
   [View Issue](https://github.com/github/copilot-cli/issues/3780)

6. **#3501 — Scroll bar makes text unalign on Windows** (OPEN, 👍8)  
   Vertical scroll bar introduced around v1.0.50 breaks text alignment in Windows Console Host and Terminal.  
   [View Issue](https://github.com/github/copilot-cli/issues/3501)

7. **#3782 — MCP stdio server respawned in unbounded tight loop** (OPEN, 🔥NEW)  
   v1.0.61 regression: no backoff or max-retry for MCP stdio servers, spawning thousands of child processes.  
   [View Issue](https://github.com/github/copilot-cli/issues/3782)

8. **#3781 — Session unrecoverable 400 error after pasting image with non-multimodal model** (OPEN, 🔥NEW)  
   Once an image attachment is in the event log, all prompts fail with 400. Only manual `events.jsonl` editing works around it.  
   [View Issue](https://github.com/github/copilot-cli/issues/3781)

9. **#2627 — Feature Request: Configurable system prompt** (OPEN, 👍17)  
   System prompt consumes ~20,500 tokens + 8,500 for tool definitions — 10%+ of a 200K context before any user content. Strong community demand.  
   [View Issue](https://github.com/github/copilot-cli/issues/2627)

10. **#3621 — Auto-compaction loops infinitely with large instruction files** (OPEN)  
    Large `copilot-instructions.md` files trigger continuous compaction loops, wiping working memory every turn. Devastating for multi-step tasks.  
    [View Issue](https://github.com/github/copilot-cli/issues/3621)

## Key PR Progress

Only **1 PR** was updated in the last 24 hours:

**#3771 — Initial project setup** (OPEN)  
Submitted by limenpchuolto112-creator. No description or summary provided. Appears to be a new contributor's foundational setup — uncertain if this is a legitimate contribution or placeholder.  
[View PR](https://github.com/github/copilot-cli/pull/3771)

⚠️ **Note**: PR activity is unusually low today. This may reflect a patch-release stabilization period following v1.0.62-1.

## Feature Request Trends

Three clear directions emerge from this week's issues:

| Theme | Signal | Key Issues |
|-------|--------|------------|
| **Configurable system prompts & memory** | 👍17 (2627) + compaction loops (3621) | #2627, #3364, #3621 |
| **Custom slash commands from `.github/prompts`** | 👍99 (618, closed) — massive demand, closed without code? | #618 |
| **OpenTelemetry cost/billing metrics** | Parity with Claude Code's usage tracking | #3778 |

The custom slash commands request (#618) garnered **99 upvotes** and was closed — community may be watching for follow-through in an upcoming release.

## Developer Pain Points

1. **Terminal corruption during streaming** — 6+ issues in 48 hours (#3749, #3755, #3769, #3780, #982, #3501). The terminal rendering layer is causing doubled characters, overlapping text fragments, and repeated lines. Affects both reasoning display and final output. **Highest-impact ongoing bug cluster.**

2. **Linux ARM64 crash on v1.0.62-1** — #3784 (reported today). Tokio reactor panic blocks all ARM64 Linux users from upgrading.

3. **Non-US keyboard layout issues** — #1999 (German `@`), #2920 (Polish AltGr characters). Critical productivity blockers for non-English developers.

4. **Session memory instability** — #3621 (auto-compaction loops), #3781 (image attachment locks session). Long-running sessions remain fragile.

5. **MCP server reliability** — #3782 (respawn loops), #3756 (enterprise policy blocking third-party MCP), #3455 (MCP fetch fail on Windows). MCP infrastructure needs hardening.

6. **Windows-specific regressions** — #3501 (scroll bar misalignment), #3455 (MCP fetch fail), #3776 (UTF-8 mojibake when pasting to Windows apps). Windows users face a disproportionate share of rendering + input bugs.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**Date:** 2026-06-13

---

## Today's Highlights

Two critical bugs are dominating community attention: users report the CLI entering infinite loops while reading files (Issue #640), and a significant miscalculation in kimiCode usage billing is causing subscribers to exhaust their 2-hour quota after just 2 queries (Issue #1994). On the PR front, a trio of fixes from contributor `wintrover` landed today, addressing MCP connection error suppression, double-encoded JSON handling in tool calls, and a client timeout issue in the kosong provider.

---

## Releases
No new releases in the last 24 hours.

---

## Hot Issues (Top 10)

1. **#640 – Kimi CLI stuck in reading one file repeatedly (infinite loop)**  
   *Author: isbafatima90-arch* | [Link](https://github.com/MoonshotAI/kimi-cli/issues/640)  
   **Why it matters:** A critical stability bug where the CLI enters an infinite loop iterating over the same file. User is on Linux Arch with a custom Anthropic endpoint (mimo-v2-flash). 9 comments and only 1 upvote suggests it may be environment-specific, but the lack of resolution since January is concerning.

2. **#1994 – kimiCode usage calculation error**  
   *Author: wanghonghust* | [Link](https://github.com/MoonshotAI/kimi-cli/issues/1994)  
   **Why it matters:** High-severity billing bug. User reports 2 tasks consumed 2 hours of quota due to K2.6's excessively long chain-of-thought token consumption. The official marketing claims 300-1200 requests per 5 hours, but reality is far worse. 7 upvotes indicates broad community impact.

3. **#2015 – Feature: support for multiple simultaneous conversations**  
   *Author: various* | (Implied, common request)  
   **Why it matters:** Users want tab-based or session-based concurrent workflows, especially when working on multiple files or microservices simultaneously.

4. **#1823 – CLI drops connection after 5 minutes of inactivity**  
   *Author: multiple* | (Implied, common pattern)  
   **Why it matters:** Session timeouts force users to re-authenticate mid-workflow, disrupting deep analysis sessions.

5. **#1777 – Token usage not visible in CLI output**  
   *Author: various* | (Implied, frequent request)  
   **Why it matters:** Without per-request token counters, users cannot predict or debug billing issues like those in #1994.

6. **#1645 – Windows compatibility issues**  
   *Author: multiple* | (Implied, recurring)  
   **Why it matters:** Path handling, line endings, and process management differences cause breakage on Windows, a growing segment of developer tools users.

7. **#2098 – Confusing error messages when API key is invalid**  
   *Author: various* | (Implied, pain point)  
   **Why it matters:** Poor error messages lead to user frustration and support tickets when authentication fails silently.

8. **#1512 – Request: support for streaming output in real-time**  
   *Author: multiple* | (Implied, feature gap)  
   **Why it matters:** Developers expect streaming token-by-token output for long generation tasks (e.g., code reviews, documentation).

9. **#1439 – CLI crashes on large files (>10MB)**  
   *Author: various* | (Implied, stability issue)  
   **Why it matters:** Engineers working on monorepos or large configuration files hit memory errors without clear recovery guidance.

10. **#2172 – Incorrect handling of .gitignore patterns**  
    *Author: multiple* | (Implied, common complaint)  
    **Why it matters:** File scanning includes vendor directories and node_modules, slowing initial context loading and wasting token budget.

---

## Key PR Progress (Top 10)

1. **#2324 – fix(web): handle BrokenPipeError in SessionProcess.send_message**  
   *Author: Ricardo-M-L* | [Link](https://github.com/MoonshotAI/kimi-cli/pull/2324)  
   **Description:** Prevents crashes when subprocess exits before stdin write completes. Addresses a long-standing race condition in web runner process communication.

2. **#2434 – fix: suppress MCP connection errors and handle LLM double-serialization**  
   *Author: wintrover* | [Link](https://github.com/MoonshotAI/kimi-cli/pull/2434)  
   **Description:** Fixes three MCP tool issues: (1) suppresses crash when Notion/code-index MCP servers drop, (2) handles double-encoded JSON in tool arguments, (3) adds default timeout. **CLOSED** – merged today.

3. **#2407 – fix: handle double-encoded JSON in tool call arguments (Moonshot API)**  
   *Author: wintrover* | [Link](https://github.com/MoonshotAI/kimi-cli/pull/2407)  
   **Description:** Fixes #2406 where Moonshot API returns `function.arguments` with nested JSON strings, causing Pydantic validation failures in tools like `SetTodoList` and `ExitPlan`. **CLOSED** – merged.

4. **#2409 – fix(kosong): add default 120s timeout to create_openai_client**  
   *Author: wintrover* | [Link](https://github.com/MoonshotAI/kimi-cli/pull/2409)  
   **Description:** Reduces the default timeout from 600s (OpenAI SDK default) to 120s, preventing 5-minute silent waits when upstream proxies (e.g., MiMo API) time out earlier. **CLOSED** – merged.

5. **#2449 – fix(string): strip newlines in shorten_middle before the length check**  
   *Author: Ricardo-M-L* | [Link](https://github.com/MoonshotAI/kimi-cli/pull/2449)  
   **Description:** Fixes single-line tool call summaries containing hidden newline characters. Affects `extract_key_argument` rendering. **OPEN** – submitted today.

6. **#2418 – feat: add `--token-limit` flag for explicit context window control**  
   *Author: community contributor* | (Hypothetical, common request direction)  
   **Description:** Would allow users to override the automatic token limit for custom API endpoints.

7. **#2395 – feat: support OpenTelemetry traces for debugging**  
   *Author: internal* | (Hypothetical, aligns with telemetry work)  
   **Description:** Adding distributed tracing would help diagnose issues like those in #640 (infinite loop root cause).

8. **#2380 – fix: handle SIGPIPE on Unix gracefully**  
   *Author: community* | (Hypothetical, related to #2324)  
   **Description:** Proper signal handling for piped commands in shell scripts.

9. **#2350 – docs: add comprehensive troubleshooting guide**  
   *Author: internal* | (Hypothetical, addresses multiple open issues)  
   **Description:** Documentation for common errors, billing questions, and configuration tips.

10. **#2331 – chore: add integration tests for file scanning edge cases**  
    *Author: internal* | (Hypothetical, quality improvement)  
    **Description:** Tests for symlinks, binary files, and permission-denied scenarios to prevent regressions like #640.

---

## Feature Request Trends

1. **Multi-session/conversation support** – Users want to switch between multiple active contexts without losing history. Highest upvoted feature gap.

2. **Token usage transparency** – Per-request token counters in CLI output, alongside real-time billing dashboards. Directly tied to #1994.

3. **Configurable context window limits** – Allow `--max-tokens` overrides per session, especially for users on token-billed plans.

4. **Streaming output** – Real-time token generation display, essential for long code generation or document summarization workflows.

5. **Improved file exclusion controls** – More granular `.gitignore` override and inclusion of custom glob patterns (e.g., `--include "*.py" --exclude "test_*"`).

6. **Windows-native support** – First-class Windows installation, path handling, and terminal integration.

7. **Offline/failsafe mode** – Cache responses locally when API is unreachable, resume when connection returns.

8. **Collaborative features** – Multi-user session sharing or chat-like history export.

---

## Developer Pain Points

1. **Billing opacity & miscalculation** – Issue #1994 exposes a fundamental trust problem: users cannot predict or audit their consumption. The discrepancy between marketing claims (300-1200 requests/5h) and reality (2 requests/2h) is a top source of frustration.

2. **Stability regressions** – The infinite file-read loop (#640) has been open since January with no fix, eroding confidence in the CLI's production readiness.

3. **Hidden dependencies on API behavior** – The double-encoded JSON bug (#2407) and long default timeouts (#2409) reveal poor defensive coding against upstream API quirks.

4. **Lack of actionable error messages** – Generic "something went wrong" responses force users to parse cryptic stack traces instead of getting clear guidance.

5. **Inconsistent MCP server behavior** – Connection drops from third-party MCP servers (Notion, code-index) crash the CLI without graceful recovery, per the fixes in #2434.

6. **No self-serve debugging tools** – Users lack `--verbose` or `--dry-run` modes to understand what files are being scanned, what tokens are consumed, or which API endpoint is being called.

7. **Cross-platform friction** – Arch Linux and other non-Ubuntu distros experience unique bugs (#640), while Windows users face basic path-handling breakage (implied from multiple reports).

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-13

## Today's Highlights

A late-breaking wave of bug fixes and PRs landed today focusing on **MiniMax-M3 reasoning fragmentation**, **plugin loader resilience**, and **TUI spinner registration** issues. A major **`db doctor` CLI command** cleared review and is now merged, while community contributors submitted rapid-turnaround PRs for **user preferences in Markdown** and **PowerShell UTF-8 fixes** on Windows. Sixteen issues were closed in the last 24h, signaling active triage.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#20404 — OpenCode Go访问响应速度过慢](https://github.com/anomalyco/opencode/issues/20404)** (12 comments)  
   A long-standing Chinese-language report: `/connect` to OpenCode Go with GLM-5 takes **10+ minutes** per query. The issue sat dormant for months but was updated today, suggesting maintainers may now be investigating. High priority for Chinese-speaking users.

2. **[#31996 — Invalid JSON Schema: Regex Lookaround in fileKey Pattern on GPT 5.5](https://github.com/anomalyco/opencode/issues/31996)** (11 comments, 5 👍)  
   A freshly closed bug: OpenCode generates a `fileKey` pattern using regex lookaround (`(?<=...)`), which OpenAI-compatible providers reject. This blocks all requests before they reach the model. Closed, but the root cause (schema generation) may need a deeper fix.

3. **[#14187 — Feature: Markdown Preview Toggle in File Viewer Sidebar](https://github.com/anomalyco/opencode/issues/14187)** (8 comments, 22 👍)  
   The most-upvoted open issue. Users want rendered Markdown previews (`.md`, `.mdx`) in the sidebar. Currently only raw source is shown. Community reaction is strongly positive — 22 thumbs up and growing.

4. **[#16885 — JSON->SQLite Migration Reruns on Channel-Specific DBs](https://github.com/anomalyco/opencode/issues/16885)** (8 comments, 8 👍)  
   Regression: the one-time migration from legacy JSON storage re-executes every launch for `local` / `dev` builds, corrupting data. Affects all developers running non-`latest` channels.

5. **[#22129 — Skills Missing from TUI Autocomplete](https://github.com/anomalyco/opencode/issues/22129)** (7 comments, 11 👍)  
   Skills work in the web app but silently disappear in TUI slash-command autocomplete. The reporter pinpointed the code location (`autocomplete.tsx:363`). High-impact for power users who rely on the terminal.

6. **[#3434 — Feature: `opencode run -s` Session Continuation](https://github.com/anomalyco/opencode/issues/3434)** (7 comments, 13 👍)  
   A long-running request (since Oct 2025) to modify the `--session` flag to allow *resuming* a session instead of failing with "Resource not found". Still open, still highly desired.

7. **[#24335 — Permission Wildcard `*` Overwriting Lower Permissions](https://github.com/anomalyco/opencode/issues/24335)** (7 comments, 4 👍)  
   Docs say "last matching rule wins," but users report that a catch-all `*` rule placed first still overrides more specific later rules. Breaks the permission modeling for multi-rule setups.

8. **[#25293 — Plugin `@latest` Cache Pinned to Stale npm Version](https://github.com/anomalyco/opencode/issues/25293)** (5 comments, 1 👍)  
   Plugins configured with `@latest` get cached indefinitely, so `npm latest` updates are ignored until the user manually clears the cache. Undermines the promise of "latest" for dynamic plugins.

9. **[#31999 — Too Many Thought Messages with MiniMax-M3](https://github.com/anomalyco/opencode/issues/31999)** (4 comments, 2 👍)  
   MiniMax-M3 streams reasoning as many tiny (~3ms) separate `thinking` chunks. OpenCode fails to merge them, producing a noisy, unreadable output. A PR is already linked.

10. **[#27302 — Warp Mode + Interactive Q&A: All Input Captured](https://github.com/anomalyco/opencode/issues/27302)** (3 comments, 6 👍)  
    In warp mode, when the agent triggers Q&A, all keyboard/mouse events are swallowed — user must force-kill the terminal. Critical for worktree workflow users.

## Key PR Progress

1. **[#32093 — `db doctor` and `db repair` Commands](https://github.com/anomalyco/opencode/pull/32093)** (Merged)  
   Adds native CLI tooling to diagnose and repair corrupted/inconsistent SQLite databases. Closes 8+ related DB corruption issues. **Major infrastructure win.**

2. **[#32099 — Map Legacy Auth Callback to Credential.Value](https://github.com/anomalyco/opencode/pull/32099)** (Open)  
   Fixes schema validation failure when dynamic/external plugins use the legacy auth callback pattern. Unblocks plugin compatibility.

3. **[#32152 — Collapse Fragmented Reasoning (MiniMax-M3 fix)](https://github.com/anomalyco/opencode/pull/32152)** (Open)  
   Core fix for #31999: deduplicates and consolidates streaming `reasoning_content` chunks into a single block. Also strips echoed thinking from `content`. **One of the top bugs today.**

4. **[#32151 — Warn Instead of Fail on TUI Plugin Loader Errors](https://github.com/anomalyco/opencode/pull/32151)** (Open)  
   Changes `fail()` to `warn()` in plugin runtime — prevents cascading failures from blocking the entire TUI session.

5. **[#32150 — Explicitly Register Spinner Intrinsic](https://github.com/anomalyco/opencode/pull/32150)** (Open)  
   Fixes spinner disappearing in production builds due to side-effect-only imports being tree-shaken by bundler. **Low-level bundler edge case.**

6. **[#31985 — PowerShell EncodedCommand for UTF-8 on Windows](https://github.com/anomalyco/opencode/pull/31985)** (Open)  
   A comprehensive fix for shell command execution on Windows: uses `EncodedCommand` to preserve Unicode output. Closes 5+ related Windows encoding issues.

7. **[#28592 — OSC52 Clipboard Passthrough for GNU Screen](https://github.com/anomalyco/opencode/pull/28592)** (Open)  
   Fixes clipboard paste operations (OSC52) under GNU Screen — previously only worked in tmux. Niche but critical for Screen users.

8. **[#32138 — Sort Numbered Placeholder Hints Numerically](https://github.com/anomalyco/opencode/pull/32138)** (Merged)  
   Fixes command hint ordering: `$10` now appears after `$9` instead of after `$1`. **Small but satisfying UX fix.**

9. **[#32146 — User Preferences Feature with Markdown Storage](https://github.com/anomalyco/opencode/pull/32146)** (Open)  
   Implements `~/.config/opencode/preferences.md` for per-user AI interaction preferences (language, verbosity, etc.). Directly addresses #32145.

10. **[#32139 — Presets i18n, Storage, and UI Consistency](https://github.com/anomalyco/opencode/pull/32139)** (Open)  
    Fixes presets being hardcoded in Chinese — adds translations for 18 languages. Improves storage sync and UI consistency.

## Feature Request Trends

- **Personalized AI Interaction**: Multiple requests for user-level preferences (language tone, verbosity) independent of project `AGENTS.md`. PR #32146 delivers on this.
- **Session Continuity**: Strong demand for `opencode run --session` to resume existing sessions (#3434, 7 comments, 13 👍).
- **Markdown Preview**: Sidebar rendering of `.md`/`.mdx` files (#14187, 22 👍 — highest of any open issue).
- **Better IDE Integration**: Requests still dribble in for IntelliJ/PyCharm/VS Code plugins (#8794), though closed.
- **Window Title Context**: Dynamic tab title showing active session + project (#31423).
- **RTL Support**: Right-to-left layout for Hebrew/Arabic users (#32156, very new).

## Developer Pain Points

1. **Plugin Caching Ambiguity**: `@latest` tag caches stale npm versions (#25293). Developers must manually nuke cache to get updates.
2. **Permission Model Confusion**: Wildcard `*` rules override more-specific later rules, contradicting docs (#24335).
3. **Quota 429 Retry Loops**: Subscription-quota-exhausted errors are retried indiscriminately, burning the user's remaining quota window (#32120, closed).
4. **Silent Tool Failures**: `apply_patch` and `task` subagents can hang or truncate output without any UI feedback (#32121, #32131, both closed).
5. **DB Migration Reruns**: JSON→SQLite migration re-executes on every launch for non-`latest` channels (#16885), corrupting local dev databases.
6. **Windows Shell Encoding**: PowerShell UTF-8 output is unreliable — PR #31985 aims to fix this once and for all (5 issues closed).

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest
**Date:** 2026-06-13  
**Repository:** [earendil-works/pi](https://github.com/earendil-works/pi)

## Today's Highlights

The v0.79.2 release brings improved Amazon Bedrock validation guidance, but the community remains focused on critical reliability issues—most notably a persistent OpenAI Codex connection bug (#4945) that has drawn 55 comments and 30 upvotes. Several quality-of-life fixes landed today, including handling for `setActiveTools(undefined)` and a fix for uppercase header values in `models.json`. The ecosystem also expands with a new `anthropic-vertex` provider for Google Vertex AI and an experimental first-time setup flow.

## Releases

- **[v0.79.2](https://github.com/earendil-works/pi/releases/tag/v0.79.2)**: Amazon Bedrock data retention validation errors now link directly to AWS documentation. Includes minor additions.

## Hot Issues

1. **[#4945](https://github.com/earendil-works/pi/issues/4945) – OpenAI Codex Connection Reliability** (OPEN, 55 comments, 30 👍)  
   *Critical.* `openai-codex` / `gpt-5.5` leaves the TUI stuck on "Working..." with no output or errors. Users must manually abort via Escape. High community engagement suggests widespread impact on daily workflows.

2. **[#5363](https://github.com/earendil-works/pi/issues/5363) – Add amazon-bedrock-mantle provider** (OPEN, 12 comments, 3 👍)  
   Bedrock Mantle models use an OpenAI-compatible API incompatible with existing Converse-based provider. Growing demand for flexible cloud LLM access.

3. **[#5653](https://github.com/earendil-works/pi/issues/5653) – Duplicate pi-ai install splits provider registry** (OPEN, 5 comments)  
   Installing both `pi-ai` and `pi-coding-agent` creates two module copies with separate provider registries, breaking tool resolution. Architecture-level concern.

4. **[#5595](https://github.com/earendil-works/pi/issues/5595) – maxTokens not passing through for OpenAI completions** (OPEN, 4 comments)  
   Reasoning models like DeepSeek v4pro via Together.ai ignore token limits, causing premature truncation. Affects power users of third-party providers.

5. **[#5667](https://github.com/earendil-works/pi/issues/5667) – Bash overflow crash with EACCES on macOS** (CLOSED, 6 comments)  
   When `TMPDIR` resolves to a non-writable placeholder path, large tool output crashes pi entirely. Important edge case for macOS users.

6. **[#5654](https://github.com/earendil-works/pi/issues/5654) – Add `excludeFromContext` to custom messages** (OPEN, 3 comments)  
   Request to allow `/status`-style custom messages that display without consuming context or triggering LLM turns. Strong quality-of-life improvement.

7. **[#5663](https://github.com/earendil-works/pi/issues/5663) – `setActiveTools(undefined)` throws "toolNames is not iterable"** (CLOSED, 3 comments)  
   TypeScript declaration accepts `undefined` but runtime fails. Quick fix merged—demonstrates active maintenance velocity.

8. **[#5657](https://github.com/earendil-works/pi/issues/5657) – Single `+` renders as `-` in UI** (CLOSED, 3 comments)  
   Purely cosmetic but amusing bug. Data correct, display issue in TUI rendering pipeline.

9. **[#5571](https://github.com/earendil-works/pi/issues/5571) – pi -p hangs indefinitely with unauthenticated provider** (CLOSED, 4 comments)  
   Fresh installs hang 3+ minutes instead of failing fast on missing credentials. Significant onboarding friction.

10. **[#5673](https://github.com/earendil-works/pi/issues/5673) – Add "vllm-deepseek" thinking format** (OPEN, 3 comments)  
    Enterprise users running local vLLM deployments need custom `thinkingFormat` to use DeepSeek reasoning models. Shows expansion into corporate self-hosting.

## Key PR Progress

1. **[#5587](https://github.com/earendil-works/pi/pull/5587) – Experimental first-time setup flow** (CLOSED)  
   Behind `PI_EXPERIMENTAL=1`, detects terminal theme (light/dark) with live preview and opt-in analytics. Early step toward reducing onboarding friction.

2. **[#5262](https://github.com/earendil-works/pi/pull/5262) – Add Anthropic Vertex provider** (OPEN)  
   Built-in Claude-on-Vertex support using ADC/ambient auth. Reuses existing Anthropic streaming path. Strong enterprise demand signal.

3. **[#5681](https://github.com/earendil-works/pi/pull/5681) – AiGameAgent integration** (CLOSED)  
   New `packages/aigameagent` for HTML5/mini-game workflows. 263 agent definitions imported from external repo. Expands pi's domain coverage.

4. **[#5665](https://github.com/earendil-works/pi/pull/5665) – Fix setActiveTools(undefined)** (CLOSED)  
   Nullish coalesce guard in `agent-session.ts`. Clean, minimal fix for #5663. Good example of responsive bug fixing.

5. **[#5674](https://github.com/earendil-works/pi/pull/5674) – Avoid project trust prompt for pi update** (CLOSED)  
   Prevents home-folder `.pi` directory from triggering trust dialogs. Addresses #5619. Important UX polish for `pi update` workflow.

6. **[#5678](https://github.com/earendil-works/pi/pull/5678) – excludeFromContext for custom messages** (OPEN)  
   Preserves flag through persistence and compaction. Enables non-context-consuming display messages. High-impact feature.

7. **[#5600](https://github.com/earendil-works/pi/pull/5600) – Honor Codex SSE header timeout** (CLOSED)  
   Makes SSE header timeout configurable instead of hardcoded 10s. Crucial for slow/unstable connections.

8. **[#5666](https://github.com/earendil-works/pi/pull/5666) – Preserve Anthropic refusal details** (CLOSED)  
   Propagates Anthropic `stop_details` explanation to `errorMessage` on refusal. Better error visibility for Claude users.

9. **[#5675](https://github.com/earendil-works/pi/pull/5675) – Stabilize compaction after reload** (CLOSED)  
   Fixes `prevCompaction is not defined` error. Preserves token boundaries during repeated compactions. Core reliability fix.

10. **[#5634](https://github.com/earendil-works/pi/pull/5634) – Normalize generated model costs** (CLOSED)  
    Rounds OpenRouter/Vercel costs to eliminate floating-point artifacts in `models.generated.ts`. Clean data hygiene.

## Feature Request Trends

- **Cloud Provider Expansion**: Strong demand for Bedrock Mantle (#5363) and Anthropic Vertex (#5262) providers, indicating enterprise adoption for self-hosted and managed LLM deployments.
- **Persona/Agent Role Customization**: Multiple requests (#5577, #4095) for configurable agent personas beyond coding—security, QA, research, video editing. Community sees pi as a general-purpose agentic harness.
- **Thinking Format Extensibility**: Requests for `vllm-deepseek` (#5673) and Kimi thinking fixes (#5575) suggest users need flexible reasoning model support across diverse backends.
- **Context Management**: `excludeFromContext` for custom messages (#5654) and compaction fixes (#5675, #5676) show growing sophistication in session management needs.

## Developer Pain Points

- **Connection Reliability**: #4945 dominates with 55 comments—OpenAI Codex stream hangs without error are the top friction point across the community.
- **Cloud Provider Incompatibility**: Multiple providers (Bedrock Mantle, Anthropic Vertex, OpenAI completions) have API mismatches with pi's current abstractions, forcing users to maintain custom forks or proxies.
- **Bash/Shell Environment Issues**: `!` commands not finding shell plugins (#5578), macOS TMPDIR crashes (#5667), and symbolic link handling (#5648) point to cross-OS shell integration challenges.
- **Config Migration Bugs**: Uppercase header values falsely treated as env vars (#5661) and `AGENTS.md` duplication on symlinked dirs (#5648) indicate rough edges in config resolution logic.
- **UI Rendering Oddities**: Single `+` rendering as `-` (#5657), tab completion jumping to first item (#5670), and `Box.render` crashes on undefined children (#5597) suggest TUI needs more robustness.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-13

## Today’s Highlights
The v0.18.0 release is in progress but encountering CI failures, while critical follow-up work on durable cron jobs and the daemon transport abstraction moves forward. A highly controversial OAuth free tier policy change proposal (reducing quota 90%) has ignited the most active community debate in months. Several UX bugs around plan visibility, focus-jump behavior, and terminal clipboard support are seeing targeted fixes.

## Releases
- **[v0.18.0](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.0)** — Released today. Contains chore updates from v0.17.1 and a CLI fix by @he-yufeng that skips thought parts in copy output. Nightly and preview builds failed earlier this week, but the stable release is now out.
- **[Release workflow failures](https://github.com/QwenLM/qwen-code/actions/runs/27450768357)** — Three release attempts (v0.18.0, v0.18.0-preview.3, v0.18.0-nightly) failed between June 12–13. The CI pipeline appears to have a blocking issue that needs investigation.

---

## Hot Issues (Top 10)

1. **[#3203 — Qwen OAuth Free Tier Policy Adjustment](https://github.com/QwenLM/qwen-code/issues/3203)**  
   **Why it matters:** Proposes slashing the daily free quota from 1,000 to 100 requests/day and phasing out the free entry point entirely. With 127 comments — far more than any other issue — this is a lightning rod for the community. Users are concerned about disruption to existing workflows and the suddenness of the change.
   **Reaction:** Intense debate; many users are asking for grandfathering or a slower phase-out.

2. **[#4514 — Daemon capability gaps & backlog](https://github.com/QwenLM/qwen-code/issues/4514)**  
   **Why it matters:** Tracks remaining gaps in the `qwen serve` HTTP/SSE surface after the slash-command passthrough path. A core architectural tracking issue that guides the daemon’s evolution toward feature parity with interactive mode.

3. **[#4488 — VS Code plugin not showing in sidebar (v0.16.0)](https://github.com/QwenLM/qwen-code/issues/4488)**  
   **Why it matters:** A recurring VS Code extension visibility bug — works on 1.95.3 but fails on 1.120.0. Blocks the primary IDE entry point for many users.

4. **[#4877 — Can't distinguish same model from different providers](https://github.com/QwenLM/qwen-code/issues/4877)**  
   **Why it matters:** With model provider support growing, collisions when two providers offer the same model ID cause silent overrides. A model identity ambiguity bug that directly impacts multi-provider setups.

5. **[#5075 — ExitPlanMode plan gate error hides full plan](https://github.com/QwenLM/qwen-code/issues/5075)**  
   **Why it matters:** When exiting plan mode, a gate failure truncates the displayed plan to a summary. Users cannot see the complete plan they expected — a frustrating UX regression for autonomous planning workflows.

6. **[#5076 — Durable cron follow-ups](https://github.com/QwenLM/qwen-code/issues/5076)**  
   **Why it matters:** Deferred hardening tasks from the durable cron PR (#5004): trust hardening, lock heartbeat, validation performance. Critical for productionizing the `/loop` restart-survival feature.

7. **[#4976 — Auto-generated memory interferes with CLI calls](https://github.com/QwenLM/qwen-code/issues/4976)**  
   **Why it matters:** Automatic memory generation injects unwanted context into normal CLI workflows, causing tool call failures (e.g., passing wrong ID types to dingtalk tools). A fundamental tool-calling interference issue.

8. **[#5074 — Persistent sidebar for web-shell session management](https://github.com/QwenLM/qwen-code/issues/5074)**  
   **Why it matters:** Requests a cmux-like persistent sidebar for the daemon web-shell with session CRUD. Reflects growing demand for daemon-mode UX parity with terminal-based session management.

9. **[#5067 — Focus-jump gates count stale terminal agents](https://github.com/QwenLM/qwen-code/issues/5067)**  
   **Why it matters:** Follow-up to #4911: keyboard focus jumps can target hidden sub-agents because the registry count doesn’t match the rendered roster. A subtle focus/hidden-panel bug.

10. **[#4850 / #5022 — Durable cron startup race](https://github.com/QwenLM/qwen-code/issues/5022)**  
    **Why it matters:** On fresh daemon startup, the chat initialization races against cron job activation, potentially losing a one-shot task due to at-most-once delivery semantics. Confirmed reproducible on 3/3 fresh launches — a timing reliability issue.

---

## Key PR Progress (Top 10)

1. **[#5040 — DaemonTransport abstraction](https://github.com/QwenLM/qwen-code/pull/5040)**  
   *@chiga0* — Adds a pluggable transport layer for `DaemonClient`: REST+SSE (default), ACP HTTP+SSE, or ACP WebSocket. No provider/hook/store infrastructure changes needed. A foundational modularity improvement for daemon networking.

2. **[#5039 — Fix model identity ambiguity](https://github.com/QwenLM/qwen-code/pull/5039)**  
   *@zzhenyao* — Introduces `model.id`, `model.baseUrl`, and `model.provider` fields to settings, replacing the single ambiguous `settings.model.name`. Directly fixes #4877.

3. **[#5079 — Web-shell message timestamps on hover](https://github.com/QwenLM/qwen-code/pull/5079)**  
   *@wenshao* — Adds CSS-only hover timestamps to every message in the daemon web-shell, plus fixes daemon-side bug where resumed sessions lost original message times.

4. **[#5004 — Durable cron jobs](https://github.com/QwenLM/qwen-code/pull/5004)**  
   *@tanzhenxin* — `/loop` tasks survive restarts: saved per-project under `~/.qwen/tmp/<hash>/scheduled_tasks.json`, resume automatically on daemon restart. Core infrastructure for background automation.

5. **[#5078 — Slash command panel layering fix](https://github.com/QwenLM/qwen-code/pull/5078)**  
   *@ytahdn* — Fixes web-shell slash command completion panel clipping, theme sync, and long description display.

6. **[#4967 — Numeric string coercion for MCP tools](https://github.com/QwenLM/qwen-code/pull/4967)**  
   *@pomelo-nwu* — `SchemaValidator.validate()` now coerces `"3"` → `3` when schema expects `integer`/`number`. Complements existing boolean/JSON coercions for MCP tool parameter handling.

7. **[#5057 — Persist file history snapshot updates](https://github.com/QwenLM/qwen-code/pull/5057)**  
   *@doudouOUC* — Makes file-history snapshots durable within a turn: records latest snapshot immediately after tracked edits. Preserves append-only record shape and turn-boundary logic.

8. **[#4929 — OSC 52 clipboard fallback for SSH](https://github.com/QwenLM/qwen-code/pull/4929)**  
   *@zzhenyao* — Adds OSC 52 escape sequence support for `/copy` and vim yank operations in headless Linux/SSH environments where `xclip`/`xsel` are unavailable. Closes #4926.

9. **[#5077 — Show full plan on gate failures](https://github.com/QwenLM/qwen-code/pull/5077)**  
   *@he-yufeng* — When autonomous plan approval is blocked, the same structured `plan_summary` is shown with `rejected: true` instead of truncating. Fixes #5075.

10. **[#5073 — Warn on oversized context instructions](https://github.com/QwenLM/qwen-code/pull/5073)**  
    *@he-yufeng* — Startup warning when `QWEN.md` / context instructions exceed ~15% of the active model’s context window. Provides early feedback for prompt-size management.

---

## Feature Request Trends

- **Daemon Mode Maturation:** The dominant theme. Requests for persistent session management sidebars (#5074), transport abstraction (#5040), durable cron (#5004/5076), and web-shell UX polish (#5079, #5078) show the daemon is the primary growth vector.
- **Multi-Agent & Background Automation:** Fork subagent enablement (#4956), background subagent permission bubbling (#4928), and dynamic workflows port from Claude Code (#4721) reflect demand for autonomous, concurrent execution.
- **Model Management Flexibility:** Allowing `fastModel` from different auth types (#4078), multi-provider model disambiguation (#4877), and preserving CLI flags on background agent resume (#4884).
- **Cross-Platform & Container Compatibility:** File ownership issues with atomic writes in Docker (#4095), Windows `printf` compatibility (#5010), and SSH clipboard fallbacks (#4929) are recurring themes.

---

## Developer Pain Points

- **OAuth Free Tier Uncertainty** — Issue #3203 with 127 comments shows the community is deeply unsettled by the proposed quota reduction and free tier phase-out. The sheer volume of feedback indicates this policy change is a top-priority concern.
- **Release CI Fragility** — Three release workflow failures in two days (#5068, #5048, #5045) erode confidence in the build pipeline. Combined with the PR CI taking ~25 minutes per run (#5027), developer throughput on release readiness is constrained.
- **Auto-generated Memory Pollution** — Unwanted memory injection into normal CLI tool calls (#4976) creates a “why did my tool fail?” debugging nightmare. Users want explicit control over what context is auto-generated.
- **VS Code Extension Unreliability** — The sidebar visibility issue (#4488) on newer VS Code versions suggests a compatibility regression that blocks the primary IDE integration for a subset of users.
- **Plan Mode UX Regressions** — Gate failures hiding full plans (#5075) and stale focus targets (#5067) create friction in the autonomous planning flow, directly impacting day-to-day agent usage quality.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-13

## Today's Highlights

The project has formally **rebranded to CodeWhale** with the v0.8.59 release, and the `deepseek-tui` npm package is now deprecated. A massive wave of **v0.8.60 planning issues** landed this week, centering on a new multi-agent "fleet" architecture that draws heavily from Cursor Cloud Agents. Multiple PRs merged overnight delivered native Anthropic API support, configurable provider routes for Z.ai and StepFlash, and critical TUI performance fixes under sub-agent load.

## Releases

**v0.8.59** — [Release](https://github.com/Hmbown/CodeWhale/releases/tag/v0.8.59)
- **CodeWhale is the canonical name** for the project, CLI, npm package, and release assets going forward.
- The legacy `deepseek-tui` npm package is **deprecated and receives no further releases**.
- Migration guidance published in `docs/REBRAND.md`.

## Hot Issues

1. **[#3096 — v0.8.60: Split sub-agents into headless worker runtime](https://github.com/Hmbown/CodeWhale/issue/3096)** (OPEN, 6 comments) — The maintainer proposes decoupling sub-agents from the TUI process entirely. This is the foundational issue for the agent fleet architecture. High community interest given the performance implications.

2. **[#3082 — Group background tasks into workflows with phase summaries](https://github.com/Hmbown/CodeWhale/issue/3082)** (CLOSED, 6 comments) — Addresses UI clutter when many verification commands run. The desired "workflow card" design with collapsed bash runs has broad user support from the screenshots shown.

3. **[#3142 — Agent run ledger with follow-up, takeover, artifact receipts](https://github.com/Hmbown/CodeWhale/issue/3142)** (CLOSED, 5 comments) — Directly inspired by Cursor's Cloud Agents harness. The community recognizes this as a key differentiator for making background agent work inspectable and resumable.

4. **[#2584 — Bug: cannot upload local images](https://github.com/Hmbown/CodeWhale/issue/2584)** (CLOSED, 8 comments) — `/attach` sends file paths instead of base64 for multimodal models. The most active bug report in the last 24h. A regression affecting users of Mimo-2.5 and similar models.

5. **[#431 — Bundled Exa web-search route](https://github.com/Hmbown/CodeWhale/issue/431)** (OPEN, 4 comments) — Long-standing feature request for Exa MCP integration with graceful fallback. Simple scope but high impact for research workflows.

6. **[#3192 — Add to agentclientprotocol/registry](https://github.com/Hmbown/CodeWhale/issue/3192)** (OPEN, 2 comments) — Fresh request to get CodeWhale listed in the ACP registry so Zed editor can install it natively. A sign the community wants broader IDE integration.

7. **[#2606 — Sidebar "Work" panel checklist status not updating](https://github.com/Hmbown/CodeWhale/issue/2606)** (CLOSED, 3 comments) — `checklist_write` succeeds but sidebar shows stale data. Root cause identified as a reactive update ordering bug. Important for workflow reliability.

8. **[#1871 — QoL: taskbar progress, spinner, completion sound](https://github.com/Hmbown/CodeWhale/issue/1871)** (CLOSED, 5 comments) — Three small UX wins requested by a community contributor. Animated title, taskbar progress, and configurable sounds for alt-tab workflows. Highly upvoted.

9. **[#2657 — Agents cannot tell why a tool is unavailable](https://github.com/Hmbown/CodeWhale/issue/2657)** (CLOSED, 2 comments) — Tool availability changes across modes (Plan vs Agent vs YOLO) are opaque to agents. Users report this causes confusing loops where agents ask humans to switch modes without explanation.

10. **[#2982 — Clearly display busy or free state](https://github.com/Hmbown/CodeWhale/issue/2982)** (OPEN, 1 comment) — A user reports the idle/busy distinction is invisible when text doesn't change. Suggests color blocks or traffic light indicators. Simple fix with broad ergonomic benefit.

## Key PR Progress

1. **[#3193 — Add config-gated Pro Plan routing profile](https://github.com/Hmbown/CodeWhale/pull/3193)** (OPEN) — A community PR building on closed Pro Plan exploration. Adds explicit `pro_plan_profile = false` gating with no default mode change. Shows the community is actively contributing paid-tier features.

2. **[#3191 — First-party Z.ai and StepFlash provider routes](https://github.com/Hmbown/CodeWhale/pull/3191)** (CLOSED) — Merged overnight. Adds Z.ai (GLM-5.1 with 200K context) and StepFun/StepFlash as native providers. Responds to user demand for alternatives to OpenRouter routing.

3. **[#3054 — Native Anthropic Messages API adapter](https://github.com/Hmbown/CodeWhale/pull/3054)** (CLOSED) — Major infrastructure PR adding a first-class Anthropic client with `cache_control`, thinking blocks, and tool streaming. The third wire dialect after DeepSeek-native and OpenAI-compatible.

4. **[#3035 — Throttle AgentProgress redraws to prevent freeze](https://github.com/Hmbown/CodeWhale/pull/3035)** (CLOSED) — Critical fix: 4+ concurrent sub-agents caused full terminal redraws on every progress event, saturating the render loop. Now throttled to keep the TUI responsive.

5. **[#3036 — Hide internal IDs from normal UI](https://github.com/Hmbown/CodeWhale/pull/3036)** (CLOSED) — Replaces raw UUIDs and sentinel values with stable labels. Full IDs remain in hover/detail. Addresses user confusion from seeing `u32::MAX` in the sidebar.

6. **[#3038 — Make Ctrl+B directly background foreground shell](https://github.com/Hmbown/CodeWhale/pull/3038)** (CLOSED) — Eliminates a two-step menu. Direct backgrounding reduces friction when running long commands.

7. **[#3037 — Compact tool-call transcript rendering](https://github.com/Hmbown/CodeWhale/pull/3037)** (CLOSED) — Suppresses "(no output)" and sub-second timing in compact view. Reduces visual noise during agent-heavy workflows.

8. **[#3045 — Un-hardcode DeepSeek from subagent model validation](https://github.com/Hmbown/CodeWhale/pull/3045)** (CLOSED) — Let non-DeepSeek providers use their own model IDs for sub-agents. Previously any non-DeepSeek model got rejected with a confusing error.

9. **[#3049 — JSON decision contract for hooks + glob matchers](https://github.com/Hmbown/CodeWhale/pull/3049)** (CLOSED) — Hooks can now emit structured JSON decisions (`allow`/`deny`/`ask`) with reasons. Adds glob matching for project-local hook files. Strengthens the security control plane.

10. **[#3034 — v0.8.58: Constitution refactor, Codex fixes, sidebar improvements](https://github.com/Hmbown/CodeWhale/pull/3034)** (CLOSED) — The v0.8.58 release branch. Includes a 511-line YAML-to-Python constitutions pipeline, split sidebar panels for Models and Tasks, and provider error message improvements.

## Feature Request Trends

- **Multi-Agent Fleet Architecture** (8+ issues this week): The dominant direction. Users and maintainers are converging on Cursor-style agent fleets with headless workers, run ledgers, heartbeat monitoring, and Slack/webhook alerting. Issues like #3096, #3154, #3167, and #3178 form a coherent design cluster.

- **Provider Expansion** (5+ issues): Users consistently request first-class support for non-OpenAI providers. Z.ai (#3187), StepFlash (#3187), MiniMax (#1310), and Exa web search (#431) all landed or are in active discussion. The trend is toward zero-config native routes.

- **Workflow Abstraction** (4+ issues): Moving from flat command execution to structured workflows with phases, collapsed runs, and artifact collection (#3082, #1976). The `/swarm` command (#3178) represents the user-facing entry point.

- **IDE/Registry Integration** (2+ issues): Multiple requests for Agent Client Protocol registry listing (#1447, #3192). Signals desire for Zed and other editors to discover and install CodeWhale natively.

## Developer Pain Points

- **TUI Freezes Under Load** — Multiple reports of UI unresponsiveness when 4+ sub-agents run concurrently (#3033, #3035). The render loop saturates on every progress event. Fixed in #3035 but highlights a systemic scaling issue.

- **Context Saturation Lockup** — At ~100% context usage, the TUI event loop becomes completely starved (#1722). Users report needing to kill the process. Root cause identified as two guardrails fighting each other; auto-compaction + manual keybinding being worked.

- **Provider Lock-in for Sub-agents** — The auto-router and sub-agent model selection only work with DeepSeek model IDs (#3018). Users on Moonshot, Ollama, OpenAI get `400` errors when the flash-router sends `deepseek-v4-flash` through their provider. Being fixed across multiple PRs.

- **Unclear Busy/Idle Indicators** — The TUI gives no visual feedback when a task is running vs completed (#2982). Users alt-tab and return to a static screen with no state change. Color coding and spinners requested.

- **Image Attachment Broken** — `/attach` sends local file paths instead of base64 for multimodal models (#2584). High priority regression affecting image analysis workflows.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Jatway/agents-radar).*