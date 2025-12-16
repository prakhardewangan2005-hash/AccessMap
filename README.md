# 🗺️ AccessMap — Accessibility-Aware Navigation Infrastructure

AccessMap is a **containerized deployment platform** for building and running an
**accessibility-focused pedestrian navigation system**.  
This repository contains all the infrastructure and services required to deploy
AccessMap, excluding raw geospatial data, which can be generated using the
[`opensidewalks-data`](https://github.com/opensidewalks/opensidewalks-data) pipeline.

---

## 🧩 Problem Statement

Most urban navigation systems optimize routes primarily for **speed and distance**,
often ignoring **accessibility constraints** faced by people with mobility impairments.
Pedestrians using wheelchairs, walkers, or strollers frequently encounter:

- Steep slopes  
- Missing or broken sidewalks  
- Unsafe crossings  
- Inaccessible pedestrian pathways  

Deploying an accessibility-aware routing platform at **city scale** is technically
challenging due to:

- Integration of heterogeneous geospatial datasets  
- Standardization of pedestrian infrastructure data  
- Efficient routing graph construction  
- Scalable deployment across development and production environments  

There is a need for a **portable, reproducible, and scalable infrastructure** that can
transform raw pedestrian data into an accessibility-aware routing system and make it
easy to deploy across different cities.

---

## 💡 Solution — AccessMap Platform

AccessMap provides an **end-to-end, Docker-based deployment infrastructure** for an
accessibility-aware pedestrian navigation platform.  
The system converts standardized geospatial data into **routable pedestrian networks**
and serves them through a **web-based interactive map interface**.

---

## 🔧 Key Features

### 1️⃣ Accessibility-Aware Routing
- Uses **OpenSidewalks-compliant GeoJSON** data  
- Considers slope, connectivity, and pathway metadata  
- Builds routing graphs using **Unweaver**, a flexible pedestrian routing engine  

### 2️⃣ Modular & Scalable Architecture
- Clear separation of concerns:
  - React-based frontend  
  - Routing engine  
  - Map tile generation  
  - User APIs  
- All services orchestrated using **Docker Compose**

### 3️⃣ Automated Build & Deployment
- Pre-builds:
  - Optimized frontend assets  
  - Vector map tiles  
  - Routing graphs  
- Simple CLI-based setup  
- Supports **development, staging, and production** workflows  

### 4️⃣ Configurable & Portable Setup
- Environment-based configuration using `.env` files  
- City-specific deployments by swapping GeoJSON datasets  
- Easy migration from local development to cloud or VPS hosting  

### 5️⃣ Privacy-Preserving Analytics (Optional)
- Integrates a self-hosted **Rakam** analytics service  
- Full control over data provenance  
- Opt-in, project-based analytics tracking  

---

## 🧩 Related Projects

- **AccessMap Web App (React)**  
  https://github.com/prakhardewangan2005-hash/AccessMapWebApp  

- **Unweaver — Routing Engine**  
  https://github.com/nbolten/unweaver  

---

## 🏗️ System Architecture

![AccessMap orchestration diagram](orchestration-diagram.png)

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
