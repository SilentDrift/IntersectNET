# IntersectNET: Traffic Flow? Managed

IntersectNET simulates traffic flow using the Cell Transmission Model (CTM) and optimizes traffic at intersections using a Genetic Algorithm (GA). The simulation models urban traffic as a network of roads (edges) and intersections (nodes), aiming to reduce congestion and improve traffic flow through optimization.

## Project Overview

The project includes:

- **Traffic Simulation**: 
  - Uses the **Cell Transmission Model (CTM)** to simulate traffic flow on a road network.
  - Models vehicle behavior along roads with varying densities and speeds.
  
- **Optimization with Genetic Algorithm**:
  - Optimizes traffic signal timings at intersections to minimize congestion.
  - Utilizes a Genetic Algorithm (GA) to adjust traffic flow based on vehicle demand and supply dynamics.
  
- **Before and After Comparison**:
  - Compares traffic conditions before and after optimization using visualizations and travel time metrics.
  
## Key Features

- **Simulation of Traffic Flow**: Simulates vehicle movement on a network of roads and intersections over time.
- **Optimization of Traffic Signals**: Optimizes traffic signal control at intersections to reduce overall travel time.
- **Data Visualization**: Provides various plots showing traffic density, travel times, and intersection flow.
- **Before and After Analysis**: Displays the improvement in traffic flow and reduction in congestion after optimization.



## Mathematical Modeling

### Cell Transmission Model (CTM)

The **Cell Transmission Model (CTM)** is a discretized version of the kinematic wave model used for simulating traffic flow. It divides each road segment into discrete cells and updates vehicle densities based on the flow of vehicles between cells.

**Key Components:**

- **Cells:** Each road (edge) is divided into multiple cells based on spatial discretization (`DELTA_X`).
- **Density (`ρ`):** Represents the number of vehicles per meter in each cell.
- **Flow (`q`):** The number of vehicles moving between cells per time step.
- **Free-Flow Speed (`v_f`):** The speed at which vehicles can travel when traffic is uncongested.
- **Congestion Wave Speed (`w`):** The speed at which congestion propagates backward through traffic.
- **Capacity (`C`):** The maximum number of vehicles that can pass through a cell per time step.

### **CTM Equations:**

#### **Sending Function (`S(i)`):**

   $$
   S(i) = \min(v_f \cdot \rho(i) \cdot \Delta t, C)
   $$

#### **Receiving Function (`R(i)`):**

   $$
   R(i) = \min(w \cdot (\rho_{\text{max}} - \rho(i)) \cdot \Delta t, C)
   $$

#### **Flow Between Cells:**

   $$
   q(i) = \min(S(i), R(i+1))
   $$

#### **Density Update:**

   $$
   \rho(i, t+\Delta t) = \rho(i, t) + \frac{q(i-1) - q(i)}{\Delta x}
   $$


### Genetic Algorithm (GA) Optimization

The **Genetic Algorithm (GA)** is employed to optimize the transition matrices at intersections, which determine the probability of traffic from incoming edges being directed to outgoing edges. The goal is to minimize the total travel time across the network by optimizing traffic signal timings.

**GA Components:**

- **Population:** A set of potential solutions (transition matrices).
- **Fitness Function:** Evaluates how good each solution is based on negative total travel time.
- **Selection:** Chooses the best-performing solutions for reproduction.
- **Crossover:** Combines parts of two parent solutions to create offspring.
- **Mutation:** Introduces random variations to offspring solutions to maintain diversity.
