# 🗺️ AccessMap — Accessibility-Aware Navigation Infrastructure

AccessMap helps people navigate cities safely when stairs, curbs, steep slopes, or missing sidewalks exist.
It builds an accessibility-aware pedestrian graph from OpenSidewalks data and serves step-free routes + warnings + alternatives via a web map and APIs.

<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/e4c2a10c-6d01-4291-9b4b-cf84c55bda4f" />



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

<img width="1333" height="991" alt="image" src="https://github.com/user-attachments/assets/8cea1030-9d57-4e0d-824e-5ec22a62570b" />




## 💡 Solution — AccessMap Platform

AccessMap provides an **end-to-end, Docker-based deployment infrastructure** for an
accessibility-aware pedestrian navigation platform.  
The system converts standardized geospatial data into **routable pedestrian networks**
and serves them through a **web-based interactive map interface**.

<img width="720" height="520" alt="image" src="https://github.com/user-attachments/assets/6bc370df-6ba3-4192-808b-06c644d9a251" />


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

<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/6c4769f4-b1fe-4fa2-93d9-54165f0d6291" />



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

