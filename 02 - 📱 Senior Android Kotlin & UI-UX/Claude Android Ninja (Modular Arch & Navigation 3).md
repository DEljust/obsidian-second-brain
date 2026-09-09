---
title: Claude Android Ninja (Modular Arch & Navigation 3)
tags:
  - android
  - kotlin
  - claude-skills
  - agent-skill
  - modularization
  - navigation3
github_repos:
  - https://github.com/Drjacky/claude-android-ninja
author: Hossein Abbasi (Drjacky)
related_notes:
  - "[[00 - 🧠 AI Agent Skills Second Brain (MOC)]]"
  - "[[Senior Android Engineer Agent Blueprint]]"
  - "[[Jetpack Compose UI-UX Master Skill]]"
  - "[[Compose Performance & Quality Audit Skills]]"
  - "[[Complete Senior Android & UI-UX .cursorrules]]"
---

# 🥷 Claude Android Ninja (Modular Arch & Navigation 3)

**Claude Android Ninja** is an opinionated, production-grade agent skill bundle created by Hossein Abbasi (`Drjacky`), a Senior Android Engineer. It establishes a rigorous set of architectural guardrails for AI coding agents working on modern Android projects.

* **Repository**: [Drjacky/claude-android-ninja](https://github.com/Drjacky/claude-android-ninja)
* **Target Platforms**: Claude Code, Cursor, Windsurf, Antigravity, Gemini Code Assist
* **Format**: Agent Skills standard (`SKILL.md`)

---

## 🔑 Core Pillars of the Ninja Skill

### 1. Modern Modular Architecture
The skill instructs the agent to avoid bloated single-module projects and automatically organize features:
```
├── app/
├── build-logic/ (Convention plugins using buildSrc or composite build)
├── core/
│   ├── common/
│   ├── designsystem/
│   ├── network/
│   ├── database/
│   └── datastore/
└── feature/
    ├── onboarding/
    ├── home/
    └── details/
```

### 2. Modern Navigation (Navigation 3 & Type-Safety)
- Eliminates brittle string-based deep links and routes.
- Enforces `@Serializable` route arguments:
  ```kotlin
  @Serializable
  data object HomeRoute

  @Serializable
  data class DetailRoute(val itemId: Long)
  ```
- Implements decoupled feature navigators so feature modules don't directly reference each other.

### 3. Clean Dependency Injection (Hilt / Koin)
- Recommends Hilt / Koin annotations.
- Ensures ViewModels are injected via `@HiltViewModel` and never instantiated manually inside Composables.
- Enforces constructor injection on all domain UseCases and Repositories.

### 4. Robust Gradle Conventions (Version Catalogs)
- Enforces Gradle Version Catalogs (`libs.versions.toml`).
- Uses custom convention plugins to share standard compileOptions, Compose compiler flags, and lint configurations across all sub-modules.

---

## 🚀 How to Install & Use

Install directly via the universal agent skills package manager:

```bash
# Install the skill into your local project
npx skills add Drjacky/claude-android-ninja
```

When prompt engineering your agent:
> *"Using the claude-android-ninja skill, scaffold a new feature module `:feature:cart` with MVI architecture, Room-backed cart repository, and Navigation 3 entry point."*
