# AccessMap — Step-Free Navigation (UX + Product Design)

Accessibility-first routing concept focused on **clarity, trust cues, and real-world constraints** (ramps/elevators/curb cuts/steepness).  
Designed to reduce uncertainty for wheelchair users, seniors, travelers with luggage, and anyone needing barrier-free routes.

**Role:** UX / Product Designer (End-to-End)  
**Artifacts:** 12+ screens · 3 iterations · 6 usability checks · 1 accessibility audit · taxonomy + component states  
**Tools:** Figma, FigJam, Notion · (optional) Fusion 360 for physical-context reasoning

---

## Quick Links
**Case Study (Notion):** 
https://giant-pantydraco-31a.notion.site/Access-Map-Repo-2d52674354cb808b921deee1c05c7eea?source=copy_link

**Json code:**  [`taginfo.json`](./taginfo.json)

**Figma Prototype & High-Fidelity UI Link:**
   https://www.figma.com/design/5lvOC2vJ5BTFLxtgBJaiVM/Access-Map?node-id=0-1&t=jZ7IHGOJJarDRuVp-1
   
**3D Tools Model (Fusion 360):**
 https://github.com/user-attachments/assets/5b2a9f57-8495-41ee-a8e7-a335377834c2


 ## Proof Docs
- Case Study (Repo): [docs/00-case-study.md](docs/00-case-study.md)
- JD Alignment: [docs/07-jd-alignment.md](docs/07-jd-alignment.md)


---

## Problem
Mainstream maps often fail to reliably express accessibility. Users face:
- **Uncertainty** (stairs/elevator dependency/steep segments)
- **Inconsistent signals** (missing data, outdated tags)
- **No decision support** (confidence, fallback routes, “what could go wrong”)

**Goal:** Make accessibility **visible, verifiable, and decision-friendly**.

---

## What I Designed
### 1) Step-Free Route Planning
- Step-free filters and route options built for **fast decision clarity**
- Trust cues: **confidence indicators + dependency warnings**
- Fallback routes when signals are weak or a key accessibility feature fails (e.g., elevator outage)

### 2) Accessibility Signal System (Taxonomy)
- Structured labels for ramps/elevators/curb cuts/steepness/surface, etc.
- Designed to scale from **prototype → future data ingestion/community verification**

### 3) State-Ready UI + Design System Thinking
- Interaction states across search → route compare → guidance
- Reusable patterns to support consistency and handoff readiness

---

## Highlights (Proof)
- Tradeoffs captured: **accuracy vs detours vs interaction cost**
- Edge cases covered: **missing data, elevator outages, steep slopes**
- Outputs: **flows/IA, interaction states, hi-fi prototype, walkthrough-ready narrative artifact**
- Customer outcomes (VOC): **confidence to start a route + less mid-route surprises**

---

## Repo Contents
- `README.md` — overview + links  
- `taginfo.json` — accessibility signal taxonomy used in the concept  
- `orchestration-diagram.(png|svg)` — routing + trust cue orchestration diagram  
- `LICENSE`, `.gitignore`

> Next planned repo upgrade (for “extreme shortlisting”):  
> `/docs` case study slices (research → IA/taxonomy → prototype specs → accessibility audit → impact metrics → JD alignment)

---

## JD Alignment (Weighted blend across 6 roles)
This project intentionally demonstrates:
- **Amazon Music UX:** iteration, prototyping, design systems, cross-functional collaboration
- **Microsoft Design Intern (0–1 lab):** experimentation mindset + prototype storytelling
- **Microsoft Product Design:** end-to-end UX, accessibility, balancing tradeoffs
- **Microsoft Content Design:** taxonomy, naming, information architecture, messaging hierarchy
- **Google Product Design Engineer signals:** real-world constraints, structured systems thinking, prototype-to-scale mindset

---

## License
MIT

