# CX4640-Final-Project

----
Name: Antoine Paletta
Topic: Numerical Optimal Control and its Application to Spacecraft Trajectory Optimization
----

## Table of Contents
1. [Introduction](#example)
2. [Example2](#example2)
3. [Third Example](#third-example)
4. [Fourth Example](#fourth-examplehttpwwwfourthexamplecom)


## Introduction to Astrodynamics and Spacecraft Trajectories
Astrodynamics (also called orbital mechanics) is an interesting field that is concerned with the application of celestial mechanics, and ballistics to the motion of rockets and spacecraft. The laws governing spaceflight are derived from Newton's 3 laws of motion, the universal law of gravitational attraction, and other perturbing forces present in the space environment (such as atmospheric drag, solar radiation pressure, etc). It is a very important discipline when it comes to space mission design, as a large part of a mission's engineering requirements are driven by the trajectory the spacecraft will follow through space. Therefore, significant effort is invested into designing trajectories that minimize the fuel, mass, life support, or power needed to support a space mission, while maximizing the payload that it can carry to achieve its mission. Additionally, when it comes to lunar or interplanetary missions, it is possible to take advantage of the gravity of planets or moons encountered on the spacecraft's trajectory (gravity assists) to reach destinations that would not be possible within the limiting constraints of the spacecraft's mass and onboard fuel.

Spacecraft trajectories are designed to satisfy mission requirements, and also usually minimize a performance index that may be relevant to the mission. Typical performance indices include minimizing the fuel needed to reach a destination, minimizing the time need to reach a destination, maximizing/minimizing range or altitude given a certain amount of fuel, etc. These problems are usually formulated as an optimal control problem for trajectory optimization, which involves finding a control law (usually duration/orientation/magnitude of rocket engine thrusting) to steer the spacecraft on a trajecotry that achieves all the mission constraints (starting from Earth and reaching the desired final destination, for example) while minimizing a certain performance index (time, fuel, etc as mentioned above).

## History and Background
Optimal control can trace its origins to the 17th century, when Johann Bernoulli challenged his peers to solve the Brachistochrone problem by using a previously developed theory called the Calculus of Variations. The resulting interest spurred Leonhard Euler to formalate the problem as one of finding a curve $x(t)$ over an interval which minimized a performance index that was a function of $t, x(t), \dot x(t)$. This initial formulation led to the development of the Euler-Lagrange equations in the late 18th centry, which came with a derivation of the first order necessary conditions for a minimum. A second order necessary condition to define a minimum was derived soon after by Legendre at the turn of the 19th century. During the 19th century, further refinement and formulation of the necessary conditions for optimality occured, with Hamilton and Weierstrauss developing new ways to guarantee that a given control law is optimal with respect to a particular system. In the early 20th century, Bliss and Bolza put finishing touches on the subject, developing rigourous formulations of the performance index/cost function. In the mid 20th century, McShane and Pontryagin extended the theory to handle inequalities in control variables, and Pontrygain developed the infamous maximum principle, which states that an optimal control for a dynamical system can be found if the Hamiltonian system (which is a two-point boundary value problem) can be solved and the control Hamiltonian is proven to be at a maximum. Finally, with the advent of the space age in the 1950's and the new availability of digital computing, optimal control became widely used and applied to solving the trajectory optimization problem for space missions.

## The Dynamics Involved in Spaceflight
### Relevant Equations of Motion
### Relevant Equations for Control
in general, since these equations are nonlinear, they have to be propagated using nonlinear numerical integration techniques

## Optimal Control Theory for Trajectory Optimization
### The General Optimal Control Problem Formulation
give the analytical formulation and the solution to it with the typical constraints
(dynamical constraints and boundary value constraints)
(also discuss additional of terminal constraints and path constraints)

### Example of Optimal Control Formulation for Low-thrust trajectory optimization
including thruster always on, and control as an angle
mention this as an example


## Numerical Optimal Control
### Indirect vs Direct vs Dynamic Programming Solution Methods
#### Indirect
#### Direct
#### Dynamic Programming

primer vector theory

can mention Trapezoidal quadrature and Hermite-Simpson
need a good initial guess with these kinds of problems, that is usually the challenge

### Shooting vs Collocation Techniques
#### single vs multiple shooting

#### collocation:
turning a trajectory optimization problem into a constrained parameter optimization problem






## Applications of numerical optimal control in commercial software packages
Talk about how the software is generalized to handle all types of optimal control problems, not just space ones
GPOPS-2, TrajOpt, PSOPT
SNOPT, IPOPT, etc
How its implemented in solvers like STK, GMAT, etc

## References
