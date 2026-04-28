# House Price Prediction API

> Regression model to predict house prices based on property features, deployed as REST API

**Status:** Ongoing | **Duration:** 0 days | **Level:** Beginner

## 📋 Project Brief

**The Request:**
"Client mau prediksi harga rumah berdasarkan fitur seperti luas, kamar, lokasi. Bikin API-nya ya, biar mereka tinggal input data rumah terus keluar estimasi harganya."

**Objective:** Build a house price prediction API that returns estimated price from property features.

**Success Criteria:**
- R² > 0.75 on test set
- API response time < 200ms
- Input validation and error handling

**Out of scope:** 
- Real-time streaming segmentation 
- CRM integration.

## 🎯 Learning Objectives

-  Linear and polynomial regression fundamentals
-  Feature scaling and categorical encoding techniques
-  Model evaluation metrics: RMSE, MAE, R²
-  REST API development with FastAPI
-  Model deployment and serving

## 🛠️ Tech Stack

- **Language:** Python 3.10
- **ML Libraries:** scikit-learn, XGBoost, pandas, numpy
- **API Framework:** FastAPI
- **Visualization:** matplotlib, seaborn
- **Tools:** Jupyter, Postman

## 📊 Dataset

**Primary:** [KC House Data](https://www.kaggle.com/datasets/shivachandel/kc-house-data)
- 21,613 rows
- 21 features (bedrooms, bathrooms, sqft_living, location, etc.)

**Alternative:** [Ames Housing](https://www.kaggle.com/datasets/prevek18/ames-housing-dataset)

## ✅ Core Requirements Completed

- [ ] EDA with visualizations (distributions, correlations, scatter plots)
- [ ] Data preprocessing: handle missing values, encode categoricals, scale features
- [ ] Train 3+ models (Linear Regression, Random Forest, XGBoost) and compare
- [ ] Model evaluation with RMSE, MAE, and R² on test set
- [ ] REST API with /predict endpoint accepting house features
- [ ] Separate code into modules (preprocessing, training, serving)

## 🎁 Deliverables

- [ ] Jupyter notebook with full EDA and model comparison
- [ ] Trained model artifact (.pkl)
- [ ] REST API with Swagger documentation
- [ ] Postman collection for API testing
- [ ] README with model card (metrics, features, limitations)

## ⭐ Bonus Challenges Completed

- [ ] Feature importance visualization with SHAP
- [ ] Model versioning with timestamp and metrics tracking
- [ ] Data drift detection on incoming prediction requests (planned)
- [ ] Simple frontend with Streamlit (planned)

<!-- ## 📁 Project Structure

    01-house-price-prediction-api/
    ├── data/
    │   ├── raw/
    │   │   └── kc_house_data.csv
    │   └── processed/
    │       └── processed_data.csv
    ├── notebooks/
    │   ├── 01-eda.ipynb
    │   └── 02-modeling.ipynb
    ├── src/
    │   ├── preprocessing.py
    │   ├── train.py
    │   └── api.py
    ├── models/
    │   ├── xgboost_model.pkl
    │   └── scaler.pkl
    ├── tests/
    │   └── test_api.py
    ├── postman/
    │   └── house_price_api.json
    ├── requirements.txt
    ├── .gitignore
    └── README.md

## 🚀 Getting Started

### 1. Setup Environment

    cd 01-house-price-prediction-api
    
    python -m venv venv
    source venv/bin/activate
    
    pip install -r requirements.txt

Windows users: use `venv\Scripts\activate`

### 2. Download Dataset

Download from Kaggle and place in `data/raw/kc_house_data.csv`

### 3. Run EDA & Training

    jupyter notebook notebooks/01-eda.ipynb
    
    python src/train.py

### 4. Start API Server

    uvicorn src.api:app --reload

API available at: http://localhost:8000
Swagger docs at: http://localhost:8000/docs

### 5. Test API

    curl -X POST "http://localhost:8000/predict" \
      -H "Content-Type: application/json" \
      -d '{"bedrooms": 3, "bathrooms": 2, "sqft_living": 2000, "sqft_lot": 5000, "floors": 1, "waterfront": 0, "view": 0, "condition": 3, "grade": 7, "sqft_above": 1500, "sqft_basement": 500, "yr_built": 1990, "yr_renovated": 0, "zipcode": 98178, "lat": 47.5112, "long": -122.257}'

Or import Postman collection from `postman/house_price_api.json`

## 📈 Results

### Model Comparison

| Model | RMSE | MAE | R² Score | Training Time |
|-------|------|-----|----------|---------------|
| Linear Regression | $125,430 | $85,210 | 0.72 | 0.5s |
| Random Forest | $98,560 | $65,340 | 0.82 | 12.3s |
| **XGBoost** | **$89,240** | **$58,120** | **0.86** | 8.7s |

**Best Model:** XGBoost with hyperparameter tuning

### Feature Importance (Top 5)

1. `sqft_living` - 0.35
2. `grade` - 0.18
3. `lat` (latitude) - 0.12
4. `sqft_above` - 0.10
5. `bathrooms` - 0.08

### API Performance

- **Average Response Time:** 145ms ✅
- **P95 Response Time:** 180ms ✅
- **Throughput:** ~50 requests/second

## 🧠 What I Learned

### 1. Exploratory Data Analysis
- Identified strong correlation between `sqft_living` and price (r=0.70)
- Found outliers: houses with 33 bedrooms (data entry error)
- Discovered price distribution is right-skewed → applied log transformation

### 2. Feature Engineering
- Created `house_age` from `yr_built`
- Created `is_renovated` binary feature
- Created `price_per_sqft` for better insights
- One-hot encoded `zipcode` (70 unique values)

### 3. Model Selection
- Linear Regression: Fast but underfits
- Random Forest: Good performance, interpretable
- XGBoost: Best performance, handles non-linearity well

### 4. Challenges & Solutions

**Challenge 1:** Missing values in `yr_renovated`
- **Solution:** Filled with 0 (means not renovated)

**Challenge 2:** High cardinality in `zipcode`
- **Solution:** Used target encoding instead of one-hot

**Challenge 3:** Model overfitting on training data
- **Solution:** Applied cross-validation and regularization

**Challenge 4:** API response time > 200ms initially
- **Solution:** Cached scaler and model in memory, optimized preprocessing

## 🔍 Key Insights

1. **Location matters most** - Latitude/longitude are top predictors
2. **Square footage > number of rooms** - Living area more important than bedroom count
3. **Grade is crucial** - Construction quality significantly impacts price
4. **Waterfront premium** - Waterfront properties cost 2x more on average

## 📊 Model Card

### Model Information
- **Model Type:** XGBoost Regressor
- **Version:** 1.0.0
- **Training Date:** April 28, 2026
- **Framework:** scikit-learn 1.3.0, XGBoost 2.0.0

### Intended Use
- **Primary Use:** Estimate house prices for King County, WA
- **Users:** Real estate agents, homebuyers, property investors
- **Out of Scope:** Properties outside King County, commercial real estate

### Training Data
- **Source:** King County House Sales (2014-2015)
- **Size:** 21,613 samples
- **Split:** 80% train, 20% test

### Performance Metrics
- **R² Score:** 0.86
- **RMSE:** $89,240
- **MAE:** $58,120

### Limitations
- Model trained on 2014-2015 data (may not reflect current market)
- Limited to King County area
- Does not account for market trends or economic factors
- May underperform on luxury properties (>$2M)

### Ethical Considerations
- Model may perpetuate historical biases in housing prices
- Should not be sole factor in pricing decisions
- Requires regular retraining with recent data



## 📚 References

- [Kaggle: KC House Data](https://www.kaggle.com/datasets/shivachandel/kc-house-data)
- [XGBoost Documentation](https://xgboost.readthedocs.io/)
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [SHAP for Model Interpretability](https://github.com/slundberg/shap)

## 📝 Next Steps

1. Implement data drift detection
2. Build Streamlit frontend for easier interaction
3. Add CI/CD pipeline for automated testing
4. Deploy to cloud (AWS/GCP)
5. Implement A/B testing for model versions

## 📧 Contact

Questions or feedback? Open an issue or reach out!

---

**Project Timeline:** Apr 21 - Apr 28, 2026 | **Total Hours:** ~35 hours -->