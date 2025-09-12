Perfect 🙌 — here’s your **menu of parameter dynamics**. You can think of it as the “toolbox” for turning dead constants into living parts of your model. 

---

# 🛠️ Menu of Parameter Dynamics

### 1. **Capacity Functions** (classic)

* **Linear:**

  $$
  Flow = k \cdot Stock
  $$
* **Saturating (HalfSat / Michaelis–Menten):**

  $$
  Flow = \frac{MaxRate \cdot Stock}{HalfSat + Stock}
  $$
* **Goal-seeking:**

  $$
  Flow = \frac{(Target - Stock)}{\tau}
  $$

---

### 2. **Delays** (slow adjustment)

* Parameters adjust to reality with a lag.
* Example:

  $$
  Perceived\ Wait\ Time = DELAY1(Actual\ Wait, \tau)
  $$
* Gives realistic inertia in perception-driven flows (orders, satisfaction, churn).

---

### 3. **Thresholds / Regime Switches**

* Parameters jump when a stock crosses a threshold.
* Example:

  $$
  Mortality\ Rate = 
  \begin{cases}
  m_\text{base}, & ICU < 80\% \\
  m_\text{high}, & ICU \ge 80\%
  \end{cases}
  $$
* Useful for “tipping points” and nonlinear policies.

---

### 4. **Adaptive Stocks** (parameters as state)

* Treat the “parameter” as its own stock with learning/decay.
* Example: workforce productivity improves over time:

  $$
  \frac{dProd}{dt} = \frac{(MaxProd - Prod)}{\tau_\text{learning}}
  $$
* Then use `Prod` as a multiplier in other flows.

---

### 5. **Multiplicative Modifiers**

* Parameters scaled by another stock or flow.
* Example:

  $$
  AdEff = BaseEff \times (1 + \alpha \cdot ActiveSubs)
  $$
* Turns a flat parameter into a feedback-sensitive one.

---

### 6. **Perceptions / Expectations**

* Modeled as smoothed stocks.
* Example:

  $$
  Expected\ Price = SMOOTH(Actual\ Price, \tau)
  $$
* Affects purchasing or adoption without being a hard “capacity.”

---

### 7. **Exogenous Noise / Shocks**

* Time-varying inputs (step functions, random noise).
* Example: sudden +20% demand for 30 days.
* Not endogenous, but useful for stress-testing loops.

---

✅ With just these 7 “moves,” you can turn almost any constant slider into a living, dynamic parameter.

---

Would you like me to show how this menu maps **back onto your subscription model** (i.e. which one you’d pick to make Signups endogenous, which to make Conversion endogenous, which to make Churn endogenous)?
