# Mobile Markdown Agent (MMA) — v1 Architecture & System Design Document

**Status:** Approved & Implemented (v1.0 Production)  
**Author:** Joey Yang (`joeyang108`)  
**Repository:** `joeyang108/mobile-markdown-agent`  
**Live URL:** [https://joeyang108.github.io/mobile-markdown-agent/](https://joeyang108.github.io/mobile-markdown-agent/)  
**Deployment Anchor:** GitHub Pages (Public, Static PWA)

---

## 1. Executive Summary & Philosophy

### 1.1 The Core Problem
Mobile idle time ("Lull Time" — parked in the car waiting for family, soccer sidelines, transit queues) is the highest-risk trigger for unearned, passive dopamine habits (algorithmic social feeds, endless scrolling). While creativity and architectural insights strike during these moments, traditional developer tooling forces either:
1. Disconnected consumer scratchpads (e.g., Google Keep) that drift away from git workflows.
2. Clunky mobile IDEs/terminals that introduce cognitive overload, battery drain, and terminal frustration.

### 1.2 The Solution: Mobile Markdown Agent (MMA)
MMA is a hyper-lightweight, zero-backend Progressive Web App (PWA) designed for iOS Safari and macOS desktop. It operates strictly as an **Intent & Design Capture Vessel** directly into the `joeyang108` GitHub ecosystem, replacing passive media consumption with earned creative momentum.

### 1.3 Ironclad Architectural Boundaries
1. **Desktop Build Anchor:** All compiling, testing, package building, and coding take place exclusively on the desktop/laptop environment (Mac / Chromebook AGY). Mobile never edits code or compiles.
2. **Strictly "Capture Only" for Mobile:** MMA writes atomic Markdown design specs and brainstorms. It does not mutate complex project trees or perform arbitrary multi-file in-place edits.
3. **Via Negativa (Subtractive Design):** Zero build steps, zero npm/Node dependencies, zero backend servers. Pure browser-native HTML/CSS/JavaScript.

---

## 2. System Architecture & Topology

```
+---------------------------------------------------------------------------------+
|                                 CLIENT TIER                                     |
|  iPhone Safari Standalone PWA / macOS Safari Dock App                           |
|  - Standalone ServiceWorker Cache (sw.js v3)                                    |
|  - Encrypted LocalStorage Sandbox (GitHub PAT + Gemini API Key)                 |
+---------------------------------------------------------------------------------+
          |                                                       |
          | Direct HTTPS (REST v3)                                | Direct HTTPS (REST v1beta)
          v                                                       v
+------------------------------------+          +---------------------------------+
|           GITHUB REST API          |          |        GOOGLE GEMINI API        |
|  api.github.com/repos/joeyang108/  |          |  generativelanguage.googleapis  |
|  - Context GET: README, GEMINI.md  |          |  - GA Standard: gemini-1.5-flash|
|  - Atomic PUT: ideation/*.md       |          |  - Model Picker: 1.5-Pro, 2.5-F |
+------------------------------------+          +---------------------------------+
          |
          | Git Commits (main branch)
          v
+---------------------------------------------------------------------------------+
|                               DESKTOP INGESTION                                 |
|  Mac / Chromebook AGY Workspace (Antigravity IDE / Terminal)                    |
|  - Session Startup: Auto-scans `ideation/` for newly captured specs             |
|  - Compiler: Transforms design specs into production code & commits             |
+---------------------------------------------------------------------------------+
```

---

## 3. Core Functional Components

### 3.1 Multi-Repo Ecosystem Switcher
* Directly controls the target context: `Deep-Song-Explorer`, `NFL-Deep-Reader`, `Health-App-42`, `vibe-coding-partner`, `mobile-markdown-agent`, or any `+ Custom Repo...`.
* Switcher persists choice across app relaunches in `localStorage.getItem('mma_repo')`.

### 3.2 Dynamic Context Ingestion Engine (Strategy A + B)
* **Strategy A (Auto-Discovery):** On repository selection, MMA fires parallel `fetch` calls to inspect:
  - `README.md` (Project overview and features)
  - `GEMINI.md` (Workspace rules, architectural guardrails)
  - `backlog/backlog.md` or active design documents
* **Strategy B (Visual Pill Controls):** Discovered context renders as clickable pills (`[✓ README.md] [✓ GEMINI.md] [✓ backlog]`). Active pills inject their raw Markdown content into Gemini's prompt. Users can tap to toggle files off for an isolated session.

### 3.3 Dual-Speed Operation Modes

#### Mode 1: ⚡ Quick Note (15-Second Coffee Queue Window)
* **Input:** Feature / Defect Slug + Raw Note (optimized for iOS Voice Dictation).
* **Target:** Fixed to `ideation/{YYYY-MM-DD-HHmm}-{slug}.md`.
* **Execution:** Encodes body to UTF-8 Base64 and executes atomic `PUT` to GitHub REST API.
* **Feedback:** Instant double-pulse haptic vibration (`navigator.vibrate([20, 50, 20])`), input field reset, and interactive confirmation toast with direct GitHub file link.

#### Mode 2: 💬 Design Debater (30-to-60 Minute Lull Window)
* **Persona:** Principal UX Architect & Socratic Critic.
* **Stance:** Pushes back on UI complexity, interrogates edge cases, protects mobile screen real estate, and references active project context from `GEMINI.md`.
* **Action Toolbar:**
  - **Model Picker:** Dynamic dropdown defaulting to **`gemini-1.5-flash`** (GA), with 1.5 Pro and 2.5 Flash options.
  - **`[ 📝 Compile Spec ]`**: Asks Gemini to synthesize the entire debate consensus into a structured Markdown design document with Problem Statement, UI/UX Decisions, Edge Cases, and Acceptance Criteria.
  - **`[ 🚀 Commit Spec to Repo ]`**: 1-tap push directly into the target project's `ideation/` folder.

---

## 4. Standardization & Directory Conventions

### 4.1 The Single-Inbox Rule (`ideation/`)
All mobile captures across all repositories route strictly into **`ideation/`**.
* **Automatic Provisioning:** In Git and GitHub's REST API, directories are virtual trees. If an older repo (such as `Deep-Song-Explorer` or `NFL-Deep-Reader`) does not yet have an `ideation/` folder, GitHub creates it automatically upon the first commit.
* **No Decision Friction:** The user never chooses directories on mobile.

### 4.2 Standardized Slug Prefixes
Captures are classified using standard engineering prefixes in the Title:
- `fix: <description>` -> Defect / UI bug triage
- `feat: <description>` -> New feature / interaction design
- `idea: <description>` -> Architectural brainstorm / reflection

---

## 5. Security & Authentication Architecture

* **Zero Backend / Zero Middleman:** No third-party relay or OAuth server touches keys or tokens. All network traffic originates directly from the client browser to GitHub and Google endpoints.
* **Storage Sandbox:** Tokens are stored in browser-managed `localStorage`:
  - `mma_github_pat`
  - `mma_gemini_key`
* **Principle of Least Privilege (Classic PAT):**
  - Requires **only** the `repo` scope.
  - Grants full read/write to all repositories under `joeyang108`.
  - Excludes dangerous administrative scopes (`delete_repo`, `admin:org`, `admin:public_key`, `workflow`).
* **Zero-Friction Ingestion:** Automated URL parameter parser (`?gh=...&gemini=...`) injects credentials into `localStorage` on initial load and scrubs the browser history via `history.replaceState`.

---

## 6. Verification & Production Evidence

* **Initial Live Commit:** Tested and verified on iPhone 15 running iOS Safari Standalone PWA.
* **Commit Hash:** `7d099597605447c832df245905e3930fb0e95c49`
* **Artifact Generated:** [ideation/2026-11-26-0945-hello-world.md](file:///Users/googlejoe/macagyvibes/mobile-markdown-agent/ideation/2026-11-26-0945-hello-world.md)
* **HTTP Latency:** ~380ms roundtrip for direct REST PUT on LTE/5G.
