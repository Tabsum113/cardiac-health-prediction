# ECG + Clinical Data Cardiac Health Prediction: Project Report

A final-year B.Tech project that combines **ECG image classification** (deep learning) with **clinical and lifestyle data analysis** (machine learning) in a Flask web application, aimed at early detection of heart conditions, including cardiac risk in patients undergoing chemotherapy (cardiotoxicity).

> **Note:** This repository is a **project write-up**. The original source code is not included here, so there are no run instructions.

> B.Tech (CSE), Srinivasa Ramanujan Institute of Technology, Ananthapuramu, 2025-26.
> Paper accepted for presentation at **ICCCSS 2025** (International Conference on Computational and Cognitive Systems Science).

> **Disclaimer:** This is an academic prototype. It is not a medical device and must not be used for real diagnosis or treatment decisions.

## Problem

Chemotherapy can damage the heart, and cardiac problems are often found late. Manual ECG reading is slow and error-prone, and most existing systems treat ECG images and clinical data separately. This project combines both in one system.

## What the system does

- Upload an ECG image and get a predicted rhythm class with a confidence score
- Enter clinical and lifestyle details (age, BMI, exercise, smoking, diabetes, etc.) to get a general health status
- Show an overall cardiac risk summary with severity, follow-up suggestion and model confidence
- User registration, login and prediction history stored in MySQL

## ECG classes

| Code | Class |
|------|-------|
| N | Normal |
| F | Atrial Fibrillation |
| M | Murmur |
| Q | Premature Ventricular Contraction |
| S | Supraventricular Tachycardia |
| V | Ventricular Tachycardia |

Health status classes (clinical data): Excellent, Very Good, Good, Fair, Poor.

## Tech stack

Python, Flask, TensorFlow / Keras, scikit-learn, XGBoost, Pandas, NumPy, Matplotlib, HTML / CSS / Bootstrap / JavaScript, MySQL.

## Approach

1. **Preprocessing:** ECG images resized to 160x160, normalised and augmented (rotation, flip, zoom). Clinical data label-encoded, imputed and scaled.
2. **Class imbalance:** handled with SMOTE, class weighting and augmentation.
3. **ECG models compared:** CNN, MobileNet (transfer learning), 3D-CNN.
4. **Clinical models compared:** Random Forest, XGBoost (CatBoost / LightGBM also compared in the paper).
5. **Evaluation:** accuracy, precision, recall, F1-score, confusion matrices.

## Results

**ECG image classification (6 classes, 24,799 test images)**

| Model | Accuracy | Notes |
|-------|----------|-------|
| CNN | ~99-100% | Best on this test set |
| 3D-CNN | 98% | Weak on Atrial Fibrillation (F1 0.60, only 161 samples) |
| MobileNet | 60% | Underperformed; unstable validation curve |

**Clinical data (general health status)**

| Model | Accuracy |
|-------|----------|
| Random Forest | 95.72% |

These results are from a held-out split of the datasets used. They have **not** been validated on external clinical data, and the near-perfect CNN score should be read with that in mind.

## Limitations and future work

- No validation on real clinical or external data
- Atrial Fibrillation is under-represented and hard to classify
- Planned: Transformer-based and hybrid CNN + Transformer models, explainable AI (SHAP, Grad-CAM), wearable ECG monitoring, mobile app

## Team

- **C. Tabsum**
- **S. Varsha**
- **V. Dinesh**

Guide: **Dr. C. Sasikala**, Associate Professor, Dept. of CSE, SRIT.

## License

Released under the [MIT License](LICENSE).
