# 🗺️ AccessMap — Accessibility-Aware Navigation Infrastructure

AccessMap helps people navigate cities safely when stairs, curbs, steep slopes, or missing sidewalks exist.
It builds an accessibility-aware pedestrian graph from OpenSidewalks data and serves step-free routes + warnings + alternatives via a web map and APIs.



## 🧩 Problem Statement

Most urban navigation systems optimize routes primarily for **speed and distance**,
often ignoring **accessibility constraints** faced by people with mobility impairments.
Pedestrians using wheelchairs, walkers, or strollers frequently encounter:

- Steep slopes  
- Missing or broken sidewalks  
- Unsafe crossings  
- Inaccessible pedestrian pathways

Success criteria
  
- Provide routes that avoid stairs / unsafe crossings when possible
- Explain *why* a route is recommended (risk/effort tradeoffs)
- Reduce route failures (dead-ends, inaccessible entrances) and increase user confidence

What AccessMap Delivers
  
- **Step-free routing** using accessibility-aware penalties (slope, missing sidewalks, crossings)
- **Warnings & alternatives** when data is incomplete or risk is high
- **Web map + APIs** so cities/teams can deploy and iterate quickly


Deploying an accessibility-aware routing platform at **city scale** is technically
challenging due to:

- Integration of heterogeneous geospatial datasets  
- Standardization of pedestrian infrastructure data  
- Efficient routing graph construction  
- Scalable deployment across development and production environments  

There is a need for a **portable, reproducible, and scalable infrastructure** that can
transform raw pedestrian data into an accessibility-aware routing system and make it
easy to deploy across different cities.



## 💡 Solution — AccessMap Platform

AccessMap provides an **end-to-end, Docker-based deployment infrastructure** for an
accessibility-aware pedestrian navigation platform.  
The system converts standardized geospatial data into **routable pedestrian networks**
and serves them through a **web-based interactive map interface**.



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

---

## 🚀 Deployment Strategy

AccessMap is deployed using **Docker Compose (v3.8+)** and follows a
**development → staging → production** workflow:

- Features are developed and tested independently  
- Stable versions are released using tags  
- The `develop` branch integrates tested services  
- Production releases are created by merging `develop` into `master`  
- The latest tag on `master` reflects the live deployment  

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

---

## 🛠️ Building Assets

Run the following commands to build all required assets:

```bash
docker-compose run build_webapp
docker-compose run build_tiles
docker-compose run build_router

## 📈 Outcomes & Learnings
- What worked: (e.g., standardized schema enabled consistent routing across datasets)
- Main challenge: incomplete sidewalk/crossing data → handled via warnings + fallbacks
- Next steps: improve accessibility scoring, add entrance-level metadata, better slope modeling

