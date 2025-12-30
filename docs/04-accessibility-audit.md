# Accessibility Audit — AccessMap (1-page)

## Goal
Ensure step-free navigation is usable, understandable, and safe for users with mobility limitations.

## Scope
- Search → Route compare → Filters → Guidance → Report/Verify
- Map + list + turn-by-turn surfaces

---

## A) Core UX Accessibility Checks
### 1) Clarity + decision safety
- Step-free status is visible on route cards (not hidden in details).
- Dependency warnings are explicit (e.g., **“Elevator required”**).
- Uncertainty is communicated (“Limited data”) + fallback route offered.
- Risk segments are previewed before starting navigation.

### 2) Error prevention + recovery
- No routes match filters → show nearest viable alternatives.
- Mid-route disruption (elevator out / blocked ramp) → reroute CTA + explanation.
- Offline/low network → cached route + minimal guidance.

### 3) Cognitive load control
- Trust cues are compact (1–2 chips) + expandable details.
- Consistent naming across list/map/guidance.
- “What to expect” uses plain language, no jargon.

---

## B) Visual & Interaction Accessibility (UI)
### 1) Contrast + readability
- Text meets WCAG contrast targets (aim ≥ 4.5:1 for body text).
- Key warnings use text + icon (not color-only).
- Minimum tap targets ~44px and clear spacing.

### 2) Motion + feedback
- Avoid excessive animations; provide subtle feedback for state changes.
- Loading states show progress and don’t block back navigation.

### 3) Keyboard / focus (for web prototypes)
- Visible focus ring on interactive elements.
- Logical tab order across route cards and filters.

---

## C) Content Design Standards (Microsoft Content-style)
- Use outcome labels: “Avoid stairs”, “Elevator required”
- Avoid vague terms: “Accessible-ish” ❌
- Pair warning with action: “Elevator required → View fallback route”
- Keep chips short (≤ 2–3 words)

---

## D) Data Reliability & Trust Layer
- Confidence indicator reflects data completeness.
- “Verified recently” shown when applicable.
- Conflicting reports → “Mixed signals” + recommend verified option.

---

## Audit Result Summary (current)
✅ Decision-first signals + dependency warnings  
✅ Edge cases covered (missing data, elevator outage, steep slope)  
✅ Trust layer concept (confidence + verification) documented  
Next: add usability check notes + demo GIF/screens for visual proof
