---
title: Android Studio & AI Agent Workflow Guide
tags:
  - android
  - android-studio
  - setup
  - workflow
  - ide
related_notes:
  - "[[00 - 🧠 AI Agent Skills Second Brain (MOC)]]"
  - "[[Senior Android Engineer Agent Blueprint]]"
  - "[[Claude Android Ninja (Modular Arch & Navigation 3)]]"
  - "[[Complete Senior Android & UI-UX .cursorrules]]"
---

# 🛠️ Android Studio & AI Agent Workflow Guide

How to integrate these Senior Android skills directly into your Android development workflow, whether you use **Android Studio (Ladybug / Meerkat / Hedgehog)**, **Cursor**, **Claude Code**, or **Antigravity CLI**.

---

## 🎯 Option A: Android Studio Native Integration (Gemini Code Assist / AI Tools)

1. **Project Rules via `.prompting` or Project Root Rules**:
   - In your project root (e.g. `C:\Users\USER\AndroidStudioProjects\YourApp`), create a `.cursorrules` or `.prompting/rules.md` file.
   - Copy the comprehensive rules from [[Complete Senior Android & UI-UX .cursorrules]].
2. **Context Sharing**:
   - Keep your `libs.versions.toml` pinned in the context so the assistant always references your exact dependency versions.
   - Ensure the agent adheres to Compose Material 3 Expressive guidelines.

---

## 🎯 Option B: Headless Agent Workflow (Claude Code / Antigravity / Windsurf)

You can run an AI agent directly in the terminal inside your Android project root while viewing and compiling in Android Studio:

```bash
# 1. Navigate to your Android Project
cd C:\Users\USER\AndroidStudioProjects\YourProject

# 2. Add Senior Android Skills via CLI
npx skills add Drjacky/claude-android-ninja
npx skills add skydoves/compose-performance-skills

# 3. Launch Agent to build a feature
# Example with Claude Code:
claude

# Or using Antigravity CLI / Cursor
```

### 🔁 The Iterative Android Loop:
1. **Agent Writes Code**: Creates feature modules, UI Composables, ViewModels, and navigation routes.
2. **Gradle Verification**: Run `./gradlew assembleDebug` or `./gradlew test` via terminal to verify zero compilation errors.
3. **Android Studio Preview**: Android Studio immediately picks up the changes, rendering the `@Preview` composables live in the IDE split view!

---

## 📋 Recommended Workflow Prompt Template

```markdown
You are a Staff Android Engineer and UI/UX Designer.
Follow the rules defined in `claude-android-ninja` and `compose-performance-skills`.

Task:
Build the [Feature Name] screen.
Requirements:
1. Architecture: Clean Architecture + MVI with Unidirectional Data Flow (StateFlow + UI Events).
2. UI/UX: Material Design 3, dynamic colors, tactile haptics on action buttons, and skeleton shimmer loading state.
3. Navigation: Type-safe Navigation 3 route with `@Serializable`.
4. Performance: All model classes annotated with `@Immutable`, zero unnecessary recompositions, explicit keys on Lazy layouts.
5. Accessibility: Minimum 48dp touch targets and descriptive TalkBack labels.
```
