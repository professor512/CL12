# 🤖 ML — Machine Learning Practicals

> A comprehensive guide to all practicals in the **ML** folder, covering the theory, code workflow, and dataset requirements.

---

## Practicals Overview

| # | Practical | File | Dataset Required | Dataset File |
|---|-----------|------|-----------------|--------------|
| 1 | Principal Component Analysis (PCA) | `ML1_PCA_wine.ipynb` | ✅ Yes | `Wine.csv` |
| 2 | Regression Analysis | `ML2_Regression_Analysis_Diabetes.ipynb` | ✅ Yes | `diabetes_prediction_dataset.csv` |
| 3 | SVM Classification | `ML3_SVM_Classification.ipynb` | ❌ No | sklearn digits dataset (built-in) |
| 4 | K-Means Clustering | `ML4_KMeans_Clustering_Iris.ipynb` | ✅ Yes | `Iris.csv` |
| 5 | Voting Mechanism (Ensemble Learning) | `ML5_Voting_Mechanism_Iris.ipynb` | ✅ Yes | `Iris.csv` |
| 6 | Q-Learning (Reinforcement Learning) | `ML6_with_visualizations.ipynb` | ❌ No | Simulated Tic-Tac-Toe environment |

---

## 📉 Practical 1 — Principal Component Analysis (PCA) on Wine Data

**File:** `ML1_PCA_wine.ipynb`
**Dataset Required:** ✅ **`Wine.csv`** (present in `ML/` folder)

### What is it?
PCA is a **dimensionality reduction** technique. When a dataset has many features (columns), PCA compresses them into fewer **principal components** that still capture most of the variation. Used here to visualize wine samples in 2D.

### Dataset (`Wine.csv`):
- Wine chemical measurements with `Customer_Segment` labels (1, 2, 3)
- Features include alcohol content, acidity, color intensity, etc.

### What the Code Does (Step by Step):

1. **Load Data:**
   ```python
   df = pd.read_csv("Wine.csv")
   ```

2. **Separate Features & Target:**
   - Features: all numeric columns except `Customer_Segment`
   - Target: `Customer_Segment` (wine type label)

3. **Standardize Features** – Uses `StandardScaler` to normalize all columns to mean=0, std=1 (required before PCA)

4. **Apply PCA:**
   ```python
   pca = PCA(n_components=2)
   X_pca = pca.fit_transform(X_scaled)
   ```
   - Reduces all features to just 2 components
   - `explained_variance_ratio_` shows how much information is kept

5. **Visualize** – 2D scatter plot with each wine type colored differently

### Key Concepts:
| Term | Meaning |
|------|---------|
| PCA | Dimensionality reduction via orthogonal transformation |
| Principal Component | A new axis that captures maximum variance |
| Explained Variance | % of data variation captured by each component |
| StandardScaler | Normalizes features to same scale before PCA |

---

## 📊 Practical 2 — Regression Analysis on Diabetes Data

**File:** `ML2_Regression_Analysis_Diabetes.ipynb`
**Dataset Required:** ✅ **`diabetes_prediction_dataset.csv`** (present in `ML/` folder)

### What is it?
Regression analysis predicts a continuous or categorical outcome from input features. This practical applies both **Linear Regression** and **Logistic Regression** to a diabetes prediction dataset.

### Dataset (`diabetes_prediction_dataset.csv`):
- **100,000 patients** with health features
- Columns: `age`, `gender`, `bmi`, `HbA1c_level`, `blood_glucose_level`, `hypertension`, `heart_disease`, `diabetes` (target)

### What the Code Does (Step by Step):

1. **Load & Explore Data:**
   ```python
   df = pd.read_csv("diabetes_prediction_dataset.csv")
   ```

2. **Preprocess:**
   - Handle missing values
   - Check duplicates
   - Encode categorical columns (e.g., `gender`) using `LabelEncoder`

3. **Linear Regression** – Predicts `blood_glucose_level` from other features:
   - Metrics: MSE, R² Score

4. **Logistic Regression** – Classifies whether a patient has `diabetes` (0 or 1):
   - Metrics: Accuracy, Confusion Matrix, Classification Report

5. **Statistical Analysis** – Uses `statsmodels` for detailed regression statistics (p-values, confidence intervals)

6. **Visualization** – Scatter plots, regression line, residual plots

### Key Concepts:
| Term | Meaning |
|------|---------|
| Linear Regression | Predicts a continuous output from input features |
| Logistic Regression | Classifies into categories using a sigmoid function |
| R² Score | How well the regression fits the data (1.0 = perfect) |
| MSE | Mean Squared Error — average squared prediction error |
| p-value | Statistical significance of each feature's contribution |

---

## 🔢 Practical 3 — SVM Classification on Digits Dataset

**File:** `ML3_SVM_Classification.ipynb`
**Dataset Required:** ❌ None (uses sklearn's built-in **digits dataset**)

### What is it?
**Support Vector Machine (SVM)** finds the optimal hyperplane that separates classes with the maximum margin. Applied here to classify handwritten digits (0–9) from 8x8 pixel images.

### Dataset (Built-in `sklearn.datasets.load_digits`):
- **1,797 images** of handwritten digits
- Each image = 8x8 pixels = 64 features
- 10 classes: digits 0 to 9

### What the Code Does (Step by Step):

1. **Load Data:**
   ```python
   from sklearn.datasets import load_digits
   digits = load_digits(n_class=10)
   ```

2. **Visualize Digits** – 8x8 grid of sample digit images

3. **Train SVM:**
   ```python
   svc = svm.SVC(gamma=0.001, C=100)
   svc.fit(main_data[:1501], targets[:1501])
   ```
   - Trains on first 1,501 samples
   - `gamma=0.001`: controls RBF kernel width
   - `C=100`: regularization parameter

4. **Predict:** Predicts labels for remaining ~296 test samples

5. **Evaluate:**
   - Confusion matrix
   - Classification report (precision, recall, F1 per digit)

### Key Concepts:
| Term | Meaning |
|------|---------|
| SVM | Support Vector Machine — maximizes margin between classes |
| Hyperplane | Decision boundary separating two classes |
| Kernel | Function that maps data to higher dimensions (RBF, Linear) |
| gamma | Controls how far the influence of a single training example reaches |
| C | Regularization: trades off correct classification vs. margin width |

---

## 🔵 Practical 4 — K-Means Clustering on Iris Data

**File:** `ML4_KMeans_Clustering_Iris.ipynb`
**Dataset Required:** ✅ **`Iris.csv`** (present in `ML/` folder)

### What is it?
**K-Means** is an unsupervised clustering algorithm. It groups data points into `k` clusters by minimizing the distance from each point to its cluster center (centroid). Applied here to cluster Iris flower measurements.

### Dataset (`Iris.csv`):
- **150 samples** of iris flowers
- 4 features: `SepalLengthCm`, `SepalWidthCm`, `PetalLengthCm`, `PetalWidthCm`
- 3 species: *Setosa*, *Versicolor*, *Virginica*

### What the Code Does (Step by Step):

1. **Load Data:**
   ```python
   data = pd.read_csv("archive/Iris.csv")
   ```

2. **Explore:** Shape, column types, basic statistics

3. **Apply K-Means:**
   ```python
   KMeans(n_clusters=3, random_state=42)
   ```

4. **Elbow Method** – Plots inertia (within-cluster sum of squares) vs. k to find optimal number of clusters

5. **Visualize Clusters** – Scatter plot of clusters with centroids marked

6. **Compare with True Labels** – Checks how well K-Means clusters match actual species

### Key Concepts:
| Term | Meaning |
|------|---------|
| K-Means | Partitions data into k groups based on distance to centroids |
| Centroid | Center point of a cluster (mean of all points in the cluster) |
| Inertia | Sum of squared distances from points to their centroids |
| Elbow Method | Finds optimal k where inertia improvement levels off |

---

## 🗳️ Practical 5 — Voting Mechanism (Ensemble Learning) on Iris Data

**File:** `ML5_Voting_Mechanism_Iris.ipynb`
**Dataset Required:** ✅ **`Iris.csv`** (present in `ML/` folder)

### What is it?
**Ensemble Learning** combines multiple models to get better predictions than any single model. A **Voting Classifier** aggregates predictions from several classifiers — each "votes" for a class and the majority wins (or probabilities are averaged for soft voting).

### Dataset (`Iris.csv`):
- **150 iris flower samples**, 3 species, 4 features
- Same as Practical 4 but used for classification (species prediction)

### What the Code Does (Step by Step):

1. **Load & Encode:**
   ```python
   df = pd.read_csv("Iris.csv")
   y = LabelEncoder().fit_transform(df['Species'])
   ```

2. **Three Base Models:**
   - **AdaBoost** – Boosts weak learners by focusing on misclassified samples
   - **Gradient Boosting** – Builds trees sequentially, each correcting previous errors
   - **XGBoost** – Highly optimized gradient boosting (requires `pip install xgboost`)

3. **Voting Classifier:**
   ```python
   VotingClassifier(estimators=[('ada', ada), ('gb', gb), ('xgb', xgb)], voting='soft')
   ```

4. **Evaluate All Models** – Accuracy, Precision, Recall, F1 for each base model and the ensemble

5. **Confusion Matrices** – For each model to compare performance

6. **Visualization** – Bar chart comparing all model accuracies

### Key Concepts:
| Term | Meaning |
|------|---------|
| Ensemble Learning | Combining multiple models for better performance |
| Voting Classifier | Aggregates predictions from multiple classifiers |
| AdaBoost | Adaptive Boosting — upweights misclassified samples |
| Gradient Boosting | Sequentially corrects errors of previous trees |
| XGBoost | Extreme Gradient Boosting — fast and optimized |
| Soft Voting | Averages predicted probabilities across classifiers |

---

## 🎮 Practical 6 — Q-Learning (Reinforcement Learning) for Tic-Tac-Toe

**File:** `ML6_with_visualizations.ipynb`
**Dataset Required:** ❌ None (agent learns by playing a simulated Tic-Tac-Toe environment)

### What is it?
**Q-Learning** is a Reinforcement Learning algorithm. An agent interacts with an environment, takes actions, receives rewards, and learns which actions maximize long-term reward — all without any labeled training data. Applied here to learn to play Tic-Tac-Toe.

### What the Code Does (Step by Step):

1. **Environment (`TicTacToeEnvironment`)**:
   - 9-cell board, players are +1 and -1
   - Checks wins and draws
   - Returns available moves per state

2. **Q-Learning Agent (`QLearningAgent`)**:
   - **Q-Table:** `3^9 x 9` matrix — one row per board state, one column per action
   - **State Index:** Encodes board state as a base-3 number
   - **Exploration vs. Exploitation:** Uses `exploration_rate=0.3` (30% random moves, 70% best known move)

3. **Training Loop** – Plays thousands of games:
   - Each move updates the Q-table:
     ```
     Q(s, a) += lr * (reward + gamma * max_Q(s') - Q(s, a))
     ```
   - `lr` = learning rate (0.9), `gamma` = discount factor (0.9)

4. **Visualization:**
   - Win/Draw/Loss rates over training episodes
   - Q-value evolution for specific states
   - Board heatmaps showing agent's preferred moves

### Key Concepts:
| Term | Meaning |
|------|---------|
| Reinforcement Learning | Learning by trial and error with rewards/penalties |
| Q-Table | Maps (state, action) pairs to expected future rewards |
| Exploration Rate | Probability of taking a random action (epsilon-greedy) |
| Discount Factor (gamma) | How much future rewards are weighted vs. immediate ones |
| Convergence | When the Q-table stops changing significantly between episodes |
