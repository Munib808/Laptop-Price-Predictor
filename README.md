# Laptop Price Predictor

## Project Overview
This project is a machine learning model that predicts laptop prices based on various features and specifications. The model uses a Voting Regressor ensemble technique combining Random Forest, Extra Trees, and Decision Tree regressors to achieve high predictive accuracy.

---

## Dataset
The dataset contains 1,303 laptop entries with the following features:

### Original Features:
- **Company:** Manufacturer brand (e.g., Dell, Apple, HP)  
- **TypeName:** Laptop type (e.g., Notebook, Ultrabook, Gaming)  
- **Inches:** Screen size  
- **ScreenResolution:** Display specifications  
- **Cpu:** Processor details  
- **Ram:** Memory size  
- **Memory:** Storage configuration  
- **Gpu:** Graphics card  
- **OpSys:** Operating system  
- **Weight:** Laptop weight  
- **Price:** Target variable (in local currency)  

### Derived Features:
After extensive feature engineering, the final dataset includes:
- One-hot encoded company and type names  
- Extracted screen features (Touchscreen, IPS, Retina, 4K)  
- Calculated PPI (Pixels Per Inch)  
- CPU type and speed features  
- GPU brand features  
- Memory breakdown (SSD, HDD, Flash Storage, Hybrid)  

---

## Data Preprocessing

### Key Transformations:
**Memory Conversion:**
- Split into separate SSD, HDD, Flash Storage, and Hybrid columns  
- Converted all values to GB (TB × 1000)  

**Screen Resolution Processing:**
- Extracted resolution dimensions (X and Y)  
- Calculated PPI (Pixels Per Inch)  
- Created binary flags for:
  - Touchscreen  
  - IPS panel  
  - Retina display  
  - 4K resolution  

**Categorical Encoding:**
- One-hot encoded:
  - Company (9 categories)  
  - Laptop Type (6 categories)  
  - Operating System (6 categories)  
  - CPU Type (5 categories)  
  - GPU Brand (3 categories)  

**Numerical Processing:**
- Cleaned and converted:
  - RAM (removed “GB” and converted to integer)  
  - Weight (removed “kg” and converted to float)  
  - CPU speed (extracted GHz value)  

**Outlier Removal:**
- Used IQR method to remove outliers in:
  - Screen size (Inches)  
  - Price  

---

## Feature Engineering

**Important Derived Features:**
- **PPI (Pixels Per Inch):** Formula based on screen resolution and size  
- **CPU Features:**  
  - Type (i3, i5, i7, AMD, Other)  
  - Speed (GHz)  
- **GPU Brand:** Intel, Nvidia, AMD  
- **Memory Configuration:** Separate columns for SSD, HDD, Flash, Hybrid  

---

## Model Development

**Algorithms Tested:**
- Linear Regression (Baseline)  
- Ridge Regression  
- Lasso Regression  
- K-Nearest Neighbors  
- Decision Tree  
- Random Forest  
- Extra Trees  
- AdaBoost  
- Voting Regressor (Ensemble)  
- Stacking Regressor  

**Hyperparameter Tuning:**
- Used GridSearchCV to optimize parameters for:
  - Decision Tree  
  - Random Forest  
  - Extra Trees  

**Final Model - Voting Regressor:**
Combines predictions from:
- Random Forest  
- Extra Trees  
- Decision Tree  

**Performance Metrics:**
- **R² Score:** 91.44%  
- **MAE:** 0.1274 (log scale)  

---

## Additional Files

- `app.py` – Streamlit web app for interactive price prediction  
- `laptop_price_predictor.pkl` – Trained Voting Regressor model  
- `model_features.pkl` – List of feature names used in model training  
- `model_files.zip` – Compressed archive containing both `.pkl` files 

---

## Results

**Model Comparison:**

| Model              | R² Score | MAE     |
|--------------------|----------|---------|
| Linear Regression  | 85.18%   | 0.1769  |
| Random Forest      | 91.16%   | 0.1308  |
| Extra Trees        | 90.82%   | 0.1333  |
| Voting Regressor   | 91.44%   | 0.1274  |
| Stacking Regressor | 91.40%   | 0.1296  |

**Key Findings:**
- RAM size showed the highest correlation with price (0.70)  
- SSD capacity was the second strongest predictor (0.64)  
- Intel Core i7 processors commanded premium prices  
- Gaming laptops and Ultrabooks were more expensive than standard Notebooks  
- Higher PPI (display quality) correlated with higher prices  

---

## How to Use

### Requirements:
- Python 3.x  

**Libraries:**
- pandas, numpy, scikit-learn, matplotlib, seaborn, joblib  

### Usage:
1. Load the saved model and feature list  
2. Prepare input data:  
   - Ensure all 41 features are present in the correct order  
   - Categorical features must be one-hot encoded  
   - Numerical features should be scaled/transformed as in training  
3. Make predictions:  
   - Predictions are returned in the original price scale  

---

## Future Improvements

**Feature Expansion:**
- Add more recent laptop models  
- Include battery life information  
- Add benchmark scores for CPU/GPU  

**Model Enhancements:**
- Experiment with neural networks  
- Implement feature importance visualization  
- Add prediction intervals  

**Deployment:**
- Create a web interface  
- Build an API endpoint  
- Develop a mobile app version  

---

## Conclusion
This laptop price predictor demonstrates how careful feature engineering and ensemble modeling can create an accurate predictive system. The Voting Regressor approach achieved over 91% accuracy in predicting laptop prices based on technical specifications, providing valuable insights for both buyers and sellers in the laptop market.
