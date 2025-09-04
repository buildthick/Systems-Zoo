## 1. **Hard min (literal capacity)**

$$
\text{Flow} = \min(\text{Demand}, \text{Capacity})
$$

* Very intuitive: you can’t admit more patients than beds, or start more rides than bikes.
* Used for **physical conservation**.
* Downside: discontinuous slope at the kink → can make sims jumpy.

## 3. **Saturation functions (HalfSat / Michaelis–Menten)**

$$
\text{EffectiveFraction} = \frac{\text{Resource}}{\text{Resource} + K}
$$

* Smooth tapering: approaches 0 when scarce, approaches 1 when abundant.
* HalfSat constant $K$ defines where the midpoint (50% effective) is.
* Good for “probability of access” or when users give up after searching.
* Less literal; more behavioral.

---

## 4. **Logistic capacity (S-curve)**

$$
f(R) = \frac{1}{1 + e^{-k(R - R^*)}}
$$

* Smooth S-shaped guard.
* `R*` = inflection point, `k` = steepness.
* Nice when you want symmetric transition around a “critical point” (e.g., ICU occupancy tipping into crisis).

---

## 5. **Queue-based / service time capacity**

$$
\text{Throughput} = \frac{\text{Resources}}{\text{ServiceTime}}
$$

* Classic in hospitals, call centers, factories.
* Ties capacity directly to service times.
* Linear until you add stochasticity or finite queues.

---

## 6. **Utilization ratio (fraction of max panel)**

$$
\text{Headroom} = \max(0, \text{MaxLoad} - \text{CurrentLoad})
$$

$$
\text{Admissions} = \frac{\text{Headroom}}{\text{StartTime}}
$$

* Explicitly uses “busy vs. free capacity.”
* Feels natural for staff/servers.

### How to choose

* **Physical resources (beds, bikes, inventory):** Hard min or soft min.
* **Human effort (staff, call center):** Service-time or utilization headroom.
* **Behavioral perception (customers give up):** Saturation / logistic.
* **Multiple demands sharing one pool:** Allocation fractions.
* **Slow response / outdated info:** Add a delay wrapper.

👉 The unifying idea: **Capacity = Resources ÷ Time**, but how you *gate* demand depends on whether you want hard physics, soft perception, or managerial decision-rules.

---

Want me to make you a quick **visual cheat sheet** (graphs of min vs. softmin vs. halfSat vs. logistic) so you can *see* the differences in shape?
