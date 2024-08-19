# Houdini Fluid Simulation Extension

### Mathematically Driven Fluid Simulation Enhancements for Houdini

---

## Overview

This project presents a Houdini extension designed to enhance the accuracy and efficiency of fluid simulations through the integration of GPU acceleration, volumetric data management, and adaptive mesh refinement. The extension leverages CUDA for computational speedup, OpenVDB for efficient data storage, and Adaptive Mesh Refinement (AMR) for dynamic resolution adjustments, creating a powerful tool for high-fidelity fluid simulations in computer graphics.

---

## Mathematical Foundations

Fluid simulation is governed by the **Navier-Stokes equations**, which describe the motion of fluid substances. These equations form the backbone of our extension:

### Navier-Stokes Equations

The Navier-Stokes equations for an incompressible fluid are given by:

\[
\frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla) \mathbf{u} = -\frac{1}{\rho} \nabla p + \nu \nabla^2 \mathbf{u} + \mathbf{f}
\]

\[
\nabla \cdot \mathbf{u} = 0
\]

where:

- \(\mathbf{u}\) is the velocity field,
- \(p\) is the pressure,
- \(\rho\) is the fluid density,
- \(\nu\) is the kinematic viscosity,
- \(\mathbf{f}\) represents external forces.

These equations are discretized using numerical methods, enabling their application in computer simulations.

---

## Module Descriptions

### 1. CUDA Integration

To overcome the computational intensity of solving the Navier-Stokes equations, this module offloads critical calculations to the GPU using NVIDIA CUDA. Parallel processing is applied to tasks such as *particle advection* and *pressure solving*, significantly speeding up the simulation process.

#### Mathematical Model

Consider the particle advection step, which updates particle positions based on their velocities:

\[
\mathbf{x}_{t+1} = \mathbf{x}_t + \mathbf{v}_t \Delta t
\]

This simple integration is computed in parallel across all particles, leveraging CUDA’s ability to execute large numbers of threads simultaneously.

### 2. VDB Grid Management

Efficiently managing volumetric data is crucial for large-scale fluid simulations. This module uses *OpenVDB*, a hierarchical data structure that represents sparse volumetric data efficiently. By storing only the active regions of the grid, memory usage is minimized without sacrificing detail.

#### Sparse Grid Representation

The VDB grid is mathematically defined by a sparse data structure:

\[
V(x, y, z) = \begin{cases} 
\text{value} & \text{if voxel is active} \\
0 & \text{if voxel is inactive}
\end{cases}
\]

This structure allows the simulation to handle large volumes while keeping computational and memory costs low.

### 3. Adaptive Mesh Refinement (AMR)

The AMR module dynamically adjusts the simulation’s mesh resolution based on the complexity of the fluid motion, applying higher resolution only where necessary (e.g., regions with high velocity gradients). This adaptive approach optimizes computational resources while maintaining accuracy where it matters most.

#### Refinement Criteria

Refinement is based on the magnitude of the velocity gradient:

\[
|\nabla \mathbf{u}| > \epsilon \implies \text{refine mesh}
\]

where \(\epsilon\) is a user-defined threshold. This criterion ensures that the mesh adapts to the fluid's behavior, offering higher detail in turbulent regions and coarser grids in more uniform areas.

---

## Implementation Details

### CUDA Integration

- **Kernel Design**: The CUDA kernels are designed to handle particle advection and pressure solving, parallelized across thousands of GPU threads.
- **Memory Management**: Data is transferred between the CPU and GPU efficiently, ensuring minimal overhead and maximum computational throughput.

### VDB Grid Management

- **Grid Construction**: VDB grids are initialized and populated based on the simulation’s needs. Sparse data representation allows the simulation to manage large volumetric data sets with high efficiency.
- **Operations**: Operations on the VDB grid, such as value interpolation and voxel activation, are optimized to leverage the sparse structure.

### Adaptive Mesh Refinement

- **Dynamic Refinement**: The AMR module continuously monitors the fluid's velocity field, refining the mesh dynamically where needed. The hierarchical structure of the mesh allows for multi-resolution simulation, with the computational cost focused on regions of interest.

---

## Getting Started

### Installation

Clone the repository and navigate to the project directory:

git clone https://github.com/yourusername/Houdini-Fluid-Simulation-Extension.git
cd Houdini-Fluid-Simulation-Extension

## Build the extension using CMake:
mkdir build
cd build
cmake ..
make

### Usage

Once installed, the extension can be accessed from within Houdini’s SOP network. Nodes for CUDA integration, VDB grid management, and AMR will be available, allowing you to create advanced fluid simulations with ease.

---

### Future Work

The current implementation provides a robust foundation for fluid simulation in Houdini. Future enhancements could include:

- **Multi-GPU Support**: Scaling the CUDA integration across multiple GPUs for even greater computational power.
- **Advanced AMR Techniques**: Implementing more sophisticated refinement criteria based on additional physical properties.
- **Custom User Interfaces**: Developing intuitive interfaces for controlling simulation parameters.

---

### References

- *NVIDIA CUDA Programming Guide*
- *OpenVDB Documentation*
- *Numerical Recipes in C: The Art of Scientific Computing*
- *Houdini Development Kit Documentation*

---

### Authors

- **Hakikat Singh**
- **Aruna**
