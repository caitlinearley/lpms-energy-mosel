# 🌍 LPMS Energy Model – Mosel

[![Language](https://img.shields.io/badge/language-Mosel-blue.svg)](https://www.fico.com/en/products/fico-xpress-optimization)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)


---

## 🧭 Overview
This project presents a **linear programming model built in Mosel** to explore the path toward **energy independence** while managing cost, emissions, and stakeholder constraints.  

Developed as a consulting case study, the project models multiple **generation technologies** and **policy scenarios** to evaluate financial and environmental trade-offs.

Includes:
- `Power.mos` — the full optimisation model.
- `Case Study Presentation.pdf` — final report with scenario results and recommendations.

---

## ⚙️ Key Features
- The model is formulated as a linear optimisation problem and solved using Xpress Optimizer’s LP solver (typically via the simplex method)**.  
- Evaluates multiple energy sources: gas, coal, nuclear, wind, hydro, solar, and interconnects.  
- Tests emissions reductions (CO₂ and SO₂) and their impact on profitability.  
- Models seasonal variation (e.g. autumn wind multiplier).  
- Recommends optimal green-energy investments for emission-free operation.

---

## 🧩 Project Stages

### **Stage 1: Base Case**
- **Assumptions:**  
  - No solar generation.  
  - Wind fixed at 6,000 MW average.  
  - Emission limit progressively reduced by 5% steps up to 50%.  
- **Findings:**  
  - A 50% emission reduction led to losses due to limited renewable capacity.

| Metric | Base Case | 50% CO₂ Reduction |
|--------|------------|------------------|
| Revenue | £13.8 M | £13.8 M |
| Cost | £12.0 M | £15.3 M |
| Profit | **£1.8 M** | **−£1.47 M** |

---

### **Stage 2: Solar + Seasonality**
- Solar power added.  
- Autumn wind output adjusted with a seasonal multiplier.  
- 50% CO₂ reduction target maintained.  
- Tested removal of fossil and nuclear sources individually.

💡 *Finding:* Introducing solar improves sustainability, but full fossil-fuel removal without nuclear remains costly (−£7.6 M profit).

---

### **Recommendations: Green-Only Model**
- Remove output limits (except solar physical maximum).  
- Expand capacities:  
  - **Wind:** → 18 GW  
  - **Solar:** → 9 GW  
  - **Hydro:** steady 0.4 GW  
- Achieves **zero CO₂ and SO₂ emissions** with £13 M profit.

| Source | CO₂ | SO₂ | Profit | Status |
|---------|------|------|----------|----------|
| Wind + Solar + Hydro | 0 | 0 | £13.1 M | ✅ Fully clean |

---

## 🧮 Model Logic
The Mosel model formulates a **linear optimisation problem**:

**Objective:**  
> Maximise total profit = Revenue – Cost  

**Decision variables:**  
Power generation per source and time period (MW).

**Constraints include:**  
- Demand satisfaction per period  
- Emission limits (CO₂, SO₂)  
- Capacity limits (modifiable by scenario)  
- Technology availability (e.g. solar ↔ daylight, wind ↔ season)

Solver: **Dual Simplex (Mosel built-in solver)**

---
## 📊 Results

### **Stage 1 – Base Case**
- **Assumptions:** No solar; wind fixed at 6 GW; incremental CO₂ reduction up to 50%.  
- **Finding:** Profit declines sharply as emission limits tighten.

| Metric | Base Case | 50 % CO₂ Reduction |
|:-------|-----------:|-------------------:|
| Revenue (£) | 13,824,000 | 13,824,000 |
| Cost (£) | 12,016,333 | 15,290,000 |
| Profit (£) | **+1,807,667** | **−1,466,000** |
| CO₂ Change | 0 % | −50 % |
| Sulphur Change | — | — |

🟢 **Interpretation:**  
At 50 % emission reduction, the model becomes loss-making. The island cannot maintain profitability with current renewable capacity.

---

### **Stage 2 – Solar Implementation & Seasonal Analysis**
- Solar generation introduced.  
- Wind adjusted using an autumn multiplier.  
- 50 % CO₂ cut maintained.  
- Explored “no gas,” “no coal,” and “no nuclear” scenarios.

| Scenario | CO₂ (units) | SO₂ (units) | Profit (£) | Comment |
|:----------|-------------:|-------------:|-------------:|:---------|
| Full Mix (with Solar) | 100 000 | 30 000 | −7,625,778 | Emission target met but costly |
| No Gas | 90 000 | 30 000 | −9,873,000 | Largest loss |
| No Coal | 100 000 | 0 | −7,625,778 | Moderate loss |
| No Nuclear | 100 000 | 0 | −13,623,000 | Unprofitable |

🟠 **Interpretation:**  
Solar improves sustainability but cannot yet offset the loss of fossil or nuclear generation under strict emissions constraints.

---

### **Stage 3 – Recommended Scenario (100 % Renewable)**
- Removed all output restrictions (except solar’s physical limit).  
- Expanded capacities:  
  - **Wind:** → 18 GW  
  - **Solar:** → 9 GW  
  - **Hydro:** → 0.4 GW  
- Achieves **zero CO₂ and SO₂ emissions** with continued profitability.

| Metric | Value |
|:--------|------:|
| Total Revenue (£) | 13,099,200 |
| Total Cost (£) | — |
| **Profit (£)** | **13,099,200** |
| CO₂ Emissions (tonnes) | 0 |
| SO₂ Emissions (tonnes) | 0 |
| Primary Sources | Wind, Solar, Hydro |

🟩 **Interpretation:**  
A clean-energy mix relying on wind, solar, and hydro achieves full emission elimination *and* maintains profitability — a viable, future-proof solution.

