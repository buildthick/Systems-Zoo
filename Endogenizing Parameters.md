
# 🛠️ Menu of Parameter Dynamics

### 1. Capacity Functions (classic)

* **Linear:**
  $Flow = k \cdot Stock$

* **Saturating (HalfSat / Michaelis–Menten):**
  $Flow = \frac{MaxRate \cdot Stock}{HalfSat + Stock}$

* **Goal-seeking:**
  $Flow = \frac{Target - Stock}{\tau}$

---

### 2. Delays (slow adjustment)

Parameters adjust to reality with a lag.

Example:
$PerceivedWaitTime = DELAY1(ActualWait, \tau)$

---

### 3. Thresholds / Regime Switches

Parameters jump when a stock crosses a threshold.

Example:

$$
MortalityRate =
\begin{cases}
m_{base}, & ICU < 0.8 \cdot Capacity \\
m_{high}, & ICU \geq 0.8 \cdot Capacity
\end{cases}
$$

---

### 4. Adaptive Stocks (parameters as state)

Treat the “parameter” as its own stock with learning/decay.

Example:
$\frac{dProd}{dt} = \frac{MaxProd - Prod}{\tau_{learning}}$

---

### 5. Multiplicative Modifiers

Parameters scaled by another stock or flow.

Example:
$AdEff = BaseEff \cdot (1 + \alpha \cdot ActiveSubs)$

---

### 6. Perceptions / Expectations

Modeled as smoothed stocks.

Example:
$ExpectedPrice = SMOOTH(ActualPrice, \tau)$

---

### 7. Exogenous Noise / Shocks

Time-varying inputs (step functions, random noise).

Example:

* Sudden $+20\%$ demand for 30 days
* $Signups = BaseSignups + Shock(t)$

---

✅ With just these 7 “moves,” you can turn almost any constant slider into a living, dynamic parameter.
