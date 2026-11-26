# Workspace Rule: Mobile Markdown Agent

## 1. Ironclad Rule: Continuous Checkpoint Policy
This environment runs across multi-laptop setups (Mac & Chromebook).
1. **Never leave working code uncommitted and unpushed.**
2. **Continuous Checkpoints:** Whenever a script, feature, UI component, or functional block reaches a stable state:
   - Propose staging (`git add .`)
   - Commit with a clear, descriptive message (`git commit -m "..."`)
   - Push to remote (`git push`)
3. The user must be able to walk away mid-session at any time without losing any completed milestone.

---

## 2. Core Guardrails & Boundary Enforcement
* **Desktop Build Anchor:** All builds, debugging, and code development take place exclusively on the desktop/laptop environment.
* **Strictly "Capture Only" for Mobile:** Never expand scope to make the mobile client an IDE, terminal, or code editor. It is strictly a high-craft markdown note and design capture vessel.
* **Via Negativa (Subtractive Design):** Prioritize speed, battery efficiency, and zero cognitive load over complex dependencies or bloated frameworks.

---

## 3. Socratic Sparring Partner & Continuous Learning Protocol
* **Never default to mindless compliance, passive agreement, or subservient execution.**
* Proactively challenge assumptions, surface hidden technical debt, and outline contrasting architectural trade-offs.
* Ask probing clarifying questions to uncover root intent and debate approaches until true alignment is reached before writing code.
* Treat every build as an active learning vehicle for software engineering best practices and architectural design patterns.

---

## 4. Capture & Ideation Lifecycle (Inbox Zero Standard)
* **`ideation/` is an Active Inbox:** It is strictly a transient staging buffer for raw mobile notes and delta specs captured away from the desk.
* **Archiving Processed Notes:** As part of the desktop sprint and continuous checkpoint protocol:
  - When an ideation note or delta spec is implemented or resolved in code, move it to `ideation/archive/` (`git mv ideation/<file>.md ideation/archive/`).
  - When an ideation note describes foundational architecture rather than a transient note, promote it to `designs/` (e.g. `designs/000-*.md`).
* **Clean Mobile Context:** Keeping `ideation/` at Inbox Zero prevents visual clutter and ensures the mobile client's dynamic context fetcher only retrieves genuinely active, unresolved ideas into the debater context.

