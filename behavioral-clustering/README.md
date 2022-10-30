# LEMON Dataset Analysis for Sigrid Juselius 2022 Grant Application
## Data Cleaning and Behavioral clustering

---
### Clustering using Bayesian Gaussian Mixture model

*Sat-Sun 29-30 Oct 2022*

#### What was done:

* Dataset clustered using scikit-learn BayesianGaussianMixture
* Dataset with bgm_clusters column saved to processed_data/clustered_behavioral_LEMON.csv
* Feature importance tested using LogisticRegression processed_data/feature_importance_max(min)_logreg.csv


#### Comments:

##### BGM clustering step

Clustering seems to have found a pattern different from PCA, which is kind of expected and normal to me. Clusters differ by BMI, but just a bit:


| bgm_cluster | BMI | Waist_cm |
|---|---|---|
| 0 | 24.609786 | 87.00 |
| 1 | 22.951595 | 84.00 |
| 2 | 24.676041 | 88.00 |
| 3 | 23.655986 | 78.30 |
| 4 | 22.459971 | 80.75 |
| 5 | 25.368990 | 84.50 |
| 6 | 23.468269 | 80.50 |
| 7 | 24.037299 | 80.50 |
| 8 | 24.811673 | 85.50 |
| 9 | 23.312965 | 78.80 |
