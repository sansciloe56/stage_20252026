## MOLECULAR DESCRIPTORS

This folder contains multiple folders:
1. computation: where to find different methods used to compute molecular descriptors (RDKit, Mordred and PaDEL), along with the datafile contaminants.csv that contains the list of substances of the study and their CAS number and SMILES (both extracted from [PubChem]([url](https://pubchem.ncbi.nlm.nih.gov/))/[ChemSpider]([url](https://www.chemspider.com/))) and another column that says if the substance has been detected by invertebrates (= 1) or not (= 0);
2. clustering: creation variable to predict, y (categorical variable where each class is a substance class) and the full final pipeline.
