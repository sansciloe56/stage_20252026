## 01. MOLECULAR DESCRIPTORS:

1. `final_pipeline_dataprep_nomet.ipynb`: where to find RDKit method used to compute molecular descriptors, along with the datafile (in the folder `data`) `contaminants.csv` that contains the list of substances of the study and their CAS number and SMILES (both extracted from [PubChem]([url](https://pubchem.ncbi.nlm.nih.gov/))/[ChemSpider]([url](https://www.chemspider.com/))) and another column that says if the substance has been detected by invertebrates (= 1) or not (= 0), and cleaning of molecular descriptors;
2. `final_pipeline_dataclassif_nomet.ipynb`: creation variable to predict, $y$ (categorical variable where each class is a substance class).

* Données utilisées et extraites dans le dossier `data`.
