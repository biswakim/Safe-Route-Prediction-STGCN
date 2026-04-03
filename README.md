# Spatiotemporal Graph Navigator (ST-GCN) for Dynamic Safe Routing

## Overview
This repository contains the backend architecture for a custom routing engine that dynamically calculates safe travel paths. Unlike standard routing algorithms that rely on static historical heatmaps, this project utilizes a Spatiotemporal Graph Convolutional Network (ST-GCN) to predict localized risk scores on a street-by-street basis across different hours of the day.

## Methodology
1. **Graph Construction:** The physical street network is constructed using `OSMnx` and `NetworkX`.
2. **Data Integration:** Crime incident data (via the Chicago Data Portal) is spatially mapped to street edges and binned temporally.
3. **ST-GCN Prediction:** A custom neural network built in `PyTorch Geometric (PyG)` processes the graph to predict future state edge weights. PyG was selected over DGL and Spektral due to superior inference latency (~1.7ms) and deployment stability.
4. **Dynamic Routing:** Dijkstra's algorithm is manipulated with a custom time-dependent cost function: `Cost = Distance + (Predicted_Risk * Penalty)`.

## Repository Structure
* `/notebooks`: Contains the experimental Google Colab notebooks with the data pipeline and framework benchmarking.
* `/src`: Contains the modularized PyTorch model and routing algorithms.

## Quick Start
```bash
git clone [https://github.com/yourusername/safe-route-stgcn.git](https://github.com/yourusername/safe-route-stgcn.git)
cd safe-route-stgcn
pip install -r requirements.txt
