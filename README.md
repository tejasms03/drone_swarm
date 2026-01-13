# Energy-Efficient Collaborative Target Tracking in UAV Swarms

This repository contains the simulation code and research paper for
**Energy-Efficient Collaborative Target Tracking in UAV Swarms via
Enhanced Voronoi Partitioning**. The project focuses on improving
tracking duration and reducing energy consumption in multi-UAV systems
through intelligent spatial partitioning and predictive coordination.

------------------------------------------------------------------------

## Overview

Collaborative drone swarms offer improved coverage and reliability for
surveillance and monitoring tasks, but they suffer from limited battery
life when all drones remain active. This work proposes an **Enhanced
Voronoi Method** that optimizes energy usage by:

-   Partitioning the operational area into Voronoi cells
-   Assigning drones to active, passive, and grounded states
-   Predicting target boundary crossings for seamless handovers
-   Reducing redundant drone activity

Simulation results show up to a **374% increase in tracking time**
compared to baseline methods.

------------------------------------------------------------------------

## Repository Structure

. ├── voronoi_tracking_sim.py ├── IEEE_TVT\_\_DroneSwarm_final (2).pdf
└── README.md

------------------------------------------------------------------------

## File Description

### voronoi_tracking_sim.py

Python-based simulation implementing: - Static Voronoi partitioning -
Edge-crossing prediction algorithm - Energy-aware drone state
transitions - Battery consumption modeling - Performance visualization

### IEEE_TVT\_\_DroneSwarm_final (2).pdf

Full research paper describing the methodology, algorithms,
implementation, and results.

------------------------------------------------------------------------

## Requirements

-   Python 3.8 or later

### Python Libraries

pip install numpy scipy matplotlib

------------------------------------------------------------------------

## Running the Simulation

python voronoi_tracking_sim.py

The script simulates drone behavior, target movement, energy
consumption, and tracking performance.

------------------------------------------------------------------------

## Performance Metrics

-   Total tracking time before battery depletion
-   Average battery consumption per drone
-   Battery depletion patterns over time
-   Scalability with increasing drone count

------------------------------------------------------------------------

## Reference

**Energy-Efficient Collaborative Target Tracking in UAV Swarms via
Enhanced Voronoi Partitioning**\
Anubhav Elhence, Tejas Sriganesh, Vinay Chamola\
IEEE Transactions on Vehicular Technology

See the included PDF for full details.

------------------------------------------------------------------------

## License

This project is intended for research and educational use.
