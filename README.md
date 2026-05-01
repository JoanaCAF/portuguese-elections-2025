# 🗳️ Portuguese Municipal Elections 2025 — Predictive Modelling

A machine learning project predicting Chega's electoral growth across Portuguese municipalities, combining **sociodemographic census data** with **historical election results** and **XGBoost classification/regression models**.

---

## 📌 Project Overview

This project investigates whether sociodemographic and historical electoral patterns can predict the growth of the Chega party (Portugal's right-wing populist party) at the municipal level, across both local (*autárquicas*) and legislative (*legislativas*) elections.

**Key questions explored:**
- Which municipalities are likely to see Chega's vote share grow in the 2025 municipal elections?
- What sociodemographic features (education, immigration rate, purchasing power, crime) best explain Chega's electoral gains?
- Can models trained on autárquicas data generalise to legislative elections?

---

## 🗂️ Project Structure

```
portuguese_elections/
│
├── notebooks/
│   ├── 01_data_preparation.ipynb           # Merge Censos 2021 + election results
│   ├── 02_exploratory_analysis.ipynb       # EDA + choropleth maps
│   ├── 03_model_chega_autarquicas.ipynb    # XGBoost classifier (municipal elections)
│   ├── 04_data_preparation_legislativas.ipynb  # Add 2024/2025 legislative data
│   ├── 05_model_chega_legislativas.ipynb   # XGBoost classifier (legislative elections)
│   ├── 06_regression_vote_share.ipynb      # XGBoost regression (vote share magnitude)
│   └── 07_scraping_legislativas_2025.ipynb # Web scraping 2025 results
│
├── data/
│   ├── raw/                                # Original source data (CSVs + shapefiles)
│   └── processed/                          # Merged feature tables (output of notebook 01)
│
├── outputs/                                # Charts, maps, model results
├── requirements.txt
└── README.md
```

---

## 📊 Data Sources

| Dataset | Source | Description |
|---|---|---|
| Censos 2021 | INE (Statistics Portugal) | Education, civil status, immigration, purchasing power, crime, population by municipality |
| Municipal Elections 2021 | CNE | Vote share by party and municipality |
| Legislative Elections 2022 | CNE | Vote share by party and municipality |
| Legislative Elections 2024 | CNE | Vote share by party and municipality |
| Legislative Elections 2025 | Wikipedia / CNE | Vote share by party and municipality |
| Municipality Shapefiles | GADM / OpenData | Geographic boundaries for choropleth maps |

---

## 🤖 Methods

### Feature Engineering
- Merged 11 sociodemographic and electoral datasets on municipality name (`Concelho`)
- One-hot encoded categorical variables (winning party, district)
- Created binary target variable: did Chega's vote share **grow** between elections?
- Handled duplicate municipality names (e.g. Calheta in Açores vs Madeira)

### Modelling
- **XGBoost Classifier** — predicts growth direction (binary: grew / didn't grow)
- **XGBoost Regressor** — predicts magnitude of vote share change
- **Leave-One-Out Cross-Validation (LOO-CV)** — chosen due to small sample size (~308 municipalities)
- **SHAP values** — for feature importance and model interpretability
- **Class balancing** via `scale_pos_weight` to handle imbalanced targets

### Evaluation Metrics
- Accuracy, F1-score, Precision, Recall
- Classification report (LOO-CV)
- R² and RMSE (regression)

---

## 🚀 Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/portuguese-elections-2025.git
cd portuguese-elections-2025
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Run the notebooks in order
Start with `01_data_preparation.ipynb` to build the feature table, then proceed sequentially.

---

## 🔍 Key Findings

*(To be updated as the 2025 autárquicas results become available)*

- Historical Chega vote share in legislative elections is the strongest predictor of municipal growth
- Municipalities with higher immigration rates and lower purchasing power show stronger Chega growth
- LOO-CV models achieve ~XX% accuracy on the binary classification task

---

## 👩‍💻 Author

**Joana Ferreira** — Data Analyst  
[GitHub](https://github.com/JoanaCAF)

*Independent project developed as part of a broader portfolio in electoral data science and predictive modelling.*

---

## 📄 License

This project is open source under the [MIT License](LICENSE).
