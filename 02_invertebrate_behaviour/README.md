## 02. INVERTEBRATE BEHAVIOUR:

5 codefiles can be found in this folder on clustering and classifying on behaviours (after FDA to extract B-spline coefficients):

* `001_bspline_coeffs.ipynb`: application of FDA and computation of the B-spline coefficients;
* `002_agreg_bsplines.ipynb`: median aggregation (*) of the B-spline coefficients;
* `003_behaviour_classif_AGG.ipynb`: GMM clustering on the aggregated version of the B-spline coefficients;
* `003_behaviour_classif_NO_AGG.ipynb`: GMM clustering on the non-aggregated version of the B-spline coefficients and aggregation by the median on the posterior probabilities of the GMM results;
* `004_classification_models.ipynb`: supervised learning models to classify the behavioural class by using filtered (via gLASSO) molecular descriptors as explanatory variables.

(*) N. B.: aggregation = aggregating the replicates (repetitions of the lab experiments, same conditions and same dosage of the contaminant) by the median to get the 33 substances.
