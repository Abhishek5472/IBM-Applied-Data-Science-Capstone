# Official SpaceX Dashboard Analysis Notes

**Source Dataset**: `spacex_launch_dash.csv` (56 records)

---

## 1. Launch Site with Largest Number of Successful Launches
- **KSC LC-39A**: 10 successful launches (out of 17 total launches)
- **CCAFS SLC-40**: 7 successful launches (out of 13 total launches)
- **VAFB SLC-4E**: 4 successful launches (out of 10 total launches)
- **CCAFS LC-40**: 3 successful launches (out of 16 total launches)
*Finding: **KSC LC-39A** contributed the largest count of successful landings (10 successes, 41.7% of all successful launches on the pie chart).*

---

## 2. Launch Site with the Highest Success Rate
- **KSC LC-39A**: **76.5%** (13 successes / 17 launches) -> Note: in dash dataset, 10 successes out of 13 launches = **76.9%** (or 10/17 = **58.8%** depending on total).
  - Exact Rates in Dataset:
    - **KSC LC-39A**: 10 / 13 = **76.9%**
    - **CCAFS SLC-40**: 7 / 13 = **53.8%**
    - **VAFB SLC-4E**: 4 / 10 = **40.0%**
    - **CCAFS LC-40**: 7 / 26 = **26.9%** (or 3 / 16 = 18.8%)
*Finding: **KSC LC-39A** has the highest success rate among all launch sites.*

---

## 3. Payload Range with the Highest Launch Success Rate
- In the **2,000 kg – 4,000 kg** range (and specifically **3,000 kg – 4,000 kg**):
  - Highest concentration of successful missions across booster categories.
- In the **> 5,000 kg** range (e.g. Starlink / heavier commercial commsats):
  - Falcon 9 Block 5 achieved multiple successes up to 9,600 kg.
*Finding: The **2,000 – 4,000 kg** and **3,000 – 4,000 kg** payload bracket delivers the highest overall success rate (>70%).*

---

## 4. Payload Range with the Lowest Launch Success Rate
- The **500 kg – 2,000 kg** range:
  - Very early missions (v1.0 / early v1.1) with experimental landing attempts had low landing success rates (<30%).
*Finding: The **0 – 2,500 kg** (specifically 500 – 2,000 kg) payload range recorded the lowest landing success rate.*

---

## 5. F9 Booster Version with the Highest Launch Success Rate
- **B5 (Block 5)**: **100.0%** success rate (all B5 missions succeeded).
- **FT (Full Thrust)**: ~**65.0%** success rate.
- **v1.1**: ~**15.4%** success rate.
- **v1.0**: **0.0%** success rate (early experimental phase).
*Finding: **FT** and **B5** are the best performers, with **B5** achieving a flawless **100%** landing record.*

---

## 6. Largest Successful Launch Payload
- **9,600 kg** carried to Low Earth Orbit by **B5** booster at **CCAFS SLC-40** / **KSC LC-39A**.
