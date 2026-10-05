# IBM Applied Data Science Capstone: SpaceX Falcon 9 First-Stage Landing Prediction

**Author**: Abhishek Kulkarni  
**Repository**: [IBM-Applied-Data-Science-Capstone](https://github.com/Abhishek5472/IBM-Applied-Data-Science-Capstone)  
**Credential**: IBM Data Science Professional Certificate (Coursera)  

---

## 🚀 Executive Summary & Project Overview

SpaceX has revolutionized access to orbit by developing the world’s first reusable orbital-class rocket, the **Falcon 9**. While traditional launch providers expend first-stage boosters costing upward of **$165 million** per launch, SpaceX charges roughly **$62 million** for a Falcon 9 flight—a cost reduction driven almost entirely by booster recovery and reuse.

This capstone project applies the complete data science lifecycle—from raw REST API data ingestion and BeautifulSoup web scraping to SQL analytics, interactive geospatial mapping with Folium, responsive dashboard development with Plotly Dash, and supervised machine learning classification.

The primary objective is to **predict whether the Falcon 9 first stage will land successfully**, empowering commercial competitors to assess launch costs, evaluate tender competitiveness, and optimize bid pricing against SpaceX.

---

## 📊 Key Findings & Results Summary

| Metric / Dimension | Executed Result | Analysis & Insight |
| :--- | :--- | :--- |
| **Total Analyzed Missions** | **90 Falcon 9 Flights** | Canonical historical mission record (2010 – 2020) |
| **Successful Landings** | **60 Landings** | Landings on Drone Ships (ASDS), Ground Pads (RTLS), and ocean |
| **Unsuccessful / Expendable** | **30 Missions** | Crashes, ocean splashes, or intentional expendable launches |
| **Baseline Success Rate** | **66.7% (66.67%)** | Program success grew from 0% (2010-2012) to >80% (2017+) |
| **Highest Success Launch Site** | **KSC LC-39A (76.9%)** | 10 successes out of 13 flights in the dashboard dataset |
| **Most Active Launch Site** | **CCAFS SLC-40 (55 flights)** | Serves primary commercial and cargo resupply traffic |
| **Optimal Payload Window** | **2,000 – 4,000 kg** | Yields the highest cluster of successful landing recoveries |
| **Top Performing Booster** | **Falcon 9 Block 5 (100%)** | 100% recovery record in evaluated dataset (FT: 66.7%) |
| **Classification Accuracy** | **83.33% across all models** | 15 / 18 correct test classifications (zero false negatives) |
| **Top Validation Model** | **Decision Tree (87.50% CV)** | Outperformed on k-fold CV across parameter grid search |

---

## 🛠 Project Architecture & Methodology

The project follows a rigorous 7-stage analytical pipeline:

```
SpaceX REST API & Wikipedia
            ↓
Data Wrangling & Binary Class Engineering (0=Unsuccessful, 1=Successful)
            ↓
Exploratory Data Analysis (Seaborn & Matplotlib)
            ↓
Relational Query Analytics (SQLite & ipython-sql)
            ↓
Geospatial Proximity Analysis (Folium & Leaflet MarkerClusters)
            ↓
Interactive Analytical Dashboard (Plotly Dash & Callbacks)
            ↓
Supervised Machine Learning & Hyperparameter Tuning (GridSearchCV)
```

---

## 📁 Repository Structure

```
├── notebooks/
│   ├── 01_data_collection_api.ipynb            # SpaceX REST API data ingestion & normalization
│   ├── 02_web_scraping.ipynb                   # BeautifulSoup extraction of Falcon 9 launch history
│   ├── 03_data_wrangling.ipynb                 # Missing value handling & binary target creation
│   ├── 04_eda_visualization.ipynb              # Visual analysis (Seaborn/Matplotlib) & dummy encoding
│   ├── 05_eda_sql.ipynb                        # SQLite analytical database queries
│   ├── 06_folium_launch_site_location.ipynb    # Geospatial analysis, coastline/infrastructure distances
│   └── 07_predictive_analysis_classification.ipynb # Logistic Regression, SVM, Tree, KNN tuning & evaluation
├── data/
│   ├── dataset_part_1.csv                      # Raw normalized launch records (90 rows, 17 cols)
│   ├── dataset_part_2.csv                      # Cleaned dataset with Class target (90 rows, 18 cols)
│   ├── dataset_part_3.csv                      # One-hot encoded feature matrix (90 rows, 80 cols)
│   ├── spacex_web_scraped.csv                  # Scraped Wikipedia launch records (121 rows, 11 cols)
│   ├── spacex_launch_dash.csv                  # Dataset powering the interactive Dash app
│   └── spacex_launch_geo.csv                   # Geospatial dataset with site coordinates
├── dashboard/
│   ├── spacex_dash_app.py                      # Interactive Plotly Dash web application
│   ├── spacex_launch_dash.csv                  # App data source
│   └── DASHBOARD_ANALYSIS_NOTES.md             # Data-driven answers to official dashboard questions
├── interactive_maps/
│   └── spacex_launch_site_map.html             # Standalone interactive Folium/Leaflet launch map
├── presentation/
│   ├── FINAL_IBM_APPLIED_DATA_SCIENCE_CAPSTONE.pptx # Comprehensive 22-slide stakeholder report
│   └── FINAL_IBM_APPLIED_DATA_SCIENCE_CAPSTONE.pdf  # High-fidelity PDF submission document
└── screenshots/
    ├── folium/                                 # Maps: all sites, clusters, coastline & infrastructure
    ├── dashboard/                              # Dash app states: all sites, dropdowns, site views, slider
    ├── eda/                                    # 6 high-resolution exploratory data charts
    └── ml/                                     # Confusion matrix & model comparison bar chart
```

---

## 🔬 Detailed Phase Summaries

### 1. Data Collection (API & Web Scraping)
- **SpaceX REST API (`data_collection_api.ipynb`)**: Queried endpoints for launches, rockets, payloads, launchpads, and cores. Normalised nested JSON data, filtered for Falcon 9, extracted sub-attributes, and handled missing payload values with mean imputation (`6,104.96 kg`). Produced `dataset_part_1.csv` (90 rows, 17 columns).
- **Web Scraping (`web_scraping.ipynb`)**: Extracted Falcon 9 historical launches from Wikipedia using `BeautifulSoup`. Handled multi-row HTML tables, regex string cleanup, and extracted dates, payloads, booster serials, and launch outcomes. Produced `spacex_web_scraped.csv` (121 records).

### 2. Data Wrangling (`data_wrangling.ipynb`)
- Analyzed launch site distributions: **CCAFS SLC 40** (55), **KSC LC 39A** (22), **VAFB SLC 4E** (13).
- Defined landing outcome categories:
  - *Successful*: `True ASDS`, `True RTLS`, `True Ocean` (60 instances).
  - *Unsuccessful*: `False ASDS`, `False RTLS`, `False Ocean`, `None ASDS`, `None None` (30 instances).
- Engineered the binary target `Class`: **1** for success, **0** for failure. Overall baseline success: **66.67%**.
- Exported `dataset_part_2.csv` (90 rows, 18 columns).

### 3. Exploratory Data Analysis with Visualization (`eda_visualization.ipynb`)
Generated 6 key analytical charts:
1. **Flight Number vs. Launch Site**: Shows early flights concentrated at CCAFS; higher flight numbers associate with dramatic landing improvements.
2. **Payload Mass vs. Launch Site**: Heavy payloads (>8,000 kg) are predominantly launched from CCAFS and KSC, with higher success rates.
3. **Success Rate vs. Orbit Type**: Orbits ES-L1, GEO, HEO, and SSO achieved **100%** landing success; GTO achieved ~51.9%.
4. **Flight Number vs. Orbit Type**: Shift over time from low-earth orbit (LEO/ISS) to polar (PO) and high-density Starlink (VLEO) constellations.
5. **Payload Mass vs. Orbit Type**: Polar orbit (PO) supports medium payloads, while GTO and VLEO support high-mass missions.
6. **Yearly Success Trend**: Success rate rose from **0% in 2010** to **>80% by 2020**, illustrating learning-curve economics.
- Performed one-hot encoding on categorical variables (`Orbit`, `LaunchSite`, `LandingPad`, `Serial`), yielding `dataset_part_3.csv` (90 rows, 80 numerical features).

### 4. Relational Data Exploration with SQL (`eda_sql.ipynb`)
Executed SQLite queries on `SPACEXTABLE`:
- **Unique Launch Sites**: CCAFS LC-40, CCAFS SLC-40, KSC LC-39A, VAFB SLC-4E.
- **5 Sites starting with 'CCA'**: CCAFS LC-40 records.
- **NASA (CRS) Total Payload**: **45,596 kg**.
- **Average Payload Mass (Booster F9 v1.1)**: **2,928.4 kg** (Exact match) / **2,534.7 kg** (including all sub-variants).
- **First Ground Pad Landing Date**: **2015-12-22** (Falcon 9 Flight 20).
- **Drone Ship Success with Payload 4,000–6,000 kg**: `F9 FT B1022`, `F9 FT B1026`, `F9 FT B1021.2`, `F9 FT B1031.2`.
- **Mission Outcomes**: 98 Success, 1 Failure in-flight, 1 Success with unclear payload, 1 Success (trailing space).
- **Max Payload Boosters**: 12 Starlink missions carrying **15,600 kg** (e.g. `F9 B5 B1048.4`, `B1049.4`).
- **2015 Drone Ship Failures**: January (`F9 v1.1 B1012`) and April (`F9 v1.1 B1015`) at CCAFS LC-40.
- **Outcome Rankings (2010-06-04 to 2017-03-20)**: `No attempt` (10), `Success (drone ship)` (5), `Failure (drone ship)` (5), `Success (ground pad)` (3).

### 5. Interactive Geospatial Analytics with Folium (`folium_launch_site_location.ipynb`)
- Built Leaflet/Folium interactive maps with OpenStreetMap tiles.
- Added color-coded Circle overlays and text labels for all 4 launch complexes.
- Implemented `MarkerCluster` with green (success) and red (failure) outcome icons.
- Measured proximity from **CCAFS SLC-40** using the Haversine distance formula:
  - **Coastline**: **0.51 KM** (ensures flight trajectory over open water for safety).
  - **Highway (Samuel C. Phillips Pkwy)**: **0.58 KM** (rapid logistics access).
  - **Railway (NASA Railroad)**: **1.28 KM** (heavy stage and booster transport).
  - **City (Cape Canaveral)**: **18.17 KM** (safe blast and acoustic buffer).
- Exported interactive map to `interactive_maps/spacex_launch_site_map.html`.

### 6. Interactive Dashboard with Plotly Dash (`spacex_dash_app.py`)
- Configured dropdown selector for launch sites and dynamic range slider for payload mass (0–10,000 kg).
- Callback 1: Generates pie chart showing total successful launches by site or success-vs-failure breakdown.
- Callback 2: Generates scatter plot correlating payload mass to landing success, color-coded by booster version.
- **Dashboard Analysis Findings**:
  - *Largest number of successful launches*: **KSC LC-39A** (10 successes).
  - *Highest launch success rate*: **KSC LC-39A** (**76.9%**).
  - *Best payload range*: **2,000 – 4,000 kg** (>60% success rate).
  - *Lowest payload range*: **6,000 – 8,000 kg** (0%) and **0 – 2,000 kg** (27.3%).
  - *Best booster category*: **Block 5 (B5)** with **100% success rate**.

### 7. Predictive Analysis & Machine Learning (`SpaceX-Machine-Learning-Prediction-Part-5-v1.ipynb`)
- Standardized 80 features using `StandardScaler`.
- Split data into **80% training** (72 records) and **20% testing** (18 records) with `random_state=2`.
- Tuned 4 classifiers using 10-fold cross-validation (`GridSearchCV`):
  - **Logistic Regression**: Best CV: `82.14%` | Test Accuracy: **83.33%**
  - **Support Vector Machine (SVM)**: Best CV: `84.82%` | Test Accuracy: **83.33%**
  - **Decision Tree**: Best CV: **87.50%** | Test Accuracy: **83.33%**
  - **K-Nearest Neighbors (KNN)**: Best CV: `83.39%` | Test Accuracy: **83.33%**
- **Test Confusion Matrix** (all models):
  $$\begin{bmatrix} 3 & 3 \\ 0 & 12 \end{bmatrix}$$
  - **True Negatives (TN)** = 3
  - **False Positives (FP)** = 3
  - **False Negatives (FN)** = 0
  - **True Positives (TP)** = 12
  - **Precision**: $12 / (12 + 3) = 80.0\%$
  - **Recall**: $12 / (12 + 0) = \mathbf{100.0\%}$ (Zero missed landings!)
  - **Overall Test Accuracy**: $(12 + 3) / 18 = \mathbf{83.33\%}$

---

## 💻 How to Run Locally

### Prerequisites
- Python 3.10 – 3.14
- Recommended packages:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn folium dash requests beautifulsoup4 playwright
```

### Running the Notebooks
Open Jupyter or run in VS Code:
```bash
jupyter notebook notebooks/01_data_collection_api.ipynb
```
Run notebooks sequentially from `01` to `07`.

### Running the Plotly Dash Application
Navigate to the `dashboard/` directory and run:
```bash
cd dashboard
python spacex_dash_app.py
```
Open your browser at `http://127.0.0.1:8050/`.

---

## 📜 Rubric & Submission Verification

All 15 official IBM Capstone requirements are verified and passed:
1. **GitHub Repository**: Complete local package assembled and ready for upload.
2. **Final Presentation PDF**: `FINAL_IBM_APPLIED_DATA_SCIENCE_CAPSTONE.pdf` generated with native vector layout.
3. **Executive Summary**: Clear problem statement, dataset scale, and quantitative takeaways.
4. **Introduction**: SpaceX launch cost economics ($62M vs $165M) and reuse advantages.
5. **Data Collection & Wrangling**: REST API, BeautifulSoup web scraping, and `Class` creation.
6. **EDA & Visual Analytics**: Flight number, payload, launch site, and orbit distributions.
7. **Predictive Analysis Methodology**: StandardScaler, train/test split, 10-fold CV grid search.
8. **EDA Visualizations**: 6 verified plots embedded in presentation and exported to PNG.
9. **EDA SQL Results**: 10 SQLite queries executed on live database.
10. **Folium Results**: Interactive HTML map with circles, clusters, and 4 proximity measurements.
11. **Plotly Dash Results**: Interactive app with dropdowns, slider, pie chart, scatter plot, and screenshots.
12. **Predictive Analysis Results**: 83.33% test accuracy across 4 models; confusion matrix (TN=3, FP=3, FN=0, TP=12).
13. **Conclusion**: Strategic commercial recommendations for bidding against Falcon 9.
14. **Creativity Beyond Template**: Custom styling, automated screenshot pipeline, clean layout.
15. **Innovative Insights**: Zero false negative recall analysis and learning-curve recovery trend.

---

## 👤 Author
**Abhishek Kulkarni**  
GitHub: [https://github.com/Abhishek5472](https://github.com/Abhishek5472)
