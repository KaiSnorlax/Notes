Finite Element Method
* Numerical method for solving differential equations
* Subdivide a large system into smaller, simpler parts -> Finite elements
* Applications
	* Structural analysis
	* Heat transfer
	* Fluid flow
	* Mass transport

1 D Mass Spring System
* 1D chain of masses and springs
* Hooke's Law: $F=kx$, Newtons Law: $F=ma$
* Numerical Integration: Euler, Verlet, ect.
* Simulate 3-mass chain with one end displaced
#### Process (No Dampening)
Initial Conditions
$x_1(t=0)=0$
$x_2(t=0)=0$

acceleration $x_1''=x_1(t=0)+x_1''dt$ -> velocity at $t+dt$
velocity $x'_1=x_1'(t)+x_1''(t+dt)dt$
position $x_1(t_0+dt)=x_1(t) +x_1'(t+dt)dt$

#### Process (With Dampening)
Initial Conditions
$x_1(t=0)=0$
$x_2(t=0)=0$

acceleration $x_1''=x_1(t=0)+x_1''dt$ -> velocity at $t+dt$
velocity $x'_1=x_1'(t)+x_1''(t+dt)dt$
position $x_1(t_0+dt)=x_1(t) +x_1'(t+dt)dt$

#### Equilibrium conditions
$F_1=0=-kx_1-k(x_1-x_2)$
$F_2=0=-k(x_2-x_1)-(x_2-1)$

#### Sequential Equilibrium
Will not show how the system moves, it only shows where the system will end up

#### Improvements for Realism
- Material Stiffness --> Variable spring constants
- Bending Resistance --> Add diagonal and bend springs

#### Simulating Deformations
For each node
* Conpute total spring forces from connected neighbors
* Add external forces (gravity or weight)
* Update position iteratively
* Keep fixed nodes in place

#### Applications
- Wave propagation of mechanical and acoustics waves
- Solid mechanics
- Neuroscience
- Mechanical and Civil Engineering

#### Limitations
- Fixed topology
- Uses empirical spring constants
- No connection to PDEs or material models
- Can be numerically unstable
-
$\fr$