# Design Spec: Root `DESIGN.md` Standard & MMA Context Ingestion

- **Target Repo:** `joeyang108/mobile-markdown-agent`
- **Problem Statement:** 
  Switching between projects in MMA during mobile capture sessions leads to a context gap: the user and the Debater agent lack instant situational awareness of the project's living architecture and recent design decisions. Adding a full file explorer or markdown viewer to MMA violates the "Via Negativa / Capture Only" boundary, bloating the 15-second capture workflow.

---

### Decided Architecture & Standard

#### 1. Universal Root Markdown Pattern
Every managed repo will adopt a standard 3-pillar root documentation model:
* **`README.md`**: Project overview, setup, and execution commands.
* **`GEMINI.md` / `AGENTS.md`**: Agent operational constraints, principles, and guidelines.
* **`DESIGN.md`**: The living architecture, data models, UX hierarchy, and active roadmap.
* **`ideation/`**: Append-only inbox for mobile-captured delta specs (staging area for desktop execution).

#### 2. The Asynchronous Desktop ⇄ Mobile Loop
* **On Mobile (MMA):** The Debater consumes `README.md`, `GEMINI.md`, and `DESIGN.md` as grounding context, spars on an atomic issue, and outputs a delta spec to `ideation/YYYY-MM-DD-feature.md`.
* **On Desktop (AGY):** The IDE agent executes the delta spec and reconciles changes into `DESIGN.md`.

---

### Decided UI/UX Solution (MMA)

1. **Zero UI Bloat / Background Ingestion:**
   * No file browser, navigation tree, or dedicated reading view is added.
   * When a repository is selected in Design Debater mode, MMA fetches `DESIGN.md` along with `README.md` and `GEMINI.md`.

2. **Context Indicator Pill:**
   * Add a third status badge to the existing Context header in the Debater chat screen:
     `[✓ README] [✓ GEMINI] [✓ DESIGN]`
   * If `DESIGN.md` is absent in the target repo, the pill gracefully shows `[- DESIGN]` or is omitted.

3. **Debater Grounding:**
   * Injected into the Gemini Debater system instructions:
     ```text
     [PROJECT CONTEXT - DESIGN.MD]
     {content_of_design_md}
     ```
   * Debater uses this to maintain strict continuity with established architecture and decisions.

---

### Edge Cases & Error States

- **Missing `DESIGN.md` (404):** Repos without `DESIGN.md` must not break context loading; the fetch returns `null` and the app continues gracefully with existing files.
- **Large Document Size / Token Budgeting:** If `DESIGN.md` exceeds 30KB (~8k tokens), truncate or slice to the top sections to prevent network latency and payload bloat on mobile networks.
- **Network / GitHub API Failure:** Non-blocking error handling; context indicator displays error state without halting conversation