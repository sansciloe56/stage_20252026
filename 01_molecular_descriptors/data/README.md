## Description databases in the 'data' folder:

1. `contaminants.xlsx`/`contaminants.csv`: the initial database with the list of all substances tested // `_dected` extension has the substances where at least one invertebrate reacted to it;
2. `rdkit_descriptors_nomet.csv`: computation of RDKit molecular descriptors (raw datafile, no cleaning done);
3. `rdkit_clean_nomet.csv`: cleaned version of the `rdkit_descriptors_nomet.csv` datafile (NAs removal, infinity values check, variance threshold => remove columns with a low variance as little info can be given from these columns, and correlation filtering => remove highly correlated columns as similar, normalisation);
4. `glasso_results_nomet.csv`: results of gLASSO on cleaned moleular descriptors;
5. `classes_df_forced_nomet_K7.csv`: classes du clustering GMM sur les descripteurs moléculaires.
