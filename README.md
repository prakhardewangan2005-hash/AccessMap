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




<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/43f3d115-9735-4ec7-b23f-6099fbf8d880" />




## 💡 Solution — AccessMap Platform

AccessMap provides an **end-to-end, Docker-based deployment infrastructure** for an
accessibility-aware pedestrian navigation platform.  
The system converts standardized geospatial data into **routable pedestrian networks**
and serves them through a **web-based interactive map interface**.




<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/9b08ed76-b997-4cb2-a5ad-648f1bace5af" />




 🧩 Key Features

### User-facing
- **Step-free routes** (avoid stairs/unsafe edges where possible)
- **Warnings + alternatives** when constraints are detected
- **Explainable steps** so users trust the route decisions

### Platform
- **Modular services** (frontend, routing, tiles, APIs)
- **Docker Compose orchestration** for reproducible deployments
- **Automated build & deploy** for dev → staging → production
- **Configurable city setup** by swapping datasets
- **Optional privacy-preserving analytics**



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




<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/71f542b0-07eb-42e9-9a9e-738c25b7c39b" />


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

