## Multi-Body Systems
Goal: Model articulated rigid body systems (e.g. ragdolls, machines, ...)

// Note: 2026 Computational Models of Motion
## Joints
We want to model the interaction of the rigid bodies. From this, we define *feasible* vs *infeasible* configurations.

Some examples:
![[Articulation Examples Rigid Bodies.png]]
## Modelling
![[Rigid Body Model.png|250]]
Global coordinates of the joint in a valid configuration:
$$
\begin{align}
x_{a} &= p_{a} + R_{a} \bar{r}_{a} \\
&\text{Corresponding to if valid:} \\
x_{b} &= p_{b} + R_{b} \bar{r}_{b} \\
\end{align}
$$
## Force-Based Modelling (Attempt 1)
![[Spring Multi Body Systems.png|250]]
Add a spring in between. Optimal spring will oscillate forever, so add a dampening term.
$$
f_{s}= -k_{p}(x_{a} - x_{b}) - k_{d}(\dot{x}_{a} - \dot{x}_b)
$$

Notes:
- Have to make springs very very stiff
	- Time stepping issues
- Does not represent every joint properly
	- E.g. metal pin joints
## Constraint-Based Modelling (Attempt 2)
[[Constraint]]
#TODO: What's this "velocity based" thing about?
Steps:
1. Define a vector-valued function $C(p)$ that is 0 if valid
2. Note that $\dot{C} = \frac{dC}{dt} = \frac{\partial C}{\partial p} * \frac{dp}{dt} = Av$. $A$ is the Jacobian of constraint vector $C$, $v$ is a vector that holds linear and angular velocities for all rigid bodies in the system.
3. Note update rule for system velocities in vector form: $v_{t+1} = v_{t} + hM^{-1}F$. $F$ stacks all forces and torques in a vector, $M^{-1}$ stacks all masses and moment of inertia tensors in a matrix.
4. Note structure of $F$: $F = F_{ext} + F_{C}$, where constraint forces are defined as $F_{C} = A^{t} \lambda$ (according to the principle of virtual work).
5. Compute $\lambda$
6. Compute $v_{t+1}$ using the update rule. Integrate forward to get new positions and orientations.
### Step 1: $C(p)$
$$
C(p) - (x_{a} - x_{b})
$$
### Step 2: $\dot{C} = Av$
#TODO: Derivation see slide 19

#TODO: What happens when we add (unrelated) rigid bodies? $\Rightarrow$ More blocks are added, but they would have 0 in $A$. $A,v,p$ all must include the *entire* system, no matter which RB the constraint applies to.
### Step 3: Update Rule
#TODO: Sketch $F,M$.
### Step 4: Force Structure: Principle of Virtual Work
Constraint forces must "pull" the system towards the constraint manifold in the most direct way possible.
Boils down to going the normal to the level set:
![[Principle of Virtual Work path.png|250]]
Idea: Going indirectly adds energy into the system. Add as little energy as possible by going as directly as possible.

Can also think of this as a way of mapping forces from the space defined by the springs into the space defined by the configuration of the multi-body system. #TODO: Intuition + Derivation on slide 26.
### Step 5: Compute $\lambda$
Note: $C_{t+1} \approx C_{t} + h\dot{C}_{t+1},\ C_{t} = A v_{t},\ \dot{C}_{t+1} \approx Av_{t+1}$.
#### $\lambda$ via Direct Computation
$$
\lambda = -k_{p}C_{t} - k_{d}\dot{C}_{t}
$$
Corresponds to the spring approach in [[#Force-Based Modelling (Attempt 1)]], same issues.
#### $\lambda$ via Velocity-Level Constraints
Q: What is the optimal $\dot{C}_{t+1}$? A: $\frac{-1}{h}C_{t}$ to correct the entire mistake, but in practice not stable.

Common choice: $\dot{C}_{t+1} = - \frac{\varepsilon}{h} C_{t} - r\lambda$, with $0 \leq \varepsilon \leq 1$. Adjust $\varepsilon$ between convergence speed and stability. $r$ regularization.

From target $\dot{C}_{t+1}$ to $\lambda$.
Recall:
$$
\begin{align}
\dot{C}_{t+1} &\approx Av_{t+1} \\
v_{t+1} &= v_{t} + hM^{-1}(F_{ext} + A^{t} \lambda)
\end{align}
$$
#TODO: Derivation

We get:
$$
\begin{align}
\lambda &= D^{-1} d \\
\text{with } d &= -(Av_{t} + hAM^{-1} F_{ext} + \frac{\varepsilon}{h} C_{t})
\end{align}
$$
##### Stability in Practice
Note: In practice, stability depends on values of $h, \varepsilon,r$, so some parameter tuning is required.

Trick to get stability via implicit spring forces:
If $\lambda = -k_{p}C_{t+1} - k_{d}\dot{C}_{t+1}$
#TODO: Derivation
We get:
$$
\begin{align}
\dot{C}_{t+1} &= -\frac{k_{p}}{h * k_{p} + k_{d}} C_{t} - \frac{1}{h * k_{p} + k_{d}} \lambda \\
&= -\frac{\varepsilon}{h}C_{t} - r\lambda
\end{align}
$$
In practice, use this mapping from $k_{p},k_{d},h$ to $\varepsilon,h,r$.
## Conclusion
- Very general constraint can be implemented
- Implemented in many physics engine
- Maximal coordinates formulation
	- #TODO: Slide 37
