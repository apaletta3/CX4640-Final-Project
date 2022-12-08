# CX4640-Final-Project

----
Name: Antoine Paletta
Topic: Numerical Optimal Control and its Application to Spacecraft Trajectory Optimization
----

## Table of Contents
- [Introduction to Astrodynamics and Spacecraft Trajectories](#introduction-to-astrodynamics-and-spacecraft-trajectories)
- [History and Background](#history-and-background)
- [The Dynamics Involved in Spaceflight](#the-dynamics-involved-in-spaceflight)
    -  [ Relevant Equations of Motion](#relevant-equations-of-motion)
    -  [ Relevant Equations for Control](#relevant-equations-for-control)
- [Optimal Control Theory for Trajectory Optimization](#optimal-control-theory-for-trajectory-optimization)

    - [The General Optimal Control Problem Formulation](#the-general-optimal-control-problem-formulation)
    - [Solving the Optimal Control Problem](#solving-the-optimal-control-problem)

- [Numerical Optimal Control](#numerical-optimal-control)
- [Indirect vs Direct vs Dynamic Programming Solution Methods](#indirect-vs-direct-vs-dynamic-programming-solution-methods)

- [Shooting vs Collocation Techniques](#shooting-vs-collocation-techniques)

- [Applications of Optimal Control Theory in Commercial Applications](#applications-of-optimal-control-theory-in-commercial-applications)

- [References](#references)

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
In order to solve the optimal control problem and prove that there is an optimal control input $u^*(t)$ that minimizes $J$, one needs to derive a set of necessary conditions to be satisfied for optimality. First, since the problem deals with constrained optimization, one needs to use the Lagrangian multiplier technique (adding a vector of "costates" $\lambda$) by adjoining the dynamic constraints to the cost function:
$$\min {\bar J} = \Phi[x(t_f),t_f] + \int\limits_{t_0}^{t_f}L[x,u,t] + \lambda^T[f(x,u,t) - \dot x]dt$$

One can pull out an important function to define from this intergral, which is the Hamiltonian:
$$H(x,u,\lambda,t) = L(x,u,t) + \lambda^T(t)f(x,u,t)$$

Finally, the necessary conditions for optimality that are based on taking a $\delta \bar J = 0$ (first order optimality necessary condition) and other theorem for second order optimality allow the definitions below: \
$$\frac{\partial H}{\partial u} = 0$$
$$-\dot \lambda^T = \frac{\partial H}{\partial x} $$
$$\lambda^T(t_f) = 0$$
The first equation ensures that the Hamiltonian will be maximized during the entire trajectory in order to guarantee that the control $u^*(t)$ is optimal. In addition, the boundary conditions impose the last two equations, called the adjoint equation and the transversality condition respectively.

## Numerical Optimal Control
There are many methods used to solve the optimal control problem numerically, and they are split up into several categories. There are indirect vs direction methods, either of which can be executed with a shooting or a collocation technique. There is also differential dynamic programming, which is slightly different than the other methods. At the root of the problem, in order to find a numerical optimal control solution, one needs to covert the problem from a function space (infinite dimensional) to a parameter or vector space (finite dimension) optimization problem, where well established parameter optimization techniques can be applied.

### Indirect vs Direct vs Dynamic Programming Solution Methods
The main difference between these methods are the order in which the discretization and optimization to find the solution occur.

#### Indirect
Indirect methods first analytically derive the first and second order conditions for optimality that the state and control variables need to satisfy, and then discretize these conditions into a numerically solvable boundary value problem. This method is shown above in the derivation of the analytical solution to the optimal control problem. The introduction of the adjoint equation and costates allow for there to be enough equations to solve for all the variables in the boundary value problem. However, this technique is not used as much these days since it is very difficult to find solutions to these when dealing with complication spacecraft trajectories since there are no simple closed form solutions.


#### Direct
Direct methods, on the other hand, first discretize the trajectory optimization problem by generating a finite time grid of points along the trajectory and considering each point to be a design variable, then solve that constrained parameter optimization problem. The process of discretizing the problem into a finite time-grid is called transcription, and it results in optimizing for a vector of the state variables as well as control variables at each discretized point in the domain. Since the constraints and equations of motion are usually non-linear, this results in a non-linear optimization problem, which has to fullfill the first order necessary optimality conditions, also know as the KKT conditions.

#### Dynamic Programming
Dynamic programming is similar to direct methods because it discretizes the optimization problem along the domain and solves it based on the result of the constraint for the dynamical equations at each point. However, the optimization itself is carried out differently than the direct method, where the optimal control is actually propagated backwards along a candidate trajectory and the cost function evaluated after this is performed in an iterative fashion, exploiting the time-dependent nature of the trajectory.


### Shooting vs Collocation Techniques
Direct and indirect methods often involve one of the following techniques to actually solve the differential equations involved in the optimal control problem and find a solution in the state variables that satisfy the dynamical equations and a solution in the control variables that produce a minimized cost.

#### Shooting Techniques
The shooting technique is meant to solve boundary value problems (like the optimal control problem) by converting it into an initial value problem. Take a nonlinear differential equation of the form

$\ddot y(t) = f(\dot y(t), y(t), t)$ with boundary value conditions $y(t_0) = y_0$ and $y(t_f) = y_f$

This can be converted into the initial value problem as follows by allowing $y(t;a)$ to be the solution for the initial value problem: \
$\ddot y(t) = f(\dot y(t), y(t), t)$ with initial conditions $y(t_0) = y_0$ and $\dot y(t_0) = a$ \
If $y(t_f;a) = y_f$, then $y(t;a)$ is also the solution to the boundary value problem.

Numerically solving this is performed by using a root finding method such as Newton's method, bisection, or Broyden's method for vector functions to find the zeros of the function below: \
$F(a) = y(t_f;a) - y_f$
and solving for the parameter $a$.

Additionally, since the solutions to the equations of motion are not known, they have to be numerically integrated to go from the initial condition to the final condition in order to check if the boundary value problem has been satisfied. This can be done with explicit numerical integration methods such as Euler's method for low order equations of motion, or Runge-Kutta methods for higher order fidelity. One disadvantage with this technique is that you are not always guaranteed to find a solution that satisfies the boundary value problem, since this technique is essentially trial and error.


#### Collocation Techniques
The collocation technique (also called the simulatenous technique, or numerical quadrature) aims to solve boundary value problems by choosing a set of finite dimensional candidate solutions (comprised of polynomials up to a certain degree) and a number of points in the domain (these are called the collocation points), in order to choose a solution that satisfies the dynamics equations at all the collocation points.

On the interval of the boundary value problem, the domain is split up into n points, and a polynomial or series of piecewise polynomials are fit to the function evaluations at those points by solving a linear system of equations for the polynomial coefficients. This is shown for one sub-interval with a monomial basis below:
$$\begin{bmatrix}
  1 & t_1 & t_1^2  \\
  1 & t_2 & t_2^2
\end{bmatrix} \begin{bmatrix} a_1 \\ a_2 \end{bmatrix} = \begin{bmatrix} y_1 \\ y_2 \end{bmatrix}$$

for interpolating polynomial of order n-1 :
$$p_{n-1}(t) = a_1 + a_2*t + ... + a_n*t^{n-1}$$

The polynomial or piecewise polynomial approximates the trajectory across the entire domain, and is less accurate than shooting methods which can perform higher order numerical integration. However, it is guaranteed to find an approximate trajectory as long as the appropriate polynomial basis functions and sub-interval spacing are properly chosen.


## Applications of Optimal Control Theory in Commercial Applications
There is a wide variety of software designed to solve optimal control problems, with certain ones focusing on specific numerical methods. The majority use direct collocation, such as GPOPS-II, PSOPT, SOS, DIRCOL, and some use other methods such as indirect collocation (DIDO).


## References

1. "A Survey on Low-Thrust Trajectory Optimization Approaches", David Morante, et. al., 2021
2. "A review of optimization techniques in spacecraft flight trajectory design", Runqi Chai, et. al., 2019
3. "Numerical Optimal Control", Moritz Diehl, 2011
4. "Numerical Methods for Solving Optimal Control Problems", Garrett Robert Rose, 2015
5. "https://en.wikipedia.org/wiki/Trajectory_optimization", Wikipedia Article, 2022
6. "https://en.wikipedia.org/wiki/Collocation_method", Wikipedia Article, 2022
7. "An Introduction to Trajectory Optimization: How to Do Your Own Direct Collocation", Matthew Kelly, 2017
