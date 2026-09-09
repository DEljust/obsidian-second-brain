---
title: Compose Performance & Quality Audit Skills
tags:
  - android
  - kotlin
  - jetpack-compose
  - performance
  - optimization
  - auditing
github_repos:
  - https://github.com/skydoves/compose-performance-skills
  - https://github.com/aldefy/compose-skill
authors:
  - Jaewoong Eum (skydoves)
  - aldefy
related_notes:
  - "[[00 - 🧠 AI Agent Skills Second Brain (MOC)]]"
  - "[[Senior Android Engineer Agent Blueprint]]"
  - "[[Jetpack Compose UI-UX Master Skill]]"
  - "[[Complete Senior Android & UI-UX .cursorrules]]"
---

# ⚡ Compose Performance & Quality Audit Skills

A hallmark of a Senior Android Engineer is writing Compose code that is 60/120 FPS buttery smooth and free of unnecessary recompositions and memory leaks.

These two specialized agent skills provide the rules and audit mechanisms needed.

---

## 📦 1. compose-performance-skills (skydoves)
* **Repository**: [skydoves/compose-performance-skills](https://github.com/skydoves/compose-performance-skills)
* **Author**: Jaewoong Eum (Google Developer Expert for Android)
* **Format**: Agent Skills standard (`SKILL.md`)

### Core Performance Principles Enforced:
1. **Recomposition Skipping & Stability**:
   - Marking data models with `@Immutable` or `@Stable` when collections (`List`, `Set`) are passed into Composable functions (or utilizing `kotlinx.collections.immutable.ImmutableList`).
   - Using method references or lambda parameters instead of allocating new anonymous lambda instances inside recomposing scopes.
2. **Deferred State Reads**:
   - Using lambda modifier variants like `Modifier.offset { IntOffset(x, y) }` instead of `Modifier.offset(x.dp, y.dp)` so that rapidly changing values (scroll positions, gestures) only trigger drawing/layout phases, completely skipping recomposition.
3. **Lazy Layout Keys & ContentType**:
   - Always supply unique `key` parameters to `items()` in `LazyColumn` / `LazyRow` to prevent UI flicker and item recycling bugs:
     ```kotlin
     items(
         items = userList,
         key = { user -> user.id },
         contentType = { user -> user.type }
     ) { user ->
         UserCard(user = user)
     }
     ```
4. **Derived State of**:
   - Wrapping calculation-heavy state or high-frequency scroll calculations in `remember { derivedStateOf { ... } }`.

---

## 🔍 2. compose-skill (aldefy)
* **Repository**: [aldefy/compose-skill](https://github.com/aldefy/compose-skill)
* **Focus**: Evidence-based AST checking & API anti-pattern auditing

### Audit Checklist Checked by Agent:
- ❌ Detects and warns against calling `rememberCoroutineScope()` inside high-frequency items.
- ❌ Flags blocking operations or heavy IO on the main thread inside Composables.
- ❌ Replaces deprecated Compose APIs with modern replacements from the latest `androidx.compose` releases.
- ❌ Flags improper Coroutine cancellations or missing DisposableEffect cleanups.

---

## 🚀 Installation & Command
```bash
# Install the performance bundle
npx skills add skydoves/compose-performance-skills

# Install the audit skill
npx skills add aldefy/compose-skill
```

To run a performance audit on your screen:
> *"Audit `HomeScreen.kt` using compose-performance-skills. Inspect recomposition stability, lambda allocations, and modifier deferred reads."*
