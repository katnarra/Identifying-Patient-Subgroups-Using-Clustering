The aim of the project was to identify patient subgroups across the liver disease spectrum using clustering techniques and multivariate analysis. 
Data dimensionality was reduced using principal component analysis. Clusters were visualized and their separability was validated with UMAP.
Below is a short report of the project.

# Introduction
This study explores the use of clustering techniques to identify patient subgroups based on a set of clinical and 
demographic variables. Preprocessing steps such as feature selection, scaling, and dimensionality reduction are applied
to improve clustering quality and interpretability. The aim is to determine whether meaningful and well-separated sub-
groups can be identified, and to characterize these groups in a way that may inform further investigation or decisionmaking.

# Methods
This study analyzed a patient dataset comprising laboratory measurements and demographic variables. The objective was to group 
patients into meaningful clusters without predefined class labels. Clustering analysis was employed to identify naturally 
occurring patterns within the data.

The dataset consists of 614 patients. Variables used in the analysis include laboratory measurements (ALB, ALP, CHOL, PROT, etc.) and demographic variables.
The demographic variables were age and gender, along with the target variable, which included: blood donor, suspected blood donor, hepatitis C and
disease stage (fibrosis/cirrhosis).

## Preprocessing
To evaluate potential outliers prior to clustering, boxplots were generated for all numerical variables. Based on
these visualizations, markedly extreme values were identified in several biomarkers associated with liver function.
To improve interpretabillity, upper thresholds were defined for these variables with the aim of highlighting the range of extreme observations.
The data was shuffled to remove any potential order bias originating from data collection or storage procedures, ensuring randomness in downstream analyses.
Given the class imbalance inherent in clinical datasets oversampling was performed on the data to balance class distributions and enhance the ability 
of clustering and classification algorithms to learn minority class patterns.
Missing numerical values were imputed with the median of the respective variables, and missing categorical values were encoded as 'unknown'.
Numerical features were scaled to ensure that all variables contribute equally to the model, particularly for
algorithms sensitive to feature magnitude, such as distance-based or regularized methods. umerical features were transformed to have zero meaan
and unit variance.

PCA was conducted for the purpose of feature selection. After examining the explained variance ratio, the first five principal components were 
chosen for further analysis. The optimal number of clusters was determined using the Elbow method. Because the plot did not exhibit a clear inflection point,
silhouette analysis was also carried out, resulting in k=2 distinct clusters. 

## Clustering Methods
This project was conducted in the hopes of successfully grouping patients into meaningful clusters based on their laboratory values and demographic features. 
To accomplish this, both K-means and hierarchical clustering were applied to explore and compare different clustering strategies and their results.

## Result Visualization
To visually assess clustering results, the samples were plotted in two-dimensional plots and coloured according to either their predicted cluster labels or 
true class labels. The Python package Uniform Manifold Approximation and Projection (UMAP) helped reduce the high-dimensionality of
the clustering results, which allowed a better visualization of cluster separability.

# Results & Discussion
The application of both K-means and hierarchical clustering methods revealed that the data naturally segregates into two
primary clusters, which aligns with the silhouette scores and dendrogram analysis indicating an optimal grouping into two distinct subgroups.
There were some misclassifications, such as samples belonging to categories 1 and 2 being grouped closely with category 0, which highlight the challenges in capturing subtle
distinctions with only a few principal components. Based on the results, category 3 is clearly identifiable and forms a distinct, though sparse cluster across
multiple visualizations. This indicates that the features used effectively separate category 3 from the rest of the data.
In contrast, categories 0, 1, and 2 tend to overlap significantly, especially in the lower-dimensional representations such as UMAP projections and the hierarchical 
clustering dendrogram. The overlaps suggest that the features do not provide enough discriminative power to distinctly separate these categories, reflecting their 
subtle differences or high similarity. This is further evidenced by the fact that both K-means and hierarchical clustering predominantly split the
data into two main groups, often combining categories 0, 1, and 2 into a single cluster.
Overall, the results suggest that current features and clustering methods are effective for identifying the primary division of the data (category 3), but more sophisticated feature 
extraction or additional data may be needed to differentiate categories 0, 1, and 2 with higher accuracy.
The fact that only the separation of patients with endstage chronic liver disease can be predicted supports the idea that cirrhosis is associated with physiological or molecular 
changes that differ significantly from earlier or less severe stages. This could mean that the laboratory values used in the dataset change significantly when moving to cirrhosis
from the other subgroups. The lack of separability between healthy or near-healthy patients and hepatitis C or fibrosis patients could be due to the laboratory results not being 
sensitive enough to detect these disease stages. 
The results of this project may be affected by the number of samples representing different subgroups. There was a major imbalance with category 0, which had over 500 samples, 
compared to the others, which had about 15-20 samples. Although oversampling of categories 1-3 was done, there still existed a lack of variance within the subgroups. It could mean 
that there were not enough different samples belonging to the same subgroups to form meaningful patterns. In addition, the reduction of dimensionalities could compress subtle distinctions 
between categories 0-2.
Incorporating additional features, such as imaging data of the liver, could also provide more precise distinctions between these patient subgroups. These methods 
offer opportunities to improve accuracy and clinical relevance of unsupervised patient classification as well as deepen our understanding of disease progression in liver
conditions.
