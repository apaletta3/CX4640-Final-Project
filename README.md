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
The dominant force that spacecraft are subjected to while in space is gravitation, which originates from all objects with a significant amount of mass. This is known as N-body gravity, where the spacecraft is subject to a force from all planets/moons in the solar system. However, when in the vicinity of a particular body (such as the Earth), the acceleration from that primary body can be considered dominant, and follows an inverse cubed law. All other accelerations acting on the spacecraft can then be considered "perturbing" (assuming a small magnitude in comparison to the primary body's gravity) and can be summed to generate the following vector equation in Cowell's form, where $\mu$ is the gravitational parameter of the primary body.
$$\ddot {\vec x}  = -\frac{\mu}{r^3}\vec r + \vec a_{perturb} $$

This is a second order ordinary differential vector equation, with an x,y,z component of the x vector defined. However, it is often more practical to transform this into a system of first order ODE's so that numerical techniques such as Runge-Kutta integration can be used to find solutions for them.
$$\dot {\vec r}  = \vec v $$
$$\dot {\vec v}  = -\frac{\mu}{r^3}\vec r + \vec a_{perturb} $$

When considering a dynamical system that is representative of a maneuvering spacecraft, we often add another equation to represent the reduction in mass as the fuel used to perform maneuvers is burned during the mission. This can usually be defined via the rocket equation for high and low thrust propulsion systems as follows, and approximated as a constant C multiplied by the rocket engine throttle setting $\tau$ (a value between 0 and 1) used.
$$\dot {m}  = -C\tau $$

### Relevant Equations for Control
Next, in order to control the spacecraft's trajectory, acceleration (or control input) must be applied to it via burning fuel in a rocket engine. This acceleration can be simplistically modelled using the ideal rocket equation shown below, where $ v_{e}$ is the exit velocity of the propellant, and $m_{i}$ and $m_{f}$ are the masses of the spacecraft before and after the burn respectively.
$$u = \triangle {v}  = v_{e} \ln{(\frac{m_f}{m_i})} $$


## Optimal Control Theory for Trajectory Optimization
### The General Optimal Control Problem Formulation
Using the equations of motion (with the state variable $x$) and control (with the control variable $u$) defined above, the optimal control problem can now be formally posed:
over the time interval $t_0 \leq t \leq t_f$, where the final time can be fixed, free, or open, there is a cost to be minimized:
$$\min J = \Phi[x(t_f),t_f] + \int\limits_{t_0}^{t_f}L[x(t),u(t),t]dt$$
that is subject to the dynamic constraints (equation of motion and control):
$$\dot x = f(x(t),u(t),t) $$
and boundary conditions (upper and/or lower)
 $$b_L\leq b(x(t_0),x(t_f),t_0,t_f) \leq b_U$$
as well as variable/path constraints (upper and/or lower)
$$g_L\leq g(x(t),u(t),t) \leq g_U$$

The boundary constraints represent starting and terminating conditions such as location at the beginning/end of the trajectory and desired time to completion of the trajectory. The variable/path constraints model limitations in the path chosen (can't fly through the Earth) or in the thrusting limits of the rocket engine.

### Solving the Optimal Control Problem
Taking the derivative of the cost function with respect to the state and control variables, and accounting for the inequality constraints we obtain the augemented Lagrangian forumation below:





## Numerical Optimal Control
The classical optimal control problem does not assume linearity, and as such these equations are not written in matrix form in the above definition.
in general, since these equations are nonlinear, they have to be propagated using nonlinear numerical integration techniques

### Indirect vs Direct vs Dynamic Programming Solution Methods
#### Indirect
#### Direct
#### Dynamic Programming

primer vector theory

can mention Trapezoidal quadrature and Hermite-Simpson
need a good initial guess with these kinds of problems, that is usually the challenge

discuss optimal control for low thrust, including thruster always on, and control as an angle, mention this as an example

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
