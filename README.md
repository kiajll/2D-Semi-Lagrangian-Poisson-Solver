# 2D-Semi-Lagrangian Poisson Solver for Incompressible Flow
![untitled01 - Copy](https://github.com/user-attachments/assets/1673b7fc-37d2-44d5-afbd-9b73a0cc47ad)
This repository contains a semi-Lagrangian Poisson solver for simulating incompressible fluid flow using a combination of Eulerian pressure correction and Lagrangian advection. The solver enforces incompressibility via the pressure Poisson equation (PPE) while advecting the velocity field using the Runge-Kutta 4th order (RK4) method.

## 📌 Features
* Solves the Pressure Poisson Equation (PPE) to ensure incompressibility.
* Semi-Lagrangian advection using RK4 for velocity transport.
* Jacobi iterative solver for solving the Poisson equation.
* Particle tracking for flow visualization.
* Fully deterministic simulation (no randomness, identical results for each run).
## 🔬 Governing Equations
### Pressure Poisson Equation (PPE)
<br/> To enforce incompressibility, the solver solves the Poisson equation for pressure:

$$\nabla^2p=−div(v)$$

where:
* $𝑝$ is the pressure field.
* $div(𝑣)=\frac{\partial 𝑣_x}{\partial x}+\frac{\partial 𝑣_y}{\partial y}$ ensures a divergence-free velocity field.
### ​Velocity Advection
Instead of explicitly solving the Navier-Stokes equations, the solver separates advection from pressure correction, following the projection method:
#### 1. Advect the velocity field using RK4:

$$v^*= v + advection~terms$$

#### 2. Solve the pressure Poisson equation to compute the pressure correction.
#### 3. Project the velocity field onto a divergence-free space:

$$ v = v^* - \nabla p $$

This method approximates the effects of the Navier-Stokes equations while keeping the simulation numerically stable.
## 📊 Numerical Methods Used
| Method                         | Purpose                                            |
|--------------------------------|----------------------------------------------------|
| **Jacobi Iteration**           | Solving the Poisson equation for pressure.        |
| **Semi-Lagrangian Advection (RK4)** | Transporting velocity and particles through the flow. |
| **Projection Method**          | Enforcing incompressibility by adjusting pressure. |
## 🌊 Key Discussion Points
### ✅ 1. Why This is a Semi-Lagrangian Poisson Solver
* The Poisson equation alone does not include advection, but advection is explicitly imposed using **RK4**.
* The solver is **Eulerian** for pressure correction and Lagrangian for advection, making it a **semi-Lagrangian method**.
### ✅ 2. No Viscous Dissipation
* The solver does not include the viscosity term $\nu\nabla^2V$, meaning there is no explicit dissipation.
* Numerical diffusion may introduce slight damping effects.
### ✅ 3. Deterministic Nature of the Solver
* Since no randomness is introduced, running the solver multiple times yields identical results.
### ✅ 4. Advection is Nonlinear
* The velocity field advects itself, meaning the advection term $(V⋅∇)V$ is nonlinear.
* Even though the Poisson equation is linear, the overall system exhibits nonlinear behavior due to the advection step.
## 📌 Future Improvements
🔹 **Add viscosity:** Implement a diffusion term $\nu\nabla^2V$ to introduce realistic dissipation.
<br/> 🔹 **Improve solver speed:** Replace Jacobi with Multigrid or Successive Over-Relaxation (SOR) for better efficiency.
<br/> 🔹 **Extend to 3D:** Generalize the solver for three-dimensional incompressible flows.
### 📝 References
* Chorin, A. J. (1968). Numerical solution of the Navier-Stokes equations.
* Stam, J. (1999). Stable Fluids, SIGGRAPH.
* Anderson, D., Tannehill, J.C., & Pletcher, R.H. (2012). Computational Fluid Mechanics and Heat Transfer (3rd ed.). CRC Press.
### 📜 License
This project is licensed under the MIT License.
