# 🗺️ AccessMap — Accessibility-Aware Navigation Infrastructure

For many people, one staircase or a missing curb ramp can turn a simple walk into a dead end. AccessMap turns sidewalk accessibility data (OpenSidewalks) into an **accessibility-first pedestrian network** that prioritizes *real-world usability* over “fastest.” It delivers **step-free routing**, **risk/constraint warnings** (slopes, curbs, gaps), and **practical route trade-offs** through a web map and APIs—so navigation works for wheelchairs, strollers, walkers, travelers, and anyone who wants low-stress routes.





## 🧩 Problem Statement

Most navigation products optimize for **speed and distance**, not **real-world walkability**. For millions of pedestrians, a “short route” can fail in the last 200 meters—because the path includes **stairs, missing curb ramps, broken sidewalks, unsafe crossings, or steep grades**.

For people using wheelchairs, walkers, strollers, carrying luggage, or managing pain/fatigue, these barriers create:

- **Route failures** (dead-ends, inaccessible entrances, forced backtracking)
- **Safety risk** (unmarked crossings, steep slopes, uneven surfaces)
- **Cognitive load + anxiety** (uncertainty: *“Will I get stuck?”*)
- **Reduced independence** (needing help, avoiding unfamiliar areas)

### Why existing systems fail
Accessibility constraints are **not consistently represented** in mainstream pedestrian graphs. Sidewalk data is often **incomplete, fragmented, and inconsistent across cities**, and routing engines rarely explain *why* a route is recommended or what tradeoffs were made.

### Success Criteria
A solution should:
- **Prioritize accessibility-first routing** (avoid stairs/unsafe crossings when possible; respect slope/curb constraints)
- **Explain decisions** with transparent *risk/effort tradeoffs* and confidence signals
- **Provide safe fallbacks** when data is missing (warnings + alternates, not silent failure)
- **Scale across cities** with a portable, reproducible infrastructure for ingesting and standardizing pedestrian data

### What AccessMap Delivers
- **Step-free routing** using accessibility-aware penalties (slope, missing sidewalks, crossings, stairs)
- **Warnings + alternatives** when confidence is low or risk is high
- **Web map + APIs** so cities/teams can deploy, iterate, and integrate accessible navigation quickly


> Designing navigation that doesn’t just find a route — it builds confidence that the route will actually work.



<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/90f774b0-66fc-4fae-aae6-8e52fed38d4f" />




## 💡 Solution — AccessMap Platform
*How AccessMap converts city pedestrian data into clear, step-free routes.*

AccessMap is an accessibility-first routing platform that turns raw pedestrian infrastructure data into an **explainable routing graph**—and serves **step-free routes** with **warnings + alternatives** when constraints or uncertainty appear.

### Data → Graph → Routes (explainable)

**1) Data (Ingest + Normalize)**
- OpenSidewalks sidewalk metadata (sidewalk segments, curb ramps, connectivity)
- Elevation/slope signals
- Crossings + risk signals (where available)

**2) Routing Graph (Accessibility-aware)**
- Standardizes heterogeneous city datasets into a walkable network
- Applies **accessibility penalties** (stairs, steep slopes, unsafe crossings, missing sidewalks)
- Generates **confidence + explainability** signals for “why this route”

**3) Routes (User-facing outputs)**
- **Step-free routing** (avoid stairs/unsafe edges when possible)
- **Route explanations** (risk/effort tradeoffs, confidence)
- **Warnings + alternatives** when constraints are detected or data is incomplete
- **Web map UI + APIs** so teams can deploy, integrate, and iterate quickly





<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/33ad9771-5f84-46bc-b694-52d88453c684" />






 ## 🧩 Key Features

### User-facing
- **Step-free routes** (accessibility-first defaults, constraint-aware)
- **Warnings + alternatives** when constraints are detected or confidence is low
- **Explainable routing** so users trust decisions (why + tradeoffs)

### Platform
- **Modular services** (frontend, routing, tiles, APIs)
- **Docker Compose orchestration** for reproducible deployments
- **Automated build & deploy** for dev → staging → production
- **Configurable city setup** by swapping datasets/configs
- **Optional privacy-preserving analytics** for monitoring and iteration




## 🏗️ System Architecture


**High-level flow:**
OpenStreetMap & City Data
↓
ETL & Standardization
↓
GeoJSON (OpenSidewalks Schema)
↓
Routing Graph + Vector Tiles
↓
Reverse Proxy
↓
Web Application & APIs




<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/81c6a876-f72f-4657-9691-d0282e773c53" />







 ## 🚀 Deployment Strategy
AccessMap is deployed as a **portable, reproducible city-scale platform** using **Docker Compose (v3.8+)**, designed to move safely from local development to production without “it works on my machine” failures.

### Goals
- **Repeatable deployments** across machines and cities
- **Fast iteration** (change data/config, redeploy quickly)
- **Production reliability** (stable routing + tiles + APIs)
- **Scalable onboarding** (swap datasets to support a new city)

### Environments
**Dev → Staging → Production**
- **Dev:** rapid local testing, hot reload, fast debugging
- **Staging:** production-like config, smoke tests, performance checks
- **Production:** hardened services, caching, monitoring, stable releases

### Containerized Services (Compose)
- **Frontend (React):** map UI + route exploration
- **Routing service:** accessibility-aware pathfinding + explanations
- **Tiles/Graph service:** serves vector tiles + routing graph artifacts
- **Reverse proxy (gateway):** routing, TLS termination, caching, rate limits
- *(Optional)* **Analytics:** privacy-preserving usage signals for iteration

### Data & Build Pipeline
1. **Ingest:** OpenStreetMap + city datasets + elevation
2. **ETL & Standardize:** convert to **OpenSidewalks schema** (GeoJSON)
3. **Build artifacts:** routing graph + vector tiles
4. **Deploy:** publish artifacts to services, restart only what changed

### Release & Safety
- **Versioned city bundles** (data + configs) for rollback
- **Health checks** on all services (compose-level readiness)
- **Zero-surprise upgrades:** pinned images + controlled updates
- **Rollback plan:** revert to previous city bundle + restart gateway/services

### Why this matters (UX impact)
Reliable deployment isn’t just engineering polish—it ensures users get:
- **Consistent step-free routing**
- **Predictable warnings + alternatives**
- **Stable performance** at city scale




<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/1988cb3d-3ee3-413c-b4c7-8eb99ceaea21" />






## ⚙️ Configuration
AccessMap is designed to be **city-portable**: you can onboard a new city by swapping datasets + a small set of configuration values—without rewriting the platform. Configuration controls **how accessibility is interpreted**, **how routes are scored**, and **how the system behaves when data is incomplete**.

### What you can configure (high-impact)
**Routing behavior**
- **Constraint mode:** step-free / avoid stairs / slope-sensitive
- **Penalty weights:** stairs, steep slope, unsafe crossings, missing sidewalks
- **Preference tuning:** prioritize safety vs. distance vs. effort

**Data quality + trust**
- **Confidence thresholds:** when to show a warning vs. failover route
- **Missing-data behavior:** conservative detours vs. “best available” route
- **Feature toggles:** enable/disable crossing risk, curb-ramp requirement, etc.

**City onboarding**
- **Dataset paths/URLs:** OpenStreetMap extract + city datasets + elevation tiles
- **ETL parameters:** schema mapping to OpenSidewalks, normalization rules
- **Region bounds:** city polygon/tiles coverage, clipping + caching settings

**Platform & API**
- **Reverse proxy rules:** routing, caching, rate limits, request timeouts
- **Service endpoints:** routing/tiles/frontend base URLs
- **Environment flags:** dev/staging/prod values, logging levels

### Recommended “city bundle” pattern
To keep deployments clean and rollback-friendly, store each city as a **versioned bundle**:

- `data/` (raw + processed inputs)
- `config/` (penalty weights, thresholds, toggles)
- `artifacts/` (routing graph + vector tiles)
- `metadata.json` (version, build time, sources)

This enables:
- **Fast city switching**
- **Reproducible builds**
- **Safe rollbacks** (revert to previous bundle)

### Why this matters (UX impact)
Configuration is not just technical setup—it directly affects user trust:
- **Fewer route failures**
- **More predictable warnings**
- **Consistent step-free experiences** across different cities and data quality levels


<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/0259db8e-808b-4e82-9fb3-cb847bbb7227" />






## 🛠️ Building Assets

Run the following commands to build all required assets:

bash
docker-compose run build_webapp
docker-compose run build_tiles
docker-compose run build_router

https://giant-pantydraco-31a.notion.site/Study-Planner-2cb2674354cb8059b86bfd089e2634f5?source=copy_link


## ✅ Outcomes & Learnings

### What worked
- Standardizing everything into an **OpenSidewalks-compatible schema** unlocked **consistent routing** across messy, heterogeneous city datasets.
- **Accessibility-aware costs** (stairs / slope / crossings / missing sidewalks) produced **safer default routes** instead of “shortest-only” decisions.
- Adding **explainability** (“why this route”) improved user trust by making tradeoffs visible (effort vs. distance vs. risk).

### Main challenge
- **Incomplete sidewalk + crossing coverage** in real-world data caused gaps, dead-ends, and edge-cases in routing.
- **Noisy / missing tags** (e.g., curb-ramp signals, entrance accessibility, temporary barriers) created uncertainty that typical navigation ignores.
- A single incorrect edge choice can lead to **unsafe detours** or **loss of independence** for mobility-impaired users.

### How we handled it
- Introduced **warnings + confidence cues** when data is incomplete or risk is high (no silent failures).
- Returned **fallback routes + alternatives** rather than forcing one “best” path.
- Used **conservative penalties** to avoid uncertain/unsafe edges by default while still allowing discovery when necessary.

### Next steps
- Improve **accessibility scoring** with context-aware weights (city/zone/time sensitivity).
- Add **entrance-level metadata** (accessible entrances, curb ramps, barriers) to reduce last-meter failures.
- Build **better slope modeling** (elevation smoothing + effort estimation) for more realistic accessibility routing.


