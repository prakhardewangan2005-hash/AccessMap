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




[Download the System Architecture image](sandbox:/mnt/data/accessmap_system_architecture_infographic.png)




---


## 🚀 Deployment Strategy

AccessMap is deployed using **Docker Compose (v3.8+)** and follows a
**development → staging → production** workflow:

- Features are developed and tested independently  
- Stable versions are released using tags  
- The `develop` branch integrates tested services  
- Production releases are created by merging `develop` into `master`  
- The latest tag on `master` reflects the live deployment



<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/68f663d6-59d9-4700-8c3b-d528e51e44bb" />



---

## ⚙️ Configuration

### Environment Variables
```bash
cp accessmap.env.sample accessmap.env
## 🚶 Pedestrian Network Data

AccessMap requires the following files inside the `data/` directory:


- **transportation.geojson**  
  Contains pedestrian pathways formatted according to the OpenSidewalks schema.

- **regions.geojson**  
  Defines service areas and default map view settings for each region.

<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/e2a43e44-b94d-4c54-8f95-e50c2b2d8200" />


---

## 🛠️ Building Assets

Run the following commands to build all required assets:

```bash
docker-compose run build_webapp
docker-compose run build_tiles
docker-compose run build_router

<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/7a1a6259-7a71-4787-8138-26906b280e44" />


## 📈 Outcomes & Learnings
- What worked: (e.g., standardized schema enabled consistent routing across datasets)
- Main challenge: incomplete sidewalk/crossing data → handled via warnings + fallbacks
- Next steps: improve accessibility scoring, add entrance-level metadata, better slope modeling

