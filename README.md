# ai-review-public

This repository serves as a collaborative space for reviewing and sharing insights about AI coding agents. It documents our evaluation process and findings to help others make informed decisions about which AI tools work best for their development workflows.

## Project Purpose

The goal of this project is to:
- Evaluate different AI coding agents for software development
- Share our experiences and findings with the community
- Help developers choose the right AI tools for their needs
- Document best practices for AI-assisted coding workflows

## AI Coding Agents Evaluation

This repository documents our evaluation of various AI coding agents, focusing on both cloud-based and local solutions. The comparison includes factors like pricing, capabilities, and performance in real-world development scenarios.

### Cloud-Based Agents

| Agent | Type | Free Tier | Paid Pricing | Best For |
|---|---|---|---|---|
| **GitHub Copilot** | IDE plugin + agent | 2,000 completions/mo (chat/agent allowance not re-checked) | Pro $10/mo · Pro+ $39/mo · Max $100/mo · Business/Enterprise custom. Chat, agent mode and code review use metered AI credits (see note below) | Best value, ubiquity (VS Code, JetBrains, GitHub.com) |
| **Cursor** | Full IDE (VS Code fork) | Free: limited | Plus $8/mo (Grok models only) · Premium $30/mo · Super $100/mo · Ultra $200/mo, each with a weekly usage allowance. Other vendors' models are billed separately at API list price | Best-polished IDE experience, strong Composer agent |
| **Claude Code** | Terminal/CLI + IDE + desktop agent | Not on the Free plan — included from Pro | Pro $20/mo ($17/mo billed annually) · Max $100/mo (5x Pro usage) · Ultra $200/mo (10x Pro usage per week) | Deepest multi-file reasoning, autonomous large tasks |
| **OpenAI Codex (CLI)** | Terminal/CLI agent | Included in ChatGPT Free (quick tasks) | Bundled in ChatGPT Go $8/mo, Plus $20/mo, Pro from $100/mo ($100 / $200 / $500 tiers) | Deterministic multi-step execution, top Terminal-Bench score |
| **Windsurf → Devin Desktop** | IDE + async agent | Free tier (generous, unlimited tab completion) | Pro $20/mo · Max $200/mo · Teams $40/user/mo | Cascade agent, codebase-wide multi-file edits |
| **Google Antigravity 2.0** | IDE + agent (Gemini) | Free for individuals | — | Gemini 3.5 Flash-powered, newer entrant |
| **Devin (Cognition)** | Fully autonomous cloud agent | — | Free trial · Pro $20/mo · Max $200/mo · Teams from $80/mo | Unattended backlog-task delegation |
| **Augment Code** | IDE agent, credit-based | Dev plan free (generous) | Indie $20/mo · Individual Pro $50/mo · Standard $60/user/mo | Large codebase context/indexing |

**Prices** for GitHub Copilot, Cursor, Claude and Codex were re-read from the vendors' own pricing pages on 2026-11-10. Copilot usage beyond completions is metered in AI credits ($0.01 each; completions use none): monthly credits are 1,500 on Pro, 7,000 on Pro+ and 20,000 on Max (base plus flex credits). Cursor's old Pro $20 and Pro+ $60 tiers no longer appear on its pricing page. **Not re-checked:** Windsurf/Devin, Antigravity, Augment — treat those rows as the July/September figures.

### Local Agents

| Agent | Cost | Model Source | Notes |
|---|---|---|---|
| **Cline** | Free (Apache 2.0) | Bring-your-own — local (Ollama/LM Studio) or cloud key | Current setup — max flexibility. Extension v4.1.26 (26 Oct 2026); it now also ships a CLI, a desktop app and an SDK |
| **opencode** | Free, open source | Any provider, model-agnostic | 180k+ GitHub stars, most-starred open agent, ships daily |
| **Aider** | Free, open source | Any provider (local or cloud) | Git-native, auto-commits per edit — slowing on updates as of mid-2026 |
| **Kilo Code / Zed** | Free (Zed has paid tier too) | Model-agnostic | Kilo Code is widely recommended as the successor for Roo Code users (third-party comparisons; not checked at the source) |
| **RooCode** | — | — | **Shut down 15 May 2026**; its repo is archived and read-only. Its README points to ZooCode (a community fork) and Cline |
| **LM Studio + Continue.dev** | Free | Fully local (GGUF/MLX models) | GUI-first alternative to Ollama for model management |

### Local Models (Open-Weight) — updated September 2026

New candidates worth knowing about since this table was first written:

| Model | Type | Notes |
|---|---|---|
| **Kimi K3** (Moonshot AI) | 2.8T total / 104B active, MoE | New open-weight #1 by most rankings, but needs cluster-class hardware — not laptop-viable |
| **Qwen3.8-27B** | 27B dense, multimodal | Apache 2.0, released Aug 14 2026 — fits comfortably on a single high-RAM Mac/GPU, a strong local daily-driver candidate |
| **Devstral Small 24B** | 24B, agentic-tuned | Purpose-built for agentic multi-file workflows specifically, not just general coding |

### What Fits Locally on Apple Silicon (36GB vs 48GB) — updated November 2026

> Planning figures collected from third-party blogs and benchmarks — **not our own measurements yet**. Treat them as expectations to test.

Token generation on Apple Silicon is mostly memory-bandwidth-bound, so moving from an M3 Pro (~150 GB/s) to an M5 Pro (~307 GB/s reported) should matter more than the extra 12GB of RAM alone. One source reports a 10–15% slowdown from thermal throttling in long sessions on a laptop, so measure tokens/sec over a long session, not just the first minute.

| Model | Approx size (Q4) | Fits 36GB | Fits 48GB | Notes |
|---|---|---|---|---|
| `qwen3-coder:30b` | ~17–20GB | ✅ | ✅ | Our current default — the baseline |
| `qwen3.8:27b` | ~14–17GB | ✅ | ✅ | Dense, ~256K context |
| `qwen3.6:27b` | ~16GB | ✅ | ✅ | 77.2% SWE-bench Verified (reported, not yet checked at the source) |
| `qwen3.6:35b-a3b` (mxfp8) | — | — | ✅ | One blogger on an M5 Pro 48GB found mxfp8 gives better code than standard Q4 |
| `devstral-small:24b` | fits comfortably | ✅ | ✅ | Agentic-tuned — test under Cline specifically |
| GLM-5.3, Kimi K2.6 / K3, DeepSeek V4 Flash | — | ❌ | ❌ | Need 128GB+ |

Watch out for mismatched benchmarks: a widely quoted ~51 tok/s figure for Qwen3-Coder was measured on an M5 with **32GB**, not 48GB.

### Ollama on macOS — Practical Notes

- Ollama's own release notes for **0.40.x** (latest 0.40.16, 9 Nov 2026) mention MLX work on Apple Silicon (0.40.7, 0.40.12, 0.40.14). Third-party posts date the MLX preview to 0.19 (March 2026) and say it became the default later, and that GGUF models still go to llama.cpp at first. We haven't checked that history against Ollama's notes, so read the notes for your version before relying on MLX for a given model.
- Raise the default context with `launchctl setenv OLLAMA_CONTEXT_LENGTH 16384` and restart the Ollama app; re-check it after every upgrade.
- If you use the Ollama .app, don't also run `ollama serve` — both want port 11434.
- After loading a model, `ollama ps` should show **100% GPU**. Anything else means the model plus its context doesn't fit in memory.

### How We Compare Local Models

Every candidate gets the same four real tasks from our own repos, run one model at a time through Cline: a single-file edit, a multi-file refactor, a task that runs terminal commands, and a long-context task. For each we record ✅ / 🟡 / ❌, tokens/sec and notes.

**Decision rule:** switch the default only if a candidate wins at least 3 of the 4 tasks **and** isn't meaningfully slower. A speed win alone doesn't count. Results will be added here once the runs are done.

**Worth keeping in mind regardless of tool:** per Stack Overflow's 2026 Developer Survey, AI coding tool adoption is ~84% monthly, but developer trust in AI-generated code's accuracy dropped to 29% (from 40% the year before). Don't treat any single agent's output — local or cloud — as final without review.

### Agent Safety: a Malicious Extension, October 2026

On 29 Oct 2026 Cursor published a [security notice](https://cursor.com/blog/claude-code-extension-security-notice): maliciously modified versions of Anthropic's Claude Code extension, **not developed by Anthropic**, were published as `Anthropic.claude-code` 2.1.312 and 2.1.313 in the Cursor VS Code Extension Marketplace for macOS and Windows, for about 11 hours on that day. Per the notice they collected host and user information and tried to add an attacker SSH key and persistence. Cursor says it removed them, rebuilt its marketplace and found no evidence that other versions or the official distribution were affected. Anyone who installed or updated to those versions in that window should follow the notice's remediation steps, since uninstalling the extension alone may not be enough.

Our takeaway: an agent extension runs with your user's permissions, so check the version and publisher after an update, and treat an extension's update the way you'd treat a new dependency.

### What an AI Code Review Costs (Two Data Points)

We run an on-demand, read-only Claude review on PRs of the public [ai-delivery-playbook](https://github.com/MikulasFrenak/ai-delivery-playbook) (see its [`docs/ci.md`](https://github.com/MikulasFrenak/ai-delivery-playbook/blob/main/docs/ci.md)), via `claude-code-action` on a subscription token. Its first two successful runs, on PRs of 7–8 changed files with Sonnet 5.5 (and Haiku 5.5 for small background tasks):

| PR | Turns | Time | Cost the run reports |
|---|---|---|---|
| Review rules and CI prompt change | 12 | 35 s | $0.25 |
| One-line prompt fix plus docs | 6 | 18 s | $0.17 |

That cost is what the run would cost at API prices; on a subscription token it counts against plan limits instead. The log doesn't include real token counts, because the action hides the model's full output. Two runs aren't a benchmark, so treat these as an order of magnitude. Failed runs that never reach the model cost $0.

## Our Setup

This repository documents our current working setup:
- **Local**: Cline (VS Code) → Ollama → `qwen3-coder:30b`, with **Qwen3.8-27B, Qwen3.6-27B and Devstral Small 24B under evaluation** as potential upgrades (see tables above)
- **Hardware**: moving from a MacBook Pro M3 Pro 36GB to an M5 Pro 48GB; the model comparison will be run on the new machine, since 36GB numbers don't transfer
- **Escalation path if quality ceiling hit**: Claude Code (Pro $20/mo) or Cursor (Premium $30/mo) for heavy multi-file / architecture-level tasks, keep Cline local for routine work

## Review Sharing

This repository is designed to be a collaborative space where we can:
1. Share our experiences with different AI coding agents
2. Document what works and what doesn't in real development scenarios
3. Help others avoid common pitfalls and make better tool choices
4. Create a reference for the community about AI coding agent capabilities

We welcome contributions from other developers who want to share their experiences, benchmarks, or insights about AI tools.

## How to Contribute

1. Fork this repository
2. Add your own experiences or findings
3. Submit a pull request with your changes
4. Share your review and insights with the community

## License

This project is licensed under the MIT License - see the LICENSE file for details.