# University Clustering — K-Means & PCA
### Unsupervised Learning · Clustering · Dimensionality Reduction · Python

![Python](https://img.shields.io/badge/Python-3.11-blue?style=flat&logo=python)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML-orange?style=flat&logo=scikit-learn)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=flat&logo=pandas)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat&logo=jupyter)
![Accuracy](https://img.shields.io/badge/Cluster%20Accuracy-78%25-brightgreen?style=flat)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=flat)

---

## Overview

This project applies **K-Means Clustering** to group 777 US universities into natural clusters based on academic and financial features — without using the Private/Public label during training.

After clustering, **Principal Component Analysis (PCA)** is used to reduce 18 features to 2 principal components for visualisation and interpretation.

This is an **unsupervised learning** project — the model receives no labels. The goal is to discover whether meaningful structure exists in the data purely from feature patterns.

---

## Problem Statement

Can a machine separate private and public universities purely from their academic stats — without ever being told which is which?

Using K-Means, the algorithm is given 18 features (applications, tuition, graduation rate, faculty stats, etc.) and asked to find 2 natural clusters. The resulting clusters are then compared against the actual Private/Public labels to evaluate quality.

---

## Dataset

**File:** `College_Data.txt` — 777 US university records

| Feature | Description |
|---|---|
| `Private` | Yes/No — used only for evaluation, NOT for training |
| `Apps` | Number of applications received |
| `Accept` | Number of applicants accepted |
| `Enroll` | Number of new students enrolled |
| `Top10perc` | % of new students from top 10% of high school class |
| `Top25perc` | % of new students from top 25% of high school class |
| `F.Undergrad` | Number of full-time undergraduates |
| `P.Undergrad` | Number of part-time undergraduates |
| `Outstate` | Out-of-state tuition ($) |
| `Room.Board` | Room and board costs ($) |
| `Books` | Estimated book costs ($) |
| `Personal` | Estimated personal spending ($) |
| `PhD` | % of faculty with PhDs |
| `Terminal` | % of faculty with terminal degrees |
| `S.F.Ratio` | Student-to-faculty ratio |
| `perc.alumni` | % of alumni who donate |
| `Expend` | Instructional expenditure per student ($) |
| `Grad.Rate` | Graduation rate (%) |

---

## Project Workflow

```
Data Loading → EDA → K-Means Clustering (K=2) → Evaluation → PCA → Visualisation
```

**1. Exploratory Data Analysis**
- `df.info()` and `df.describe()` for structure and statistics
- Distribution plots and pairplots coloured by Private/Public
- Scatter plots: Grad Rate vs Outstate, Room.Board vs Outstate

**2. K-Means Clustering**
- `KMeans(n_clusters=2)` from Scikit-learn
- Trained on all numeric features, excluding the `Private` label
- Cluster labels (0, 1) assigned to each university

**3. Cluster Evaluation**
- `Private` column converted to binary (1 = Private, 0 = Public)
- Compared against KMeans cluster labels using confusion matrix and classification report
- Overall accuracy: **78%** — without ever seeing the labels during training

**4. PCA — Dimensionality Reduction**
- Applied `StandardScaler` before PCA
- Reduced 18 features → 2 principal components (PC1, PC2)
- PCA component heatmap to interpret feature contributions
- Scatter plot of universities in 2D PCA space coloured by cluster

---

## Results

### Cluster Evaluation vs Private/Public Labels

| Class | Precision | Recall | F1-Score | Support |
|---|---|---|---|---|
| 0 (Public) | 0.79 | 0.94 | 0.86 | 565 |
| 1 (Private) | 0.69 | 0.35 | 0.46 | 212 |
| **Overall Accuracy** | | | **0.78** | **777** |

### Confusion Matrix

```
              Predicted 0    Predicted 1
Actual 0         531             34
Actual 1         138             74
```

### Key Findings

- The model correctly grouped **78% of universities** without any label supervision
- Public universities (Cluster 0) are identified with high recall (94%) — the model rarely misclassifies a public university
- Private universities (Cluster 1) are harder to isolate — some private universities share financial profiles with public ones
- PCA revealed that **out-of-state tuition, expenditure per student, and graduation rate** drive the primary axis of separation (PC1)

---

## Tech Stack

| Tool | Purpose |
|---|---|
| Python 3.11 | Core language |
| Pandas | Data loading & manipulation |
| NumPy | Numerical operations |
| Scikit-learn | KMeans, PCA, StandardScaler, metrics |
| Seaborn | Heatmaps, pairplots |
| Matplotlib | Scatter plots, PCA visualisation |
| Jupyter Notebook | Development environment |

---

## How to Run

**1. Clone the repository**
```bash
git clone https://github.com/SouravDey1/university-kmeans-clustering.git
cd university-kmeans-clustering
```

**2. Install dependencies**
```bash
pip install pandas numpy scikit-learn seaborn matplotlib jupyter
```

**3. Add the dataset**

Place `College_Data.txt` in the project root folder.

**4. Open the notebook**
```bash
jupyter notebook project_K_Means_Clustering.ipynb
```

---

## Repository Structure

```
university-kmeans-clustering/
│
├── project_K_Means_Clustering.ipynb   # Full notebook — EDA, KMeans, PCA
├── College_Data.txt                   # Dataset (add manually)
└── README.md                          # This file
```

---

## What I Learned

- The fundamental difference between **supervised and unsupervised learning** — no labels, no loss function, just structure in the data
- How **K-Means works** — centroid initialisation, distance assignment, iterative updating until convergence
- Why **PCA matters** — visualising 18-dimensional data is impossible; reducing to 2 components makes patterns visible and interpretable
- Why **StandardScaler is essential before PCA** — PCA is variance-based; unscaled features with large ranges dominate all components
- How to **evaluate unsupervised clusters** when ground truth labels are available as a sanity check — not for training, but for post-hoc validation
- That **78% cluster accuracy with zero label supervision** is genuinely impressive — the data naturally separates by institutional type

---

## Author

**Sourav Dey**
Final-Year EEE Student · Ahsanullah University of Science and Technology (AUST)
📧 sourav41dey@gmail.com
🔗 [LinkedIn](https://www.linkedin.com/in/sourav-dey-754298251/)
🐙 [GitHub](https://github.com/SouravDey1)

---

*Part of my Data Science & Machine Learning portfolio.*

*Other projects:*
- [California Housing — Random Forest](https://github.com/SouravDey1/california-housing-random-forest)
- [Diabetes Prediction — KNN](https://github.com/SouravDey1/diabetes-knn-classification)
- [Ad Click Prediction — Logistic Regression](https://github.com/SouravDey1/ad-click-logistic-regression)
- [E-Commerce Spending — Linear Regression](https://github.com/SouravDey1/ecommerce-linear-regression)
