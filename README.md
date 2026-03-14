This project builds a data-driven pricing framework for 21,613 residential property sales in King County, Seattle (2014–2015). It covers end-to-end EDA, feature engineering (HouseAge, LivingToLotRatio, BathsPerBedroom), outlier treatment, and benchmarks Linear Regression, Decision Tree, Random Forest, and Gradient Boosting models for both regression (price prediction) and classification (market tier segmentation). A Gradio UI allows interactive price estimation by property attributes.

Notebook Sections
Business Problem & Hypotheses — Pricing inefficiency, H1: larger homes sell for more, H2: renovated homes command premium, H3: ensemble models beat linear
​

Data Loading — 21,613 observations, 21 variables from King County Assessor's Office (May 2014–May 2015)
​

Summary Statistics & EDA — Right-skewed price distribution (mean ~$540K, median ~$450K); correlation heatmap showing sqft_living (r=0.70) and grade (r=0.67) as top predictors
​

Data Wrangling — Zero missing values, 0 duplicates, IQR outlier removal (6,679 flagged; waterfront/yr_renovated masked to preserve premium listings)
​

Feature Engineering — Create HouseAge, YearsSinceRenovation, LivingToLotRatio, BasementPresent, BathsPerBedroom, Renovated
​

Model Training — Linear Regression, Decision Tree, Random Forest, Gradient Boosting (both regression + classification into price tiers)
​

Gradio UI — Interactive price predictor with sliders for sqft, grade, bedrooms, etc.
