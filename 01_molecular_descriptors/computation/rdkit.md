## MOLECULAR DESCRIPTORS CALCULATION (3D) - Eg with RDKit


#### 1. Set-up:

```python
## packages to install if required (remove hashtag and run):
#!pip install pysmiles
#!pip install descriptastorus
#!pip install rdkit

```

```python
## import necessary libraries:
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

from pysmiles import read_smiles

from descriptastorus.descriptors.DescriptorGenerator import MakeGenerator

from rdkit import Chem
from rdkit import DataStructs
from rdkit.Chem import Draw
from rdkit.Chem.Draw import IPythonConsole
from rdkit.Chem import Descriptors
from rdkit.Chem import AllChem, PandasTools
from rdkit.ML.Descriptors import MoleculeDescriptors

```

```python
## export dataframe with substances + SMILES:
smiles_df = pd.read_csv('contaminants.csv', delimiter = ";")
smiles_df.head(5)

```

```python
## data cleaning:
print(f"Length of database with NAs: {len(smiles_df.SMILES)}")

if smiles_df.SMILES.isna().sum() > 0:
    smiles_cleaned = smiles_df.loc[smiles_df.SMILES.notna()].copy()#smiles_df.dropna() ## remove NAs (cannot compute molecular descriptor if no SMILES structure present)
    print(f"Length of database without NAs (cleaned version): {len(smiles_cleaned.SMILES)}")
else:
    None

```

```python
## extract list of molecules from their SMILES:
smiles_list = smiles_cleaned.SMILES

mol_list = []

for s in smiles_list:
    mol = Chem.MolFromSmiles(s)
    mol_list.append(mol)

```

```python
## add molecule column to df:
PandasTools.AddMoleculeColumnToFrame(smiles_cleaned, "SMILES", "molecule", includeFingerprints = True)
smiles_cleaned.molecule = mol_list
smiles_cleaned.head(2)

```

```python

```

#### 2. Basic chemical analysis of database:

```python
## visualise 2D rep of substances from their SMILES (just to see, for fun):
pic = Draw.MolsToGridImage(mol_list, molsPerRow = 4, maxMols = 70, subImgSize = (200, 200), legends = list(smiles_cleaned.name), returnPNG = False)
#pic

```

```python
## save molecular visualisation of present substances:
pic.save("plots/2d_rep_mols.png")

```

```python

```

#### 3. Calculation of molecular descriptors:

```python
Desc_list_func = MoleculeDescriptors.MolecularDescriptorCalculator(x[0] for x in Descriptors._descList)
names = Desc_list_func.GetDescriptorNames()

```

```python
des = []

for mol in smiles_cleaned["molecule"]:
  des.append(Desc_list_func.CalcDescriptors(mol))

rdkit_df = pd.concat([smiles_cleaned, pd.DataFrame(des)], axis = 1)
rdkit_df.head()
```

```python

```

#### 4. Export results to .csv file:

```python
rdkit_df.to_csv("rdkit_descriptors.csv", index = False)
```

```python

```

```python

```
