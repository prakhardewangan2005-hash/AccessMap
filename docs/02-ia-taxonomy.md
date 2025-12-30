# IA + Taxonomy — AccessMap

## Why IA matters here
Accessible routing fails when labels are inconsistent, buried, or unverifiable. The product must surface **route viability signals** fast, clearly, and with trust cues.

## Information Architecture (Top-level)
1) **Search**
2) **Route Options (Compare)**
3) **Filters (Step-free + constraints)**
4) **Route Guidance**
5) **Trust Layer (Confidence + dependencies + verification)**
6) **Report / Verify (Community loop)**

## Primary user jobs
- Decide: “Which route is actually step-free and reliable?”
- Understand: “What’s the risk (stairs/elevator/steepness) before I start?”
- Recover: “If an elevator is out / path blocked, what’s my fallback?”
- Improve the system: “Report/verify to help future users.”

## Taxonomy principles
- **Decision-first:** prioritize the few signals that change viability.
- **Consistency:** same label across list, map, and guidance.
- **Explainability:** every warning includes a plain-language reason.
- **Scalable:** supports future ingestion + verification.

## Signal hierarchy (what gets shown first)
### Level 1 — Hard blockers (show always)
- **Stairs present**
- **No curb cut**
- **Narrow passage**
- **Elevator required** (dependency)

### Level 2 — Route risks (show when relevant)
- **Steep slope**
- **Rough surface**
- **Construction / temporary closure** (if known)
- **Long detour tradeoff** (time/cost)

### Level 3 — Trust cues (show as compact chips)
- **Verified recently**
- **Confidence score** (data completeness)
- **Conflicting reports** (mixed signals)

## Content design rules (naming + microcopy)
- Use **outcome language**: “Elevator required”, “Avoid stairs”
- Avoid vague labels: “Accessible-ish” ❌
- Pair warning with action: “Elevator required → See fallback route”
- Keep chips short (≤ 2–3 words), details in expandable “What to expect”.

## Where taxonomy lives in this repo
- Source of truth: `data/taginfo.json`
- Drives: **filters**, **warnings**, **map pins**, **route notes**, and **edge-case states**.

## Example: decision flow
Search → Compare routes → See “Elevator required” + low confidence → Switch to fallback → Start guidance with higher confidence.
