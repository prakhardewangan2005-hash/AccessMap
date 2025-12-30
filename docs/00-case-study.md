# AccessMap — Case Study (1-page)

## Overview
AccessMap is an accessibility-first routing concept that helps users choose **step-free routes** with confidence by making accessibility signals **visible, reliable, and decision-friendly**.

**Audience:** wheelchair users, seniors, people with temporary injuries, travelers with luggage  
**Core promise:** fewer mid-route surprises + clearer route confidence  
**Outputs:** user flows/IA, accessibility taxonomy, hi-fi prototype, state specs, orchestration diagram

---

## Problem
Mainstream maps often do not surface accessibility reliably. Users face:
- unexpected stairs / elevator dependency
- incomplete or outdated accessibility information
- no “trust layer” to assess reliability before starting a route

---

## Goals
1) Make accessibility signals **easy to understand** (clear labels + hierarchy)  
2) Add **trust cues** (confidence + dependency warnings)  
3) Handle real-world failures (missing data, elevator outage, steep slope)  
4) Keep the experience fast: **search → compare → go**

---

## Approach
### 1) Research → Insights
- Identified repeated failure points: elevator dependency, missing curb cuts, steep segments, broken elevators
- Prioritized signals that affect “route viability” most

### 2) Information Architecture + Taxonomy
- Built a scalable taxonomy for accessibility tags (used in `taginfo.json`)
- Created consistent names and categories to reduce cognitive load

### 3) UX + Visual Design
- Designed route compare with **confidence indicators**
- Added “what to expect” notes and fallback options
- Designed state-ready UI for key screens and edge cases

---

## Edge Cases (Handled)
- Missing/low-confidence data → show uncertainty + alternatives
- Elevator outage dependency → warn early + reroute option
- Steep slope segments → flag + accessible alternative

---

## What I’d Measure (Impact)
- Time-to-decision before starting a route
- Reduction in route abandonment due to surprises
- Comprehension score of accessibility signals (label clarity)

---

## Links
- Case Study (Notion): https://giant-pantydraco-31a.notion.site/Access-Map-Repo-2d52674354cb808b921deee1c05c7eea?source=copy_link  
- Figma Prototype: https://www.figma.com/design/5lvOC2vJ5BTFLxtgBJaiVM/Access-Map?node-id=0-1&t=jZ7IHGOJJarDRuVp-1
