# Ocean Heatwave Prediction System

A full-stack, real-time monitoring and predictive dashboard for Marine Heatwaves (MHWs). This system ingests live global oceanic temperatures, applies standardized detection algorithms to identify current heatwaves, and uses machine learning to forecast future MHW severity up to 14 days in advance.

## The Problem
**Marine Heatwaves (MHWs)** are prolonged periods of extreme oceanic temperatures that severely damage marine ecosystems (e.g., coral bleaching) and impact global weather patterns.

## Methodology
This project implements the internationally standardized **Hobday et al. (2016)** MHW mathematical definition:
- Establishes a moving 30-day climatological baseline for specific geographic coordinates.
- Records an "event" only when the Sea Surface Temperature (SST) continuously exceeds the **90th percentile** of that historical baseline for **5 or more consecutive days**.

## Architecture & Data Pipeline
The system utilizes a dynamic, API-driven ingestion pipeline, connecting directly to the **NOAA CoastWatch ERDDAP** servers.
- **Target Dataset:** `ncdcOisst21Agg_LonPM180` (NOAA's 0.25-degree Daily Optimum Interpolation Sea Surface Temperature v2.1).
- Processes global geospatial datasets dynamically with **0 bytes of local CSV storage**.

## Machine Learning & Predictive Modeling
Employs a dual-model ensemble pipeline:
1. **Random Forest (RF) Classifier**: Analyzes the real-time thermal state of the ocean and categorizes it into severity tiers (Normal, Moderate, High alert).
2. **Gradient Boosting (GB) Regressor**: Generates an accurate 14-day chronological projection of future ocean temperatures and calculates the probability of an impending heatwave.

## Frontend & Visualization
- **Framework**: React.js (Vite)
- **UI**: Custom-built, modern dashboard with glass-morphism panels.
- **Geospatial Mapping**: D3.js `geoOrthographic` projections for a fully interactive 3D globe plotting active oceanic stations.
- **Data Visualization**: Recharts for dynamic multi-layered charts comparing baselines, active SST trajectories, and threshold markers.

## Fallback System (`sstEngine`)
Features a highly robust synthetic fallback engine. If the NOAA API server is unreachable, the application dynamically generates its own hyper-realistic historical data pool using sinusoidal physics, quasi-periodic ENSO oscillations, and anthropogenic global warming trends to ensure 100% uptime.

## Setup & Installation

### Backend (Python)
Navigate to the `backend` directory:
```bash
cd backend
pip install -r requirements.txt
python app.py
```

### Frontend (React/Vite)
Navigate to the `frontend` directory:
```bash
cd frontend
npm install
npm run dev
```

## Credits
Dashboard and code designed developed by Puneeth Mattam, Deepika Shahapur, and Vojeshwini M V. Data provided by NOAA.
