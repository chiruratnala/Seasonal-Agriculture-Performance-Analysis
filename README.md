# 🌾 Seasonal Agriculture Performance Analysis

## 📌 Project Overview

Agricultural output and resource efficiency vary significantly across seasons, regions, and crop types. This project conducts an end-to-end Exploratory Data Analysis (EDA) on the **Seasonal Agriculture Performance Dataset (`seasonal_agriculture_performance_dataset_3.csv`)**, examining multi-year cultivation patterns across **10 Indian states**, **8 major crops**, and **4 distinct cropping seasons (Kharif, Rabi, Summer, Zaid)**.

The primary objective is to evaluate seasonal yield efficiency, compare irrigated vs. rainfed performance, analyze the impact of soil moisture and fertilizer usage on crop productivity, and provide actionable recommendations for sustainable agricultural planning.

## 🛠️ Tech Stack & Tools Used

* **Programming Language:** Python 3
* **Data Manipulation & Cleaning:** `Pandas`, `NumPy`
* **Data Visualization:** `Matplotlib`, `Seaborn`
* **Development Environment:** Jupyter Notebook (`Seasonal_Agriculture_Performance_Analysis.ipynb`)

## 📂 Dataset Description

The dataset (`seasonal_agriculture_performance_dataset.csv`) contains **1,165 historical agricultural records** across **11 variables** spanning **2015–2024**:

* **Categorical Features:**
  * `Region` (10 states: *Andhra Pradesh, Bihar, Gujarat, Karnataka, Madhya Pradesh, Maharashtra, Punjab, Rajasthan, Tamil Nadu, Uttar Pradesh*)
  * `Season` (*Kharif, Rabi, Summer, Zaid*)
  * `Crop` (*Barley, Cotton, Groundnut, Maize, Mustard, Rice, Sugarcane, Wheat*)
  * `Irrigation_Type` (*Irrigated, Rainfed*)
* **Temporal Feature:**
  * `Year` (2015 – 2024)
* **Numerical Features:**
  * `Area_Hectares` (Cultivated land area in hectares)
  * `Yield_Tonnes_Per_Hectare` (Crop productivity per hectare)
  * `Total_Production_Tonnes` (Total crop output in metric tonnes)
  * `Rainfall_mm` (Seasonal rainfall in millimeters)
  * `Soil_Moisture_Index` (Normalized soil moisture level, ranging from ~0.10 to 0.72)
  * `Fertilizer_Usage_Kg_Per_Hectare` (Fertilizer intensity in kg/ha)

## ⚠️ Problems Encountered & Data Solutions

During data profiling and preprocessing, several structural and analytical challenges were identified and resolved:

| Problem Identified | Root Cause / Impact | Solution Implemented |
| :--- | :--- | :--- |
| **1. Extreme Scale Disparity Across Crops** | High-density cash crops like **Sugarcane** (~55–85 tonnes/ha) operate on a completely different yield scale than grains, pulses, and oilseeds (~1.5–4.5 tonnes/ha), distorting aggregate averages. | Analyzed **Crop-Specific Yield Benchmarks** separately from aggregate production totals, preventing Sugarcane from skewing cross-crop comparisons. |
| **2. Overlapping Seasonal Definitions (`Summer` vs. `Zaid`)** | Both `Summer` and `Zaid` represent pre-monsoon/summer cultivation windows in Indian agriculture, requiring careful grouping to avoid fragmented seasonal insights. | Evaluated all four recorded seasons (`Kharif`, `Rabi`, `Summer`, `Zaid`) individually to capture granular differences in irrigation reliance and yield stability. |
| **3. Multi-Collinearity Between Area & Total Production** | `Total_Production_Tonnes` is directly derived from $\text{Area\_Hectares} \times \text{Yield\_Tonnes\_Per\_Hectare}$, which can mask true land efficiency when evaluating states with large acreage. | Used **`Yield_Tonnes_Per_Hectare`** as the primary efficiency KPI while treating **`Total_Production_Tonnes`** as a volume/scale metric. |
| **4. Skewed Distribution & Outliers in Resource Inputs** | `Area_Hectares` and `Fertilizer_Usage_Kg_Per_Hectare` exhibited wide variance across regions and irrigation regimes. | Used **Median and IQR (Boxplots)** alongside Mean values to ensure robust statistical summaries unaffected by extreme farm-size outliers. |

## 📊 Key Results & Quantitative Findings

### 1. Irrigated vs. Rainfed Performance Gap
* **Consistent Yield Advantage:** Across every season and crop type, **Irrigated** farms significantly outperform **Rainfed** farms in `Yield_Tonnes_Per_Hectare`.
* **Soil Moisture Retention:** Irrigated records maintain substantially higher `Soil_Moisture_Index` values even during low-rainfall seasons (`Rabi`, `Summer`, `Zaid`), directly stabilizing harvest output.

### 2. Seasonal Dynamics (`Kharif`, `Rabi`, `Summer`, `Zaid`)
* **Kharif Season:** Driven by peak monsoon `Rainfall_mm` and elevated `Soil_Moisture_Index`, supporting water-intensive crops like **Rice**, **Cotton**, and **Sugarcane**.
* **Rabi Season:** Demonstrates strong yield consistency for **Wheat**, **Barley**, and **Mustard**, heavily supported by structured irrigation infrastructure (`Irrigated` share) and controlled fertilizer application.
* **Summer & Zaid Seasons:** Characterized by lower natural `Rainfall_mm`, making `Soil_Moisture_Index` and `Irrigation_Type` the primary determinants of crop survival and yield.

### 3. Crop-Level Productivity & Resource Intensity
* **Highest Yield per Hectare:** **Sugarcane** leads all crops in biomass yield per hectare, followed by **Rice**, **Maize**, and **Wheat**.
* **Fertilizer & Input Correlation:** Higher `Fertilizer_Usage_Kg_Per_Hectare` positively correlates with `Yield_Tonnes_Per_Hectare` primarily when paired with adequate `Soil_Moisture_Index` and irrigation; applying heavy fertilizer under low soil moisture yields diminishing returns.

### 4. Regional Performance Trends (2015–2024)
* **High-Efficiency States:** States with established canal/groundwater networks (such as **Punjab**, **Uttar Pradesh**, and **Andhra Pradesh**) consistently achieve higher mean yields per hectare.
* **Rainfed-Vulnerable States:** Regions with higher reliance on monsoon rainfall (such as **Rajasthan**, **Maharashtra**, and **Madhya Pradesh**) exhibit wider year-over-year yield fluctuations correlated with seasonal `Rainfall_mm`.

## 💡 Strategic Insights

1. **Moisture Is the Multiplier for Fertilizer:** Fertilizer efficiency is heavily gated by water availability. Increasing `Fertilizer_Usage_Kg_Per_Hectare` without sufficient `Soil_Moisture_Index` fails to maximize crop yield.
2. **Irrigation Buffers Climate Volatility:** While `Rainfall_mm` drives seasonal fluctuations in rainfed zones, `Irrigation_Type` decouples crop productivity from erratic monsoon patterns, especially in `Rabi` and `Zaid` seasons.
3. **Volume vs. Efficiency Distinction:** High `Total_Production_Tonnes` in large states is often driven by vast `Area_Hectares` rather than superior farming efficiency; evaluating `Yield_Tonnes_Per_Hectare` reveals where true agronomic optimization is occurring.

## 🚀 Actionable Recommendations

### 🌱 For Agricultural Policy & Irrigation Planning
* **Expand Micro-Irrigation in Rainfed Regions:** Prioritize drip and sprinkler irrigation subsidies in rainfed-heavy states (e.g., Rajasthan, Maharashtra, Madhya Pradesh) to boost `Soil_Moisture_Index` during `Rabi` and `Summer`/`Zaid` windows.
* **Align Crop Selection with Regional Water Profiles:** Encourage water-intensive crops (Sugarcane, Rice) in high-moisture/irrigated zones while promoting drought-resilient crops (Barley, Mustard, Groundnut) in low-rainfall regions.

### 🧪 For Input & Soil Management
* **Moisture-Linked Fertilizer Advisory:** Align `Fertilizer_Usage_Kg_Per_Hectare` recommendations with real-time `Soil_Moisture_Index` readings to prevent nutrient runoff, soil degradation, and wasted input costs.

### 📈 For Future Data Science & Modeling Enhancements
* **Yield Prediction Modeling:** Build regression models (`Random Forest`, `XGBoost`, or `Gradient Boosting`) using `Region`, `Season`, `Crop`, `Irrigation_Type`, `Rainfall_mm`, `Soil_Moisture_Index`, and `Fertilizer_Usage_Kg_Per_Hectare` to forecast `Yield_Tonnes_Per_Hectare`.
* **Drought Stress Early-Warning System:** Define threshold alerts when `Soil_Moisture_Index` drops below critical crop-specific levels during peak growing stages.

## 📁 Repository Structure

```text
├── Seasonal_Agriculture_Performance_Analysis.ipynb  # Main Jupyter Notebook with EDA, cleaning & visualizations
├── seasonal_agriculture_performance_dataset.csv   # Agricultural dataset (2015–2024, 1,165 records)
├── Seasonal Agriculture Performance Analysis.pdf    # Executive presentation deck summarizing findings
└── README.md                                        # Project documentation
```

## ⚙️ How to Run Locally

1. **Clone the repository:**
   ```bash
   git clone <https://github.com/chiruratnala/Seasonal-Agriculture-Performance-Analysis.git>
   cd seasonal-agriculture-analysis
   ```

2. **Install required dependencies:**
   ```bash
   pip install pandas numpy matplotlib seaborn jupyter
   ```

3. **Launch Jupyter Notebook:**
   ```bash
   jupyter notebook Seasonal_Agriculture_Performance_Analysis.ipynb
   ```
