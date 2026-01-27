## MOLECULAR DESCRIPTORS CALCULATION (3D) - Eg with Mordred


#### 1. Set-up:

```python
## packages to install if required (remove hashtag and run):
#!pip install pysmiles
#!pip install descriptastorus
#!pip install mordred

```

```python
## import necessary libraries:
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

from pysmiles import read_smiles

from rdkit import Chem
#from rdkit.Chem import Descriptors
from rdkit.Chem import AllChem, PandasTools

from mordred import Calculator, descriptors

from descriptastorus.descriptors.DescriptorGenerator import MakeGenerator

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
#PandasTools.AddMoleculeColumnToFrame(smiles_cleaned, "SMILES", "molecule", includeFingerprints = True)
#smiles_cleaned.molecule = mol_list
#smiles_cleaned.head(2)

```

```python

```

#### 2. Calculation of molecular descriptors:

```python
## set-up Mordred calculator:
calculator_mordred = Calculator(descriptors, ignore_3D = True)

```

```python
## calculate molecular descriptors:
md_df = calculator_mordred.pandas(mol_list)

```

```python

```

#### 3. Cleaning of MD full of NAs (remove these columns):

```python
mordred_md = pd.concat([smiles_cleaned, pd.DataFrame(md_df)], axis = 1)
mordred_md.head()

```

```python
## convert df back to numeric (so descriptors with errors can be converted to NAs & then later removed):
mordred_md_num = mordred_md.iloc[:, 5:-1].apply(pd.to_numeric, errors = "coerce")

mordred_md_clean = mordred_md_num.dropna(axis = 1, how = "all")
mordred_md_clean.head()

```

```python
## append MD to original df (now that MD are cleaned => rows full of NAs removed):
mordred_df = pd.concat([smiles_df, mordred_md_clean], axis = 1)
mordred_df.head()

```

```python

```

#### 4. Export results to .csv file:

```python
mordred_df.to_csv("mordred_descriptors.csv", index = False)

```

```python

```

#### A1. Simple example of Mordred on 3 molecular structures (from SMILES):

https://github.com/mordred-descriptor/mordred/tree/develop/examples


```python
#### 1. ONE MOLECULE + ONE DESCRIPTOR:
from rdkit import Chem

from mordred import Chi, ABCIndex

benzene = Chem.MolFromSmiles('c1ccccc1')

# create descriptor instance
abci = ABCIndex.ABCIndex()

# calculate descriptor value
result = abci(benzene)

print(str(abci), result)

# create descriptor instance with parameter
chi_pc4 = Chi.Chi(type='path_cluster', order=4)

# calculate
result = chi_pc4(benzene)

print(str(chi_pc4), result)

```

```python
#### 2. ONE MOLECULE + MULTIPLE DESCRIPTORS:
from multiprocessing import freeze_support

from rdkit import Chem

from mordred import Chi, ABCIndex, RingCount, Calculator, is_missing, descriptors

if __name__ == "__main__":
    freeze_support()

    benzene = Chem.MolFromSmiles("c1ccccc1")

    # Create empty Calculator instance
    calc1 = Calculator()

    # Register descriptor instance
    calc1.register(Chi.Chi(type="path_cluster", order=4))

    # Register descriptor class using preset
    calc1.register(RingCount.RingCount)

    # Register all descriptors in module
    calc1.register(ABCIndex)

    # Calculate descriptors
    result = calc1(benzene)

    print(result)
    # >>> [0.0, 1, 0, 0, 0, 1, (snip)

    # Calculator constructor can register descriptors
    calc2 = Calculator(Chi.Chi)

    # Descriptors module contains all descriptors
    calc3 = Calculator(descriptors)

    # User can access all descriptor instances by descriptors property
    print(calc3.descriptors)
    # >>> (mordred.EccentricConnectivityIndex.EccentricConnectivityIndex(), (snip)

    # Calculate descriptors
    result = calc3(benzene)

    # get first missing value
    na1 = next(r for r in result if is_missing(r))

    # get reason
    print(na1.error)
    # >>> missing 3D coordinate

    # Delete all missing value
    result = result.drop_missing()

    # convert to dict
    print(result.asdict())

```

```python
#### 3. MULTIPLE MOLECULES + MULTIPLE DESCRIPTORS:

from multiprocessing import freeze_support

from rdkit import Chem

from mordred import Calculator, descriptors

if __name__ == "__main__":
    freeze_support()

    mols = [
        Chem.MolFromSmiles("c1ccccc1"),
        Chem.MolFromSmiles("c1ccccc1Cl"),
        Chem.MolFromSmiles("c1ccccc1C"),
    ]

    # Create Calculator
    calc = Calculator(descriptors)

    # map method calculate multiple molecules (return generator)
    print(list(calc.map(mols)))

    # pandas method calculate multiple molecules (return pandas DataFrame)
    print(calc.pandas(mols))

```

```python

```
