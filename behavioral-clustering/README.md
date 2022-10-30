# LEMON Dataset Analysis for Sigrid Juselius 2022 Grant Application
## Data Cleaning and Behavioral clustering

---
### Clustering using Bayesian Gaussian Mixture model

*Sat-Sun 29-30 Oct 2022*

#### What was done:

[x] Dataset clustered using scikit-learn BayesianGaussianMixture
[x] Dataset with bgm_clusters column saved to processed_data/clustered_behavioral_LEMON.csv
[x] Feature importance tested using LogisticRegression processed_data/feature_importance_max(min)_logreg.csv


#### Comments:

##### BGM clustering step

Clustering seems to have found a pattern different from PCA, which is kind of expected and normal to me.  
Clusters differ by BMI (median), and are promising on that account at a first glance:


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

However, the BGM algorithm is a variational inference algorithm. I provided 10 clusters and expected that it would only use a few. It would be seen as zero weights assigned to clusters. But I got the following result:

```python
array([0.07, 0.11, 0.09, 0.15, 0.08, 0.08, 0.13, 0.07, 0.11, 0.11])
```

To me that gives ambiguity as there are no zero-weight clusters (even when I added 20 instead of 10). Because of that I am thinking to try another algorithm like Gaussian Mixture or something simpler. Also introducing a BMI threshold and clustering only overweight subjects might be a good idea. PCA already shows behavioral differences between normal weight and overweight subjects. So with clustering I could focus only on overweight at this stage.  
In the proposal that's a good idea to emphasize the need for BIOBANK acsess as it has behavioral data as well together with wider BMI range.

###### To-do:
[] Try a simpler clustering
[] Split data and cluster only overweight (quite few for clustering?)

##### Cluster description/feature importance step (Logistic Regression)

I used multimodal logistic regression to assess which features drive which clusters. BMI or other anthropometric features were not among the top-1 ones. I constructed tables of features with maximal and minimal coefficients.  

Features of maximal coefficients for each cluster:
| 0 | COPE_Acceptance |
| 1 | CVLT_1 |
| 2 | NEOFFI_Extraversion |
| 3 | TAP_WM_11 |
| 4 | FSoZu_Zuf |
| 5 | NYC-Q_lemon_21 |
| 6 | TeiQueSF_sociability |
| 7 | RWT_1 |
| 8 | TICS_WorkDiscontent |
| 9 | TAP_I_24 |

Features of minimal coefficients for each cluster:

| 0 | MDBF_Day2_WM_Scale |
| 1 | MARS_Cognitive_Distraction |
| 2 | TICS_PressuereToPerform |
| 3 | COPE_Humor |
| 4 | CERQ_Acceptance |
| 5 | MDBF_Day2_GS_Scale |
| 6 | NYC-Q_lemon_14 |
| 7 | COPE_activeCoping |
| 8 | NYC-Q_lemon_18 |
| 9 | TAP_WM_11 |


###### To-do:
[] Read more on interpretation of clusters in multidimensional data
[] Read on logistic regression and maybe there are better algorithms for my aim?
[] What would be the best visualization for cluster description?
[] Read about all the tests/tasks which have high/low coefficients
