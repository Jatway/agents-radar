# OpenClaw Ecosystem Digest 2026-06-13

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-13 07:10 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [NullClaw](https://github.com/nullclaw/nullclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyagi)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-13

## Today's Overview

The OpenClaw project is in a period of **sustained high activity** with 500 issues and 500 PRs updated in the last 24 hours. Of the updated issues, 177 remain open/active while 323 closed; of the PRs, 355 are still open and 145 were merged or closed. A single new release, v2026.6.6, shipped today with substantial security hardening across transcripts, sandbox binds, host environment inheritance, MCP stdio, Codex HTTP access, native search policy, sender checks, deleted-agent ACP bypasses, loopback tools, Discord moderation, and Teams group actions. The project appears to be aggressively addressing a backlog of security regressions and session-state bugs while also processing feature requests and quality-of-life improvements. A critical memory leak (P0) remains open and unresolved.

---

## Releases

**v2026.6.6** (2026-06-13) — `openclaw 2026.6.6`

### Security Hardening (Explicit)
- **Transcripts:** Tighter security boundaries
- **Sandbox binds:** Strengthened isolation enforcement
- **Host environment inheritance:** Reduced leakage surface
- **MCP stdio:** Additional access controls
- **Codex HTTP access:** Restricted exposure
- **Native search policy:** Hardened defaults
- **Elevated sender checks:** Stricter identity verification
- **Deleted-agent ACP bypasses:** Closed a privilege escalation path
- **Loopback tools:** Blocked unintended localhost access
- **Discord moderation:** Strengthened command validation
- **Teams group actions:** Tighter group-level controls

### Breaking Changes / Migration Notes
No explicit breaking changes were documented in the release highlights. The security tightening may require configuration adjustments for users who relied on permissive access patterns (e.g., private network `web_fetch`, unrestricted sandbox workspaces).

---

## Project Progress

### Merged/Closed PRs Tracking (today)
The following PRs were merged or closed today, representing resolved features and fixes:

| PR ID | Title | Type | Status |
|-------|-------|------|--------|
| #92612 | fix(slack): emit accurate message_sent hooks | Bug fix | Closed |
| #92512 | Fix WebChat backscroll during streaming | Bug fix | Closed |
| #92615 | Add GitHub Actions workflow for iOS build | Build infra | Closed |
| #90627 | fix(memory-wiki): accept wiki_apply CLI op aliases | Bug fix | Closed |
| #90242 | fix(providers): skip unreadable Mistral tool schemas | Bug fix | Closed |
| #78103 | Fix plugin webhooks for Slack reply delivery | Bug fix | Closed |

### Key Feature Advances
- **WebChat:** Fixed backscroll lock during streaming (PR #92512) — users can now scroll up without being forcibly pulled back
- **Slack:** Accurate `message_sent` hooks finally emitted on outbound delivery (PR #89943 open, PR #92612 closed)
- **Memory-wiki:** `wiki_apply` CLI now accepts `synthesis` and `metadata` op aliases (PR #90627)
- **Mistral:** Unreadable tool schemas are now safely skipped instead of crashing (PR #90242)

---

## Community Hot Topics

### Most Active Issues (by comment count)

1. **#32473** — [OPEN] *"control ui requires device identity (use HTTPS or localhost secure context)"*  
   Comments: 17 | 👍: 5  
   URL: https://github.com/openclaw/openclaw/issues/32473  
   *Analysis:* A regression in Docker/VPS environments where the control UI refuses to load without HTTPS/localhost. Users on hosted infrastructure (Hostinger VPS) report being unable to access the UI after configuring API keys. This is a blocker for managed hosting deployments.

2. **#22438** — [OPEN] *"feat: Tiered bootstrap file loading for progressive context control"*  
   Comments: 17 | 👍: 0  
   URL: https://github.com/openclaw/openclaw/issues/22438  
   *Analysis:* A detailed feature request asking for smart bootstrap loading to conserve LLM token budget. Users with large workspaces want sub-agents and cron jobs to only load relevant bootstrap files instead of all files every session. High-value optimization request.

3. **#88929** — [CLOSED] *"Feishu streaming card: abnormal typewriter effect and final content truncated"*  
   Comments: 15 | 👍: 2  
   URL: https://github.com/openclaw/openclaw/issues/88929  
   *Analysis:* Feishu (Lark) users experienced broken streaming where text came out 1-2 characters at a time and final content was truncated to a single character. This was a significant UX regression for the Feishu integration. Now closed, likely fixed in v2026.6.6.

4. **#39604** — [OPEN] *"Add tools.web.fetch.allowPrivateNetwork to allow private network access"*  
   Comments: 13 | 👍: 9  
   URL: https://github.com/openclaw/openclaw/issues/39604  
   *Analysis:* Users need an opt-in config flag to allow `web_fetch` to reach internal network addresses (localhost, 10.x, 192.168.x). The current blanket block breaks many internal tool workflows. This is the **second-most upvoted open issue** and signals strong demand for controlled private network access.

5. **#18160** — [CLOSED] *"Direct Exec Mode for Cron Jobs"*  
   Comments: 13 | 👍: 11  
   URL: https://github.com/openclaw/openclaw/issues/18160  
   *Analysis:* This was the **most upvoted closed issue** (👍 11). Users complained that cron jobs forced LLM interpretation of simple commands, causing timeouts and reliability issues. The fix introduces a direct execution mode bypassing the agent turn cycle. Now closed, likely shipped in v2026.6.6 or a recent prior release.

---

## Bugs & Stability

### Critical (P0)

| Issue | Summary | Fix PR? |
|-------|---------|---------|
| **#91588** — OPEN | **Gateway Memory Leak:** RSS grows from 350MB to 15.5GB over 2-3 days, causing repeated OOM crashes and `launchd-handoff` restart cycles. First reported 2026-06-09, still open. | No fix PR identified |
| **#91778** — CLOSED | **memory_search broken since v2026.6.1:** Index metadata missing, all agents blind to vector memory. French reporter, P0 severity. | Closed (likely fixed) |

### High Severity (P1)

| Issue | Summary | Fix PR? |
|-------|---------|---------|
| **#31583** — OPEN | `exec` tool does not inherit `skills.entries.*.env` environment variables (regression). Secrets cannot be injected into subprocesses. | No fix PR linked |
| **#39476** — OPEN | A2A `sessions_send` causes duplicate messages when target agent calls back to requester. Message duplication in channels. | No fix PR linked |
| **#47975** — OPEN | Subagent sessions persist after completion, main session becomes unresponsive. Reproduced on WSL2. | No fix PR linked |
| **#38327** — OPEN | "Cannot convert undefined or null to object" error with Google Vertex/Gemini models (regression in v2026.3.2). | No fix PR linked |
| **#84569** — OPEN | WhatsApp session stalls on long model calls → `stalled_agent_run` → reply never delivered. Message loss on slow models. | No fix PR linked |
| **#53599** — OPEN | Chrome extension browser relay removed with no cross-machine replacement (regression). Breaks managed hosting providers. | No fix PR linked |
| **#66443** — OPEN | Context overflow recovery duplicates role=user messages in session JSONL, amplifying transcript growth. | No fix PR linked |
| **#92617** — OPEN (PR) | `openclaw plugins update whatsapp` silently wipes Baileys session — full QR re-pair required after every minor update. | PR #92617 open |
| **#84644** — OPEN | Windows node-host connects but reports no commands to Linux gateway. Nodes show "(none reported)". | No fix PR linked |

### Regressions (Notable)

- **#31583, #32473, #38439, #38327, #53599, #84644** — All tagged as regressions, indicating the v2026.6.x release cycle has introduced several backward-incompatible behaviors that previously worked.

### Stability Trends
The project is actively addressing a **security regression wave** (at least 6 open security-tagged issues) and a **session-state degradation pattern** (10+ issues with `impact:session-state`). The unresolved P0 memory leak (#91588) remains the highest-risk stability threat.

---

## Feature Requests & Roadmap Signals

### Strongest Signals (high demand, active discussion)

1. **Private network access for web_fetch** (#39604, 👍 9) — An opt-in `tools.web.fetch.allowPrivateNetwork` config key. **Prediction:** Likely to land in v2026.6.7 or v2026.7.0 given the 9 upvotes and active maintainer discussion.

2. **Tiered bootstrap file loading** (#22438, 17 comments) — Progressive context control to conserve tokens. **Prediction:** Strong candidate for next minor release; addresses a real token-waste pain point.

3. **Memory Trust Tagging by Source** (#7707, 9 comments) — Tag memory entries by trust level (user vs. web scrape vs. third-party) to prevent poisoning. **Prediction:** Longer-term roadmap item; requires new memory core data model.

4. **Post-subagent completion extension hook** (#22358, 12 comments) — Hook for generating trajectory files after subagent finishes. **Prediction:** Medium-term; depends on extension hook system maturity.

5. **Pre-reset agentic memory flush** (#45608, 9 comments) — Run memory flush before `/new` and daily reset. **Prediction:** High-value UX improvement; may appear in v2026.7.x.

6. **Fallback approval mode + model attribution** (#33975, 6 comments) — Transparent reporting when model fallback occurs. **Prediction:** Niche but requested; could ship as config toggle.

### Predicted Next-Release Content
- Private network access flag (if maintainers accept the pattern)
- Memory leak fix (P0 blocker for production deployments)
- WhatsApp session stall fix (high pain for WhatsApp users)
- Tiered bootstrap loading (engineering effort is moderate)

---

## User Feedback Summary

### Pain Points (most frequently reported)
1. **Security regressions breaking existing setups** — Multiple users (RafaelLee, cwebb77, LuanBSPinheiro, Yixn) report that updates break previously working functionality, especially around authentication, environment variable inheritance, and network access.
2. **Message loss / duplication in messaging channels** — Users on Telegram (#70628), WhatsApp (#84569), Slack (#92498), Feishu (#88929), and A2A (#39476) all report messages either going missing or being duplicated — a cross-channel reliability concern.
3. **Session state corruption** — Subagent sessions persisting after completion (#47975), context overflow amplification (#66443), and stalled agent runs (#84569) suggest the session management layer has systemic issues.
4. **Onboarding friction** — In Android (#61005) and control-UI HTTPS requirements (#32473), new users hit configuration walls before first successful use.
5. **CJK/Unicode rendering** — Markdown tables misaligned with CJK characters on Telegram/Discord (#55596 PR) — a quality-of-life issue for non-Latin script users.

### Satisfaction Signals
- The **security hardening in v2026.6.6** addresses long-standing community concerns about permission boundaries and data leakage.
- **Slack message_sent hooks** (#89943, #92612) — plugin developers and Slack integrators have been requesting proper hook emissions for months; this is a clear win.
- **Cron direct execution mode** (#18160, 👍 11) — highly upvoted request now delivered; users should see significant reliability improvements for automated tasks.
- **WebChat backscroll fix** (#92512) — a subtle but appreciated UX improvement that addresses a common pain point.

---

## Backlog Watch

### Issues Needing Maintainer Attention (long-unanswered, high impact)

| Issue | Age | Impact | Notes |
|-------|-----|--------|-------|
| **#29736** | ~3.5 months | Security | `exec-approvals.json` writes to `~/.openclaw` instead of configured state root. Tagged `needs-product-decision`. |
| **#30381** | ~3.5 months | Auth provider | `chatCompletions` endpoint ignores model override when agent header is present. Tagged `needs-product-decision`. |
| **#37634** | ~3 months | Session state | Sandbox `workspaceAccess: none` mounts workspace read-only, breaking tools. 6 upvotes. |
| **#33413** | ~3 months | UX | Slack tool-level progress not shown in thread status. Has a queueable-fix label. |
| **#91588** | 4 days | CRITICAL | P0 memory leak — most urgent open issue. No fix PR yet. |

### PRs Awaiting Maintainer Review

| PR | Age | Risk | Notes |
|----|-----|------|-------|
| **#91078** | 6 days | Security | Fixes `fs bridge stat` for Codex sandbox writes — blocks all Codex operations in Docker sandboxes |
| **#92606** | Today | Low | QA suite scenario runner — new feature, needs design sign-off |
| **#92495** | 1 day | Compatibility | Restore Zen model catalog for opencode extension |
| **#92498** | 1 day | Session state | Fix Slack same-channel final reply mirroring — blocks Slack reliability |
| **#89039** | 12 days | Availability | Prevent silent message loss from `EmbeddedAttemptSessionTakeoverError` — high severity |

### Notable Stale Items (no activity for 60+ days)
- **PR #12581** (2026-02-09) — Session prune lifecycle event hook. Stale, needs proof.
- **PR #51822** (2026-03-21) — Reject cron webhook URLs with embedded credentials. Stale, waiting on author. Security-relevant.
- **PR #39245** (2026-03-07) — Fix mangled tool names/IDs from OpenAI-compatible providers (Kimi). Stale, needs proof. Addresses ongoing Kimi integration issues.

---

*Generated 2026-06-13 13:00 UTC. Data sourced from openclaw/openclaw GitHub repository.*

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant Open-Source Ecosystem
**Date:** 2026-06-13

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is experiencing a **polarized growth phase**, with established projects like OpenClaw and Hermes Agent processing 500+ daily updates while smaller projects like NullClaw and Moltis see single-digit activity. A clear **"platform vs. appliance" divide** is emerging: OpenClaw, ZeroClaw, and NanoClaw are evolving toward enterprise-grade agent platforms with sophisticated security, memory management, and multi-channel delivery, while projects like PicoClaw and TinyClaw focus on lightweight, embeddable deployments. The ecosystem is converging on several technical challenges—particularly session reliability, memory persistence, and secure sandboxing—but diverging sharply in architectural philosophy, with **Rust-based projects (OpenClaw, ZeroClaw) gaining performance advantages** over Python-heavy counterparts like CoPaw and LobsterAI.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Today? | Health Score | Primary Language |
|---------|---------------------|-------------------|----------------|--------------|------------------|
| **OpenClaw** | 500 | 500 | ✅ v2026.6.6 | ⚠️ Critical P0 leak | Rust |
| **Hermes Agent** | 50 | 50 | ❌ | ✅ High velocity | Rust |
| **ZeroClaw** | 13 | 50 | ❌ | ⚠️ 5 S1 bugs | Rust |
| **IronClaw** | 43 | 50 | ❌ | ⚠️ CI blocked | Rust |
| **NanoClaw** | 4 | 18 | ❌ | ✅ Productive surge | Python/Rust |
| **CoPaw (QwenPaw)** | 20 | 19 | ❌ (beta) | ⚠️ Regression wave | Python |
| **PicoClaw** | 2 | 11 | ✅ Nightly | ✅ Steady progress | Go |
| **LobsterAI** | 4 | 8 | ❌ | ✅ Post-release stable | TypeScript |
| **NanoBot** | 8 | 34 | ❌ | ⚠️ Startup crash | Python |
| **Moltis** | 3 | 0 | ❌ | ⚠️ Consolidation | Python |
| **NullClaw** | 2 | 3 | ❌ | ❌ 13-day unaddressed bug | Zig |
| **TinyClaw** | 0 | 0 | ❌ | ❌ Inactive | Unknown |

**Key:** ✅ Healthy | ⚠️ Concerning | ❌ At risk

---

## 3. OpenClaw's Position

### Advantages vs. Peers
- **Release cadence**: v2026.6.6 shipped today with 10+ explicit security hardening items—none of its peers matched this volume or velocity
- **Community scale**: 500 daily issue/PR updates dwarfs the next largest (Hermes Agent at 50). This is a 10x activity advantage
- **Security posture**: Explicitly addressing deleted-agent ACP bypasses, loopback tools, host environment inheritance—areas untouched by competitors
- **Resolution speed**: 323 closed issues and 145 merged PRs in 24 hours demonstrates exceptional maintainer bandwidth

### Technical Approach Differences
- **Architecture**: OpenClaw's "gateway" model with launchd-handoff restart cycles is unique—NanoClaw uses Python/Rust hybrid, while IronClaw uses Rust with engine V2
- **Security philosophy**: OpenClaw is aggressively hardening defaults (private network blocking, sender checks) while ZeroClaw still ships without functional web dashboard on source installs
- **Memory management**: OpenClaw's P0 memory leak (#91588, 350MB→15.5GB) is a weakness vs. NanoClaw's working disaster recovery system and IronClaw's DeferredBusy drain mechanics

### Community Size Comparison
- **OpenClaw** dominates: 500+ daily interactions, 177 open issues, 355 open PRs
- **Second tier** (50 daily): Hermes Agent, ZeroClaw, IronClaw
- **Third tier** (10-20 daily): NanoClaw, CoPaw, PicoClaw
- **Long tail** (<10 daily): LobsterAI, NanoBot, Moltis, NullClaw, TinyClaw

---

## 4. Shared Technical Focus Areas

Across 6+ projects, consistent requirements are emerging:

| Requirement | Projects Affected | Specific Evidence |
|------------|------------------|-------------------|
| **Session state reliability** | OpenClaw, Hermes, NanoBot, NanoClaw, IronClaw | Message dedup bugs (#2506 NanoClaw), context overflow (#66443 OpenClaw), memory loss (#4044 NanoBot), WAL corruption (#45383 Hermes) |
| **Secure sandboxing** | OpenClaw, ZeroClaw, PicoClaw, Moltis | Workspace isolation, private network access (#39604 OpenClaw), symlink escape (PR #4119 NanoBot), Kubernetes sandbox (#1118 Moltis) |
| **Multi-channel delivery parity** | OpenClaw, Hermes, NanoClaw, CoPaw | Discord attachments (#11860 Hermes), WhatsApp group targeting (#18646 Hermes), Signal reactions (PR #2203 NanoClaw), Zalo support (#5168 CoPaw) |
| **Token budget management** | OpenClaw, NanoBot | Tiered bootstrap loading (#22438 OpenClaw), idleCompact data loss (#4264 NanoBot), context overflow recovery (#66443 OpenClaw) |
| **Configuration persistence** | Hermes, ZeroClaw, IronClaw, CoPaw | Model switch persistence (PR #6719 ZeroClaw), always-allow approvals across threads (#4835 IronClaw), memory config loss (PR #5144 CoPaw) |
| **Cron/scheduled job reliability** | OpenClaw, Hermes, NullClaw, CoPaw | Direct exec mode (#18160 OpenClaw), agent-type cron not spawning (#941 NullClaw), scheduled tasks fail to trigger (#5064 CoPaw) |

---

## 5. Differentiation Analysis

| Dimension | Enterprise Platforms | Lightweight/Embedded | Specialized |
|-----------|---------------------|---------------------|-------------|
| **Projects** | OpenClaw, ZeroClaw, IronClaw | PicoClaw, TinyClaw | LobsterAI, CoPaw |
| **Target users** | Power users, enterprise deployments | Developers embedding AI | Regional/Chinese market |
| **Architecture** | Rust core, multi-gateway, WASM plugins | Go single-binary, minimal dependencies | TypeScript/Python, UI-heavy |
| **Key strength** | Security & scale | Simplicity & portability | UX polish & ecosystem integration |
| **Key weakness** | Memory leaks, regression velocity | Limited features, smaller community | Backward compatibility, dependency lag |
| **Example divergence** | OpenClaw blocks private network by default; ZeroClaw adds Kubernetes sandbox (#1118); IronClaw builds attachment link system (#4644) | PicoClaw focuses on Go-native protocol handling; TinyClaw has zero activity | CoPaw prioritizes Chinese IM (Feishu, Zalo); LobsterAI integrates with NetEase ecosystem |

---

## 6. Community Momentum & Maturity

**Tier 1: Rapid Iteration (30+ daily PRs)**
- **OpenClaw** — Most mature, shipping security hardening weekly; resolving 145+ PRs/day
- **Hermes Agent** — High-velocity bug fixing (50 PRs/day), preparing for stable release candidate
- **ZeroClaw** — Architectural consolidation (unifying 3 turn engines into 1), 30 PRs merged today
- **IronClaw** — Multi-track feature development (attachment system, DeferredBusy UX), blocked by CI

**Tier 2: Steady Growth (8-20 daily PRs)**
- **NanoClaw** — Productive surge with 10 merged PRs today including disaster recovery and Signal integration
- **CoPaw (QwenPaw)** — Beta release cycle, 5 PRs merged, but regression velocity is a concern
- **PicoClaw** — Consistent Go-native development, 3 PRs merged, approaching v0.3.0
- **NanoBot** — Maintenance-heavy with 10 PRs merged, but startup crash (#4322) undermines reliability

**Tier 3: Stabilizing/At Risk (<8 daily PRs)**
- **LobsterAI** — Post-release stabilization, 5 PRs merged, healthy but quiet
- **Moltis** — Consolidation phase, 0 PRs merged, feature-driven community
- **NullClaw** — Low activity, 13-day unaddressed bug (#941), risk of contributor churn
- **TinyClaw** — **Inactive** (0 updates in 24 hours)
- **ZeptoClaw** — **Inactive** (0 updates in 24 hours)

**Maturity Assessment:** Two projects (TinyClaw, ZeptoClaw) show no activity, suggesting abandonment risk. OpenClaw dominates by volume but carries a critical P0 memory leak. The most balanced momentum sits with ZeroClaw (architectural progress + responsive maintainers) and NanoClaw (community contribution surge + working features).

---

## 7. Trend Signals

**Technical Trends (from community feedback)**

1. **"Session state is the new database"** — 10+ issues across projects involve context corruption, message dedup, memory loss, or session persistence. The community is demanding **deterministic conversation state** that survives crashes, resets, and tool failures.

2. **Multi-agent orchestration is emerging** — CoPaw's agent swarm request (#5139), ZeroClaw's skill collaboration system, and OpenClaw's subagent management all point toward **agent-to-agent workflows** as the next paradigm beyond single-agent chat.

3. **Security hardening is driving breakage** — OpenClaw's aggressive security defaults (blocking private network, tightening sandbox binds) caused 6+ regression tags. This tension between **security and backwards compatibility** is the ecosystem's defining operational challenge.

4. **Local-first AI is gaining traction** — ZeroClaw's llama.cpp model router (#7539), PicoClaw's Ollama multimodal support (PR #2072 NanoClaw), and Moltis' local STT request (#1102) signal a shift from cloud-only to **hybrid local/cloud deployments**.

5. **Channel fragmentation is a cost** — Projects support 8-12 messaging platforms each, but every platform has its own bugs (Discord attachments, WhatsApp pairing, Feishu streaming, Signal reactions). The ecosystem could benefit from a **unified channel abstraction layer**.

**Value for AI Agent Developers**

- **If building for production**: OpenClaw offers the most complete security model but watch for memory leaks; ZeroClaw's architecture consolidation suggests it's maturing rapidly
- **If building for specific channels**: NanoClaw's Signal integration and CoPaw's Chinese IM support are best-in-class; Hermes Agent has the most Discord/Telegram bug fixes in flight
- **If prioritizing developer experience**: PicoClaw's Go-native build and LobsterAI's TypeScript stack offer simpler onboarding than Rust-heavy alternatives
- **Avoid**: TinyClaw and ZeptoClaw (no activity); NullClaw (unresponsive maintainers); NanoBot (startup crashes)

**Watch list for next 30 days**: OpenClaw's P0 memory leak fix, ZeroClaw's v0.8.1 release, CoPaw's AgentScope 2.0 migration, and whether IronClaw's CI blockage is resolved—these events will reshape the competitive landscape.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the project digest for **NanoBot** on **2026-06-13**.

---

## NanoBot Project Digest — 2026-06-13

### 1. Today's Overview

This has been a high-activity, maintenance-heavy day for NanoBot. While there were no new releases, the project saw significant churn with **34 PRs updated** and **8 issues updated** in the last 24 hours. The pulse of the project is focused on **bug fixing and stability**, with a particular emphasis on memory management, tool execution safety, and WebUI configuration parity. A major theme is addressing "lost context"—both in short-term memory for user conversations and in server prompts—indicating a community push for reliability in long-running sessions.

### 2. Releases
**No new releases today.** The project remains at the previously available version.

### 3. Project Progress (Merged/Closed PRs)
**10 PRs were merged or closed today** (out of 34 updated). Key advancements include:

- **Audit System Introduction:** Three PRs by `bjoshuanoah` ([#4319](https://github.com/HKUDS/nanobot/pull/4319), [#4318](https://github.com/HKUDS/nanobot/pull/4318), [#4320](https://github.com/HKUDS/nanobot/pull/4320)) introduced a new `tools.audit` feature for agent action observability, including logging tool invocations to loguru, HTTP webhooks, or JSONL files.
- **WebUI/Config Parity:** PR [#4313](https://github.com/HKUDS/nanobot/pull/4313) by `La-Volpe` was merged, closing the gap between WebUI settings and `config.json` by adding write endpoints for temperature, tool limits, and memory fields.
- **MCP Server Fix:** PR [#4303](https://github.com/HKUDS/nanobot/pull/4303) fixed a crash (`RuntimeError: Attempted to exit cancel scope...`) when an MCP server session terminates and reconnects.

### 4. Community Hot Topics
The most active threads reveal developer frustration with agent context and configuration management:

- **#4044 [Short Term Memory Loss](https://github.com/HKUDS/nanobot/issues/4044) (5 comments):** Users report that the agent asks a question, gets an answer, and then has no memory of asking it. This is a high-priority UX issue, as it breaks the conversational flow entirely.
- **#4203 [Find Legal Message Start Bug](https://github.com/HKUDS/nanobot/issues/4203) (3 comments):** A critical logical bug in `find_legal_message_start` where "orphaned tool results" cause the entire message history to be discarded. While closed, the underlying problem of tool result management is still being seen in other issues.
- **#4264 [Idle Compact Data Loss](https://github.com/HKUDS/nanobot/issues/4264) (1 comment):** A user reports that the `idleCompact` mechanism ignores the last 8 messages, missing user corrections and leading to incorrect historical logs. A fix PR ([#4326](https://github.com/HKUDS/nanobot/pull/4326)) is already open.

### 5. Bugs & Stability
Bugs reported today are **high severity**, centered on data integrity and startup crashes.

- **[CRITICAL] #4322 [Startup Crash](https://github.com/HKUDS/nanobot/issues/4322):** `NameError: name 'session_key' is not defined` crashes the agent on startup after a merge. This is a regression that blocks any user from running the latest code.
- **[HIGH] #4307 [Post-turn Consolidation Wipes Agent Message](https://github.com/HKUDS/nanobot/issues/4307):** When context window limits are hit, the agent's own delivery message is archived during consolidation, destroying thread continuity.
- **[HIGH] #4309 [Zero Token Usage](https://github.com/HKUDS/nanobot/issues/4309):** The `/v1/chat/completions` endpoint always returns `usage` fields as `0`, making it non-compliant with OpenAI API standards.
- **[MEDIUM] #4264 [Idle Compact Data Loss](https://github.com/HKUDS/nanobot/issues/4264):** Partial history summarization leads to permanent error logging.
- **Fix PRs exist for:** #4264 (PR [#4326](https://github.com/HKUDS/nanobot/pull/4326) open), and the env-var resolution bugs (PRs [#4323](https://github.com/HKUDS/nanobot/pull/4323), [#4324](https://github.com/HKUDS/nanobot/pull/4324), [#4325](https://github.com/HKUDS/nanobot/pull/4325)).

### 6. Feature Requests & Roadmap Signals
- **Custom Provider Multiplicity (Issue [#4305](https://github.com/HKUDS/nanobot/issues/4305)):** A request for supporting multiple "custom" and "openai" providers (e.g., to use two different OpenAI-compatible backends). This suggests users are scaling their usage across multiple self-hosted or commercial LLM endpoints. **Prediction:** Likely to be included in the next minor release given the infrastructure work already being done on provider config.
- **TTS Integration (PR [#4316](https://github.com/HKUDS/nanobot/pull/4316)):** A new TTS configuration system with OpenAI, Groq, and ElevenLabs support is currently an open PR. **Prediction:** This is a strong candidate for the next release, adding significant agent interactivity.

### 7. User Feedback Summary
- **Friction Point:** The agent’s memory loss is the most vocalized pain point. Users are frustrated by the agent forgetting the context of its own questions or recent user corrections, requiring them to repeat information.
- **Data Integrity Satisfaction:** Users are dissatisfied with the reliability of historical logs, specifically the `idleCompact` and `history.jsonl` records, which they feel misrepresent the actual conversation.
- **Developer Experience Issues:** The environment variable resolution bug (env vars like `${GROQ_API_KEY}` not being parsed) is causing silent failures, leading to a perception of poor configuration reliability.

### 8. Backlog Watch
- **[Issue #4006](https://github.com/HKUDS/nanobot/issues/4006) - Orphaned Tool Results (Updated 2026-06-12):** While closed, this issue flagged a root cause that is still causing downstream bugs (see #4203). The community may need a more comprehensive fix to prevent recurrence.
- **[Issue #4305](https://github.com/HKUDS/nanobot/issues/4305) - Multiple Custom Providers (Updated 2026-06-12):** This feature has received no formal maintainer comment or milestone assignment yet, despite being a clear need for advanced users.
- **[PR #4119](https://github.com/HKUDS/nanobot/pull/4119) - Block Symlink Escapes (Updated 2026-06-12):** addresses a security concern regarding workspace sandboxing. While high-value, it remains unmerged after two weeks, potentially leaving a security gap open.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the **Hermes Agent Project Digest** for **2026-06-13**, based on the provided GitHub activity.

---

## 1. Today’s Overview

The **Hermes Agent** project shows extremely high activity today with **50 updated issues** and **50 updated pull requests**, indicating a healthy and responsive development cycle. The majority of the open items are **P2 (High)** priority, with a significant cluster of bugs related to the **Windows CLI environment**, **Discord/Telegram gateway delivery**, and **Desktop renderer stability**. While no new releases were published today, the team merged or closed **8 PRs** and saw a flurry of new fix PRs submitted (over a dozen in the last 24 hours). The project appears to be in a **high-velocity bug-fixing and polish phase**, likely preparing for a stable release candidate.

## 2. Releases

**No new releases** were published in the last 24 hours.

## 3. Project Progress

**Merged/Closed PRs Today (8 total):** The following notable PRs were closed today, indicating recent progress:
- **Discord Tool Row Dismissal:** PR #45255 (`fix(desktop): dismiss settled tool rows`) was closed, solving a UI complaint where completed tool activity could not be cleared from the chat view.
- **Telegram DM Documentation:** PR #45436 (`docs(telegram): document private DM topic read-state limitation`) was merged, improving user guidance.
- **Anthropic Model ID Normalization:** PR #45405 (`fix(models): normalize Anthropic dash-style IDs to dot-style`) was closed, fixing a regression where aggregator providers (like OpenRouter) rejected model IDs after a format change.
- **WhatsApp Group Targeting:** PR #45438 (`fix(send_message): recognize WhatsApp JIDs`) was merged, directly resolving the high-severity bug reported in Issue #18646.
- **Model Provider Auto-Detect:** PR #45434 (`fix(models): respect config.model provider+base_url before OpenRouter auto-detect`) was closed, fixing a configuration conflict where explicit provider settings were ignored.

## 4. Community Hot Topics

The community is most engaged around **session reliability** and **cross-platform delivery failures**:

- **Issue #7237 (Closed) - [Bug]: Response truncated due to output length limit** (42 comments, 5 👍)  
  *URL:* [NousResearch/hermes-agent Issue #7237](https://github.com/NousResearch/hermes-agent/issues/7237)  
  This was the **most commented issue** in history. Users reported that long-form responses (CLI chat, Telegram, Discord, Slack) are frequently cut off mid-stream. The high volume of comments suggests this is a **critical user-facing flaw** affecting core usability across all platforms.

- **Issue #44927 (Open) - [Feature]: add back streaming auto-follow as an opt-in setting** (2 comments, 3 👍)  
  *URL:* [NousResearch/hermes-agent Issue #44927](https://github.com/NousResearch/hermes-agent/issues/44927)  
  Users are requesting a return of the **auto-scroll-to-bottom** feature during streaming. The underlying need is for a **non-breaking user experience improvement**—many users found the manual scrolling disruptive.

**Analysis:** The community is prioritizing **reliability over new features**. The top-voted requests are about fixing broken core behaviors (truncation, delivery, scrolling) rather than adding exotic new tools.

## 5. Bugs & Stability

Several new high-severity bugs were reported today, with several accompanied by fix PRs:

| Severity | Issue # | Title & Link | Fix PR Exists? |
|----------|---------|--------------|----------------|
| **P1** | #45456 | [Gateway auto-resume races with inbound messages, creating duplicate AIAgent instances](https://github.com/NousResearch/hermes-agent/issues/45456) | ❌ No PR yet |
| **P2** | #45383 | [state.db recurring B-tree corruption from WAL TRUNCATE checkpoint](https://github.com/NousResearch/hermes-agent/issues/45383) | ❌ No PR yet |
| **P2** | #45401 | [subdirectory_hints.py crashes with RuntimeError when $HOME is unset](https://github.com/NousResearch/hermes-agent/issues/45401) | ❌ No PR yet |
| **P2** | #45360 | [Cron WebUI runs can show prompt-only sessions and unknown platform delivery errors](https://github.com/NousResearch/hermes-agent/issues/45360) | ✅ PR #45459 |
| **P2** | #45335 | [hermes cron edit --profile <name> returns "Job not found" for all jobs](https://github.com/NousResearch/hermes-agent/issues/45335) | ✅ PR #45451 |
| **P2** | #45409 | [Windows: uv.exe spawns blank console window on every subprocess.run call](https://github.com/NousResearch/hermes-agent/issues/45409) | ✅ PR #45453 |
| **P3** | #45374 | [Bundled Node 22 is behind current LTS (Node 24)](https://github.com/NousResearch/hermes-agent/issues/45374) | ❌ (Dependency issue) |
| **P3** | #45388 | [Renderer crash: "Maximum call stack size exceeded" when sending UI-attached image](https://github.com/NousResearch/hermes-agent/issues/45388) | ❌ No PR yet |
| **P3** | #41693 | [Hermes Desktop renderer crashes with "tapClientLookup: Index N out of bounds"](https://github.com/NousResearch/hermes-agent/issues/41693) | ❌ (Related to #45388) |

**Critical Risk:** The **P1 race condition** (#45456) where duplicate agents process messages concurrently is a **session corruption bug** that could lead to data loss or inconsistent state. The **B-tree corruption** (#45383) is also extremely dangerous as it affects `state.db` integrity directly.

## 6. Feature Requests & Roadmap Signals

The following user-requested features signal likely **next-version priorities**:

- **P3: Streaming Auto-Follow (Issue #44927)** – High demand (3 👍) for a familiar UX pattern. Highly likely to be implemented given it’s a small toggle.
- **P3: Public API for programmatic session compression (Issue #45132)** – Requested by plugin developers. Given the increase in plugin activity, this may land in a minor release.
- **P3: 1Password Integration (PR #45439)** – A security-focused feature to eliminate plaintext credential storage. This aligns with the current trend toward **secret redaction/security hardening** seen in today’s PRs (#45416, #45444). Likely to be accepted.
- **P3: Vity (Maximem AI) Memory Provider (PR #41959)** – A new memory provider plugin. Plugin ecosystem growth suggests this is on the roadmap.

**Prediction:** The **next version** will likely focus on **session reliability fixes** (WAL corruption, agent races) and **platform parity** (WhatsApp groups, Discord threads, Telegram images).

## 7. User Feedback Summary

**Pain Points (Most Common):**
- **Cross-platform inconsistency:** Users report that **Discord attachments** (#11860), **Telegram images** (#31733), and **WhatsApp group targeting** (#18646) all behave differently than expected. There is a clear frustration with the app not "just working" the same way on every platform.
- **Desktop stability:** Multiple users report the **"tapClientLookup: Index out of bounds"** crash that forces a hard reload (#41693, #45403). This is a recurring issue affecting workflow continuity.
- **HOME environment corruption:** Several reports (#27250, #25114, #36144) describe tools failing because `$HOME` is incorrectly set to the Hermes profile directory. This breaks CLI tools and user scripts.

**Satisfaction Signals:**
- The **swift merging of fix PRs** (WhatsApp targeting, Anthropic model IDs) suggests the team is responsive to urgent community reports.
- The **high volume of pull requests** (50 total today) indicates a **strong, engaged contributor base** beyond just the core team.

## 8. Backlog Watch

The following important issues remain **open without a fix PR** and have been unanswered or unassigned for an extended period:

- **Issue #16484 (P2, 28 days old)** – [Gemini provider: /model selection cannot route to /v1beta](https://github.com/NousResearch/hermes-agent/issues/16484)  
  *Problem:* Users cannot select Gemini native models. One 👍, but no maintainer response in weeks. This affects a significant provider segment.

- **Issue #13149 (P2, 54 days old)** – [Discord: inbound video attachments are rejected instead of cached](https://github.com/NousResearch/hermes-agent/issues/13149)  
  *Problem:* Video files in Discord are silently dropped. A known gap in attachment handling. No fix PR exists.

- **Issue #11860 (P2, 56 days old)** – [Discord attachments are not reliably passed into agent context](https://github.com/NousResearch/hermes-agent/issues/11860)  
  *Problem:* HTML and other files are ignored by the agent. This is a **long-standing usability bug** with no apparent progress.

- **Issue #27250 (P2, 27 days old)** – [Docker/profile mode should avoid different HOME values](https://github.com/NousResearch/hermes-agent/issues/27250)  
  *Problem:* Home directory mismatch in Docker deployments. A common production use case currently broken. Related to #25114 and #36144.

**Maintainer Attention Needed:** The **Discord attachment pipeline** (#11860, #13149) is the **oldest unresolved bug cluster** and continues to receive user reports. It represents a growing risk to user trust in Hermes as a reliable Discord bot.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-13

## 1. Today's Overview
PicoClaw shows **moderate-to-high activity** over the past 24 hours, with 11 pull requests and 2 issues updated. The project released a **nightly v0.2.9-nightly** build and merged 3 PRs, signalling ongoing feature development and bug-fixing momentum. The community is engaged on WebSocket protocol improvements and media handling, while maintainers are addressing serialization error handling across channels and tools. The presence of two stale items suggests some backlog drag, but overall the project is progressing steadily.

## 2. Releases
- **Nightly build** (v0.2.9-nightly.20260613.c362114c) published as an automated, potentially unstable build.  
- **Changelog** covers changes since v0.2.9; no explicit breaking changes or migration notes documented.  
- **No stable release** this digest. Users on stable should remain on v0.2.9.

## 3. Project Progress
**3 PRs merged/closed today:**

- [#3113 – fix(channels): check json marshal/unmarshal errors in toChannelHashes](https://github.com/sipeed/picoclaw/pull/3113) — Fixes silent error discarding in channel config serialization.  
- [#3112 – fix(tools): handle json.Marshal error in toolloop tool call arguments](https://github.com/sipeed/picoclaw/pull/3112) — Prevents loss of tool call data when JSON marshaling fails.  
- [#2551 – refactor: standardize channel identification and decouple name from provider type](https://github.com/sipeed/picoclaw/pull/2551) — Large refactor allowing multiple instances of the same channel provider; introduces `ChannelType` for consistent provider tracking.

**Open PR momentum:**  
- Media routing to image models ([#3117](https://github.com/sipeed/picoclaw/pull/3117))  
- Remote WebSocket mode for CLI agent ([#3118](https://github.com/sipeed/picoclaw/pull/3118))  
- Delta Chat gateway integration ([#3063](https://github.com/sipeed/picoclaw/pull/3063))  
- `turn.done` lifecycle signaling ([#3116](https://github.com/sipeed/picoclaw/pull/3116))

## 4. Community Hot Topics
- **#2984 – [OPEN] Add explicit turn completion signal for Pico WebSocket clients**  
  [View Issue](https://github.com/sipeed/picoclaw/issues/2984) — 2 comments, 2 👍  
  *Needs:* Clients need deterministic end-of-turn detection. Being actively addressed by PR [#3116](https://github.com/sipeed/picoclaw/pull/3116) which adds `turn.done` lifecycle events. High demand signal.

- **#3012 – [OPEN] Continuous token consumption every minute when evolution is enabled**  
  [View Issue](https://github.com/sipeed/picoclaw/issues/3012) — 3 comments, 0 👍  
  *Needs:* A bug causing runaway token usage under Evolution mode; no fix PR yet. Potentially costly for users on paid APIs.

## 5. Bugs & Stability
| Severity | Issue / PR | Description | Fix PR? |
|----------|-----------|-------------|---------|
| 🔴 High | [#3012](https://github.com/sipeed/picoclaw/issues/3012) | Continuous token consumption every minute with Evolution enabled | No |
| 🟡 Medium | [#3108](https://github.com/sipeed/picoclaw/issues/3108) | Media turns not routed to image models | Yes: [#3117](https://github.com/sipeed/picoclaw/pull/3117) |
| 🟡 Medium | [#3115](https://github.com/sipeed/picoclaw/pull/3115) | Session-history corruption from inline data URLs in tool output | Open PR in review |
| 🟢 Low | [#3113](https://github.com/sipeed/picoclaw/pull/3113) | Silent JSON marshal/unmarshal errors in channel manager | Merged today |
| 🟢 Low | [#3112](https://github.com/sipeed/picoclaw/pull/3112) | Silent JSON marshal errors in tool loop | Merged today |

**Summary:** The Evolution token drain (#3012) is the most severe open bug. Media routing and history corruption are being actively patched.

## 6. Feature Requests & Roadmap Signals
- **Explicit turn completion signal** (Issue #2984) — Nearly complete via PR #3116; likely in next stable release.
- **Remote Pico WebSocket mode** (PR #3118) — Allows CLI agent to connect to remote WebSocket endpoints; early stage but high value for distributed deployments.
- **Delta Chat gateway** (PR #3063) — Adds a new channel for the Delta Chat messenger; expands reach beyond web/Telegram.
- **Image input compression pipeline** (PR #2964, stale) — Configurable compression for vision inputs; stalled, but signals demand for bandwidth/cost optimization.
- **Shift+Enter hint** (PR #3097) — UX improvement for web chat composer; small but polished change.

**Prediction for next stable:** `turn.done` signaling + remote WS mode + Delta Chat gateway are most likely to ship together in v0.3.0.

## 7. User Feedback Summary
- **Pain point:** Users on Evolution mode are experiencing unexpected token drain costing real money (#3012). No workaround documented yet.
- **Pain point:** External WebSocket clients lack a reliable "done" signal, forcing polling or heuristic-based detection (#2984). Fix in progress.
- **Pain point:** Image handling in tool output can corrupt session history when base64 data appears in text (#3115). Temporarily avoid tools like `read_file` with image-heavy content.
- **Satisfaction signal:** Two contributors independently submitted JSON error handling fixes (#3112, #3113), indicating user appreciation for robustness improvements.
- **Satisfaction signal:** Community PRs show active experimentation with new providers (NEAR AI, Delta Chat) and remote modes.

## 8. Backlog Watch
- **#2964 – Feat/image input compression** — Stale since 2026-05-28. No activity for 16 days despite 0 comments from maintainers. Could use triage: approve, request changes, or close.
- **#2917 – NEAR AI Cloud provider** — Open since 2026-05-21, no comments from maintainers. Good candidate for merging or requesting tests/docs.
- **#3012 – Evolution token drain** — No fix PR after 8 days; needs maintainer investigation or workaround documentation.
- **#2984 – Turn completion signal** — Active discussion but PR #3116 only opened today; monitor for merge conflicts with #2984.

**Total stale open items: 2** (#2964, #2551 was closed today, reducing stale count).

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-13

## Today's Overview

NanoClaw is experiencing a surge of activity with 18 PRs updated in the last 24 hours—10 merged or closed and 8 open—representing one of the most productive days in recent weeks. The project shows strong forward momentum across reliability, security, and infrastructure features, with major fixes landing for agent crash loops, routing issues, and attachment handling. Four bug reports remain active, including a critical silent-response bug in the message deduplication system and a concerning security issue where the `create_agent` MCP tool is ungated despite being documented as admin-only. The community is actively contributing, with multiple external contributors submitting PRs for security hardening and stability improvements.

## Releases

No new releases were published today. The upstream is at approximately v2.0.64 (commit d144721).

## Project Progress

The following 10 PRs were merged or closed today, representing significant forward progress:

**Feature Completions:**
- [#2203](https://github.com/nanocoai/nanoclaw/pull/2203) — **Signal reaction support**: bi-directional reactions now mirror the chat-sdk-bridge contour, enabling agents to call `add_reaction` MCP tool with emoji landing as Signal reactions
- [#2072](https://github.com/nanocoai/nanoclaw/pull/2072) — **Ollama multimodal support**: `ollama_generate` now accepts workspace-relative `images` paths for local multimodal models
- [#2071](https://github.com/nanocoai/nanoclaw/pull/2071) — **Signal full attachment routing**: all non-audio attachments now route through inbox path, supporting PDFs, docs, archives, and images
- [#2070](https://github.com/nanocoai/nanoclaw/pull/2070) — **Host-path attachment support**: native channel adapters can now pass on-disk files instead of inline base64
- [#2040](https://github.com/nanocoai/nanoclaw/pull/2040) — **Signal outbound attachments**: previously dropped files now properly deliver via signal-cli JSON-RPC
- [#2084](https://github.com/nanocoai/nanoclaw/pull/2084) — **Disaster recovery backup system**: daily snapshots with pluggable storage backends (local + optional S3) and CLI for full/per-agent restore

**Critical Fixes:**
- [#2670](https://github.com/nanocoai/nanoclaw/pull/2670) — **Poisoned-resume crash loop fix**: prevents infinite crash loops from corrupt resumed transcripts with `thinking`/`redacted_thinking` blocks
- [#2277](https://github.com/nanocoai/nanoclaw/pull/2277) — **Routing refresh on follow-ups**: solves routing freeze where null-routed cron tasks misroute real chat follow-ups
- [#2267](https://github.com/nanocoai/nanoclaw/pull/2267) — **Agent-to-agent reply routing**: fixes split-brain where a2a replies always landed in newest session instead of originating session
- [#2692](https://github.com/nanocoai/nanoclaw/pull/2692) — **Transient 5xx API error retry**: SDK exhaustion of API retries now properly retried rather than silently failing

## Community Hot Topics

**Most Active Issues:**

1. **Issue #2506** — `bug: send_message dedup silently drops responses when turns complete within 60 seconds of each other` ([link](https://github.com/nanocoai/nanoclaw/issues/2506))
   - 3 comments, remains open since May 16
   - **Analysis**: This is the longest-running unresolved bug with no fix PR in sight. The core issue—agent responses silently dropped with client timeout under two scenarios (rapid turns or follow-ups during streaming)—represents a fundamental reliability gap. The deduplication logic appears to conflate separate agent turns, suggesting a need for turn-boundary tracking rather than temporal deduplication.

2. **Issue #2632** — `Clarify status of Telegram agent-swarm / multi-bot identity in v2` ([link](https://github.com/nanocoai/nanoclaw/issues/2632))
   - 1 comment, open since May 28
   - **Analysis**: A real user migration blocker. The v1 Telegram swarm feature was added but its v2 migration path is ambiguous. This signals community reliance on multi-bot/swarm patterns that may not have clear documentation or parity in v2.

**Most Active PRs (by context, not comments):**

The cluster of 5 open PRs submitted on 2026-06-12 by multiple contributors indicates a coordinated community effort:
- [#2753](https://github.com/nanocoai/nanoclaw/pull/2753) — pre-commit PATH fix (sturdy4days)
- [#2752](https://github.com/nanocoai/nanoclaw/pull/2752) — Discord attachment staging (jsigwart)
- [#2750](https://github.com/nanocoai/nanoclaw/pull/2750) — outbound.db journal recovery (sturdy4days)
- [#2749](https://github.com/nanocoai/nanoclaw/pull/2749) — npm package release age gating (boazdori)
- [#2748](https://github.com/nanocoai/nanoclaw/pull/2748) — container security hardening (boazdori)

This surge of external contributions suggests growing community investment in the project's security and reliability posture.

## Bugs & Stability

**High Severity:**

1. **Issue #2506** — `send_message dedup silently drops responses` ([link](https://github.com/nanocoai/nanoclaw/issues/2506))
   - **Severity**: Critical — users get no response with no error indication
   - **Status**: Open since May 16, no fix PR identified
   - **Impact**: Affects any scenario with rapid turn-taking or follow-ups during streaming

2. **Issue #2668** — `Agent sessions have no per-tool timeout: hung MCP tool blocks session up to 30 min` ([link](https://github.com/nanocoai/nanoclaw/issues/2668))
   - **Severity**: High — single hung tool call stalls entire session
   - **Status**: Open since June 1, no fix PR identified

**Medium Severity:**

3. **Issue #2751 (CLOSED)** — `Budget-exhausted LLM turns are silently dropped` ([link](https://github.com/nanocoai/nanoclaw/issues/2751))
   - **Severity**: Medium — silent failure when cloud spending cap reached
   - **Status**: Closed (likely acknowledged/knowledge-base issue)

4. **Issue #2711** — `create_agent MCP tool is ungated despite "admin-only" comment` ([link](https://github.com/nanocoai/nanoclaw/issues/2711))
   - **Severity**: **Critical (Security)** — any agent container can create new agent groups
   - **Status**: Open since June 7, no fix PR — but note that PR [#2748](https://github.com/nanocoai/nanoclaw/pull/2748) from boazdori addresses container security hardening broadly, though not this specific gating issue

**Recently Fixed Bugs:**

- [#2670](https://github.com/nanocoai/nanoclaw/pull/2670) — Poisoned-resume crash loop (merged today)
- [#2692](https://github.com/nanocoai/nanoclaw/pull/2692) — Transient 5xx API error handling (merged today)
- [#2750](https://github.com/nanocoai/nanoclaw/pull/2750) — outbound.db journal stale handles (open PR)
- [#2752](https://github.com/nanocoai/nanoclaw/pull/2752) — Discord attachment URL staging (open PR)

## Feature Requests & Roadmap Signals

**Clear Roadmap Signals from Merged PRs:**
- **Signal channel maturity**: Multiple Signal-related PRs (reactions, attachments, file routing) suggest Signal is becoming a first-class channel
- **Disaster recovery**: The backup system ([#2084](https://github.com/nanocoai/nanoclaw/pull/2084)) indicates enterprise/deployment readiness focus
- **Ollama/offline AI**: Multimodal support ([#2072](https://github.com/nanocoai/nanoclaw/pull/2072)) suggests continued investment in local AI model support

**Open Feature PRs Likely for Next Version:**
- [#2747](https://github.com/nanocoai/nanoclaw/pull/2747) — OneCLI SDK 2.2.1 bump with credential-stub mounts and machine-checkable pins (omri-maya)
- [#2746](https://github.com/nanocoai/nanoclaw/pull/2746) — Provider capability registry (`agent-surfaces capability seam`) (omri-maya)
- [#2745](https://github.com/nanocoai/nanoclaw/pull/2745) — Opt-in persistent memory scaffold for providers (omri-maya)

These three PRs from the same author suggest a cohesive infrastructure layer for provider extensibility—enabling providers to declare capabilities (e.g., "I support memory") and receive structured scaffolding. This could significantly simplify third-party provider development.

**User-Requested Features (from Issues):**
- [#2632](https://github.com/nanocoai/nanoclaw/issues/2632) — Telegram agent-swarm/multi-bot identity in v2 (migration/documentation request)
- The swarm skill reference in commit `126b3f4` suggests this exists but may need stabilization/documentation

## User Feedback Summary

**Pain Points:**

1. **Silent failures dominate frustration** — Two of the top bugs (#2506, #2751) involve agent responses being dropped without any user notification. Users report clients timing out with no error indication, and spending cap hits producing fake HTTP 200s that mask budget exhaustion.

2. **Migration uncertainty** — A real user (arthurkrupa) explicitly states they're "trying to plan a v1 to v2 migration for a fork" and finding the current state "a little ambiguous." This is a concrete signal that v2 migration documentation needs attention.

3. **Security concerns** — The `create_agent` gating issue ([#2711](https://github.com/nanocoai/nanoclaw/issues/2711)) was reported by a community member noting the discrepancy between documentation and implementation. This suggests community users are auditing security boundaries and finding gaps.

**Satisfaction Signals:**
- The PR surge from multiple external contributors (boazdori, sturdy4days, jsigwart, omri-maya) on the same day suggests active, healthy community engagement
- The Signal channel work addresses real user needs for multi-channel agent deployment

## Backlog Watch

**Stale Critical Issues Needing Maintainer Attention:**

1. **Issue #2506** — `send_message dedup silently drops responses` ([link](https://github.com/nanocoai/nanoclaw/issues/2506))
   - **Age**: 28 days (since May 16)
   - **Severity**: Critical
   - **No fix PR exists** — this is the single highest-priority unresolved bug

2. **Issue #2668** — `Agent sessions have no per-tool timeout` ([link](https://github.com/nanocoai/nanoclaw/issues/2668))
   - **Age**: 12 days (since June 1)
   - **Severity**: High
   - **No fix PR exists**

3. **Issue #2711** — `create_agent MCP tool is ungated despite "admin-only"` ([link](https://github.com/nanocoai/nanoclaw/issues/2711))
   - **Age**: 6 days (since June 7)
   - **Severity**: Critical (Security)
   - **No fix PR exists** — though note container hardening PR [#2748](https://github.com/nanocoai/nanoclaw/pull/2748) addresses adjacent security concerns

**Long-Open Issues with Maintenance Risk:**
- No issues in the backlog have maintainer responses pending or appear abandoned. The most "at risk" item is #2506, which has remained open for nearly a month without a fix PR.

**PRs Needing Review:**
- [#2753](https://github.com/nanocoai/nanoclaw/pull/2753) — Pre-commit PATH fix (submitted 2026-06-12, contributor: sturdy4days)
- [#2752](https://github.com/nanocoai/nanoclaw/pull/2752) — Discord attachment fix (submitted 2026-06-12, contributor: jsigwart)
- [#2749](https://github.com/nanocoai/nanoclaw/pull/2749) — npm package security gating (submitted 2026-06-12, contributor: boazdori)
- [#2748](https://github.com/nanocoai/nanoclaw/pull/2748) — Container security hardening (submitted 2026-06-12, contributor: boazdori)
- [#2750](https://github.com/nanocoai/nanoclaw/pull/2750) — outbound.db journal recovery (submitted 2026-06-12, contributor: sturdy4days)

These five open PRs represent a substantial community contribution queue that would benefit from timely maintainer review.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-06-13

## 1. Today's Overview

NullClaw is seeing moderate activity, with 2 issues and 3 pull requests updated in the last 24 hours, though no new releases were cut. All three open PRs are fixes submitted by contributor **vernonstinebaker**, targeting configuration flexibility, error handling hygiene, and Discord gateway resilience — indicating ongoing investment in reliability and polish. The project's two active issues include a verified bug affecting Telegram agent cron jobs and a feature request for JIRA integration, both of which have gone 13+ days without maintainer resolution. Overall, the project appears stable but would benefit from closing the loop on these open items.

## 2. Releases

No new releases were published today. The latest available version remains unreported in the 24-hour window.

## 3. Project Progress

No pull requests were merged or closed today. Three PRs remain open, all submitted by **vernonstinebaker** and updated within the last 24 hours:

- **#949** — `fix: make queue_mode configurable from config.json` — Adds a new `agent.default_queue_mode` config field and refactors the `QueueMode` enum into `config_types.zig`.
- **#951** — `fix(agent_runner): suppress stderr initialization logs on agent failure` — Prevents verbose initialization logs from being posted to channels when the agent subprocess exits with a non-zero code.
- **#953** — `fix(discord): recover closed gateway sockets` — Implements gateway socket reconnection logic, including heartbeat thread cleanup and a grace window for stalled pre-HELLO reconnects.

These represent meaningful stability and usability improvements, but none have been reviewed or merged yet.

## 4. Community Hot Topics

Two items are driving discussion today:

- **#941 [OPEN] Agent-type cron jobs don't spawn a subprocess — Telegram delivery never happens**  
  *Author: weissfl | Updated: 2026-06-13 | Comments: 2*  
  [GitHub Issue #941](https://github.com/nullclaw/nullclaw/issues/941)  
  This is the most active issue, with a clear reproduction scenario: scheduled tasks using `job_type: "agent"` with Telegram delivery complete without spawning the agent subprocess, resulting in no messages. The two comments suggest the reporter has provided steps but no maintainer has responded. The bug directly breaks a core feature (scheduled agent execution) and is now 13 days old.

- **#914 [OPEN] [enhancement] Create JIRA access tool**  
  *Author: sayjeyhi | Updated: 2026-06-13 | Comments: 1*  
  [GitHub Issue #914](https://github.com/nullclaw/nullclaw/issues/914)  
  A feature request for a native JIRA integration tool. The single comment likely requests scope clarification or triage. This issue has been open for a full month with no maintainer response, signaling a potential gap in feature prioritization.

## 5. Bugs & Stability

One confirmed bug is currently active, ranked **High severity**:

- **#941 — Agent-type cron jobs don't spawn a subprocess**  
  **Severity: High** — Scheduled agent tasks with Telegram delivery are silently failing. The job is marked complete but the subprocess never executes, which means no output, no notifications, and a misleading success signal. There is currently no fix PR associated with this issue. Given that `schedule` and `agent` are core NullClaw primitives, this should be treated as a priority regression. No response from maintainers has been observed in 13 days.

No crashes, memory leaks, or regressions were reported today beyond this issue.

## 6. Feature Requests & Roadmap Signals

One new feature request is under discussion:

- **#914 — Create JIRA access tool** — User `sayjeyhi` requests OAuth-based JIRA integration for reading issues, creating tickets, updating statuses, adding comments, and retrieving sprint data. This aligns with a trend toward enterprise workflow automation and could be a strong candidate for the next minor release if maintainers prioritize productivity tooling. No maintainer acknowledgment or roadmap tag has been applied.

## 7. User Feedback Summary

The user feedback signal today is sparse but pointed:

- **Pain point (High visibility):** *weissfl* reports a broken scheduled agent workflow — setup is correct per documentation but the agent subprocess never launches. The user likely spent significant time debugging, only to find a backend logic gap. Absence of maintainer response for 13 days is itself a source of dissatisfaction.
- **Unmet need (Long-standing):** *sayjeyhi* suggests JIRA integration, implying users want NullClaw to serve as a bridge between chat-based AI agents and professional project management tools. The silence on this request may discourage further community contributions.

Overall, sentiment appears neutral-to-frustrated, with users reporting clear defects that remain unacknowledged.

## 8. Backlog Watch

Two important items are overdue for maintainer attention:

- **#941 — Agent-type cron jobs don't spawn a subprocess**  
  *Opened: 2026-05-31 | Last updated: 2026-06-13 | No response from maintainers*  
  [GitHub Issue #941](https://github.com/nullclaw/nullclaw/issues/941)  
  A verified, high-severity bug affecting a core feature (scheduled agent execution with Telegram delivery). 13 days without a reply. Risk of user churn if this remains unresolved.

- **#914 — [enhancement] Create JIRA access tool**  
  *Opened: 2026-05-13 | Last updated: 2026-06-13 | No response from maintainers*  
  [GitHub Issue #914](https://github.com/nullclaw/nullclaw/issues/914)  
  A reasonable feature request left unacknowledged for one month. Even a "under consideration" label would improve community trust.

Both items would benefit from triage labeling and a brief maintainer response to set expectations.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-13

## 1. Today's Overview

IronClaw saw high activity over the past 24 hours, with 43 issues updated and 50 pull requests in motion, reflecting a major push across the Reborn v2 platform. The project is in an intensive feature-integration phase, particularly around the attachment system (Track 6 of #4644), DeferredBusy drain mechanics, and Slack delivery improvements. While 17 issues and 17 PRs were closed or merged, the high open count (26 issues, 33 PRs) suggests sustained development pressure. Notably, there were zero new releases, and CI is currently blocked by a cargo-deny advisory failure affecting all branches. The engineering team is clearly executing on a multi-track roadmap, with 10+ PRs from multiple core contributors active simultaneously.

## 2. Releases

**No new releases** in the last 24 hours. The last release PR (#3708) remains open since May 16, 2026, pending closure of the API breaking changes it proposes.

## 3. Project Progress

**Merged/Closed PRs today (17):**
- **#4812** (closed) — *Drain DeferredBusy messages when the blocking run reaches terminal state*: Core feature completing the blocked-thread UX arc, enabling automatic message drain after gate resolution.
- **#4655** (closed) — *Carry attachment refs through the Reborn transcript contract*: Enables attachment persistence in transcripts (Track 2 of #4644).
- **#4654** (closed) — *Extensible attachment format registry*: Replaces scattered hardcoded lists with a single source of truth.
- **#4839** (open, new) — *Fix Slack re-approval loop*: Preserves invocation identity across auth-gate re-dispatch, preventing infinite approval cycles.
- **#4838** (open, new) — *Explicit gate-open feedback for busy threads*: Replaces defer-and-drain approach with clear rejection and user retry.
- **#4836** (open, new) — *Runtime-context slice for connected channels/delivery state*: Gives the model ambient knowledge of channel and delivery state.
- **#4837** (open, new) — *Gated final-answer nudge*: Issues a final model call when the agent would otherwise end with an empty reply.
- **#4835** (open, new) — *Persist "always allow" approvals across threads*: Fixes re-prompting for already-approved capabilities.

**Key feature advances:**
- Attachment system tracks #4654, #4655, #4668, #4670, #4672, #4675, #4676, #4677, #4680, #4738 moving in parallel.
- DeferredBusy drain replaced with user-facing rejection feedback (#4838 → superseding #4812).
- Approval persistence scope expanded from per-thread to per-user/agent (#4835).
- 20+ UI fixes merged from a batch of sunglow666 UX bug reports.

## 4. Community Hot Topics

| Issue/PR | Comments | Key Topic |
|----------|----------|-----------|
| [#4817] DeferredBusy drain follow-ups | 3 | Three deferred architectural decisions for drain design |
| [#4825] Persistent approvals across threads | 3 | User trust in "always allow" being broken across threads |
| [#4703] Model picker saves display name | 3 | UX bug in inference provider configuration |
| [#4831] Route drain through replay entry point | 2 | Architectural alignment for drain design |
| [#4705] SSO fails in local environment | 2 | Critical onboarding blocker for developers |

The **most active threads** reveal two underlying needs: (1) **Trust and persistence** — users expect durable settings (approvals, model selections, drafts) to survive thread switches, and current behavior undermines confidence; (2) **Developer onboarding friction** — SSO failures in local environments create a high barrier for new contributors.

## 5. Bugs & Stability

**Critical:**
- **CI blocked** — [#4824] `cargo-deny` failing repo-wide due to new RUSTSEC advisories against postgres crates (SCRAM iteration DoS, hstore panic, DataRow panic). Blocks all PRs. No fix PR open yet.
- **Nightly E2E failure** — [#4108] (open since May 27). Failed with `v2-engine` job errors.

**High:**
- **Failed tool workflow corrupts message ordering** — [#4762]: After a tool fails, follow-up messages and activity ordering become inconsistent. No fix PR.
- **LLM unaware of current date/time** — [#4796]: Model assumes wrong dates even with time tools available, affecting calendar/scheduling workflows.

**Medium (fixes in progress):**
- **Slack re-approval loop** — Fix PR #4839 open.
- **SSO setup fails locally** — [#4705]: GitHub/Google sign-in broken. No fix PR.
- **Active provider state inconsistency** — [#4697]: UI shows one provider, chat uses another.
- **Ollama test connection false positive** — [#4696]: Reports success when Ollama is not running.

**Low (UI polish, fix PRs not yet identified):**
- Attachment warning difficult to read in Light theme ([#4819])
- Delete running conversation gives no UI feedback ([#4823])
- Composer hover styling issues ([#4723], [#4719])
- No user/assistant identity display in conversations ([#4722])
- "PINNED" section shows active instead of pinned ([#4721])

## 6. Feature Requests & Roadmap Signals

**Likely for next version:**
- **Attachment system** (Track 6 of #4644) — 7 interdependent PRs active (#4668, #4670, #4672, #4675, #4676, #4677, #4738) nearing the finish line. This is the top roadmap item.
- **Runtime context awareness** — [#4836] giving the model channel/delivery state is critical for Slack use cases.

**Possible:**
- **Batch drain** ([#4832]) — Batching deferred busy messages for efficiency, dependent on route refactoring.
- **Per-thread DeferredBusy index** ([#4833]) — Filesystem optimization to avoid full transcript scans.

**Long-term signals:**
- **Slack delivery decomposition** ([#4818]) — The `~4k` line `slack_delivery.rs` needs modularization.
- **Engine V2 usage tracking** ([#4822]) — Admin usage endpoint needs Reborn support.
- **CI sharding** ([#4813]) — Long test jobs are slowing PR turnaround.

## 7. User Feedback Summary

**Pain points (real user reports from issues):**
- **SSO setup fails** — Developers trying to run IronClaw locally hit immediate barriers with GitHub/Google sign-in.
- **Approvals don't persist** — Users who "always allow" a capability must re-approve it in every thread, causing frustration.
- **Slack re-approval loops** — The infamous "4 consecutive approval gates for one logical call" pattern breaks workflow.
- **No feedback on failed deletion** — Users can't tell why deleting a running conversation fails.
- **Attachment UX gaps** — Warning banners persist incorrectly across conversations, attachments lost on thread switch.

**Satisfaction signals:**
- The **attachment system** (#4644) is receiving heavy investment aligned with user needs for document/image support.
- **DeferredBusy UX** has been iterated rapidly (#4812 → #4838) — the team is responsive to feedback on message-drain behavior.

## 8. Backlog Watch

**Critical — requires immediate attention:**
- **#4108** — Nightly E2E failure (open 17 days) — Repeated failures suggest a systemic issue.
- **#4824** — Cargo-deny advisory failure (open 1 day) — Blocks all CI, high impact.

**Long-stale with no activity:**
- **#4813, #4818, #4822, #4823, #4828** — Several issues from June 12 have zero follow-up; none should be stale yet, but no assignee or PR exists for most.

**No maintainer response:**
- **#4696** — Ollama test connection false positive (open 3 days, no assignee, no comments from maintainers).
- **#4762** — Tool failure corrupts message ordering (open 2 days, no assignee, no fix PR).
- **#4796** — LLM unaware of date/time (open 1 day, no assignee).

All links: nearai/ironclaw [Issue/PR #number]

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the **LobsterAI Project Digest** for **2026-06-13**.

---

## 1. Today's Overview
LobsterAI showed **moderate activity** today, driven largely by the orchestration of a release merge and related fix-ups. **5 merged/closed PRs** (including the `release/2026.6.11` merge) indicate a successful release cycle, but the **active issue count (4 open)** remains stable. The project is currently in a **post-release stabilization phase**, with a cluster of **stale issues (opened April 3)** regarding skills UX and OpenClaw compatibility still awaiting maintainer attention. No new releases were cut today, but the codebase advanced with fixes for Computer Use runtime and image saving.

## 2. Releases
**No new releases today.**
*The last known release is the merge target `release/2026.6.11`, which was integrated into `main` today.*

## 3. Project Progress
Today saw **5 merged/closed PRs**, advancing stability and release management:

- **Release Merge:** `#2158` (liuzhq1986) - **Merged `release/2026.6.11` into `main`.** Key features in this release include: Computer Use MVP + built-in kit, realtime ASR voice input for cowork, HTML artifact sharing mode selection, and image/SVG artifact sharing support. *(Link: [PR #2158](https://github.com/netease-youdao/LobsterAI/pull/2158))*
- **Computer Use Runtime:** `#2156` (btc69m979y-dotcom) - **Bumped Computer Use runtime to 1.0.7**, updating the installer CDN metadata and adding UIA breadcrumbs for better diagnostics. *(Link: [PR #2156](https://github.com/netease-youdao/LobsterAI/pull/2156))*
- **Media Bug Fix:** `#2157` (liugang519) - **Fixed a bug where generated images were saved with incorrect extensions** (e.g., PNG content saved as .jpg). Now uses byte signature detection instead of trusting the server extension. *(Link: [PR #2157](https://github.com/netease-youdao/LobsterAI/pull/2157))*
- **UI Polish:** `#1466` (linlihua) - **Fixed modal close button unreachability** when MCP server form content exceeds the viewport. *(Link: [PR #1466](https://github.com/netease-youdao/LobsterAI/pull/1466))*
- **Platform Compatibility:** `#1467` (linlihua) - **Fixed macOS shortcut display** to show Cmd (⌘) instead of Ctrl in the Settings panel. *(Link: [PR #1467](https://github.com/netease-youdao/LobsterAI/pull/1467))*

## 4. Community Hot Topics
The most debated issue today remains **Issue #1**, despite being closed. Feature discussions remain blocked on two major PRs.

**1. Issue #1:** `hit API error with OpenAI API Type`
- **Activity:** 7 comments. This closed issue details a failed API call when switching from MiniMax to OpenAI message type on Mac OS. The error suggests invalid params or a version mismatch.
- **Underlying Need:** Users need a **seamless LLM provider switch** without requiring manual workarounds or encountering silent param validation failures. *(Link: [Issue #1](https://github.com/netease-youdao/LobsterAI/issues/1))*

**2. PR #1441:** `feat(artifacts): add extensible preview pipeline for HTML, React and Mermaid`
- **Status:** Open (stale). This PR is a conflict-resolved version of a long-standing feature. It adds extensible artifact previews but has no comments since creation.
- **Underlying Need:** The community wants a **richer, live-preview experience** for Cowork artifacts beyond static output. *(Link: [PR #1441](https://github.com/netease-youdao/LobsterAI/pull/1441))*

## 5. Bugs & Stability
**Severity: Medium.** While no critical crashes were reported today, two UI/UX regressions from April remain active.

- **[Medium] Skill Duplication & Import Naming:** `#1445` (PR, gongzhi-netease) - Directly addresses two related bugs: (1) ZIP imports create random temp directory names, and (2) duplicate skill imports are not validated, causing silent system prompt pollution. **Fix exists in this open PR.** *(Link: [PR #1445](https://github.com/netease-youdao/LobsterAI/pull/1445))*
- **[Medium] Scheduled Task UI Freeze:** `#1437` (Issue) - Creating a non-repeating task freezes the UI with no error feedback when the calendar is cleared. **No fix PR yet.** *(Link: [Issue #1437](https://github.com/netease-youdao/LobsterAI/issues/1437))*
- **[Low] Deactivated Skills Still Callable:** `#1439` (Issue) - Toggling a skill off does not prevent it from being triggered via chat keywords. **No fix PR yet.** *(Link: [Issue #1439](https://github.com/netease-youdao/LobsterAI/issues/1439))*
- **[Low] Quoted Skills Disappear After First AI Response:** `#1442` (Issue) - Agent-selected skills are shown initially but vanish after the first AI turn, requiring a session switch to reappear. This creates confusion about skill scope. **No fix PR yet.** *(Link: [Issue #1442](https://github.com/netease-youdao/LobsterAI/issues/1442))*

## 6. Feature Requests & Roadmap Signals
**Strong Signal: OpenClaw Compatibility**
- **Issue #1443:** `有计划支持新版本的openclaw吗？` - A user explicitly requests support for OpenClaw v2026.3.24, noting breaking changes block their local setup. Given OpenClaw is a core dependency (seen in recent PRs `#2158` and `#2156`), this is a **high-priority roadmap item likely for the next release**. *(Link: [Issue #1443](https://github.com/netease-youdao/LobsterAI/issues/1443))*
- **User Confusion on Skill Scoping:** Request from `#1442` highlights a need for **better UX around skill lifecycle**—specifically clarifying whether skills fire only for their trigger keywords or are always active.

## 7. User Feedback Summary
**Pain Points:**
- **API Configuration Friction:** Issue #1 shows a user successfully configured a MiniMax API key but hit an opaque error switching to OpenAI. This indicates inadequate param validation or error messaging in the settings UI.
- **OpenClaw Migration Blocked:** Issue #1443 explicitly states the user cannot start the app due to breaking changes in a core dependency.
- **Skill UX Confusion:** Multiple users (devilszy in #1439, #1442) are confused about skill lifecycle—skills that are disabled or "used" still affect responses, undermining the mental model of on/off toggles.

**Satisfaction Signals:**
- The **active PR volume** (3 open, 5 closed) and the **successful release merge** (#2158) suggest core developers are actively shipping improvements, which correlates with healthy project engagement.

## 8. Backlog Watch
The following stale items (last updated 2026-06-13 after 2+ months of silence) are **critical for maintainer attention**:

1. **PR #1445** `fix(skills): 修复技能重复导入无校验` - **High Priority.** This PR fixes two bugs (duplicate imports, random dir names) that affect skill stability. No maintainer review yet. *(Link: [PR #1445](https://github.com/netease-youdao/LobsterAI/pull/1445))*
2. **Issue #1443** `有计划支持新版本的openclaw吗？` - **High Priority.** A direct blocker for current users. No official reply to date. *(Link: [Issue #1443](https://github.com/netease-youdao/LobsterAI/issues/1443))*
3. **Issue #1437** `创建定时任务时...按钮没反应` - **Medium Priority.** UI freeze with zero error feedback. No associated fix PR. *(Link: [Issue #1437](https://github.com/netease-youdao/LobsterAI/issues/1437))*
4. **PR #1440** `feat(cowork): 将已选技能标签移至输入框内顶部展示` - **Medium Priority.** Clean UX improvement for skill badges to declutter the input toolbar. No reviews. *(Link: [PR #1440](https://github.com/netease-youdao/LobsterAI/pull/1440))*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

**Moltis Project Digest – 2026-06-13**

---

### Today's Overview
Activity in the Moltis project is moderate but focused. Three open issues received updates in the last 24 hours, with no new pull requests or releases. The team and community are engaging primarily on bug reports and feature proposals, indicating active maintenance and forward-looking development. The lack of merged PRs or closed issues suggests a consolidation phase, where maintainers are reviewing open contributions and addressing quality-of-life improvements. Overall, the project appears stable but with clear community-driven momentum for expansion.

### Releases
No new releases were published in the last 24 hours. The latest release remains unchanged.

### Project Progress
- **No pull requests** were merged or closed in the last 24 hours. No new features or bug fixes have been officially integrated into the codebase during this period.

### Community Hot Topics
- **#1115 – [Bug]: Fastmail MCP Authorisation** (2 comments)  
  *Author: kmath313* · [Link](https://github.com/moltis-org/moltis/issues/1115)  
  This bug report describes a failure in Fastmail’s Model Context Protocol (MCP) authorization flow. It has the most recent community engagement, with two comments on the issue. The underlying need is reliable email integration for agent workflows, a critical feature for enterprise and productivity use cases.

- **#1118 – [Feature]: Add Kubernetes-native sandbox backend with runtimeClassName support** (1 comment)  
  *Author: AzgadAGZ* · [Link](https://github.com/moltis-org/moltis/issues/1118)  
  This proposal for a Kubernetes sandbox backend has generated community discussion. The user rationale—running untrusted LLM-generated code with VM-level isolation (Kata Containers, gVisor)—points to growing demand for secure, scalable agent execution environments.

- **#1102 – [Feature]: Add FunASR/SenseVoice as local STT engine** (1 comment)  
  *Author: LauraGPT* · [Link](https://github.com/moltis-org/moltis/issues/1102)  
  Request to integrate high-performance local speech-to-text engines. The comment highlights a desire for low-latency (<70ms), streaming voice capabilities, which would be a major enhancement for real-time voice agent interactions.

### Bugs & Stability
- **#1115 (Open) – Fastmail MCP Authorisation**  
  *Severity: Medium* – This is the only bug reported/updated in the last 24 hours. No fix PR currently exists. It affects the email integration module, which may impact users relying on Fastmail for agent-driven email tasks. The issue remains open; a workaround or fix has not yet been suggested by maintainers.

No other bugs, crashes, or regressions were reported or updated today.

### Feature Requests & Roadmap Signals
Two notable feature requests were updated today:

1. **#1118 – Kubernetes-native sandbox backend** – Strong signal of enterprise-grade security needs. If the maintainers prioritize this, it could become a key differentiator for production deployments. Likelihood of inclusion in next minor release: **Moderate**.

2. **#1102 – FunASR/SenseVoice local STT engine** – This request has been open since June 4 and is gaining traction. The performance numbers cited (70ms for 10s audio) are compelling for voice-first agents. Likelihood of inclusion in next major release: **High**, as it aligns with the project’s voice assistant ambitions.

### User Feedback Summary
- **Pain points:** Authorization flows (Fastmail MCP) continue to be a friction point for email integration. Users are also expressing security concerns around executing LLM-generated code, wanting stronger isolation defaults.
- **Use cases:** Voice interaction (STT) is a clear emerging use case, with users specifically requesting ultra-fast, local processing—suggesting dissatisfaction with latency from cloud-based STT or current built-in options.
- **Satisfaction:** While no overtly negative feedback was posted, the lack of new releases or merged fixes may be a subtle indicator of impatience among early adopters. Community engagement remains constructive and feature-focused.

### Backlog Watch
- **#1102 – FunASR/SenseVoice local STT engine**  
  *Opened: 2026-06-04* · Last update: 2026-06-12  
  This issue has been open for 9 days without a response from maintainers. Interest is building (1 comment, positive reception), and it represents a significant feature request that may become stale if unaddressed.

- **#1115 – Fastmail MCP Authorisation**  
  *Opened: 2026-06-11* · Last update: 2026-06-12  
  This bug has received community comments but no maintainer acknowledgment or assignment yet. For a bug impacting a core integration, a triage note or workaround would improve community trust.

---

*Generated from GitHub data snapshot at 2026-06-13. Data reflects activity in the last 24 hours unless otherwise noted.*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Based on the provided GitHub data for CoPaw (QwenPaw) on 2026-06-13, here is the project digest.

---

## CoPaw Project Digest — 2026-06-13

### 1. Today's Overview
The CoPaw (QwenPaw) project is exhibiting high activity, with 20 issues and 19 pull requests updated in the last 24 hours. The community is highly engaged, reporting numerous bugs, requesting features, and contributing code. A significant **backend migration from AgentScope 1.x to 2.0** (#4727) is a major strategic initiative currently under discussion. The project maintains a healthy release cadence, with a beta version (1.1.12b1) being prepared, indicating ongoing iterative development. Overall, the project is in a phase of active stabilization and feature expansion.

### 2. Releases
**No new production releases were published today.** The team has prepared a new beta version:
- **`1.1.12b1`**: A new beta release was prepared to align the package version for the next build cycle. This involved a version format correction via PR #5159 (`fix(release): switch version to 1.1.12b1`), which was merged.

### 3. Project Progress
Several significant PRs were merged today, advancing features and fixing critical bugs:
- **Plugin & Desktop Improvements:**
    - **Skill Batch Download**: PR #4969 (merged) added tag filtering for skill batch downloads to workspaces.
    - **Desktop Readiness Check**: PR #4144 (merged) fixes the `qwenpaw desktop` command so it correctly checks server readiness when bound to `0.0.0.0` on Windows.
    - **Agent Workspace Security**: PR #5022 (merged) added validation to prevent agent workspaces from being placed inside sensitive QwenPaw-managed directories (e.g., `plugins`, `secrets`, `backups`).
- **Bug Fixes & UI Polish:**
    - **Memory Config Loss**: PR #5144 (merged) fixed a critical bug where long-term memory and vector model configurations were lost in the UI if a settings panel was not expanded before saving.
    - **Coding Mode Session Reset**: PR #5147 (merged) fixed a bug where refreshing the page in "Coding Mode" would lose the current session and revert to the first one.
    - **Memory Search UI**: PR #5154 (merged) resolved a UI rendering bug where the memory search tool performed correctly but displayed `unknown` data in the results table.
- **Release Pipeline:**
    - **Release Verification Gate**: PR #5121 (merged) introduced a new CI step that performs end-to-end installation and health checks before artifacts are published to PyPI/DockerHub, improving release quality.

### 4. Community Hot Topics
The community is most engaged with three major themes:
- **AgentScope 2.0 Migration**: Issue #4727 ([Link](agentscope-ai/QwenPaw Issue #4727)) remains the most upvoted open issue, gathering 2 👍. The discussion around the breaking change to upgrade the backend is critical to the project's future direction. A related question (#5149) asking "when will it be upgraded?" shows clear user anticipation.
- **Scheduled Task Failures**: Issue #5064 ([Link](agentscope-ai/QwenPaw Issue #5064)) has the most comments at 11. Users report that agents can create scheduled tasks normally, but they fail to trigger at the designated time, rendering the feature non-functional. This is a high-impact bug for workflow automation.
- **Agent Team/Swarm Collaboration**: Issue #5139 ([Link](agentscope-ai/QwenPaw Issue #5139)) requesting native multi-agent collaboration capabilities (similar to competitor "WorkBuddy" and "JiuwenSwarm") is a feature request with significant activity (3 comments). This signals a growing demand for more complex agent orchestration patterns.

### 5. Bugs & Stability
Several bugs were reported and fixed today, with a few critical regressions surfacing.

| Severity | Bug Description | Fix Status |
| :--- | :--- | :--- |
| **High** | **Scheduled tasks created by agents fail to trigger** (#5064). | Open. No fix PR yet. |
| **High** | **Automatic crash/restart in Docker environment** after upgrading to v1.1.11 (#5155). | Open. No fix PR yet. |
| **Medium** | **Memory/Vector config loss** on save when UI panels are not expanded (#5137). | Fixed in PR #5144 (merged). |
| **Medium** | **Gemini tool calling regression** between v1.1.10 and v1.1.11.post2 (#5163). | Open. A regression is confirmed. |
| **Medium** | **Download fails for non-plain-text files (docx/pdf)** in v1.1.11.post2 (#5140). | Closed. |
| **Low** | **Long conversations cause QwenPaw to stop responding** (#5161). | Open. |
| **Low** | **Conversation thinking logic enters infinite loop** (#5162). | Open. |

### 6. Feature Requests & Roadmap Signals
Several feature requests signal the community's desired direction:
- **Agent Swarm Collaboration**: Issue #5139 ([Link](agentscope-ai/QwenPaw Issue #5139)) is a strong signal for multi-agent teams. This is a complex feature but likely a roadmap item given the competition.
- **New Communication Channels**:
    - **Slack Support**: Issue #5152 ([Link](agentscope-ai/QwenPaw Issue #5152)) is a popular request for enterprise integration.
    - **Zalo Bot (Vietnam)**: Issue #5168 ([Link](agentscope-ai/QwenPaw Issue #5168)) shows demand in the Vietnamese market.
- **Desktop System Tray & Service Management**: Issue #5164 ([Link](agentscope-ai/QwenPaw Issue #5164)) requests system tray, auto-start, and background service capabilities for the desktop app.
- **New Model Provider Support**: Issue #5156 ([Link](agentscope-ai/QwenPaw Issue #5156)) requests adding `kimi-for-coding` to the provider whitelist, reflecting user desire to integrate existing paid subscriptions.

**Prediction for v1.1.12:** The new *Slack Channel* support (#5152) is a plausible addition. An *Agent OS Driver* (PR #5067) for MCP/A2A is under review and could be a major feature. The *DataPaw plugin* (PR #4622) for data analysis is also a strong candidate for inclusion.

### 7. User Feedback Summary
User feedback shows a mix of satisfaction with rapid iteration and frustration with stability.
- **Pain Points:** Users are experiencing significant regressions between minor versions, most notably the **Gemini tool calling regression** (#5163) and the **Docker crash/restart loop** (#5155). The unreliability of **agent-created scheduled tasks** (#5064) is a critical workflow blocker.
- **Use Cases:** Feedback reveals diverse use cases including coding assistants, data analysis, and regional messaging platforms (Vietnam's Zalo). The demand for **swarm collaboration** (#5139) suggests users are pushing beyond single-agent interactions.
- **Dissatisfaction:** There is clear dissatisfaction with the **Feishu CardKit streaming card** performance for long replies (#5167), where the experience is described as "one word at a time."

### 8. Backlog Watch
- **Issue #4727 ([Link](agentscope-ai/QwenPaw Issue #4727)) - *[Breaking Change] Migrate backend from AgentScope 1.x to AgentScope 2.0***: This has been open since May 27th. While it has a question-based spin-off (#5149), the main issue lacks a direct commit or PR link showing progress. Given it's a breaking change, community and maintainer attention is critical to plan the migration roadmap.
- **PR #4900 ([Link](agentscope-ai/QwenPaw PR #4900)) - *Decouple plugin loader initialization from agent startup***: Open since June 2nd. This is a critical fix for desktop users (PyInstaller/Tauri), yet it remains unmerged. This could be blocking other releases or features.
- **Issue #5163 ([Link](agentscope-ai/QwenPaw Issue #5163)) - *Gemini tool calling regression***: This is confirmed as a regression between v1.1.10 and .post2. A bisect and hotfix are needed to restore compatibility for a significant portion of the user base.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-13

## Today's Overview

ZeroClaw is in a period of intense development activity, with 50 pull requests and 13 issues updated in the last 24 hours. The project is clearly advancing toward a significant milestone, likely **v0.8.1**, as evidenced by the dedicated integration tracker (#6970) and a massive consolidation PR (#7540) that unifies three separate agent turn engines into one. However, the pace comes with friction: one critical bug report (#7553) reveals that source installs ship without a functioning web dashboard, and a new user’s onboarding is completely blocked (#7537). The maintainer team appears responsive, merging or closing 30 PRs today, but several high-risk PRs are stalled waiting for author action—a pattern that may create bottlenecks if unresolved.

## Releases

**No new releases today.** The last tagged release remains v0.8.0 (or earlier). The v0.8.1 tracking issue (#6970) indicates a next release is in active preparation, with channel, provider, and tool additions queued for it.

## Project Progress

**30 PRs were merged or closed today**, representing significant consolidation and bugfix work:

- **Core architecture consolidation**: PR #7540 (still open) is the headline change—it merges three separate agent turn engines (`run_tool_call_loop`, `Agent::turn_streamed_with_steering_state`, and `Agent::turn`) into a single unified loop. This is a direct implementation of RFC #7415, which was created just four days ago and already executed.

- **Plugin infrastructure stabilized**: PR #7413 (merged) reconciles plugin install paths with runtime discovery, fixing a critical mismatch where CLI-installed WASM plugins were invisible to the agent.

- **Installation fixes**: PR #7302 (merged) addresses the web dashboard copy issue on source installs (linked to #7553), though a companion fix (#7554) is still open.

- **Config menu improvements**: Two PRs (#7555 closed, #7556 open) add declarative section grouping to the Config menu, improving UI organization.

- **Skill system maturation**: Multiple skill-related PRs (#6716, #6717, #6718) add architecture review, PR review session integration, and work queue documentation to skill definitions.

## Community Hot Topics

**Most active discussion items today:**

1. **RFC #7415 — Unify agent turn engines** (3 comments) — This RFC was proposed, reviewed, and executed as a consolidation PR (#7540) within 4 days. The fast turnaround suggests strong maintainer alignment on this architectural direction. [Issue #7415](https://github.com/zeroclaw-labs/zeroclaw/issues/7415)

2. **Issue #5470 — Multiple runtime issues** (5 comments, closed) — A long-standing bug (filed April 7) finally closed today. The user reported duplicate memory saves in Telegram, channel double-triggers via cron, and tool execution failures with GPT-5.4. [Issue #5470](https://github.com/zeroclaw-labs/zeroclaw/issues/5470)

3. **Issue #5570 — Faster SQLite vector search** (5 comments, closed) — Another long-lived enhancement (April 9) closed today. The request to replace O(n) vector scans with ANN indexing was ultimately addressed. [Issue #5570](https://github.com/zeroclaw-labs/zeroclaw/issues/5570)

4. **Issue #6723 — Hardcoded OpenAI timeout** (2 comments, closed) — A bug where `timeout_secs` config was silently ignored by the native OpenAI provider, fixed via a closed PR today. [Issue #6723](https://github.com/zeroclaw-labs/zeroclaw/issues/6723)

**Underlying need**: The community is pushing for three things: (1) **architectural simplicity** (fewer code paths to maintain), (2) **configurability** (timeouts, model routing, workspace paths), and (3) **LLM integration maturity** (proper handling of high-reasoning models like GPT-5.4).

## Bugs & Stability

**Critical/Blocking bugs reported today:**

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **S1** | #7553 | Source installs serve no web dashboard (assets never copied) | #7554 (open) |
| **S1** | #7537 | `zeroclaw quickstart` fails on Windows 10 with config parsing error | None yet |
| **S1** | #7542 | `ask_user` tool fails instantly in gateway WebSocket sessions | None yet |
| **S1** | #7533 | Docker build fails during `cargo web build` due to missing `++` | None yet |
| **S2** | #7541 | V3 legacy paths use shared `data_dir` as agent workspace | None yet |
| **S2** | #7554 fix | Per-agent workspace dir not created in `for_agent` | #7284 (open) |

- **#7553** is the most impactful infrastructure bug: `install.sh --source` builds the web dashboard but never copies it to the data directory, so the systemd daemon serves a blank dashboard. A fix (#7554) was opened the same day.
- **#7537** blocks all new Windows users from onboarding—the `quickstart` command crashes with a config parsing error ("no map-keyed/list section at peer-groups").
- **#7542** breaks a core user interaction pattern—when an agent asks the user a question via the web dashboard, the response channel is already dead.
- **#7533** is a regression in Docker build infrastructure, possibly related to recent Rust toolchain changes.

## Feature Requests & Roadmap Signals

**New feature requests filed today:**

1. **#7543 — Multi-session support in gateway web chat** — Users want session management (new/switch/rename/delete) for independent conversations per agent. This is a significant UX gap for the web dashboard.

2. **#7539 — llama.cpp model router** — A user wants the ability to quickly switch between local LLM models, not just use the default.

3. **#7531 — Streaming card messages for Chinese IM channels** — QQ, DingTalk, WeChat, and Feishu users are experiencing anxiety from long waits for card messages (interactive UI components). Streaming rendering would improve perceived responsiveness.

**Prediction for v0.8.1**: Based on the tracker (#6970), the next release will include additive channels, providers, and tools. The consolidation PR (#7540) may slip in if merged in time. The multi-session feature (#7543) is likely too large for v0.8.1 and may target v0.9.0.

## User Feedback Summary

**Positive signals:**
- Users are actively building on ZeroClaw—a user (#abdulhakam) is running smaller local models and finding the app "very useful" for smaller tasks.
- The skill system is being adopted—contributors like JordanTheJet are adding architecture review, PR review, and work queue skills organically.

**Pain points and dissatisfaction:**
- **Onboarding friction**: A new Windows user (#7537) was immediately blocked by `quickstart`. This is a first-impression-breaking issue.
- **Configuration not honored**: The OpenAI timeout bug (#6723) meant user-set timeouts were silently ignored—users may have been experiencing unexplained timeouts for weeks.
- **Runtime inconsistency**: The V3 workspace path issue (#7541) means agents may be writing to the shared data directory instead of isolated workspaces, causing potential data mixing.
- **Web dashboard limitations**: Multiple issues (#7553, #7542, #7543) point to the web dashboard being the weakest component of the stack—broken on source installs, broken for user interaction, and lacking basic session management.

## Backlog Watch

**Items needing maintainer attention:**

1. **PR #6719 — Model switch persistence** (open since May 16) — `needs-author-action`, stale-candidate. This is a P1 bug fix for `model_switch` tool behavior, but the author hasn't responded in nearly a month.

2. **PR #6667 — Skills background review fork** (open since May 14) — `needs-author-action`, XL size, high risk. This is the foundational skill improvement PR that wires up the `SkillImprover`. It's been stalled for 30 days.

3. **PR #6693 — Dream mode memory consolidation** (open since May 16) — `needs-author-action`, XL size, high risk. Adds periodic memory consolidation with 5-phase engine. Stalled for 28 days.

4. **PR #7351 — MCP auto-reconnect** (open since June 7) — `needs-author-action`. Remote MCP servers that restart leave the client pinned to dead sessions. Important for reliability.

5. **Issue #6970 — v0.8.1 tracker** (open since May 27, 0 comments) — The maintainer's own tracker for the next release has no discussion, suggesting it may be a personal checklist rather than a collaborative planning tool.

**Risk**: The concentration of high-risk, XL-sized PRs awaiting author action creates a delivery risk for v0.8.1. If these PRs are abandoned or need significant rework, the release timeline may slip.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Jatway/agents-radar).*