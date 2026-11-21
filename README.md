# Residency Day 2 – Project Deliverable 3
## Classification, Clustering, and Pattern Mining

### Project Overview
This project applies supervised classification, model evaluation, clustering, and association rule mining to the California Housing dataset. The notebook continues the housing-data analysis and uses engineered housing attributes to support the analysis.

**Execution status:** The notebook is still running. This README records only the results visible in the screenshots supplied so far. Hyperparameter tuning, clustering, and Apriori results have not yet been confirmed and will be added after those notebook cells finish.

---

### Dataset
- **Dataset:** California Housing
- **Source:** `sklearn.datasets.fetch_california_housing`
- **Number of observations:** 20,640
- **Original columns:** 8 predictor variables and the median house value target
- **Missing values:** 0 in the displayed missing-value check
- **Training observations:** 16,512
- **Testing observations:** 4,128

The target variable, `median_house_value`, is continuous. For classification, it was converted into two classes using the dataset median:
- **Class 0:** Median house value at or below the median
- **Class 1:** Median house value above the median

The target is expressed in units of $100,000.

### Data Preparation and Feature Engineering
The notebook:
1. Loaded the California Housing dataset.
2. Checked the dataset structure, summary statistics, missing values, and duplicate rows.
3. Examined the distribution of median house values.
4. Created additional predictors:
   - `rooms_per_household`
   - `bedrooms_per_room`
   - `population_per_household`
   - `income_per_room`
5. Created a binary housing-value class using the median target value.
6. Split the data into training and testing sets using an 80/20 split and stratification.

The displayed data checks show no missing values. The dataset contains 20,640 observations.

### Classification Models
Two classification models were trained and evaluated:
- Decision Tree Classifier
- Random Forest Classifier

The test-set results visible so far are:

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Decision Tree | 0.8530 | 0.8507 | 0.8560 | 0.8533 | 0.9092 |
| Random Forest | 0.8861 | 0.8957 | 0.8740 | 0.8847 | 0.9559 |

**Current result:** The Random Forest performs better than the Decision Tree on all five displayed evaluation metrics. Its test accuracy is approximately 88.61%, and its ROC-AUC is approximately 0.9559.

#### Classification report results
The screenshots show the following rounded class-level results:

**Decision Tree**
- Class 0: precision 0.86, recall 0.85, F1-score 0.85
- Class 1: precision 0.85, recall 0.86, F1-score 0.85
- Overall accuracy: 0.85

**Random Forest**
- Class 0: precision 0.88, recall 0.90, F1-score 0.89
- Class 1: precision 0.90, recall 0.87, F1-score 0.88
- Overall accuracy: 0.89

#### Confusion matrices
The displayed confusion matrices use rows for actual labels and columns for predicted labels.

**Decision Tree**
| Actual / Predicted | Lower/equal | Higher |
|---|---:|---:|
| Lower/equal | 1,755 | 310 |
| Higher | 297 | 1,766 |

**Random Forest**
| Actual / Predicted | Lower/equal | Higher |
|---|---:|---:|
| Lower/equal | 1,855 | 210 |
| Higher | 260 | 1,803 |

The Random Forest makes fewer errors than the Decision Tree on the displayed test set.

#### ROC curve
The ROC curve screenshot reports:
- Decision Tree AUC: **0.909**
- Random Forest AUC: **0.956**

The Random Forest ROC curve is closer to the upper-left corner, indicating stronger discrimination between the two housing-value classes on this test set.

### Hyperparameter Tuning
The notebook includes a GridSearchCV procedure to tune the Random Forest using three-fold cross-validation and F1-score as the selection metric.

**Status:** The tuning cell has not yet produced a confirmed result in the screenshots provided. Add the best parameter values and tuned test metrics after execution finishes.

### K-Means Clustering
The notebook standardizes the engineered housing predictors and evaluates candidate cluster counts from 2 through 6 using inertia and silhouette score. It then fits K-Means and uses PCA to visualize the clusters.

**Status:** Clustering results are still pending. Add the selected number of clusters, silhouette score, cluster sizes, and cluster-profile interpretation after the relevant cells finish.

### Apriori Association Rule Mining
The notebook converts housing attributes into descriptive categories for:
- Income band
- House-age band
- Average-rooms band
- House-value band

Apriori is then used to identify frequent itemsets and association rules.

**Important limitation:** The California Housing dataset is not a transaction or shopping-basket dataset. Each district is represented by a set of derived housing categories. Therefore, any rules describe co-occurrence among housing categories; they do not describe customer purchases or prove causal relationships.

**Status:** Frequent itemsets and association rules are still pending. Add the generated rule count and strongest rule after execution finishes.

### Current Interpretation
Based on the classification outputs available so far, Random Forest is the stronger of the two initial classification models. It achieves higher accuracy, precision, recall, F1-score, and ROC-AUC than the Decision Tree on the held-out test set.

The remaining tuning, clustering, and association-rule outputs are necessary before the full deliverable can be considered complete.

### Files to Include in the GitHub Repository
- `Residency_Day_2_Deliverable_3.ipynb`
- `README.md`
- `classification_model_results.csv`
- `classification_comparison_results.csv`
- `kmeans_cluster_selection.csv`
- `kmeans_cluster_profiles.csv`
- `apriori_frequent_itemsets.csv`
- `apriori_association_rules.csv` (if rules are generated)

The CSV files are created by the notebook near the end of execution. Include them after the corresponding cells have completed successfully.

### How to Run
1. Open Google Colab.
2. Upload `Residency_Day_2_Deliverable_3.ipynb`.
3. Select **Runtime → Run all**.
4. Allow the notebook to download the dataset and install the Apriori dependency.
5. Wait until all cells finish.
6. Review the outputs and confirm that there are no failed cells.
7. Download the generated CSV files.
8. Update this README with the final tuning, clustering, and Apriori results before submission.

### References
Scikit-learn developers. (n.d.). *California Housing dataset*. https://scikit-learn.org/stable/datasets/real_world.html#california-housing-dataset

Scikit-learn developers. (n.d.). *Supervised learning*. https://scikit-learn.org/stable/supervised_learning.html

Scikit-learn developers. (n.d.). *Clustering*. https://scikit-learn.org/stable/modules/clustering.html

Raschka, S., & contributors. (n.d.). *Mlxtend: A library of machine learning and scientific computing tools*. https://rasbt.github.io/mlxtend/
