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
| **GitHub Copilot** | IDE plugin + agent | 2,000 completions, 50 chat/agent requests/mo | Pro $10/mo · Pro+ $39/mo · Business/Enterprise custom | Best value, ubiquity (VS Code, JetBrains, GitHub.com) |
| **Cursor** | Full IDE (VS Code fork) | Hobby: limited agent requests | Pro $20/mo · Pro+ $60/mo · Ultra $200/mo | Best-polished IDE experience, strong Composer agent |
| **Claude Code** | Terminal/CLI + IDE + desktop agent | Bundled with Claude Pro ($20/mo) | Pro $20/mo · Max 5x/20x tiers up to ~$200/mo | Deepest multi-file reasoning, autonomous large tasks |
| **OpenAI Codex (CLI)** | Terminal/CLI agent | Included in ChatGPT Free (limited) | Bundled in ChatGPT Plus $20/mo, Pro $200/mo | Deterministic multi-step execution, top Terminal-Bench score |
| **Windsurf → Devin Desktop** | IDE + async agent | Free tier (generous, unlimited tab completion) | Pro $20/mo · Max $200/mo · Teams $40/user/mo | Cascade agent, codebase-wide multi-file edits |
| **Google Antigravity 2.0** | IDE + agent (Gemini) | Free for individuals | — | Gemini 3.5 Flash-powered, newer entrant |
| **Devin (Cognition)** | Fully autonomous cloud agent | — | Free trial · Pro $20/mo · Max $200/mo · Teams from $80/mo | Unattended backlog-task delegation |
| **Augment Code** | IDE agent, credit-based | Dev plan free (generous) | Indie $20/mo · Individual Pro $50/mo · Standard $60/user/mo | Large codebase context/indexing |

### Local Agents

| Agent | Cost | Model Source | Notes |
|---|---|---|---|
| **Cline** | Free (Apache 2.0) | Bring-your-own — local (Ollama/LM Studio) or cloud key | Current setup — max flexibility |
| **opencode** | Free, open source | Any provider, model-agnostic | 180k+ GitHub stars, most-starred open agent, ships daily |
| **Aider** | Free, open source | Any provider (local or cloud) | Git-native, auto-commits per edit — slowing on updates as of mid-2026 |
| **Kilo Code / RooCode / Zed** | Free (Zed has paid tier too) | Model-agnostic | RooCode often cited as strongest on large multi-file changes |
| **LM Studio + Continue.dev** | Free | Fully local (GGUF/MLX models) | GUI-first alternative to Ollama for model management |

### Local Models (Open-Weight) — updated September 2026

New candidates worth knowing about since this table was first written:

| Model | Type | Notes |
|---|---|---|
| **Kimi K3** (Moonshot AI) | 2.8T total / 104B active, MoE | New open-weight #1 by most rankings, but needs cluster-class hardware — not laptop-viable |
| **Qwen3.8-27B** | 27B dense, multimodal | Apache 2.0, released Aug 14 2026 — fits comfortably on a single high-RAM Mac/GPU, a strong local daily-driver candidate |
| **Devstral Small 24B** | 24B, agentic-tuned | Purpose-built for agentic multi-file workflows specifically, not just general coding |

**Worth keeping in mind regardless of tool:** per Stack Overflow's 2026 Developer Survey, AI coding tool adoption is ~84% monthly, but developer trust in AI-generated code's accuracy dropped to 29% (from 40% the year before). Don't treat any single agent's output — local or cloud — as final without review.

## Our Setup

This repository documents our current working setup:
- **Local**: Cline (VS Code) → Ollama → `qwen3-coder:30b`, with **Qwen3.8-27B under evaluation as a potential upgrade** (see table above)
- **Escalation path if quality ceiling hit**: Claude Code or Cursor Pro ($20/mo) for heavy multi-file / architecture-level tasks, keep Cline local for routine work

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