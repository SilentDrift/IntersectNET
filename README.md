# IntersectNET: Traffic Flow? Managed

IntersectNET implements a traffic simulation and signal optimization model for a **four-street intersection**, where each street has two lanes: one inbound and one outbound. The project models traffic flow using macroscopic traffic flow equations, with specific focus on optimizing signal timings to minimize total travel time (TTT) across the network.

## Project Overview

The primary objective is to simulate traffic dynamics at an intersection, model vehicle flow, and optimize traffic signal timings to reduce congestion. The simulation incorporates **vehicle density, speed**, and **flow dynamics** across each lane and at the intersection, using **mathematical models** based on the conservation of mass and momentum principles. A **gradient descent-based optimization algorithm** is employed to adjust signal timings dynamically and improve traffic throughput.

### 1. Mathematical Modeling

The traffic flow is modeled using **macroscopic traffic flow models**. This involves the Payne-Whitham (PW) model, which combines both **first-order flow equations** and **second-order momentum equations** to capture vehicle behavior more realistically.

#### Lane Dynamics

Each lane follows a set of partial differential equations (PDEs) to represent the relationship between vehicle density, flow, and speed:

1. **Continuity Equation (Conservation of Mass):**

    $$
    \frac{\partial \rho}{\partial t} + \frac{\partial (\rho v)}{\partial x} = 0
    $$
    
   - \( \rho \): Vehicle density (vehicles/m)
   - \( v \): Vehicle speed (m/s)
   - \( x \): Position along the lane (m)
   - \( t \): Time (s)
   
   This equation ensures that the number of vehicles entering a segment equals the number of vehicles exiting, adjusted by changes in density.

2. **Momentum Equation (Conservation of Momentum):**

    $$
    \frac{\partial v}{\partial t} + v \frac{\partial v}{\partial x} = -\frac{1}{\rho} \frac{\partial p}{\partial x} + \frac{V_{\text{eq}}(\rho) - v}{\tau}
    $$
    
   - \( V_{\text{eq}}(\rho) \): Equilibrium speed as a function of vehicle density
   - \( p \): Traffic pressure \( p = k \rho^\gamma \)
   - \( \tau \): Relaxation time (how fast vehicles adapt to changing conditions)

   The momentum equation allows vehicles to adjust their speed based on density and external forces, introducing a pressure-like effect.

#### Intersection Dynamics

At intersections, the project uses **transition matrices** to direct traffic flow from inbound lanes to outbound lanes. Each transition matrix element \( T_{ij} \) defines the probability that vehicles from inbound lane \( i \) will move to outbound lane \( j \). The sum of transition probabilities for each inbound lane equals 1:

$$
\sum_{j} T_{ij} = 1 \quad \forall i
$$

Movements are categorized into:
- **Straight**: From inbound to the same street's outbound lane.
- **Left Turn**: Turning left to the adjacent street's outbound lane.
- **Right Turn**: Turning right to the opposite street’s outbound lane.

The flow \( M_{ij} \) for each movement from inbound lane \( i \) to outbound lane \( j \) is computed as:

$$
M_{ij} = T_{ij} \cdot q_i(t)
$$

Where \( q_i(t) \) is the flow in the inbound lane \( i \).

### 2. Optimization Approach

To optimize the traffic signal timings at the intersection, the project uses a **gradient descent** method. The objective is to minimize the total travel time (TTT) across all lanes, defined as:

$$
\text{TTT} = \sum_{\text{lanes}} \sum_{t=1}^{T} \rho(t) \cdot \Delta x
$$

- \( \rho(t) \): Density of vehicles at time \( t \)
- \( \Delta x \): Lane segment length

#### Signal Phasing

Each traffic signal phase controls non-conflicting movements, such as allowing vehicles from specific streets to move straight or turn left/right. The duration of each signal phase (green time) is optimized to reduce congestion. The signal timing optimization process involves computing the gradient of TTT with respect to the green time \( G_p \) of each phase and updating the green times iteratively:

$$
G_p^{(n+1)} = G_p^{(n)} - \alpha \frac{\partial \text{TTT}}{\partial G_p}
$$

Where \( \alpha \) is the learning rate, and \( \frac{\partial \text{TTT}}{\partial G_p} \) is the gradient of TTT with respect to the green time for phase \( p \).

### 3. Results

The project produces several outputs to analyze traffic performance, including:
- **Density and Speed Heatmaps**: Show how vehicle density and speed evolve over time and space along each lane.
- **Flow Over Time**: Visualizes vehicle flow at the end of each lane over the entire simulation.
- **Queue Lengths at Intersection**: Tracks queue lengths at each inbound lane, highlighting congestion points.
- **Total Travel Time (TTT)**: Evaluates the overall performance of the traffic network.

### 4. Conclusion

The project demonstrates the use of macroscopic traffic models and signal optimization techniques to effectively manage traffic flow at a four-street intersection. Through dynamic adjustment of signal timings, the model reduces congestion and improves overall efficiency, as measured by a decrease in total travel time.

---

This README provides an overview of the **mathematical models**, **traffic dynamics**, and **optimization techniques** used in the project, as well as the results achieved through simulation. For a deeper dive into the code, please see the full implementation in the provided files.
