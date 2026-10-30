# CL12 — Computational Lab 12

> A complete reference for all practicals across **Bio**, **IR**, **ML**, and **DMV** folders.
> Each folder has its own detailed README — this file provides a quick-reference master table.

---

## 📁 Folder Structure

```
CL12/
├── Bio/    → Bioinformatics Practicals        (README inside)
├── IR/     → Information Retrieval Practicals  (README inside)
├── ML/     → Machine Learning Practicals       (README inside)
└── DMV/    → Data Mining & Visualization       (README inside)
```

---

## 📋 Master Practicals Table

| Folder | Prac # | Practical Name | Notebook File | Dataset Required | Dataset File |
|--------|--------|----------------|---------------|-----------------|--------------|
| **Bio** | 1 | DNA Sequence Analysis | `1_DNA_Sequence_Analysis.ipynb` | ❌ No | Hardcoded in code |
| **Bio** | 2 | RNA-Seq Data Analysis | `2_RNA_Seq_Data_Analysis.ipynb` | ❌ No | Generated in code |
| **Bio** | 3 | Protein Structure Prediction | `3_Protein_Structure_Prediction.ipynb` | ❌ No | Fetched from PDB online |
| **Bio** | 4 | Molecular Docking & Virtual Screening | `4_Molecular_Docking_Virtual_Screening_Colab_FIXED_v2.ipynb` | ❌ No | Downloaded from PDB (ID: 1HVR) |
| **Bio** | 5 | ML for Genomic Data (SVM) | `5_Genomic_Data_ML_SVM.ipynb` | ✅ Yes | `Leukemia_GSE9476.csv` |
| **Bio** | 6 | Agricultural Genomics & GWAS | `6_Agricultural_Genomics_GWAS.ipynb` | ✅ Yes | `Genotypic_data.csv` + `Phenotypic_data.txt` |
| **IR** | 6 | Text Preprocessing | `6_Text_PreProcessing.ipynb` | ❌ No | Hardcoded in code |
| **IR** | 7 | Inverted Files (Inverted Index) | `7_Inverted_Files.ipynb` | ❌ No | Hardcoded in code |
| **IR** | 8 | Bayesian Network — Heart Disease | `8_Bayesian_Network_Heart_Data.ipynb` | ✅ Yes | `heart.csv` |
| **IR** | 9 | Agglomerative Hierarchical Clustering | `9_Agglomerative_Hierarchical_Clustering.ipynb` | ✅ Yes | `CC_GENERAL.csv` |
| **IR** | 10 | PageRank Algorithm | `10_Page_Rank_Algorithm.ipynb` | ❌ No | Hardcoded in code |
| **ML** | 1 | Principal Component Analysis (PCA) | `ML1_PCA_wine.ipynb` | ✅ Yes | `Wine.csv` |
| **ML** | 2 | Regression Analysis | `ML2_Regression_Analysis_Diabetes.ipynb` | ✅ Yes | `diabetes_prediction_dataset.csv` |
| **ML** | 3 | SVM Classification | `ML3_SVM_Classification.ipynb` | ❌ No | sklearn digits dataset (built-in) |
| **ML** | 4 | K-Means Clustering | `ML4_KMeans_Clustering_Iris.ipynb` | ✅ Yes | `Iris.csv` |
| **ML** | 5 | Voting Mechanism (Ensemble Learning) | `ML5_Voting_Mechanism_Iris.ipynb` | ✅ Yes | `Iris.csv` |
| **ML** | 6 | Q-Learning (Reinforcement Learning) | `ML6_with_visualizations.ipynb` | ❌ No | Simulated Tic-Tac-Toe environment |
| **DMV** | 1 | Weather API Data & Visualization | `DMV_1_WeatherAPIcheck.ipynb` | ❌ No | Fetched via OpenWeatherMap API |
| **DMV** | 2 | Telecom Customer Churn Analysis | `DMV_2_Telecom_Customer_Churn.ipynb` | ✅ Yes | `Telecom_Customer_Churn.csv` |
| **DMV** | 3 | Real Estate Price Analysis | `DMV_3_Real_Estate.ipynb` | ✅ Yes | `Bengaluru_House_Data.csv` |
| **DMV** | 4 (10B) | Delhi AQI Data Visualization | `DMV4_AQI.ipynb` | ✅ Yes | `delhi-weather-aqi-2025.csv` |
| **DMV** | 5 (11B) | Retail Sales Performance Analysis | `DMV5_Retail.ipynb` | ✅ Yes | `customer_shopping_data.csv` |

---

## 📦 Datasets Summary

| Dataset File | Folder | Used In | Size / Info |
|-------------|--------|---------|-------------|
| `Leukemia_GSE9476.csv` | `Bio/` | Bio P5 | 64 samples, 22,283 gene expression features |
| `Genotypic_data.csv` | `Bio/` | Bio P6 | 337 wheat lines, 23,130 SNPs |
| `Phenotypic_data.txt` | `Bio/` | Bio P6 | Wheat trait measurements |
| `heart.csv` | `IR/` | IR P8 | 303 patients, 14 features (Cleveland Heart Disease) |
| `CC_GENERAL.csv` | `IR/` | IR P9 | ~8,950 credit card customers, 17 features |
| `Wine.csv` | `ML/` | ML P1 | Wine chemical measurements, 3 customer segments |
| `diabetes_prediction_dataset.csv` | `ML/` | ML P2 | 100,000 patients, diabetes prediction |
| `Iris.csv` | `ML/` | ML P4, P5 | 150 iris flower samples, 3 species |
| `Telecom_Customer_Churn.csv` | `DMV/` | DMV P2 | 7,043 telecom customers, churn labels |
| `Bengaluru_House_Data.csv` | `DMV/` | DMV P3 | 13,000+ Bengaluru property listings |
| `delhi-weather-aqi-2025.csv` | `DMV/` | DMV P4 | Hourly AQI data for Delhi, 2025 |
| `customer_shopping_data.csv` | `DMV/` | DMV P5 | Retail transaction records from Istanbul malls |

---

## 📖 Detailed READMEs

For full explanations of each practical (theory, step-by-step code walkthrough, and key concepts), see the folder-level READMEs:

- 📂 [Bio/README.md](Bio/Readme.md) — Bioinformatics Practicals (P1–P6)
- 📂 [IR/README.md](IR/README.md) — Information Retrieval Practicals (P6–P10)
- 📂 [ML/README.md](ML/README.md) — Machine Learning Practicals (P1–P6)
- 📂 [DMV/README.md](DMV/README.md) — Data Mining & Visualization Practicals (P1–P5)
