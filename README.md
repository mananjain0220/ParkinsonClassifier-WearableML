
# 🧠 Parkinson’s Disease Classification Using Smartwatch Sensor & Clinical Data (PADS Dataset)

## 🧾 Introduction
This project explores the use of wearable sensor data and clinical metadata to classify individuals with Parkinson's Disease (PD) versus non-Parkinsonian subjects. The aim is to build an **interpretable, high-performance binary classifier** using motion signals and non-motor symptoms.

---

## Dataset Overview

- **Source**: [PADS – Parkinson’s Disease Smartwatch Dataset v1.0.0](https://physionet.org/content/parkinsons-disease-smartwatch/1.0.0/)
- **Participants**: 469 subjects
- **Labels**: Binary — PD vs. non-PD (includes healthy & other movement disorders)
- **Sensors**: Accelerometer & gyroscope (mostly wrist-mounted)
- **Clinical Data**:
  - Questionnaire responses (30+ non-motor symptoms)
  - Demographic metadata (age, sex, diagnosis info)
- **Tasks Used**: TouchNose, Relaxed, PointFinger

---

## Data Exploration

- Visualized and summarized demographics & labels
- Mapped patient IDs across motion/questionnaire/metadata files
- Previewed sample sensor signals from wrist tasks
- Verified PD label distribution (291 PD, 178 non-PD)

---

## Data Preprocessing

- Loaded motion signals & questionnaire responses
- Merged all data by patient ID
- Normalized motion time-series data
- Extracted sensor data per task
- Filtered for consistent format and quality

---

## Feature Engineering

- Extracted motion features:
  - **Time-domain**: RMS, entropy
  - **Frequency-domain**: dominant frequency
- Performed task-wise feature extraction on:
  - `TouchNose`, `Relaxed`, `PointFinger`
- Merged features with:
  - Age, gender, diagnosis delay, handedness
  - Questionnaire binary responses (e.g., taste loss, urinary urgency)

---

## Model Building

- Split data into train/test sets (stratified)
- Models trained:
  - Random Forest (baseline, pruned, tuned)
  - XGBoost (for SHAP explainability)
- Feature selection:
  - Used SHAP to reduce from 97 → Top 30
- Hyperparameter tuning:
  - GridSearchCV on Random Forest for final AUC

---

## Model Evaluation

- **Best Model:** Random Forest (Top 30 features, tuned)
- **AUC:** 0.9150
- Other metrics:
  - Accuracy: 86%
  - Precision/Recall/F1
  - MCC: 0.685
  - Brier Score: 0.114
- Feature importance: SHAP, Fisher Discriminant Ratio

---

## 📈 Results & Visualizations

- SHAP summary: Top clinical & motion features
- PCA & t-SNE: Visual class separability
- Confusion matrix: Model balance on PD vs. non-PD

---

## Conclusion

- **What did the model learn?**
  - Non-motor symptoms like `taste_smell_loss`, `sleep_talk_move`
  - Dynamic task signals (e.g., `TouchNose` entropy)
- **Most informative features:**
  - `diagnosis_delay`, `urinary_urgency`, `gyro_z_entropy`
- **Limitations:**
  - Small sample size, only 3 motion tasks used
- **Future Work:**
  - Expand to all 11 tasks (e.g., HoldWeight, CrossArms)
  - Real-time smartwatch integration
  - Add UPDRS for severity scoring

---

---

## 📦 Dataset Access & Setup

This notebook uses the [PADS – Parkinson’s Disease Smartwatch Dataset v1.0.0](https://www.kaggle.com/datasets/eren2222/pads-parkinsons-disease-smartwatch-v1-0-0).

To run this notebook on Kaggle:

1. Go to **Add Data** → **Kaggle Datasets**
2. Search for: `pads-parkinsons-disease-smartwatch-v1-0-0`
3. Add it to your notebook session
4. The data will be available at:
   ```
   /kaggle/input/pads-parkinsons-disease-smartwatch-v1-0-0/
   ```

💡 Tip: Make sure your file paths in code match this location when loading `.json`, `.txt`, or `.csv` files.
