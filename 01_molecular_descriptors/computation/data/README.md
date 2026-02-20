## Description databases in the 'data' folder:

1. contaminants.xlsx/contaminants.csv: the initial database with the list of substances used;
2. mordred_descriptors.csv: computation of Mordred molecular descriptors (raw datafile, no cleaning done);
3. rdkit_descriptors.csv: computation of RDKit molecular descriptors (raw datafile, no cleaning done);
4. mordred_clean.csv: cleaned version of the mordred_descriptors.csv datafile (NAs removal, infinity values check, variance threshold => remove columns with a low variance as little info can be given from these columns, and correlation filtering => remove highly correlated columns as similar);
5. rdkit_clean.csv: cleaned version of the rdkit_descriptors.csv datafile (NAs removal, infinity values check, variance threshold => remove columns with a low variance as little info can be given from these columns, and correlation filtering => remove highly correlated columns as similar).
