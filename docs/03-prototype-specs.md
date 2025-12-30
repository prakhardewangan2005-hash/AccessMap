# Prototype Specs — States, Edge Cases, Handoff Notes

## Core flow
**Search → Route Compare → Apply filters → Start guidance → Report/verify**

## Screen specs (state-ready)

### 1) Search
**States**
- Default + recent places
- No results
- Location permission denied (recovery CTA)
- Offline (limited suggestions)

**Notes**
- Keep first action fast: type → pick → route options.

---

### 2) Route Options (Compare)
**Each route card includes**
- ETA + distance
- Step-free badge
- Trust cue (confidence chip)
- Dependency warnings (e.g., Elevator required)
- “What to expect” (expandable)

**States**
- Normal: 2–3 route cards
- Low data: “Limited accessibility data” + safe fallback suggestion
- Conflicting reports: “Mixed signals” chip + recommend verified route

---

### 3) Filters (Step-free + constraints)
**Filters**
- Step-free only
- Avoid elevator dependency
- Avoid steep slopes (threshold-based)
- Prefer verified signals (trust-first)
- Surface preference (if available)

**States**
- Filters applied (route list updates)
- No routes match → show nearest viable alternatives

---

### 4) Route Guidance
**Elements**
- Turn-by-turn
- Next risk chip (e.g., steep segment ahead)
- Dependency reminders (elevator coming up)

**States**
- Mid-route disruption: elevator outage/blocked ramp → reroute CTA
- Low network/offline: cached route + minimal guidance
- Uncertain segment: show caution + optional alternate

---

### 5) Report / Verify
**Report types**
- Elevator out
- New stairs / blocked ramp
- Missing curb cut
- Surface issue

**States**
- Quick report success
- Add detail (optional)
- Verification confirmation

---

## Edge cases (must handle)
- Missing data → show uncertainty + alternatives
- Elevator dependency → warn early + fallback route
- Steep slope segment → flag + alternate option
- Conflicting reports → prioritize verified + show “mixed signals”

## Tradeoffs captured
- **Accuracy vs detours vs interaction cost**
- **Trust cues vs clutter** (kept to 1–2 compact chips per card)
- **Speed vs completeness** (fast decision path prioritized)

## Implementation notes (handoff-friendly)
- Signals driven by taxonomy keys in `data/taginfo.json`
- Route card warnings triggered by severity + confidence thresholds
- Trust cues should be cacheable and updateable (verification recency)
