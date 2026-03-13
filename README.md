# Driver Risk Score Modelling

> Predicting high-risk drivers from telematics behavioural patterns using machine learning.

---

## Overview

Usage-Based Insurance (UBI) programmes use telematics data — collected from in-vehicle sensors or smartphone apps — to assess driving behaviour and personalise premiums. This project builds a complete driver risk scoring system that ingests raw telematics signals, engineers composite behavioural features, trains classification models, and outputs an interpretable **0–100 risk score** per driver with tier classification.

---


## Project Structure

```
driver-risk-score/
│       
├── driver_risk_score.ipynb
│
├── outputs/
│   ├── driver_risk_scores.csv    
│   ├── 01_eda_overview.png       
│   ├── 02_model_evaluation.png   
│   ├── 03_risk_score_distribution.png  
│   ├── 04_driver_profiles_radar.png    
│   └── driver_risk_score_slide.pptx
│
└── README.md
```

---

## Features

### Raw Telematics Signals (12)

| Category | Feature | Description |
|---|---|---|
| Speed | `speeding_pct` | % of time driven above speed limit |
| Speed | `max_speed_kmh` | Maximum speed recorded (km/h) |
| Harsh Events | `harsh_braking_per100km` | Hard braking events per 100 km |
| Harsh Events | `harsh_accel_per100km` | Harsh acceleration events per 100 km |
| Harsh Events | `cornering_per100km` | Sharp cornering events per 100 km |
| Temporal | `night_driving_pct` | % of trips between 22:00–05:00 |
| Temporal | `rush_hour_pct` | % of trips during peak hours |
| Usage | `avg_trip_km` | Average trip distance (km) |
| Usage | `monthly_km` | Total monthly distance (km) |
| Distraction | `phone_use_per_trip` | Phone interaction events per trip |
| Driver | `age` | Driver age (years) |
| Vehicle | `vehicle_age_yrs` | Vehicle age (years) |

### Engineered Features (6)

| Feature | Formula | Purpose |
|---|---|---|
| `harsh_event_index` | Weighted sum of braking, accel, cornering | Single composite harsh-driving score |
| `speed_risk_index` | Speeding % × 0.55 + normalised max speed × 0.45 | Combined speed risk signal |
| `risk_time_pct` | Night driving × 0.6 + rush hour × 0.4 | High-risk time exposure |
| `distraction_score` | Phone use / max, clipped 0–1 | Normalised distraction level |
| `mileage_band` | Binned monthly km (0–3) | Exposure category |
| `age_risk_flag` | 1 if age < 25 or age > 65 | U-shaped age risk indicator |

---
