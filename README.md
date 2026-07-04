# 🕵️ Skill Scout

> 发现 GitHub 高星 AI Agent 技能，两次确认，一键安装。

<p align="center">
  <b>中文</b> · <a href="README_EN.md">English</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Hermes-skill-8b5cf6" alt="Hermes Skill">
  <img src="https://img.shields.io/badge/Cursor-compatible-blue" alt="Cursor">
  <img src="https://img.shields.io/badge/Claude_Code-compatible-orange" alt="Claude Code">
  <img src="https://img.shields.io/badge/Codex-compatible-green" alt="Codex">
  <img src="https://img.shields.io/badge/license-MIT-brightgreen" alt="MIT">
</p>

---

## 这是什么

**Skill Scout** 是一个 AI Agent 技能发现与安装工具。

GitHub 上 agent skill 项目太多了——合集、平台、安全专项、已弃用的——靠肉眼筛选效率低。Skill Scout 自动搜索、智能过滤、让你确认后安装。**搜 → 过滤 → 展示 → 你选项目 → 你选位置 → 装完报告。**

## 为什么需要它

| 痛点 | Skill Scout 怎么解决 |
|------|---------------------|
| GitHub 上项目太多，不知道哪些靠谱 | 多关键词搜索，按星数排序，过滤非编码类 |
| 高星的不一定适合装（合集、平台） | 自动排除 awesome-list、完整框架、安全专项 |
| 装完还要手动适配中文和不同工具格式 | 自动翻译提炼中文，自动适配 Hermes/Cursor/AGENTS.md |
| 怕 agent 自作主张乱装 | **两次确认**：先选项目，再选位置，不给默认值 |

## 效果演示

```
👤 用户: 找高星 skill

🤖 Skill Scout:
  搜索 GitHub 20k+ stars agent 技能项目...

  发现 5 个可安装项目：

  | # | 项目 | 星 | 类型 |
  |---|------|----|------|
  | 1 | obra/superpowers | ★245k | 技能包 |
  | 2 | addyosmani/agent-skills | ★68k | 技能包 |
  | 3 | Leonxlnx/taste-skill | ★55k | 技能包 |
  | 4 | NeekChaw/RIPER-5 | ★2.6k | 协议 |
  | 5 | Kulaxyz/self-learning-skills | ★778 | 技能 |

  回复编号选择，如 "1 3 5" 或 "全部"

👤 用户: 1 2

🤖 Skill Scout:
  安装到哪？
  1. 全局（所有 Hermes 会话可用）
  2. 当前项目（.cursor/rules/ + AGENTS.md）
  3. 都要

👤 用户: 3

🤖 Skill Scout:
  ✅ obra/superpowers → 已安装 6 个技能（全局 + 项目）
  ✅ addyosmani/agent-skills → 已安装 4 个技能（全局 + 项目）
  完成。
```

## 安装和使用

### Hermes Agent

```bash
# Skill Scout 本身就是一个 Hermes skill
# 已安装在 ~/.hermes/skills/software-development/skill-scout/

# 使用时说：
"skill-scout" 或 "找高星 skill"
```

### 支持的 Agent 工具

| Agent | 安装格式 |
|-------|---------|
| Hermes | `~/.hermes/skills/<name>/SKILL.md` |
| Cursor | `.cursor/rules/<name>.mdc` |
| Claude Code | `CLAUDE.md` 或 skills 目录 |
| Codex | `AGENTS.md` 或 skills 目录 |

## 搜索策略

多关键词组合搜索，去重合并：

| 关键词 | 命中类型 |
|--------|---------|
| `agent skills coding` | 通用技能包 |
| `agent rules cursor` | Cursor 规则 |
| `AGENTS.md rules` | 跨 agent 规则 |
| `claude code skills` | Claude Code 技能 |
| `coding agent discipline` | 行为协议 |

## 过滤规则

| ✅ 保留 | ❌ 排除 |
|---------|---------|
| 可安装规则文件（AGENTS.md / CLAUDE.md） | 完整 agent 平台（ECC, DeerFlow） |
| 可安装技能包（skills/ 目录） | 纯合集（awesome-* 系列） |
| 紧凑行为协议/章程 | 非编码类（安全攻防、法律） |
| | 作者已弃用 |

## 已收录项目 (20k+ stars)

| 项目 | 星 | 类型 | 收录 |
|------|----|------|:--:|
| obra/superpowers | 245k | 技能包 | ✅ |
| multica-ai/andrej-karpathy-skills | 187k | 规则 | 🔍 |
| JuliusBrussee/caveman | 82k | 技能 | 🔍 |
| addyosmani/agent-skills | 68k | 技能包 | ✅ |
| Leonxlnx/taste-skill | 55k | 技能包 | ✅ |

> ✅ = 已收录  🔍 = 新发现待评估  📚 = 合集（不可安装）  🏗️ = 平台（太重）

### 合集 & 平台（不可直接安装）

| 项目 | 星 | 类型 |
|------|----|------|
| affaan-m/ECC | 225k | 🏗️ 平台 |
| bytedance/deer-flow | 76k | 🏗️ 平台 |
| ruvnet/ruflo | 62k | 🏗️ 平台 |
| hesreallyhim/awesome-claude-code | 47k | 📚 合集 |
| PatrickJS/awesome-cursorrules | 40k | 📚 合集 |

## 项目结构

```
skill-scout/
├── README.md        # 中文
├── README_EN.md     # English
├── AGENTS.md        # 项目 agent 规则
├── installed.md     # 已安装清单
└── .gitignore
```

## License

MIT
