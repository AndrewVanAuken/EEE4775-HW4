# EEE4775 HW4
**Name**: Andrew VanAuken

## Part A – Liu & Layland practice
### Set 1: τ₁ (T=10, C=2) · τ₂ (T=25, C=5) · τ₃ (T=100, C=20)
**Total Utilization (U):** 2/5 + 5/25 + 20/100 = 0.60

**RMS Sufficient Bound:** 3(2^1/3 - 1) = 0.7798

**Feasibility Conclusion:**  Since U = 0.6000 less than or equal to 0.7798, the task set is guaranteed to be RMS-feasible and EDF-feasible.

### Set 2: τ₁ (T=4, C=1) · τ₂ (T=6, C=2) · τ₃ (T=10, C=3)
**Total Utilization (U):** 1/4 + 2/6 + 3/10 = 0.8833

**RMS Sufficient Bound:** 3(2^1/3 - 1) = 0.7798

**Feasibility Conclusion:**   Since U = 0.8833 > 0.7798, the bound is inconclusive for RMS. However, since U is less than or equal to 1, it is guaranteed to be EDF-feasible.

### Set 3: τ₁ (T=5, C=1) · τ₂ (T=10, C=2) · τ₃ (T=20, C=4) · τ₄ (T=50, C=10)
**Total Utilization (U):** 1/5 + 2/10 + 4/20 + 10/50 = 0.80

**RMS Sufficient Bound:** 4(2^1/4 - 1) = 0.7568

**Feasibility Conclusion:**   Since U = 0.80 > 0.7798, the bound is inconclusive for RMS. However, since U is less than or equal to 1, it is guaranteed to be EDF-feasible.

---

## Part B – Response-Time Analysis
### Task 1 (τ₁)
**Iterations:** No higher-priority tasks interfere. R1 = C1 = 2ms

**Status:** Feasible

### Task 2 (τ₂)
**Iterations:**
- (R2)^0 = C2 = 5ms
- (R2)^1 = 5 + (5/10) * 2 = 7ms
- (R2)^2 = 5 + (7/10) * 2 = 7ms

**Status:** Feasible

### Task 3 (τ₃)
**Iterations:**
- (R3)^0 = C3 = 20ms
- (R3)^1 = 20 + (20/10) * 2  + (20/25) * 5 = 29ms
- (R3)^2 = 20 + (29/10) * 2 + (29/25) * 5 = 36ms
- (R3)^3 = 20 + (36/10) * 2 + (36/25) * 5 = 38ms
- (R3)^4 = 20 + (38/10) * 2 + (38/25) * 5 = 36ms

**Status:** Feasible

---

## Part C – A failure scenario
C4 scales from 10ms to 25ms
U = 1/5 + 2/10 + 4/20 + 25/50 = 1.1

The set is not RMS-feasible by the bound. Because U > 1.0, the processor is over-utilized, and RTA will confirm this failure by showing that τ₄ diverges past D4 = 50ms.

Because RMS utilizes fixed priorities based entirely on task periods, changes in a lower-priority task τ₄ cannot interfere with higher-priority tasks τ₁, τ₂.

**RTA for τ₁:** R1 = C1 = 1ms (Feasible)

**RTA for τ₂:** 
- (R2)^0 = 2 
- (R2)^1 = 2 + 2/5 * 1 = 3
- (R2)^2 = 2 + 3/5 * 1 = 3ms (Feasible)

**Design Modification 1:** Period Extension. 
- Increase τ₄ from 50ms to greater than or equal to 125ms. This drops τ₄'s utilization to less than or equal to 0.20, dragging total utilization back to less than or equal to 0.80, making the system schedule-feasible without modifying hardware capacity.

**Design Modification 2:** Task Splitting. 
- Subdivide τ₄ into three sequential sub-tasks across separate periods, or optimize algorithms to bring C4 less than or equal to 20ms. Trimming C4 ensures total utilization drops back to U less than equal to 1.0, satisfying general uniprocessor scheduling conditions.

---

## Part D – Industry anchor
In safety-critical avionics, scheduling analysis provides mandatory compliance evidence. A DO-178C team uses tools like RapiTime to measure worst-case execution times (WCETs) and verify deadline adherence. Engineers archive task periods, priorities, measured WCETs, utilization, and RTA results into the project’s formal verification records. During audits, priorities are reviewed to guarantee safety-critical functions receive correct scheduling precedence. If RTA indicates a deadline violation, the failure blocks certification. Engineers resolve misses by optimizing code to reduce execution time, lengthening task periods, or splitting large operations into smaller tasks. The timing analysis is then re-run to provide objective evidence that the real-time system remains deterministic under worst-case operating conditions.

**Citation**

https://www.rapitasystems.com/blog/do-178b-do-178c-and-worst-case-execution-time

Google AI was used as well
