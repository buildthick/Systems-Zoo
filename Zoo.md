
# Core building blocks

**General stock-and-flow form**

* Continuous: $\displaystyle \frac{dS}{dt} = \text{Inflow}(t) - \text{Outflow}(t)$
* Discrete: $\displaystyle S_{t+1} = S_t + (\text{Inflow}_t - \text{Outflow}_t)\,\Delta t$

Where:

* $S$ = stock (level)
* Inflow/Outflow = rates (per unit time)
* $\Delta t$ = time step

---

# Reinforcing loops (R)

## R1. Pure compounding growth (autocatalytic)

$$
\frac{dX}{dt} = rX
\quad\Rightarrow\quad
X(t) = X_0 e^{rt}
$$

Discrete: $X_{t+1} = X_t(1 + r\Delta t)$

* $X$ = population, users, capital, etc.
* $r>0$ = growth rate (per time)

## R2. Word-of-mouth / virality

$$
\frac{dU}{dt} = \beta U (M-U)
$$

* $U$ = current adopters/users
* $M$ = addressable market size
* $\beta$ = contact/contagion coefficient

(When $M$ is large relative to $U$, this behaves like $dU/dt\approx \beta MU$, i.e., R1.)

## R3. Success-to-the-successful (resource reallocation)

Two competitors $A,B$ vying for shared resource $R$:

$$
\frac{dA}{dt} = \alpha \frac{A}{A+B}\,R,\qquad
\frac{dB}{dt} = \alpha \frac{B}{A+B}\,R
$$

* $A,B$ = performance/size of each actor
* $R$ = new resources arriving per time
* $\alpha$ = conversion of resources into performance
  The share term $\frac{A}{A+B}$ reinforces whoever is currently ahead.

## R4. Compounding learning curve (experience effects)

$$
\frac{dC}{dt} = -\eta C \frac{dQ}{dt}
$$

* $C$ = unit cost
* $Q$ = cumulative output (a stock: $dQ/dt = q$ = production rate)
* $\eta>0$ = learning elasticity
  As $Q$ grows, costs fall, which can fuel more demand → more $Q$ (an indirect R loop).

---

# Balancing loops (B)

## B1. Simple goal-seeking (first-order)

$$
\frac{dY}{dt} = -k \,(Y - Y^{*})
$$

$$
Y(t) = Y^{\ast} + \bigl( Y_{0} - Y^{\ast} \bigr) e^{-k t}
$$

Discrete: 

$$
Y_{t+1} = Y_{t} - k \,\Delta t \,(Y_{t} - Y^{*})
$$

* $Y$ = controlled variable  
* $Y^{*}$ = goal/target  
* $k>0$ = adjustment speed


## B2. Inventory control (stock + proportional correction)

$$
\frac{dI}{dt} = O - D,\qquad
O = D + k(I^* - I)
$$

* $I$ = inventory stock
* $O$ = order/production rate
* $D$ = demand rate (exogenous or modeled)
* $I^*$ = inventory target
* $k>0$ = correction gain

## B3. Price equilibration (supply–demand)

$$
\frac{dP}{dt} = \gamma\,(Q_D(P) - Q_S(P))
$$

* $P$ = price
* $Q_D, Q_S$ = demand and supply as functions of $P$
* $\gamma>0$ = price adjustment speed
  At equilibrium $Q_D(P^*)=Q_S(P^*)$, deviations are corrected (balancing).

## B4. Error correction with delay (oscillation-prone)

$$
\frac{dY}{dt} = -k\,[Y(t-\tau) - Y^*]
$$

* $\tau>0$ = information/actuation delay
  Sufficient delay + high $k$ → overshoot & oscillation (still fundamentally balancing).

---

# Mixed loops (R + B together)

## M1. Logistic growth (growth with carrying capacity)

$$
\frac{dX}{dt} = rX\left(1 - \frac{X}{K}\right)
$$

* $r>0$ = intrinsic growth (reinforcing)
* $K>0$ = carrying capacity (balancing)
  R dominates when $X\ll K$; B dominates near $K$.

## M2. Limits to growth (generic constraining resource)

$$
\frac{dX}{dt} = rX \cdot f(R),\qquad
\frac{dR}{dt} = a - bX - cR
$$

* $X$ = growing focal stock
* $R$ = limiting resource (e.g., attention, capacity)
* $f(R)\in(0,1]$ increasing in $R$ (e.g., $f(R)=\frac{R}{R+h}$)
* $a$ = replenishment of $R$; $b$ = depletion by $X$; $c$ = decay
  R loop in $X$; B enters via depletion of $R$.

## M3. Bass diffusion (innovation + imitation)

$$
\frac{dA}{dt} = p(M-A) + q\,\frac{A}{M}(M-A)
$$

* $A$ = adopters, $M$ = market size
* $p$ = innovation (external) coefficient (B-like saturator)
* $q$ = imitation (R-like) coefficient

## M4. Epidemic SIR (infection R vs recovery B)

$$
\frac{dS}{dt} = -\beta \frac{S I}{N},\quad
\frac{dI}{dt} = \beta \frac{S I}{N} - \gamma I,\quad
\frac{dR}{dt} = \gamma I
$$

* $S,I,R$ = susceptible, infectious, removed
* $\beta$ = transmission rate, $\gamma$ = recovery rate
  Reinforcing: infections grow via $SI$; Balancing: recovery drains $I$.

## M5. Predator–prey (Lotka-Volterra)

$$
\frac{dH}{dt} = aH - bHP,\qquad
\frac{dP}{dt} = -cP + dHP
$$

* $H$ = prey, $P$ = predator
* $a$ = prey growth; $b$ = predation; $c$ = predator death; $d$ = conversion
  R in each population via interaction terms; B via losses.

---

# “Human systems” controls (practical B variants)

## B5. Proportional-Integral-Derivative (PID) control

$$
u(t) = K_P e(t) + K_I \int_0^t e(\tau)\,d\tau + K_D \frac{de}{dt},\quad
e(t) = Y^* - Y(t)
$$

Actuator: $\frac{dY}{dt} = g(u,\,\cdot)$ (domain-specific)

* $u$ = control action; $e$ = error
* $K_P,K_I,K_D$ = gains
  Balances to target with better stability/overshoot control.

## B6. Goal erosion (moving goal under pressure)

$$
\frac{dY}{dt} = -k\,(Y - Y^{\ast}), \qquad
\frac{dY^{\ast}}{dt} = -\phi\,\bigl(\text{Pressure}(Y)\bigr)
$$


* $Y^*$ drifts downward under pressure $\phi>0$, weakening the balancing loop (archetype: “Eroding Goals”).

---

# Resource competition (R vs B in markets/ops)

## M6. Capacity-constrained growth (throughput saturates)

$$
\frac{dQ}{dt} = \min\{ \lambda D,\; \mu C \}
$$

* $Q$ = completed work (cumulative)
* $D$ = demand stock or rate; $\lambda$ = conversion of demand to starts
* $C$ = capacity; $\mu$ = service rate per capacity unit
  As $D$ swells, R-like intake grows until capacity $\mu C$ imposes B.

## M7. Queue (Little’s Law core)

$$
\frac{dWIP}{dt} = \text{Arrival} - \text{Departure},\qquad
\text{LeadTime} \approx \frac{WIP}{\text{Throughput}}
$$

* $WIP$ grows → LeadTime rises → policies reduce arrivals (balancing), or add capacity (which can re-enable reinforcing arrival growth).

---

# Variable glossary (common across models)

* $X,Y,I,A,U,Q,H,P,S,I,R$ (contextual) = stocks/levels named in each loop
* $r,k,\beta,\gamma,\alpha,\eta,\lambda,\mu$ = positive rate/elasticity parameters
* $K, M, I^*, Y^*$ = capacities/market sizes/targets
* $\tau$ = delay; $\Delta t$ = discrete time step
* $f(\cdot), Q_D(\cdot), Q_S(\cdot), g(\cdot)$ = domain-specific functions (monotone or specified as needed)
