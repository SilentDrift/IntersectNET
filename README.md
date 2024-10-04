# IntersectNET: Traffic Flow? Managed

IntersectNET models and optimizes urban traffic flow using the **Cell Transmission Model (CTM)** and a hybrid **Genetic Algorithm (GA)** combined with **Simulated Annealing (SA)**. The simulation focuses on improving traffic efficiency by managing vehicle movement on road networks (edges) and optimizing traffic signals at intersections (nodes) to minimize congestion and travel time.

## Project Overview

The project includes:

- **Traffic Simulation**:
  - Simulates traffic flow using the **Cell Transmission Model (CTM)**.
  - Models different vehicle types (cars, buses, trucks) with varying speeds and lengths, moving along roads with different densities.

- **Hybrid Optimization**:
  - Optimizes traffic signal timings and flow between intersections using a hybrid **Genetic Algorithm (GA)** and **Simulated Annealing (SA)**.
  - Minimizes total travel time and ensures flow stability across the network.

- **Before and After Comparison**:
  - Visualizes traffic flow, density, and travel time metrics before and after optimization.

## Key Features

- **Multi-Vehicle Simulation**: Models heterogeneous traffic, including cars, buses, and trucks, with varying behavior on roads.
- **Dynamic Traffic Signal Control**: Optimizes traffic signal timings at intersections based on real-time traffic demand and queue lengths.
- **Hybrid Optimization**: Uses both GA and SA to optimize traffic flow and minimize travel time across the network.
- **Data Visualization**: Provides various plots showing vehicle density, flow, queue lengths, and travel time metrics.
- **Before and After Analysis**: Compares traffic conditions before and after optimization to show improvements in traffic flow and reduction in congestion.

## Mathematical Modeling

### 1. **Cell Transmission Model (CTM)**

The **Cell Transmission Model (CTM)** is used to simulate the movement of vehicles across roads, which are divided into discrete cells. Vehicle density and flow between cells are updated based on traffic conditions.

**Key Components:**
- **Cells**: Roads (edges) are divided into discrete segments (cells) with a fixed length (`Δx`).
- **Density (`ρ`)**: The number of vehicles per meter in each cell.
- **Flow (`q`)**: The number of vehicles moving between cells per time step.
- **Free-Flow Speed (`v_f`)**: The speed at which vehicles can travel when traffic is uncongested.
- **Congestion Wave Speed (`w`)**: The speed at which traffic jams propagate backward.
- **Capacity (`C`)**: The maximum number of vehicles that can pass through a cell per time step.

### CTM Equations:

#### **Sending Function (`S(i)`)**:

$$
S(i) = \min(v_{\text{free-flow}} \cdot \rho(i) \cdot \Delta t, C)
$$

#### **Receiving Function (`R(i)`)**:

$$
R(i) = \min(w \cdot (\rho_{\text{max}} - \rho(i)) \cdot \Delta t, C)
$$

#### **Flow Between Cells (`q(i)`)**:

$$
q(i) = \min(S(i), R(i+1))
$$

#### **Density Update**:

$$
\rho(i, t+\Delta t) = \rho(i, t) + \frac{q(i-1) - q(i)}{\Delta x}
$$

### 2. **Intersection Signal Control**

Intersections are modeled as nodes where incoming and outgoing flows are managed by traffic signals. Traffic lights at intersections switch between red and green phases, controlling vehicle movements.

- **Signal Phases**: Intersections alternate between green and red phases, controlling the flow of vehicles.
- **Queue Dynamics**: Vehicles waiting at intersections form queues when the inflow exceeds the available capacity.

The queue length \( Q(t) \) at an intersection is updated as:

$$
Q(t+1) = Q(t) + \Delta t \cdot (q_{\text{in}} - q_{\text{out}})
$$

### 3. **Hybrid Optimization (GA + SA)**

The hybrid optimization approach combines **Genetic Algorithms (GA)** and **Simulated Annealing (SA)** to find optimal traffic signal timings and flow control strategies at intersections.

- **Genetic Algorithms (GA)**:
  - **Selection**: Selects the best-performing solutions based on fitness.
  - **Crossover**: Combines parts of two solutions to create offspring.
  - **Mutation**: Introduces random changes to solutions to maintain diversity.

- **Simulated Annealing (SA)**:
  - **Temperature Parameter (`T`)**: Controls the probability of accepting worse solutions as the algorithm explores the solution space.
  - **Cooling Schedule**: Gradually reduces the temperature to fine-tune the optimization process.

#### **Objective Function**:

The objective function aims to:

1. **Minimize Total Travel Time**:

$$
\text{Total Travel Time} = \sum_{\text{edges}} \text{travel time} \times \rho
$$

2. **Maximize Flow Stability**:

$$
\text{Flow Stability} = \sum_{\text{edges}} \text{stable flow}
$$

## Visualization

The project provides comprehensive visualizations of traffic flow, density, and signal timings:

- **Density Over Time**: Visualizes how traffic density changes over time across different road segments.
- **Flow and Speed**: Shows the traffic flow and average speed at each time step.
- **Queue Lengths**: Displays the queue lengths at intersections, providing insights into how congestion is managed.
- **Before and After Comparison**: Compares traffic metrics before and after optimization to show improvements in flow and reduced travel times.
