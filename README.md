# Mobile Markdown Agent

A lightweight, distraction-free mobile web application (PWA) designed for iPhone to capture structured app designs, sprint ideation, and notes directly into GitHub Markdown files across the Vibe Coding ecosystem.

---

## 🎯 Purpose & Dopamine Defense Anchor
* **Earned Dopamine Substitution:** Built as an intentional alternative to passive phone habits (algorithmic feeds, social scrolling). When "bad dop" urges arise away from the desk, this tool provides an immediate outlet for structured creative thought.
* **Strict "Capture Only" Boundary:** This is **not** an IDE or code editor. Code creation and builds remain strictly anchored to the desktop laptop environment.
* **Via Negativa Design:** Minimal friction, instant load, distraction-free typing, and direct GitHub API commits to `notes/` and `ideation/` directories.

---

## 🧱 Architecture (Candidate)
* **Client:** Lightweight, offline-capable Progressive Web App (PWA) installable on iPhone Home Screen.
* **Data Layer:** Direct GitHub REST/GraphQL API integration using a fine-grained Personal Access Token (PAT).
* **Target Destinations:** Commits Markdown drafts directly into designated repositories (e.g. `vibe-coding-partner/notes/`, `vibe-coding-partner/ideation/`, or spoke project directories).

---

## 📁 Project Structure
```text
mobile-markdown-agent/
├── designs/      # Scoped 45-min sprint briefs and acceptance criteria
├── ideation/     # Vision docs, architecture trade-offs, and backlog
├── notes/        # Retrospectives, lessons learned, and dopamine defense logs
└── src/          # Application source code (Sprint 1+)
```
