

# 📊 DRL-Powered Urban Air Quality Management in Delhi (PPO-based)

---

## 📖 Overview

Urban air pollution remains one of the most pressing environmental and public health crises globally, particularly in densely populated, traffic-intensive cities like **Delhi**. As industrial activity, vehicular emissions, and urban development increase, managing air quality becomes increasingly challenging. Traditional mitigation strategies, like fixed regulations or green infrastructure, often fall short because they lack adaptability to dynamic urban scenarios.

This project introduces a **Deep Reinforcement Learning (DRL)**-based framework to intelligently **optimize the placement of air purification booths** across Delhi. We use **Proximal Policy Optimization (PPO)** — a powerful reinforcement learning algorithm — to iteratively learn and identify high-impact booth locations, leveraging spatial, environmental, and demographic data.

---

## 🎯 Objectives

The primary goals of this project include:

- 📌 **Developing a multi-source data integration framework** using station-based AQI readings, live API data, and contextual urban information (population, traffic, green zones, etc.)
- 📌 **Optimizing booth placements dynamically** based on air quality, traffic, and population density using PPO.
- 📌 **Benchmarking RL-based placement strategies** against traditional random and greedy AQI-based approaches.
- 📌 **Predicting pollution trends** using machine learning models to inform future booth deployments.
- 📌 **Providing real-time, visual feedback and evaluation metrics** for urban planners and policymakers.

---

## 🛠️ Methodology

The core components of this project can be broadly classified into these parts:

### 📡 Data Collection & Preprocessing

- **Station-based AQI data**: Collected from Delhi’s official government data repositories via [data.gov.in](https://data.gov.in)
- **Ozone3 API data**: Live, high-resolution AQI estimates to fill spatial gaps.
- **Custom spatial datasets**: Green spaces, traffic hotspots, population density, industrial zones (via OpenStreetMap and DDA datasets)

> Interpolations, median imputations, and normalization were applied to clean, scale, and spatially align data into a **multi-channel 50x50 grid**.

---

### 🗺️ Environment Design

The urban environment of Delhi is modeled as a **multi-channel grid** (50x50 cells), where each cell contains:
- 📊 AQI values
- 🧑‍🤝‍🧑 Population density
- 🚦 Traffic density
- 🏭 Industrial area influence
- 🌳 Green cover information
- 📍 Existing booth presence

Each RL agent episode simulates **booth placements across this grid**, with the environment dynamically updating AQI values based on placements.

---

### 🧠 Agent Design: PPO with Spatial Attention

**DelhiAQIAgent** uses:
- **Convolutional layers** to process grid data
- **Spatial Attention layers** to focus on high-impact zones
- **Residual connections** for stability
- **Dual heads**:
  - **Policy head** for selecting actions
  - **Value head** for estimating expected rewards

We enhance PPO by:
- **Action masking** (invalid or unnecessary booth placements are masked)
- **Attention-weighted feature aggregation**
- **Multiple exploration strategies** (Boltzmann, UCB, High-AQI prioritization)

---

### 🔄 PPO Training Process

**DelhiPPOTrainer** is responsible for:
- Initializing agent, memory, optimizer
- Collecting episode trajectories (state, action, reward, value, log-probability)
- Updating network using:
  - **Clipped objective**
  - **Generalized Advantage Estimation (GAE)**
  - **Dynamic entropy regularization**
- Tracking:
  - Total rewards
  - AQI improvements
  - Policy and value losses
  - Entropy trends
  - Custom environmental metrics (population, traffic, green policy violations)

---

### 📈 Validation and Testing

Validation involves:
- ✅ Ensuring proper action-space alignment
- ✅ Verifying AQI reductions after booth placements
- ✅ Inspecting action logits, value predictions, and entropy levels
- ✅ Confirming action validity masks work correctly

---

## 📊 Results

| Placement Strategy | Average AQI Improvement | Spatial Coverage | Policy Stability |
|:------------------|:------------------------|:----------------|:----------------|
| **Random**             | 3.2%                     | Low              | Stable           |
| **Greedy AQI**         | 7.1%                     | Medium           | Risk of redundancy|
| **RL PPO (Ours)**      | **13.5%**                | **High**         | **Stable**        |

The PPO-based agent achieved **over 13% AQI improvement**, with superior spatial distribution and minimal green space violations.

---

## 📌 Key Features

- **Multi-source, real-time data fusion**
- **High-resolution spatial modeling**
- **Attention-augmented deep RL agent**
- **Dynamic entropy scheduling for stable exploration**
- **Flexible exploration strategies**
- **Extensive diagnostic metrics**
- **Comparative benchmarking**

---

## 🔍 Why PPO?

Proximal Policy Optimization (PPO) is:
- **Stable**: Uses clipped objectives to avoid large policy updates.
- **Efficient**: Less sensitive to hyperparameters than alternatives like TRPO.
- **Adaptable**: Handles continuous, discrete, and multi-dimensional action spaces well.
- **Proven**: Successful in complex control tasks, robotics, and simulated environments.

In this work, PPO's stability and trust-region-like updates are crucial because:
- The environment is **non-stationary**
- Rewards (AQI improvements) are **delayed and sparse**
- The **state-action space is very high-dimensional**

---

## 📝 Configuration

| Parameter         | Value      |
|:-----------------|:-----------|
| Learning Rate      | 2.5e-4     |
| Discount Factor γ  | 0.97       |
| GAE λ              | 0.95       |
| PPO Clip Ratio      | 0.15       |
| Entropy Coefficient | 0.1        |
| Max Grad Norm       | 1.0        |
| Batch Size          | 64         |
| Max Steps per Episode | 300      |
| Num Episodes        | 100        |

---

## 📚 Dependencies

- Python 3.10+
- PyTorch
- Numpy
- Pandas
- Gymnasium
- Matplotlib
- TQDM
- IPython
- Scipy
- OpenStreetMap, DDA, Ozone3 API access

---

## 📌 Future Work

- 🔍 **Multi-agent RL models** — collaborating booths and distributed placement
- 🌐 **Real-time API integration** for continuous learning
- 🏙️ **Deployable smart-city dashboards**
- 🎛️ **Policy transfer learning** to other cities (Mumbai, Bangalore, Beijing)
- 🚦 **Traffic-AQI interaction modeling**
- 🎮 **Sim-to-real policy validation**
- 📱 **Mobile/web-based air quality visualizations**

---

## 📈 Outcome Summary

✔️ DRL-PPO framework dynamically optimizes urban AQI control  
✔️ Significant improvements over static or heuristic strategies  
✔️ Demonstrates real-world feasibility for **smart cities and environmental policy applications**

---

## 📊 Visualizations

- 📈 Training rewards and losses
- 📉 AQI improvement over episodes
- 🌍 Heatmaps of AQI before and after booth placements
- 📊 Action selection distributions
- 📍 Booth placement overlays on the city grid

---

## 📚 References

The full list of 40+ references is available in the `paper` and included official datasets from:
- [data.gov.in](https://data.gov.in)
- Ozone3 AQI API
- OpenStreetMap (OSM)
- DDA open datasets

---

## 💡 Conclusion

This project showcases how **AI-driven adaptive strategies can transform traditional urban management challenges**. The PPO-based DRL system outperforms static, rule-based heuristics by:
- Learning dynamically from real AQI, population, traffic, and land-use data  
- Adapting to complex, evolving environments  
- Supporting better-informed, scalable smart city air quality management  

