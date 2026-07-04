# 🕵️ Skill Scout

> Discover high-star AI agent skills on GitHub. Two-step confirm, one-click install.

<p align="center">
  <a href="README.md">中文</a> · <b>English</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Hermes-skill-8b5cf6" alt="Hermes Skill">
  <img src="https://img.shields.io/badge/Cursor-compatible-blue" alt="Cursor">
  <img src="https://img.shields.io/badge/Claude_Code-compatible-orange" alt="Claude Code">
  <img src="https://img.shields.io/badge/Codex-compatible-green" alt="Codex">
  <img src="https://img.shields.io/badge/license-MIT-brightgreen" alt="MIT">
</p>

---

## What

**Skill Scout** discovers and installs high-star AI agent coding skills/rules from GitHub. It searches, filters, presents a ranked list, and waits for your confirmation on both project selection and install target before proceeding.

Search → Filter → List → You pick projects → You pick target → Install → Report.

## Why

| Pain point | How Skill Scout solves it |
|------------|--------------------------|
| Too many repos, hard to filter manually | Multi-keyword search, sorted by stars, non-coding filtered out |
| High stars doesn't mean installable | Auto-exclude awesome-lists, platforms, security-only |
| Manual Chinese translation and format adaptation | Auto-translate, auto-adapt Hermes/Cursor/AGENTS.md formats |
| Agent might install without asking | **Two-step confirmation**: pick projects, then pick target, no defaults |

## Demo

```
👤 User: find high-star skills

🤖 Skill Scout:
  Searching GitHub for 20k+ stars agent skill repos...

  Found 5 installable projects:

  | # | Repo | Stars | Type |
  |---|------|-------|------|
  | 1 | obra/superpowers | ★245k | Skill pack |
  | 2 | addyosmani/agent-skills | ★68k | Skill pack |
  | 3 | Leonxlnx/taste-skill | ★55k | Skill pack |
  | 4 | NeekChaw/RIPER-5 | ★2.6k | Protocol |
  | 5 | Kulaxyz/self-learning-skills | ★778 | Skill |

  Reply with numbers, e.g. "1 3 5" or "all"

👤 User: 1 2

🤖 Skill Scout:
  Install where?
  1. Global (all Hermes sessions)
  2. Current project (.cursor/rules/ + AGENTS.md)
  3. Both

👤 User: 3

🤖 Skill Scout:
  ✅ obra/superpowers → 6 skills installed (global + project)
  ✅ addyosmani/agent-skills → 4 skills installed (global + project)
  Done.
```

## Install & Usage

### Hermes Agent

```bash
# Skill Scout is itself a Hermes skill
# Installed at ~/.hermes/skills/software-development/skill-scout/

# Trigger:
"skill-scout" or "find high-star skills"
```

### Supported Agents

| Agent | Install format |
|-------|---------------|
| Hermes | `~/.hermes/skills/<name>/SKILL.md` |
| Cursor | `.cursor/rules/<name>.mdc` |
| Claude Code | `CLAUDE.md` or skills directory |
| Codex | `AGENTS.md` or skills directory |

## Search Strategy

Multi-keyword combined search, deduplicated:

| Keyword | Matches |
|---------|---------|
| `agent skills coding` | General skill packs |
| `agent rules cursor` | Cursor rules |
| `AGENTS.md rules` | Cross-agent rules |
| `claude code skills` | Claude Code skills |
| `coding agent discipline` | Behavioral protocols |

## Filter Rules

| ✅ Keep | ❌ Skip |
|---------|---------|
| Installable rule files (AGENTS.md / CLAUDE.md) | Full agent platforms (ECC, DeerFlow) |
| Installable skill packs (skills/ directory) | Pure collections (awesome-* series) |
| Compact behavioral protocols/charters | Non-coding (security/legal) |
| | Deprecated by author |

## Indexed Projects

| Repo | Stars | Type | Indexed |
|------|-------|------|:--:|
| obra/superpowers | 245k | Skill pack | ✅ |
| addyosmani/agent-skills | 68k | Skill pack | ✅ |
| Leonxlnx/taste-skill | 55k | Skill pack | ✅ |
| PatrickJS/awesome-cursorrules | 40k | Collection | 📚 |
| ciembor/agent-rules-books | 2k | Rules | ✅ |
| NeekChaw/RIPER-5 | 2.6k | Protocol | ✅ |
| intellectronica/ruler | 2.7k | Framework | ✅ |
| Kulaxyz/self-learning-skills | 778 | Skill | ✅ |
| entropyvortex/meta-llm-charter | 245 | Charter | ✅ |
| madebyaris/advance-minimax-m3-cursor-rules | 124 | Rules | ✅ |
| sisyphusse1-ops/claude-code-pro-pack | 30 | Rules | ✅ |

## Project Structure

```
skill-scout/
├── README.md        # Chinese
├── README_EN.md     # English (this file)
├── AGENTS.md        # Agent rules
├── installed.md     # Install manifest
└── .gitignore
```

## License

MIT
