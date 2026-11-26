# Sprint 1 Design Brief: Mobile Markdown Agent (MMA)

## 1. Objectives & Boundaries
* **Purpose:** Mobile-first, distraction-free capture & design debate vessel for iPhone during "Lull Time" (car waiting, kids soccer games, coffee queues) to replace passive scrolling with earned dopamine.
* **Strict Boundary:** "Capture & Reason Only" — NO code compilation, NO mobile IDE, NO multi-file project editing. Output is strictly high-craft Markdown specs committed to GitHub.
* **Target Repositories:** `joeyang108` ecosystem (`Deep-Song-Explorer`, `NFL-Deep-Reader`, `Health-App-42`, `vibe-coding-partner`, `mobile-markdown-agent`).

---

## 2. Core Functional Specifications

### A. Dual Modes
1. **⚡ Quick Note Mode:**
   - Rapid capture for 15-second windows.
   - Title input + Markdown body textarea.
   - Instant 1-tap push to target repo: `ideation/{YYYY-MM-DD-HHmm}-{slug}.md`.
2. **💬 Design Debater Mode:**
   - Conversational design sparring for 20-40 minute lulls.
   - Powered by Gemini 2.0 Flash directly from the browser.
   - System prompt acts as a Socratic, subtractive design critic (poking edge cases, UI hierarchy, error handling).
   - Dynamic context injection: Loads selected project `.md` files.
   - **`[ 📝 Compile Spec ]`** action converts the entire debate into an airtight design spec.
   - **`[ 🚀 Commit to GitHub ]`** pushes the compiled spec directly to `ideation/{YYYY-MM-DD-HHmm}-{slug}.md`.

### B. Context Ingestion (Strategy A + B)
* On repository switch, MMA auto-probes:
  - `README.md`
  - `GEMINI.md`
  - Active files in `designs/` or `backlog/`
* Discovered files render as toggleable pills:
  `[✓ README.md] [✓ GEMINI.md] [✓ backlog.md]`
* Pre-selected by default, un-selectable with a single tap.

### C. Authentication & Setup
* Stored purely client-side in `localStorage`:
  - `GITHUB_PAT`: Fine-grained or classic token with repo contents read/write.
  - `GEMINI_API_KEY`: Google AI Studio API key for Gemini 2.0 Flash.
  - `ACTIVE_REPO`: Last selected repository.
* Setup Modal: Accessible via gear icon on header, with quick paste fields.

---

## 3. Technical Architecture (Via Negativa)
* Single static bundle (`index.html`) containing vanilla HTML, CSS, and JS.
* Zero build steps, zero npm dependencies, zero server backend.
* Hosted via GitHub Pages with full HTTPS.
* PWA manifest + iOS Apple Mobile Web App tags for full-screen native feel on iPhone.
