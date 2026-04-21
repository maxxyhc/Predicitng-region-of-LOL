# 🎮 Predicting League of Legends Player Region

## 📌 Project Overview
This project aims to predict the **competitive region (league)** of professional League of Legends players based on in-game performance statistics.

We build machine learning models to classify players into major regions:
- LPL (China)
- LCK (Korea)
- LEC (Europe)
- LTA (Americas)
- LCP (Pacific)

---

## 📊 Dataset
- Source: Oracle’s Elixir
- ~24,000 player-game records after filtering
- 164 original features → reduced to ~40 selected features

### Data Processing
- Filtered only major leagues (LPL, LCK, LEC, LTA, LCP)
- Removed non-player rows (`position != 'team'`)
- Merged LTA North/South into a single region
- Selected key features:
  - Combat stats: `kills`, `deaths`, `assists`, `dpm`
  - Economy stats: `gold`, `cs`, `xp`
  - Vision stats: `wards`, `control wards`
  - Early game stats: `gold@15`, `cs@15`, etc.

---

## 🧹 Data Cleaning
- Many features contained missing values (some >30%)
- Missing values were handled using:
  - League-level mean imputation
  - Global mean fallback
- Applied preprocessing:
  - `StandardScaler` for numeric features
  - `OneHotEncoder` for categorical features

---

## 📈 Exploratory Data Analysis
Performed EDA using:
- Boxplots (kills, deaths, assists, gold, xp)
- Champion usage distribution across leagues
- Scatter plots (kills vs assists, dpm vs wpm)

### Key Insight
Certain regions (e.g., LPL) exhibit distinct playstyles, making them easier to classify.

---

## 🤖 Modeling

### Baseline
- Random classifier  
- Accuracy: ~20%

---

### KNN Model
- Pipeline: Encoding + Scaling + KNN  
- Accuracy: ~53%

---

### Logistic Regression (Global Model)
- Multinomial logistic regression  
- Accuracy: ~35%

---

### 🚀 Final Model: Position-Specific Logistic Regression
Trained separate models for each role:
- top / jungle / mid / bot / support

#### Final Performance
- **Accuracy: ~61.5%**

#### Per-role Accuracy
- Top: ~62%
- Jungle: ~62%
- Mid: ~60%
- Bot: ~60%
- Support: ~61%

---

## 💡 Key Insights
- Player role significantly impacts classification performance
- LPL is the easiest region to classify
- Some regions overlap in playstyle, making classification harder
- Model design (feature engineering + segmentation) matters more than complexity

---

## 🛠️ Tech Stack
- Python (Pandas, NumPy)
- Scikit-learn (Pipeline, KNN, Logistic Regression)
- Matplotlib / Seaborn

---

## 📦 How to Run

```bash
pip install pandas numpy scikit-learn matplotlib seaborn
