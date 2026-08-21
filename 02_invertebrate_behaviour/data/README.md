## Data files used:

* `pre_FDA_{}_IGT.csv`: trajectories of each invertebrate species (*), IGT metric;
* `fPCA_score_agg_Default_IGT.csv`: used to extract the full substance names;
* `multispec_bsplines_IGT.csv`: application of FDA and computation of B-spline coefficients;
* `multispec_bsplines_median_agreg2_IGT.csv`: median aggregation of the substances on B-spline coefficients (used on the datafile above);
* `classes_df_nomet_behaviour_K7_IGT_AGG.csv`: GMM clustering on aggregated B-spline coefficients;
* `classes_df_nomet_behaviour_K7_IGT.csv`: GMM clustering on non-aggregated B-spline coefficients;
* `classes_df_forced_nomet_K7.csv`: molecular classes (cf. folder `01_molecular_descriptors`);
* `glasso_results_nomet.csv`: filtered molecular descriptors with gLASSO (cf. folder `01_molecular_descriptors`).

(*): E = Erpobdella (leeches), G = Gammarus (freshwater crustaceans), R = Radix (gastropods).
