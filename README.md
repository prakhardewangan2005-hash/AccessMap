# 🗺️ AccessMap — Accessibility-Aware Navigation Infrastructure

A “shortest” route isn’t helpful if it ends at a staircase. **AccessMap** turns sidewalk accessibility data (OpenSidewalks + OpenStreetMap + elevation) into an **accessibility-first pedestrian network** that prioritizes *real-world usability* over speed. It serves **step-free routes**, **constraint/risk warnings** (slopes, curbs, gaps), and **clear trade-offs** via a web map + APIs—so navigation works for wheelchairs, strollers, walkers, travelers with luggage, and anyone who wants low-stress routes.

- ✅ Step-free routing (accessibility-first defaults)  
- ⚠️ Risk + constraint warnings when confidence drops  
- 🔎 Explainable decisions (why this route + trade-offs)  
- 🧩 City-portable infrastructure (swap datasets/configs, redeploy fast)

 
**    **
- File: [`taginfo.json`](./taginfo.json)
- Prototype & High-Fidelity UI Link:
   https://www.figma.com/design/5lvOC2vJ5BTFLxtgBJaiVM/Access-Map?node-id=0-1&t=jZ7IHGOJJarDRuVp-1
- FUSION-360 (3D Model) Link :
   <div style="width:100%; background:#0b0b0b; padding:16px; border-radius:16px;">
  <img
    src="PASTE_IMAGE_URL_HERE"
    alt="3D Model Preview"
    style="width:100%; height:auto; display:block; border-radius:12px;"
  />
</div>



   

  





## 🧩 Problem Statement

Most navigation products optimize for **time and distance**, not **walkability under constraints**. In practice, that means a route can “work” on a map—and still fail in the last 200 meters because of:

- **Stairs** or missing curb ramps  
- **Broken/missing sidewalks**  
- **Unsafe crossings** or incomplete connectivity  
- **Steep grades** that exceed someone’s comfort/safety threshold  

For people using wheelchairs, walkers, strollers, carrying luggage, or managing pain/fatigue, these barriers create:

- **Route failures** (dead-ends, inaccessible entrances, forced backtracking)  
- **Safety risk** (steep slopes, unmarked crossings, uneven surfaces)  
- **Cognitive load + anxiety** (*“Will I get stuck?”*)  
- **Reduced independence** (needing help or avoiding unfamiliar areas)

### Why existing systems fail
Accessibility constraints are **not consistently represented** in mainstream pedestrian graphs. Real sidewalk data is often **incomplete, fragmented, and inconsistent across cities**, and routing engines rarely explain **why** a route is recommended—or what trade-offs were made.

### Success criteria
A strong accessibility routing system must:
- **Route for accessibility first** (avoid stairs/unsafe edges when possible; respect slope/curb constraints)
- **Make decisions legible** (show *why* + reveal risk/effort trade-offs with confidence signals)
- **Fail safely** (warnings + alternatives when data is missing—not silent failure)
- **Scale to new cities** (portable, reproducible ingestion + standardization + deployment)

### What AccessMap delivers
- **Step-free routing** using accessibility-aware penalties (slope, missing sidewalks, crossings, stairs)
- **Warnings + alternatives** when confidence is low or risk is high
- **Web map + APIs** so teams can deploy and integrate accessible navigation faster

> Navigation shouldn’t just find a path—it should build confidence that the path will actually work.



<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/90f774b0-66fc-4fae-aae6-8e52fed38d4f" />





## 💡 Solution — AccessMap Platform
*How AccessMap turns city pedestrian data into clear, step-free routes.*

AccessMap is an **accessibility-first routing platform** that transforms raw pedestrian infrastructure data into an **explainable routing graph**, then serves routes with **constraints, warnings, and practical trade-offs**.

### Data → Graph → Routes (explainable)

**1) Data (ingest + normalize)**
- OpenSidewalks sidewalk metadata (sidewalk segments, curb ramps, connectivity)
- Elevation / slope signals
- Crossings + risk signals (where available)

**2) Routing graph (accessibility-aware)**
- Standardizes heterogeneous datasets into one walkable network
- Applies **penalties** for stairs, steep slopes, unsafe crossings, missing sidewalks
- Produces **confidence + explainability** signals (why this route, where risk is)

**3) Routes (user-facing outputs)**
- **Step-free routing** (avoid stairs/unsafe edges when possible)
- **Route explanations** (risk/effort trade-offs + confidence)
- **Warnings + alternatives** when constraints are detected or data is incomplete
- **Web map UI + APIs** for integration and iteration




<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/33ad9771-5f84-46bc-b694-52d88453c684" />





## 🧩 Key Features

### User-facing
- **Step-free routes** with accessibility-first defaults
- **Warnings + alternatives** when constraints appear or confidence drops
- **Explainable routing** so users understand “why this route” (and what’s risky)

### Platform
- **Modular services** (frontend, routing, tiles, APIs)
- **Docker Compose orchestration** for reproducible deployments
- **Dev → staging → production** workflow support
- **Configurable per city** by swapping datasets + configs
   




## 🏗️ System Architecture


**High-level flow**
OpenStreetMap & City Data  
→ ETL & Standardization  
→ GeoJSON (OpenSidewalks Schema)  
→ Routing Graph + Vector Tiles  
→ Reverse Proxy  
→ Web Application & APIs  

**Why this architecture**
- Keeps the platform **portable** (swap city datasets)
- Keeps builds **reproducible** (versioned artifacts)
- Keeps routing **fast + explainable** (graph + tiles optimized for serving)



<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/81c6a876-f72f-4657-9691-d0282e773c53" />





## 🚀 Deployment Strategy

AccessMap is deployed as a **portable, reproducible city-scale platform** using **Docker Compose (v3.8+)**—so shipping changes doesn’t depend on one developer machine.

### Goals
- **Repeatable deployments** across environments and cities  
- **Fast iteration** (update data/config → rebuild → redeploy)  
- **Production reliability** (stable routing + tiles + APIs)  
- **Scalable onboarding** (plug in a new city with minimal changes)

### Environments
**Dev → Staging → Production**
- **Dev:** rapid testing + debugging  
- **Staging:** production-like config + smoke tests + perf checks  
- **Production:** hardened gateway, caching, controlled releases  

### Containerized services (Compose)
- **Frontend (React):** map UI + route exploration  
- **Routing service:** accessibility-aware pathfinding + explanations  
- **Tiles/Graph service:** serves vector tiles + routing artifacts  
- **Reverse proxy (gateway):** routing, caching, TLS termination, rate limits  


### Release & safety
- **Versioned city bundles** (data + configs + artifacts) for rollback  
- **Health checks** to catch failures early  
- **Pinned images** + controlled updates to avoid surprise breakage  
- **Rollback plan:** revert bundle → restart services  



<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/1988cb3d-3ee3-413c-b4c7-8eb99ceaea21" />




## ⚙️ Configuration

AccessMap is **city-portable**: onboarding a new city is primarily swapping datasets + tuning a small set of configuration values. Configuration defines **how accessibility is interpreted**, **how routes are scored**, and **how the system behaves when data is incomplete**.

### What you can configure (high-impact)

**Routing behavior**
- **Constraint mode:** step-free / avoid stairs / slope-sensitive  
- **Penalty weights:** stairs, steep slope, unsafe crossings, missing sidewalks  
- **Preference tuning:** prioritize safety vs. distance vs. effort  

**Data quality + trust**
- **Confidence thresholds:** when to warn vs. when to fall back  
- **Missing-data behavior:** conservative detours vs. best-available route  
- **Feature toggles:** enable/disable crossing risk, curb-ramp requirements, etc.  

**City onboarding**
- **Dataset paths/URLs:** OSM extract + city data + elevation tiles  
- **ETL parameters:** schema mapping, normalization rules  
- **Region bounds:** coverage area, clipping + caching strategy  

**Platform & API**
- **Gateway rules:** caching, rate limits, timeouts  
- **Service endpoints:** routing/tiles/frontend base URLs  
- **Environment flags:** dev/staging/prod logging + runtime settings  

### Recommended “city bundle” pattern
Keep deployments rollback-friendly by versioning each city as:

- `data/` (raw + processed inputs)  
- `config/` (weights, thresholds, toggles)  
- `artifacts/` (routing graph + vector tiles)  
- `metadata.json` (version, build time, sources)




<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/0259db8e-808b-4e82-9fb3-cb847bbb7227" />



  
## 🧱 Building Assets

Build all required artifacts (web app, tiles, router):

``bash
docker-compose run build_webapp
docker-compose run build_tiles
docker-compose run build_router



<img width="1700" height="980" alt="accessmap_building_assets_light_infographic_v2" src="https://github.com/user-attachments/assets/c70d34fa-06c0-48af-b01b-cc19f73f9ad4" />




## Outcomes & Learnings


**What worked**
- Standardizing into an OpenSidewalks-compatible schema enabled consistent routing across heterogeneous city datasets.
- Accessibility-aware costs produced safer defaults than “shortest-only” routing.
- Explainability (why + trade-offs) improved user trust by making decisions legible.

**Main challenge**
-Real-world sidewalk/crossing data is often incomplete → gaps, dead-ends, edge cases.
-Noisy/missing tags (curb ramps, entrances, temporary barriers) increase uncertainty.
-A single wrong edge can mean unsafe detours or loss of independence.

**How we handled it**
-Warnings + confidence cues when data is missing or risk is high.
-Fallback routes + alternatives instead of silent failure.
-Conservative penalties to avoid uncertain/unsafe edges by default.

**Next steps**
-Improve scoring with context-aware weights (city/zone/time sensitivity).
-Add entrance-level metadata to reduce last-meter failures.
-Strengthen slope modeling (smoothing + effort estimation) for realistic accessibility routing.

<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/5d276888-a255-48dd-bb76-5690d2afd7e8" />


