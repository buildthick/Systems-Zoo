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


---
---


Here’s a compact “cheat sheet” with **all three families** (queue-based, utilization/headroom, and half-sat), each with multiple concrete examples.

---

# 🔹 Queue-based (resources ÷ service time)

Formula:

$$
\text{Throughput (jobs/time)} = \frac{\text{Resources (servers)}}{\text{ServiceTime (time/job)}}
$$

**Examples**

1. **Call center**

   * 25 agents, avg call length = 6 min = 0.1 hr
   * Capacity = $25 ÷ 0.1 = 250$ calls/hr

2. **Restaurant kitchen**

   * 4 cooks, avg dish prep = 15 min = 0.25 hr
   * Capacity = $4 ÷ 0.25 = 16$ dishes/hr

3. **Manufacturing line**

   * 3 machines, avg cycle = 2 min = 1/30 hr
   * Capacity = $3 ÷ (1/30) = 90$ parts/hr

---

# 🔹 Utilization / headroom (panel size & start time)

Formulas:

$$
\text{ConcurrentCap (jobs)} = \text{Resources} \times \text{PanelSize (jobs/resource)}
$$

$$
\text{Headroom (jobs)} = \max(0, \text{ConcurrentCap} - \text{JobsInService})
$$

$$
\text{Starts (jobs/time)} = \frac{\text{Headroom (jobs)}}{\text{StartTime (time/job)}}
$$

**Examples**

1. **Hospital ward**

   * 10 doctors × 8 patients each = 80 concurrent cap
   * Current load = 72 → headroom = 8
   * Admission takes 0.5 hr/patient → starts = $8 ÷ 0.5 = 16$ admits/hr

2. **IT helpdesk tickets**

   * 6 techs × 12 tickets = 72 cap
   * Current load = 65 → headroom = 7
   * Setup = 0.25 hr/ticket → starts = $7 ÷ 0.25 = 28$ tickets/hr

3. **Car repair shop**

   * 5 bays × 2 cars = 10 cap
   * Current load = 8 → headroom = 2
   * Intake = 1 hr/car → starts = $2 ÷ 1 = 2$ cars/hr

---

# 🔹 Saturation guard / Half-Sat (smooth availability)

Formula:

$$
\text{EffectiveFraction} = \frac{\text{Resource}}{\text{Resource} + K}
$$

$$
\text{Flow} = \text{Desired} \times \text{EffectiveFraction}
$$

* $K$ = “half-saturation constant”: the resource level where only 50% of desired flow succeeds.
* Used when access probability or search effort matters.

**Examples**

1. **Bike share (user patience)**

   * Desired starts = 1000/day
   * Bikes in dock = 200
   * HalfSat $K=200$ → fraction = 200/(200+200) = 0.5
   * Actual starts = 1000 × 0.5 = 500/day

2. **Hospital supplies (probability of availability)**

   * Desired treatments = 50/day
   * Supplies on hand = 20
   * HalfSat = 10 → fraction = 20/(20+10) = 0.67
   * Actual = 33/day (2/3 of desired can be treated)

3. **Website load handling**

   * Desired requests = 10,000/s
   * Server threads available = 4000
   * HalfSat = 2000 → fraction = 4000/(4000+2000) ≈ 0.67
   * Actual served ≈ 6700/s

---

# ✅ Summary

* **Queue-based:** sequential service → throughput = resources ÷ service time.
* **Utilization/headroom:** concurrent load → flow = headroom ÷ start time.
* **Half-sat (saturation):** probabilistic access → flow = desired × (resource/(resource+K)).

Each one is the same pattern: *resources + time anchor → jobs/time*.
The difference is how you gate demand: **hard sequential, concurrent slots, or smooth availability.**

---

Want me to make you a **visual side-by-side plot** of these three forms (so you can see “hard min vs soft-sat vs capacity line” shapes)?

