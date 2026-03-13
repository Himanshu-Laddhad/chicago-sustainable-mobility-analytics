# 🌿 MyEcoPool — Sustainable Urban Mobility for Chicago

> **Course:** MGMT 59000V — Visual Analytics
> **Project Type:** Team Project — Team 9
> **Author (Data Analysis):** Himanshu Laddhad

---

## Overview

**MyEcoPool** is a data-driven proposal for a sustainable urban carpooling platform designed for Chicago. The project analyzes real-world transportation data to quantify the environmental and economic trade-offs between rideshare (Uber/Lyft), taxis, and public transit (CTA buses) — making the case for a greener, smarter commute option.

The analysis uses open Chicago city data to model **travel time**, **cost**, and **CO₂ emissions** across transportation modes, producing the visual evidence that anchors the MyEcoPool pitch.

---

## The Problem

Chicago's transportation landscape is dominated by carbon-heavy, single-occupancy rides. Uber and Lyft trips generate significantly more CO₂ per passenger-mile than shared alternatives, yet they remain the default for millions of commuters. MyEcoPool addresses this gap by making carpooling the path of least resistance — economically attractive *and* environmentally responsible.

---

## Project Structure

```
Team project/
├── Code/
│   ├── Data Analysis for EcoPool.ipynb    # Full data analysis notebook
│   └── Killer Figure.png                  # Hero visualization for the pitch
│
├── Presentation/
│   ├── EcoPool_Chicago_Pitch_Final.pptx   # Final pitch deck
│   ├── EcoPool_Chicago_Pitch_DarkMode.pptx
│   ├── MyEcoPool_Team9_Report.docx        # Full written report
│   ├── MyEcoPool_Team9_Report.pdf
│   ├── Script.docx                        # Presentation script
│   └── Final Report - Initial Draft.docx
│
├── Team_9_MyEcoPool.pdf                   # Executive brief
├── Safari.pdf                             # Supporting reference
└── README.md
```

---

## Data Sources

| Dataset | Source | Records |
|---|---|---|
| **TNP Trips** (Uber/Lyft) | [City of Chicago Open Data Portal](https://data.cityofchicago.org/resource/m6dm-c72p.csv) | 20,000 trips |
| **Taxi Trips** (Carpool proxy) | [City of Chicago Open Data Portal](https://data.cityofchicago.org/resource/wrvz-psew.csv) | 20,000 trips |
| **CTA Bus Reference** | [CTA GTFS](https://www.transitchicago.com/developers/gtfs/) | Synthetic (20,000 samples, based on CTA fleet averages) |

---

## Analysis Breakdown

### 1. Data Ingestion & Cleaning
- Pulled live samples from Chicago's open data APIs (20K rows each for TNP and Taxi)
- Standardized column names and parsed numeric fields
- Removed nulls in core trip metrics (`trip_miles`, `trip_seconds`, `fare`)

### 2. Feature Engineering — CO₂ Emissions
Emissions were computed using EPA-aligned emission factors:

| Mode | CO₂ Factor |
|---|---|
| Uber/Lyft | ~0.21 kg per mile (single-occupancy gasoline vehicle) |
| Taxi (Carpool proxy) | ~0.14 kg per mile (higher occupancy) |
| CTA Bus | ~0.021 kg per mile (per passenger, fleet average) |

### 3. Outlier Removal
- Applied IQR-based filtering on `travel_time_min`, `cost_usd`, and `co2_kg`
- Reduced noise from extreme values while preserving distributional integrity

### 4. Descriptive & Comparative Analysis
- Computed per-mode summary statistics (10th, 50th, 90th percentiles)
- Multi-dimensional scatter plot: **Cost vs. CO₂ vs. Travel Time** across all modes
- Identified the "green sweet spot" where bus + carpool beat rideshare on all three dimensions

### 5. Killer Figure
The centerpiece visualization plots cost, CO₂ emissions, and travel time simultaneously — making the environmental and economic case for MyEcoPool in a single, compelling chart.

---

## Key Findings

- **Uber/Lyft emits ~10× more CO₂** per trip than a CTA bus on a per-passenger basis
- **Taxi (carpool proxy) offers a middle ground** — lower cost than TNP with meaningfully reduced emissions
- **Carpooling at Uber-like convenience levels** could replicate taxi efficiency at scale
- At median trip length, switching from Uber to EcoPool-style carpool saves ~**$4–6 per trip** and ~**1.2 kg CO₂**

---

## The Pitch

MyEcoPool was pitched as a **Chicago-first** carpooling app that:
- Routes commuters into shared rides algorithmically
- Incentivizes green choices with a dynamic rewards system
- Targets the price-sensitive segment currently defaulting to Uber/Lyft

The pitch deck and full written report are included in the `Presentation/` folder.

---

## Tech Stack

| Tool | Purpose |
|---|---|
| Python 3 | Core analysis language |
| Pandas | Data ingestion and manipulation |
| NumPy | Numerical computation & sampling |
| Matplotlib / Seaborn | Visualizations |
| Chicago Open Data API | Live data ingestion |
| Jupyter Notebook | Interactive analysis environment |

---

## How to Run

1. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib seaborn jupyter requests
   ```
2. Launch the notebook (requires internet access for live API calls):
   ```bash
   jupyter notebook "Code/Data Analysis for EcoPool.ipynb"
   ```
3. Run all cells — data is fetched live from Chicago's open data portal

> **Note:** The CTA bus sample is synthetically generated based on published CTA fleet averages. Real GTFS trip-level data can be substituted for production use.

---

## Team

**Team 9 — MyEcoPool**
Purdue University — MGMT 59000V Visual Analytics

*Data Analysis & Visualization by Himanshu Laddhad*
