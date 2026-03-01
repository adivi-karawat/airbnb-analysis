# US Airbnb Market Structure & Pricing Strategy (2020)

## 📌 Project Overview

This project analyzes **225,901 Airbnb listings across the United States (2020)** to understand:

- What drives Airbnb listing prices?
- How professional hosts differ from casual hosts
- Whether pricing power varies by host scale and geography
- What supply/demand signals explain listing performance

This project evaluates whether Airbnb pricing power is driven primarily by geography, host scale, or inventory specialization. The goal is to combine **market structure analysis** with **pricing regression modeling** to extract strategic insights for new and existing hosts.

---

## 📂 Data Source

Dataset: U.S. Airbnb Open Data (2020)  
Source: Kaggle  

Link: https://www.kaggle.com/datasets/kritikseth/us-airbnb-open-data/data 

The dataset includes listing-level information such as price, room type, host ID, availability, review counts, and geographic coordinates.

---

### 🛠 Tools Used
- **SQL (SQLite)** – Data cleaning, validation, anomaly detection
- **Python (pandas, seaborn, matplotlib)** – Exploratory analysis
- **Statsmodels & Scikit-learn** – Pricing regression models
- **JupyterLab** – Reproducible workflow

---

## 📂 Project Structure

1. Market Structure Analysis  
2. Host Professionalization  
3. Supply–Demand Dynamics  
4. Pricing Regression Model  
5. Interaction Model (Room Type × City)  
6. Strategic Implications  

---

# 🧹 Data Cleaning & Validation

The dataset was audited and cleaned in SQL before analysis in Python.

### Key Cleaning Steps

### 1. Duplicate ID Conflict
- Listing ID `43806155` was assigned to two different properties across different cities.
- Since listing ID should uniquely identify a property, both rows were removed.

### 2. Invalid Price Values
- Removed 62 listings with `price = 0`.
- These would distort pricing analysis and regression modeling.

### 3. Unrealistic Minimum Nights
- Removed 65 listings with `minimum_nights > 365`
- Included extreme values such as 100,000,000 nights (likely scraping errors).

### 4. Geographic Validation
- Verified US latitude/longitude ranges.
- No anomalies detected.

### Final Dataset
**225,901 listings**

---

# 📊 Exploratory Findings

## 1️⃣ Market Concentration

Airbnb is meaningfully professionalized.

- ~27% of listings are controlled by hosts with 6+ properties.
- Enterprise hosts (20+ listings) control ~15% of total supply.

**Conclusion:**  
Airbnb is not purely casual — a meaningful portion of inventory is professionally managed.

---

## 2️⃣ Inventory Specialization

Percentage distribution of listings by room type within each host tier:

| Host Tier              | Entire Home/Apt | Hotel Room | Private Room | Shared Room |
|------------------------|-----------------|------------|--------------|-------------|
| Enterprise (20+)       | 85.78%          | 2.04%      | 9.34%        | 2.84%       |
| Professional (6–20)    | 63.84%          | 2.94%      | 29.25%       | 3.97%       |
| Single Listing         | 69.75%          | 0.06%      | 29.17%       | 1.01%       |
| Small Host (2–5)       | 57.55%          | 0.54%      | 40.41%       | 1.51%       |

### Interpretation

- Enterprise hosts are heavily concentrated in **Entire Home/Apt** listings.
- Small hosts maintain the highest exposure to **Private Rooms**.
- Hotel Room supply remains small across all tiers.
- Inventory specialization increases with host scale.

This supports the hypothesis that larger operators strategically focus on full-unit rentals, where pricing power is stronger.

---

## 3️⃣ Geographic Concentration

Enterprise pricing power is partially geographic.

- Heavy concentration in vacation markets (e.g., Hawaii).
- Hawaii median price:
  - Enterprise: **$219**
  - Smaller hosts: **$155–179**

Enterprise premium is amplified in high-demand vacation markets.

---

## 4️⃣ Pricing Premium by Host Tier

Enterprise hosts:
- Charge the highest median prices overall.
- Premium strongest in Entire Home segment.
- Maintain premium even when controlling for geography.

> Enterprise operators appear to concentrate in high-demand vacation markets and focus on entire-home inventory, where they command a median price premium relative to smaller hosts.

---

## 5️⃣ Supply–Demand Signals

### Availability vs Price
Correlation ≈ 0.03

Availability does **not** linearly predict price.

- Low availability ≠ premium pricing
- High-priced listings are not necessarily “scarce”

### Reviews vs Availability
Higher availability is associated with lower review counts — suggesting that occupancy drives review accumulation.

---

# 📈 Pricing Regression Model

A log-linear regression model was built to predict listing price using:

- Room type  
- City  
- Host tier  
- Minimum nights  
- Availability  
- Review metrics  

### Baseline Linear Model

- **R² ≈ 0.35**
- **Mean Absolute Error ≈ $100**
- **Mean Absolute % Error ≈ 48%**

The model captures broad location and segment effects but does not include property-level amenities (bedrooms, bathrooms, ratings, etc.), limiting precision.

---

# 🔄 Interaction Model (Room Type × City)

To test whether pricing premiums vary by geography, an interaction model was estimated:

```python
log_price ~ room_type * city + host_tier + controls
```

## 📊 Results

- **Baseline Adjusted R²:** 0.349  
- **Interaction Adjusted R²:** 0.358  
- **F-test p-value:** < 0.001  

The interaction terms are statistically significant, but the practical improvement in explanatory power is modest.

### Conclusion

- **Location is the dominant pricing driver.**
- Room-type premiums vary by city, but geography explains most price variation.

---

## 🧠 Key Insights

- Airbnb is partially professionalized.
- Enterprise hosts specialize in entire homes.
- Geographic concentration amplifies pricing power.
- Pricing differences are driven primarily by city and room type.
- Availability is not a strong price predictor.
- Demand signals (reviews) correlate more with occupancy than price.

---

## 💼 Strategic Implications for New Hosts

#### 1️⃣ Market Positioning Matters
Competing in the Entire Home segment against enterprise operators may require differentiation.

#### 2️⃣ Geography > Host Scale
Location selection may matter more than expanding inventory.

#### 3️⃣ Scarcity Signaling Is Weak
Lower availability does not guarantee higher pricing power.

#### 4️⃣ Professionalization Is Real
Markets are partially institutionalized — particularly in vacation cities.

---

## 🚀 Future Improvements

- Compare with nonlinear models (Random Forest, Gradient Boosting)
- Conduct city-level price elasticity analysis
- Analyze seasonal pricing dynamics
- Build an interactive dashboard (Power BI / Tableau)
- Extend analysis to the 2023 dataset and compare structural changes in:
  - Host professionalization
  - Pricing power
  - Market concentration
  - Post-pandemic supply shifts

---

## 📌 Summary

This project combines structural market analysis with regression modeling to examine how pricing power emerges in a partially professionalized Airbnb market.

The primary pricing driver is geography.  
Host scale matters — but mostly through specialization and market concentration.
