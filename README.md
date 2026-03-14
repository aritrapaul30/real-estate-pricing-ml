This project builds a data-driven pricing framework for 21,613 residential property sales in King County, Seattle (2014–2015). It covers end-to-end EDA, feature engineering (HouseAge, LivingToLotRatio, BathsPerBedroom), outlier treatment, and benchmarks Linear Regression, Decision Tree, Random Forest, and Gradient Boosting models for both regression (price prediction) and classification (market tier segmentation). A Gradio UI allows interactive price estimation by property attributes.

## 📒 Notebook Sections

---

### 1️⃣ 🏢 Business Problem & Hypotheses
> Tackling the inefficiency of traditional property valuation methods.

- 📐 **H1** — Larger homes (higher `sqft_living`) sell for significantly higher prices
- 🔨 **H2** — Recently renovated homes command a price premium over unrenovated ones
- 🤖 **H3** — Ensemble models (Random Forest, Gradient Boosting) outperform Linear Regression

---

### 2️⃣ 📦 Data Loading
> King County Assessor's Office residential sales dataset

| Detail | Value |
|---|---|
| 📊 Observations | 21,613 rows |
| 📋 Variables | 21 columns |
| 📅 Time Period | May 2014 – May 2015 |
| 🌐 Source | Kaggle — King County House Sales |

---

### 3️⃣ 🔍 Summary Statistics & EDA
> First look at distributions, skewness, and feature relationships

- 💰 Price is **right-skewed** — Mean ~$540K vs Median ~$450K (luxury outliers pull the mean up)
- 🔥 **Top correlations with price:**

| Feature | Correlation (r) | Meaning |
|---|---|---|
| `sqft_living` | **0.70** 🟢 | Bigger homes = higher price |
| `grade` | **0.67** 🟢 | Better construction = higher price |
| `bathrooms` | 0.53 🟡 | Design quality matters |
| `view` | 0.40 🟡 | Scenic views add value |
| `sqft_lot` | 0.09 🔴 | Lot size barely matters |

---

### 4️⃣ 🧹 Data Wrangling
> Cleaning and preparing the dataset for modelling

- ✅ **Missing values** — None found (0 nulls across all 21 columns)
- ✅ **Duplicates** — Zero duplicate entries detected
- 🔎 **Outlier Detection** — IQR method flagged **6,679 outliers** across numeric variables
- 🛡️ **Smart Masking** — `waterfront` and `yr_renovated` outliers were **preserved**, not removed
  - *(Removing them would erase legitimate luxury & premium listings from the model)*

---

### 5️⃣ ⚙️ Feature Engineering
> Creating new business-meaningful variables from existing data

| 🆕 Feature | 📐 Formula | 💡 Why It Matters |
|---|---|---|
| `HouseAge` | `sale_year - yr_built` | Captures depreciation effect |
| `YearsSinceRenovation` | `sale_year - yr_renovated` | Recent upgrades = higher value |
| `LivingToLotRatio` | `sqft_living / sqft_lot` | Land-use efficiency (urban premium) |
| `BasementPresent` | `1 if sqft_basement > 0` | Extra liveable space indicator |
| `BathsPerBedroom` | `bathrooms / bedrooms` | Home layout quality & comfort |
| `Renovated` | `1 if yr_renovated > 0` | Binary renovation flag |

---

### 6️⃣ 🤖 Model Training
> Benchmarking regression and classification models

**🔢 Regression — Predicting Exact Price**

| Model | Performance |
|---|---|
| 📏 Linear Regression | Baseline — interpretable but misses non-linear patterns |
| 🌿 Decision Tree | Captures non-linearity, prone to overfitting |
| 🌲 Random Forest | ⭐ Best performer — stable, handles interactions |
| 🚀 Gradient Boosting | Competitive — excellent on complex patterns |

**🏷️ Classification — Predicting Price Tier**

| Tier | Price Range |
|---|---|
| 🟢 Budget | < $300K |
| 🟡 Mid-Range | $300K – $650K |
| 🔴 Premium | > $650K |

---

### 7️⃣ 🖥️ Gradio Interactive Dashboard
> A live, user-friendly property price estimator

**Input Sliders & Dropdowns:**
- 📐 Living Area (`sqft_living`)
- ⭐ Construction Grade (`grade` 1–13)
- 🛏️ Number of Bedrooms
- 🚿 Number of Bathrooms
- 🌊 Waterfront View (`yes / no`)
- 📅 Year Built
- 🔨 Year Renovated

**Output:**
- 💵 **Estimated Sale Price** (in USD)
- 🏷️ **Market Tier** (Budget / Mid-Range / Premium)
