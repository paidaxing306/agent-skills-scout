---
name: skill-scout
description: 搜索 GitHub 上 20k+ stars 的 AI agent 编码技能/规则项目，列表供用户选择后自动安装到全局和项目。
---

# Skill Scout — 高星 Agent 技能发现与安装

搜索 GitHub 上高星 agent 编码技能项目，列出供选择，用户确认后一键安装到全局 Hermes + 当前项目。

## 触发条件

- "找高星 skill" / "搜索 agent 技能" / "有没有好的 agent 规则"
- "skill-scout" / "技能侦察"

## 搜索流程

### 第1步：多维度搜索

用 GitHub API 搜索，代理走 `https_proxy=http://127.0.0.1:7890`：

```bash
# 搜索关键词组合
- "agent skills coding stars:>20000"
- "agent rules cursor stars:>20000"
- "AGENTS.md rules stars:>20000"
- "claude code skills stars:>20000"
```

去重，按星数降序排列。

### 第2步：过滤

排除：
- 完整 agent 平台/框架（如 ECC、DeerFlow）
- 纯合集/awesome-list（不能直接安装）
- 非编码相关（安全攻防、法律等）
- 作者已弃用的项目

保留：可安装的规则文件、技能包、行为协议。

### 第3步：输出列表 + 等待用户选项目

格式：

```
发现 N 个可安装项目：

| # | 项目 | 星 | 类型 | 简介 |
|---|------|----|----|------|
| 1 | owner/repo | ★xxxk | 规则 | 一句话 |
| 2 | owner/repo | ★xxk | 技能 | 一句话 |

回复编号选择项目，如 "2 4" 或 "全部" 或 "跳过"
```

**必须等用户回复确认后才继续，绝不自动安装。**

### 第4步：确认安装位置

用户选了项目后，询问安装位置：

```
安装到哪？
1. 全局（所有 Hermes 会话可用）
2. 当前项目（.cursor/rules/ + AGENTS.md）
3. 都要

回复 1 / 2 / 3
```

**必须等用户回复确认后才安装，不给默认值。**

### 第5步：安装

用户确认后，逐个安装。**重要规则：**

1. **优先用原版开源 skill，不自己总结。** 如果原项目有 SKILL.md/CLAUDE.md/AGENTS.md，直接提取精华安装，不要自己编。
2. **必须转中文。** 原版英文内容自动翻译提炼为中文版再安装。
3. **安装到指定位置：**
   - 全局：`skill_manage(action='create')` 写入 `~/.hermes/skills/`
   - 项目：写入 `.cursor/rules/<name>.mdc`（always on 的用 `alwaysApply: true`）
4. **项目 README 分语言。** 中英文分别写 `README.md` 和 `README_EN.md`，不混在一个文件里。

### 第6步：输出安装摘要

```
已安装:
  owner/repo → skill-name (全局)
  owner/repo → skill-name (项目 .cursor/rules/xxx.mdc)
```

## 搜索查询模板

```bash
export https_proxy=http://127.0.0.1:7890

curl -s "https://api.github.com/search/repositories?q=agent+skills+coding+stars:>20000&sort=stars&per_page=20" | python -c "
import json,sys
for r in json.load(sys.stdin).get('items',[]):
    print(f\"{r['stargazers_count']}|{r['full_name']}|{r.get('description','')[:150]}\")
"
```

## 参考

- `references/pitfalls.md` — 已知陷阱（ComfyUI-Manager URL、模型下载镜像、Docker 容器、GitHub API）
- `references/indexed-projects.md` — 已索引和跳过的项目清单
