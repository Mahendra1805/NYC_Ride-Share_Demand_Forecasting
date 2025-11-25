"""
# NYC Ride-Sharing Demand Forecasting & Dynamic Surge Pricing using GCN + LSTM + Weather AI

## Problem Statement

New York City is one of the busiest mobility ecosystems in the world. Millions of daily trips occur across Yellow Taxis, Green Cabs, FHVs, Uber, Lyft, and Via.  
However, demand fluctuates heavily across:

- Time of day  
- Weather conditions  
- Boroughs and taxi zones  
- Events, traffic, and local conditions  

Ride-sharing companies depend on accurate demand forecasting, real-time surge pricing, and better driver allocation to maintain efficiency and reduce passenger wait times.

This project builds an end-to-end AI system that predicts next-hour demand across 263 NYC Taxi Zones and transforms it into a surge price multiplier.

---

## Why We Built This

Traditional forecasting models often ignore:

- Spatial influence between neighboring zones  
- Weather impact  
- Dynamic demand variability  

We solve this using:

- Graph Convolutional Networks (GCN)  
- LSTM for time-series prediction  
- Weather-aware enhancements  
- Rule-based surge pricing engine  

This pipeline supports real-time decision-making, zone-level demand forecasting, data-driven surge pricing, and driver placement optimization.

---

## How We Built It (4-Stage Pipeline)

### 1. Taxi Zone Graph Construction
- Loaded 263 NYC taxi zones (.shp)
- Built polygon adjacency using GeoPandas and NetworkX
- Generated adjacency matrix (A_hat) for GCN model

### 2. GCN + LSTM Demand Prediction
- Created hourly demand matrix (time × zones)
- Built training sequences (past 6 hours → next hour)
- Trained a hybrid GCN + LSTM model
- Predicted next-hour demand for all NYC taxi zones

### 3. Weather Integration
- Collected hourly weather: temperature, rainfall, snow, wind, visibility
- Merged weather with hourly demand using timestamps
- Retrained the model using a combined input: demand + neighbor demand + weather

### 4. Surge Pricing Calculation
- Computed baseline median demand per zone
- Calculated load index = predicted / baseline
- Applied surge rules:
  - >1.05 → 1.2x  
  - >1.15 → 1.5x  
  - >1.30 → 2.0x  
  - >1.50 → 2.5x  
- Generated final surge multipliers for each taxi zone

---

## Project Structure

NYC_TLC_Project/
│
├── 1.NYC_Taxi_Zones_Adjacency_Graph.ipynb                 # Problem Statement 1  
├── 2.(GCN) + LSTM_For_Demand_Prediction.ipynb             # Problem Statement 2  
├── 3.Real-Time_Weather_Features_Integration.ipynb         # Problem Statement 3  
├── 4.Implementing_surge_pricing_prediction_logic.ipynb    # Problem Statement 4  
│
├── adj_matrix_for_demand_prediction_final.xlsx            # Final adjacency matrix  
├── demand_matrix_for_demand_prediction_with_time.xlsx     # Final hourly demand matrix  
│
└── README.md                                              # Documentation  

---

## System Overview

This project is implemented entirely through Jupyter Notebooks.  
Each notebook represents one stage in the pipeline.

To run them:

1. Open each notebook in Jupyter Notebook or VS Code  
2. Run in order: Notebook 1 → 2 → 3 → 4  
3. Use "Kernel → Restart & Run All" or run all cells manually in sequence  

---

## Notebook-Wise Summary

### Notebook 1 — Taxi Zone Graph (Adjacency Matrix)
- Loads taxi zone shapefile
- Builds adjacency graph
- Outputs final adjacency matrix

### Notebook 2 — GCN + LSTM Demand Prediction
- Loads demand matrix
- Aligns zones and adjacency matrix
- Builds spatial + temporal inputs
- Trains GCN + LSTM model
- Predicts zone-level demand

### Notebook 3 — Weather Integration
- Loads weather dataset
- Aligns timestamps
- Adds weather features as model inputs
- Retrains enhanced model

### Notebook 4 — Surge Pricing Logic
- Loads predicted demand
- Computes baseline demand
- Calculates load index
- Applies surge multiplier rules
- Generates final surge pricing table

---

## Installation & Setup

### 1. Clone Repository
git clone https://github.com/YourGitHubUsername/NYC_TLC_Project.git  
cd NYC_TLC_Project

### 2. Create Python Environment
conda create -n tlc_env python=3.10  
conda activate tlc_env

### 3. Install Dependencies
pip install numpy pandas matplotlib plotly geopandas networkx tensorflow

### 4. Launch Jupyter Notebook
jupyter notebook

### 5. Run Notebooks
Execute in order: 1 → 2 → 3 → 4  

---

## Final Outputs

### Zone-Level Demand Forecasting
Predicts next-hour demand for all 263 NYC zones.

### Weather-Aware Demand Prediction
Captures effects of rain, snow, wind, visibility, etc.

### Surge Pricing Engine
Computes surge multipliers (1.2x to 2.5x) for every NYC taxi zone.

### Business Use Cases
- Real-time ride-share operations  
- Driver allocation optimization  
- Dynamic pricing  
- Mobility analytics  

---

## Summary

This project demonstrates an end-to-end AI pipeline:

Taxi Zones → Graph → GCN + LSTM → Weather → Surge Pricing

It combines spatial modeling, time-series forecasting, weather intelligence, and dynamic pricing logic to create a practical, real-world NYC mobility prediction system.
"""

---

## Acknowledgements

- NYC Taxi & Limousine Commission (TLC) for open datasets  
