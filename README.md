# ☀️ Solar Panel Efficiency Prediction Challenge

## 🧠 Approach Summary

This project focused on predicting solar panel efficiency through a structured, multi-stage modeling strategy. Below are the key steps and decisions that shaped the final solution:

### 🔧 Feature Engineering
- Engineered a rich set of features capturing various dimensions of solar panel behavior:
  - **Power-based features**: Raw power, power-to-irradiance ratios
  - **Temperature-related features**: Module and ambient temperature differentials, modeled efficiency loss
  - **Environmental impact features**: Effective irradiance, temperature influence
  - **Panel degradation metrics**: Capturing performance decay over time

### 🚀 Model 1: XGBoost
- Trained a complex **XGBoost** model using the engineered features
- Hyperparameter optimization done using **Optuna**, with **500 trials**
- Despite optimization, observed **overfitting**: high training scores vs. low validation scores
- Determined that the model was likely capturing **noise** instead of generalizable patterns

### 🔁 Model 2: Ridge Regression
- Switched to a **Ridge Regression** model for better generalization
- Implemented a full pipeline including:
  - **SimpleImputer** for handling missing values
  - Ridge model with alpha optimization via **Optuna** (500 trials)
  - Searched over `alpha` values from `1e-4` to `100.0` on a **log scale**
- The Ridge model showed **more stable and reliable** validation performance

### 🧠 Final Model Decision
- ✅ **Effectively used only Ridge Regression for final predictions**  
  Although both models (XGBoost and Ridge Regression) were trained and available, the final submission used a **weighted ensemble** where **XGBoost predictions were given zero weight** and **Ridge Regression predictions full weight**:  
  `Final Prediction = 0 * XGBoost + 1 * Ridge Regression`

  This decision was based on strong evidence that:
  - **XGBoost was overfitting**, with poor generalization despite complex modeling and extensive optimization
  - The **simpler Ridge model**, when properly regularized and optimized, consistently delivered **better validation results**
  
  This experience reinforced an important principle:  
  > **In noisy or complex datasets, a simpler, well-regularized model with strong feature engineering can outperform more complex algorithms.**

---

## 🏆 Competition Details

- 🌐 Challenge: **Solar Panel Efficiency Prediction**  
- 👥 Total Registrations: **7,400+**
- 📊 Active Participating Teams: **1,500+** (teams of 1 to 4 members)
- 🧍 Solo Participation: Yes
- 🏅 **Final Rank**: **87**

---
