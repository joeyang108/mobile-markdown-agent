# Ideation: Mobile Markdown Agent Vision & Architecture

## 1. Problem Statement & Motivation
* **Context:** Away from the desk, sudden creative insights, sprint improvements, and app iterations occur. 
* **Current State:** Quick thoughts are jotted down into Google Keep. While functional, Keep notes are disconnected from the GitHub repository workflow, lacking structure, markdown hierarchy, and seamless integration into future desktop coding sprints.
* **Dopamine Defense Vector:** Idle phone time is the highest-risk trigger for "bad dopamine" (scrolling feeds, passive media). Replacing that reflex with an instant-access, high-craft capture vessel channels focus directly into creative, earned dopamine.

---

## 2. Core Functional Requirements
1. **Repository Selector:** Choose target repository (e.g. `vibe-coding-partner`, `Deep-Song-Explorer`, `NFL-Deep-Reader`, `Health-App-42`).
2. **Directory Routing:** Automatically route entries into:
   - `ideation/` (App concepts, architectural ideas)
   - `notes/` (Daily reflections, dopamine defense check-ins)
   - `designs/` (Sprint drafts, feature requirements)
3. **Structured Templates:** Pre-populated templates for:
   - *Quick Thought / Idea*
   - *Sprint Scoping Spec*
   - *Dopamine / Health Check-in*
4. **Seamless GitHub Sync:** Push directly via GitHub REST API with an automated commit message (e.g. `docs(mobile): capture new idea [timestamp]`).

---

## 3. Architectural Paths & Trade-Offs

### Path A: Zero-Backend Static PWA (Recommended)
* **Stack:** Vanilla HTML/CSS/JS or lightweight Preact/Tailwind, hosted on GitHub Pages or Cloudflare Pages.
* **Auth:** Fine-grained GitHub Personal Access Token (PAT) stored locally in browser `localStorage`.
* **Pros:** Zero server maintenance, zero cost, instant load time, fully responsive on iOS Safari PWA.
* **Cons:** User needs to paste a GitHub PAT once during initial setup.

### Path B: Serverless Relay (Next.js / Cloudflare Worker)
* **Stack:** Cloudflare Worker / Next.js with GitHub OAuth App.
* **Pros:** Cleaner login without manual PAT generation.
* **Cons:** Additional infrastructure and secret management, violates Via Negativa for Sprint 1.

---

## 4. Sprint 1 Candidate Scope (45-Minute Window)
* Build single-page standalone mobile UI with iOS-friendly styling.
* Local storage configuration for GitHub PAT + default repo.
* Simple form: Title, Category (Ideation/Notes/Designs), Body (Markdown).
* Single-button commit directly to GitHub via REST API.
