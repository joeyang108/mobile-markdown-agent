# Mobile Markdown Agent (MMA)

A lightweight, distraction-free Progressive Web App (PWA) designed for iPhone and macOS to capture structured design specs, sprint ideation, and bug fixes directly into GitHub Markdown files across the Vibe Coding ecosystem.

🔗 **Live App:** [https://joeyang108.github.io/mobile-markdown-agent/](https://joeyang108.github.io/mobile-markdown-agent/)

---

## 🎯 Purpose & Dopamine Defense Anchor
* **Earned Dopamine Substitution:** Built as an intentional, high-craft alternative to passive phone habits (algorithmic feeds, social media scrolling). When "bad dop" urges arise away from the desk (waiting in the car, transit queues, soccer games), MMA provides an immediate outlet for structured creative thought.
* **Strict "Capture Only" Boundary:** This is **not** an IDE, code editor, or compiler. Code creation, debugging, and builds remain strictly anchored to the desktop laptop environment (Mac/Chromebook AGY).
* **Via Negativa Design:** Zero build steps, zero server maintenance, zero npm dependencies. A pure browser-native app that communicates directly with GitHub and Google Gemini REST APIs.

---

## ⚡ Core Capabilities

### 1. ⚡ Quick Note Mode
* Rapid capture for 15-second windows.
* Dictation-friendly input with automatic title slugification.
* Instant 1-tap atomic push to `ideation/{YYYY-MM-DD-HHmm}-{slug}.md`.

### 2. 💬 Design Debater Mode (Gemini 2.0 / 1.5 Flash)
* Socratic design sparring for 30–60 minute lulls (parked in the car, sidelines).
* Interrogates UI complexity, tests failure states, and respects mobile screen constraints.
* **Dynamic Context Pills (Strategy A + B):** Automatically fetches and injects `README.md`, `GEMINI.md`, and backlog context from the selected repository.
* **`[ 📝 Compile Spec ]`**: Synthesizes the debate consensus into an airtight Markdown spec.
* **`[ 🚀 Commit Spec to Repo ]`**: Directly pushes the compiled spec into the project's `ideation/` folder.

### 3. Unified Ingestion Standard (`ideation/`)
* Automatically provisions the `ideation/` folder on any repository that doesn't have it yet.
* Uses standard title prefixes:
  - `fix: <description>` (Bug triage & defect capture)
  - `feat: <description>` (New feature design spec)
  - `idea: <description>` (Architectural thought)

---

## 📱 Installation

### On iPhone (Safari PWA)
1. Open [https://joeyang108.github.io/mobile-markdown-agent/](https://joeyang108.github.io/mobile-markdown-agent/) in Safari.
2. Tap the **Share** button (box with up arrow).
3. Tap **Add to Home Screen**.
4. Launch from your Home Screen in full-screen distraction-free mode.

### On macOS (Dock Web App)
1. Open the URL in Safari on your Mac.
2. Click **File > Add to Dock...**.
3. It opens in its own clean window directly from your Dock.

---

## 🔑 Authentication & Setup

MMA stores all credentials strictly in your device's private browser `localStorage`:
1. Tap the **⚙️ (Settings)** icon in the top right.
2. Enter your **GitHub Personal Access Token (Classic PAT)** with the `repo` scope.
3. Enter your **Google Gemini API Key** from [Google AI Studio](https://aistudio.google.com/app/apikey).
4. Tap **Save Settings**.

---

## 📁 Repository Structure
```text
mobile-markdown-agent/
├── designs/
│   ├── 000-mobile-markdown-agent-vision.md     # Foundational Vision Doc
│   ├── 001-sprint-1-design-debater.md          # Sprint 1 Brief
│   └── 002-v1-architecture-and-system-design.md # Full System Architecture & Spec
├── ideation/
│   ├── archive/                                # Resolved/implemented captures
│   └── *.md                                    # Active inbound captures from mobile (Inbox Zero)
├── notes/
│   └── 2026-11-25-sprint-1-checkpoint.md       # Session handovers & logs
├── index.html                                  # Standalone PWA frontend
├── manifest.json                               # Web App Manifest
└── sw.js                                       # Service Worker cache
```
