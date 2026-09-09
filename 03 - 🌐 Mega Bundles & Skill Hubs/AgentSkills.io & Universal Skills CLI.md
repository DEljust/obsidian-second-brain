---
title: AgentSkills.io & Universal Skills CLI
tags:
  - meta-hub
  - skills-hub
  - cli
  - package-manager
  - agentskills
github_repos:
  - https://github.com/vercel-labs/skills
documentation: https://agentskills.io
related_notes:
  - "[[00 - 🧠 AI Agent Skills Second Brain (MOC)]]"
  - "[[VoltAgent Awesome Agent Skills (1000+ Skills)]]"
  - "[[Awesome Claude Skills & Composio Ecosystem]]"
  - "[[Agent Skills Best Practices & Progressive Disclosure]]"
---

# 🚀 AgentSkills.io & Universal Skills CLI

**Agent Skills** (`agentskills.io` / `vercel-labs/skills`) is the open standard and package management ecosystem for AI agent capabilities. It solves the problem of giant, bloated monolithic system prompts by providing modular, version-controlled skill packages that agents discover and execute on demand.

---

## 📦 What is a Skill?
A skill is a self-contained directory with a `SKILL.md` file:
```
my-skill/
├── SKILL.md       <-- Frontmatter metadata + procedural instructions
├── scripts/        <-- Executable scripts (Node, Python, Bash)
└── resources/      <-- Schemas, templates, reference docs
```

### The Power of "Progressive Disclosure"
Instead of injecting hundreds of thousands of tokens into the context window:
1. The agent first only reads the **name** and **description** in the skill catalog.
2. When the user's task matches a skill's intent, the agent loads the detailed instructions from `SKILL.md`.
3. If necessary, it invokes helper scripts or tools defined in the skill.

---

## 🛠️ The `npx skills` CLI: Universal Package Manager

The `npx skills` CLI acts like `npm` or `pip` for AI agents:

| Command | Description |
| :--- | :--- |
| `npx skills find <keyword>` | Search public GitHub repos for relevant skills |
| `npx skills add <owner/repo>` | Install all skills from a GitHub repository |
| `npx skills add <owner/repo> --skill <name>` | Install a specific single skill |
| `npx skills list` | List all active skills installed in current project |
| `npx skills update` | Update installed skills to the latest git commits |
| `npx skills remove <name>` | Uninstall a skill |

---

## 🌐 Supported AI Agents
Skills installed via `npx skills` work seamlessly across:
- **Claude Code** (`.claude/skills/`)
- **Cursor** (`.cursor/skills/` or `.cursorrules`)
- **Antigravity CLI** (`.gemini/skills/` or `.agents/skills/`)
- **Windsurf** (`.windsurfrules` / skills)
- **Cline / Roo Code** (`.clinerules/`)

---

## 🔗 Connected Repositories
* Browse 1,000+ engineering skills: [[VoltAgent Awesome Agent Skills (1000+ Skills)]]
* Browse MCP servers: [[Awesome MCP Servers Directory]]
