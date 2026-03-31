# Compressor-Pre-Assembly-Pressure-Validation-Defect-Detection

This project aims to identify potentially faulty compressors **before assembly** by analyzing industrial sensor data and detecting abnormal pressure patterns.

## Overview

Using the MetroPT3 air compressor dataset, I built an end-to-end analytics workflow in **Google Colab** with **SQLite, SQL, and Python**:

- Loaded a large compressed CSV dataset into SQLite in chunks
- Explored and profiled pressure and current measurements with SQL
- Created anomaly labels using a Z-score based SQL approach
- Trained a Random Forest classifier in Python
- Evaluated model performance and feature importance

## Dataset

- **Dataset:** MetroPT3 Air Compressor Dataset
- **Source:** UCI / Kaggle
- **Scale:** ~15 million rows, 17 columns
- **Key features used in modeling:**
  - `TP2`
  - `TP3`
  - `Reservoirs`
  - `Oil_temperature`
  - `Motor_current`

## Tech Stack

- Google Colab
- SQLite
- SQL
- Python
- pandas
- scikit-learn

## Method

### 1. Data loading
The raw CSV file was uploaded into Colab, extracted from ZIP, and inserted into SQLite in chunks to avoid RAM issues.

### 2. SQL anomaly labeling
I calculated Z-scores for `TP2` and `TP3` in SQLite and labeled observations as anomalies when pressure values exceeded a selected threshold.

### 3. Supervised model
Using the SQL-generated labels, I trained a `RandomForestClassifier` with the following inputs:

- TP2
- TP3
- Reservoirs
- Oil_temperature
- Motor_current

## Results

### Class balance
- Normal: 97.1%
- Anomaly: 2.9%

### Model performance
On the test set:
- Precision (class 1): 1.00
- Recall (class 1): 1.00
- F1-score (class 1): 1.00

### Feature importance
The model relied most strongly on:
1. **TP2**
2. **Motor_current**
3. TP3
4. Reservoirs
5. Oil_temperature

This suggests that pressure behavior and motor current are the strongest signals for identifying abnormal compressor states.

## Repository Structure

```text
.
├── README.md
├── notebooks/
│   └── compressor_anomaly_colab.ipynb
├── sql/
│   └── labeling_queries.sql
├── assets/
│   └── feature_importance.png
```

## Next Steps

- Test unsupervised methods such as Isolation Forest
- Add time-based features
- Build a dashboard in Tableau or Power BI
- Simulate a real-time monitoring workflow

## Contact

a.urkmez@outlook.com
