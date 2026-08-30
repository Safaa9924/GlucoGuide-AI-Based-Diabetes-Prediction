# 💧 GlucoGuide

**AI-Based Diabetes Prediction, Classification & Personalized Recommendation System**
*Predict. Explain. Personalize. Prevent.*

A graduation project developed under the **DIGILIANS, Track: Applied AI & Data Analytics.

---

## 🎯 The Problem

Diabetes is one of the fastest-growing global health challenges — **589M adults** live with it worldwide (projected to reach **853M by 2050**), and **43% of them don't know it yet**. Egypt has the **highest diabetes burden in the MENA region**, with **13.2 million adults affected** and an age-standardised prevalence roughly double the global average.

Existing tools fall short in several ways:
- **Prediction without explanation** — models optimize accuracy but give no rationale clinicians or patients can trust.
- **No personalized guidance** — few systems translate a risk score into actionable, individual advice.
- **No lifestyle simulation** — users can't explore "what if" scenarios (e.g. quitting smoking, sleeping more, becoming active).
- **Fragmented features** — clinical and behavioral/lifestyle data are rarely combined in one predictive framework.
- **Limited real-world deployment** — most models stay inside research notebooks.

## 💡 The Solution

**GlucoGuide** is an end-to-end AI platform that turns raw patient data into a trustworthy, actionable prevention plan:

`Patient Data → AI Risk Prediction → SHAP Explanation → RAG Nutrition Support → Web Interface → Doctor Monitoring`

It combines **machine learning risk prediction**, **explainable AI (SHAP)**, an **evidence-grounded RAG nutrition assistant**, and an **interactive Streamlit web application** — unifying accuracy, explainability, personalization, and real-world usability in a single platform.

## 👥 Who It's For

- **Patients / at-risk individuals** — enter their data, get a risk score with a plain explanation, simulate lifestyle changes, and ask nutrition questions.
- **Doctors & clinicians** — monitor multiple patients, prioritize high-risk cases, verify OCR-extracted lab values, and use SHAP explanations to support clinical discussion.
- **Clinics & health platforms** — integrate a transparent, auditable AI layer into existing care workflows.

## ✅ Value Delivered

Better decisions · Healthier outcomes · Lower costs · Stronger prevention — by connecting AI, clinical expertise, and nutrition science into one proactive care loop (Prediction → Explainability → Personalization → Prevention).

---

## 🧠 What We Built

### Dataset
- **100,000 patient records**, **31 original features** (Kaggle Diabetes Healthcare Dataset)
- Feature groups: **Demographic** (age, gender, ethnicity, education, income, employment), **Lifestyle** (smoking, alcohol, physical activity, diet score, sleep, screen time), **Medical History** (family history, hypertension, cardiovascular history), **Clinical & Laboratory** (BMI, waist-hip ratio, blood pressure, HDL/LDL, triglycerides, glucose, insulin, HbA1c)
- Target variable: `diagnosed_diabetes`. Leakage-prone fields (`diabetes_risk_score`, `Diagnosis_encoded`) were explicitly excluded.

### Machine Learning Pipeline
Data → Preprocessing → Feature Engineering → Feature Selection → Model Training → Model Evaluation → Final Model

- **Preprocessing:** cleaning & validation, encoding & scaling, stratified 80/15/5 train/validation/test split.
- **Feature engineering:** created clinically meaningful ratios — BMI-to-Waist-Hip Ratio (central obesity), Total Cholesterol-to-HDL Ratio (cardiometabolic risk), Triglyceride-Glucose (TyG) Index (insulin resistance), Sleep-to-Screen Time Ratio (lifestyle balance), and a Postprandial-to-Fasting Glucose Ratio.
- **Feature selection:** Mutual Information analysis to retain the strongest predictive features; a PCA experiment reduced the feature space from 32 features to 3 components while retaining 95.57% of variance.
- **Class imbalance study:** compared Original vs. ROS vs. SMOTE vs. SMOTEENN resampling — the original (imbalanced) data gave the best overall performance and was used for final training.
- **Model training & tuning:** GridSearchCV with stratified cross-validation, identical preprocessing across all models, all experiments tracked in MLflow.

### Models Compared
Five algorithms were trained and evaluated on identical data: **SVM**, **Random Forest**, **XGBoost**, **LightGBM**, and a **Multi-Layer Perceptron (MLP)** neural network used as the deep learning benchmark for capturing nonlinear feature interactions.

| Model | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
|---|---|---|---|---|---|
| SVM | 86.93% | 87.40% | 86.93% | 86.95% | 93.88% |
| **MLP (Neural Network)** | 90.47% | 91.23% | 90.47% | 90.42% | 94.42% |
| Random Forest | 91.63% | 92.59% | 91.63% | 91.52% | 94.86% |
| **XGBoost (Final Model)** | **91.63%** | **92.58%** | **91.63%** | **91.54%** | **95.12%** 🏆 |
| LightGBM | 91.20% | 91.95% | 91.20% | 91.10% | 94.95% |

**XGBoost** was selected as the final model for its highest overall performance, robustness, ability to handle feature complexity, native SHAP compatibility, and efficient deployment footprint.

### Explainable AI
Used **SHAP** to turn every prediction into a transparent explanation:
- **Global importance:** ranks features by overall impact — **HbA1c** is the strongest predictor, followed by postprandial and fasting glucose, then family history and age.
- **Individual explanation:** shows how each feature influenced a specific patient's risk score.
- This builds clinical trust and lets doctors verify *why* a patient was flagged as high-risk.

### RAG Nutrition Assistant
An evidence-grounded Retrieval-Augmented Generation (RAG) assistant answers patient nutrition questions using a trusted clinical source (*Nutritional Management of Diabetes Mellitus* — Frost, 2003), processed into **271 pages / 312 chunks**:

`Document Cleaning → Section-Aware Chunking → BM25 + Semantic Index → Hybrid Retrieval (50/50 lexical + semantic) → Cross-Encoder Reranking → Context Filtering → Grounded Answer`

This ensures every nutrition answer is generated **only from retrieved, verified evidence** — not hallucinated.

### Platform Features
- **Risk prediction** with confidence score and diabetes-stage classification
- **SHAP-based explainability** for every prediction
- **Lifestyle simulation** — explore how changing smoking, activity, sleep, or BMI affects risk
- **RAG-powered nutrition Q&A assistant**
- **OCR** for automated extraction from lab reports
- **Interactive Streamlit web app** with separate Patient and Doctor portals
- **Doctor dashboard** for monitoring multiple patients and reviewing high-risk cases

---

## 🛠️ Tech Stack
`Python` · `Scikit-learn` · `XGBoost` · `LightGBM` · `MLP / Neural Networks` · `SHAP` · `RAG (BM25 + Semantic Search + Cross-Encoder Reranking)` · `OCR` · `LLMs` · `Streamlit` · `MLflow`

## 🔭 Future Work
CGM (Continuous Glucose Monitor) integration · Clinical/EHR integration · Longitudinal patient monitoring · RAG knowledge base expansion · Advanced OCR for diverse lab formats · Automated model recalibration · Smart clinical alerts

## 🎓 About the Project
Graduation project — **Digital Pioneers Initiative (رواد رقميون)**, Track: Applied AI & Data Analytics
Supervisor: Dr. Kamel El-Hadad · Track Head: Dr. Aya Hossam

**Team:** Shahinaz Abdelawad · Samah Mohamed Mesilhy · Samar Ahmed Mahmoud · Safaa Samy Mohamed · Haidy Ashraf AbdElazeam · Sally El Sayed Mostafa

### My Role
Worked on the machine learning modeling track — building and evaluating the **MLP neural network model** as the deep learning benchmark, contributing to **feature engineering** (clinically-derived ratio features and their evaluation via Mutual Information/PCA), and developing the **RAG-based nutrition assistant** (document processing, hybrid retrieval, and grounded answer generation).

---

*"From Prediction to Prevention."*
