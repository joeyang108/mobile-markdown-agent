# Design Spec: Fix WebKit Postal Address Autofill Hijack on Debater Input

- **Target Repo:** joeyang108/mobile-markdown-agent
- **Problem Statement:** In iOS Safari, the Debater input field triggers the native contact card autofill (specifically prompting for physical/postal "State" address) instead of offering QuickType predictive text. This hijacks the keyboard accessory view, destroys typing ergonomics, and prevents smooth mobile conversational entry.

---

### Decided UI/UX Solution
Ensure the Debater text input element explicitly suppresses WebKit's form autofill heuristics while keeping standard mobile writing aids (predictive QuickType, auto-capitalization, and spellcheck) active.

1. **Purge Heuristic Triggers:**
   - Audit the Debater input element's `id`, `name`, `placeholder`, and surrounding labels/attributes.
   - Remove any substrings matching address tokens (e.g., `state`, `address`, `zip`, `street`, `province`, `country`).
   - If placeholder reads something like *"State your argument..."*, change it to a non-trigger alternative like *"Enter prompt..."* or *"Spar your idea..."*.
2. **Explicit Attribute Hardening:**
   Apply explicit HTML attributes to the Debater input field (`<textarea>` or `<input>`):
   ```html
   <textarea
     id="debater-input"
     name="debater-prompt-input"
     placeholder="Spar with the Debater..."
     autocomplete="off"
     autocorrect="on"
     autocapitalize="sentences"
     spellcheck="true"
     enterkeyhint="send">
   </textarea>
   ```

---

### Edge Cases & Error States
- **Safari Autofill Persistence:** Standard `autocomplete="off"` is occasionally ignored by aggressive WebKit heuristics on forms containing generic `name` or `id` attributes. If Safari continues to guess postal fields, set `autocomplete="one-time-code"` or a non-standard value like `autocomplete="do-not-autofill"`.
- **Keyboard Accessory Clashing:** The Debater input should not lose iOS QuickType sentence prediction. Attributes must keep `autocorrect="on"` and `spellcheck="true"`.
- **Quick Notes Consistency:** Quick Notes tab does not exhibit this behavior because it acts as a long-form document editor (`<textarea>`). Ensure the Debater input mimics the non-form behavior of the Quick Notes element.

---

### Acceptance Criteria
- [ ] Inspect the Debater input element in the mobile client code (`index.html` / app bundle).
- [ ] Ensure `name` and `id` contain no address-related tokens (e.g., rename any instances of `state`, `prompt-state`, etc.).
- [ ] Set `autocomplete="off"`, `autocorrect="on"`, `autocapitalize="sentences"`, and `spellcheck="true"` directly on the Debater input element.
- [ ] Verify that opening the Debater tab in iOS Safari and tapping the input field activates the predictive text bar without displaying personal contact card / postal address suggestions.