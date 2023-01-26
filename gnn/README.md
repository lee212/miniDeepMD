# Graph Neural Network for molecules

## Overview

We use NWChem dataset to implement molecules structure in GNN using
PyTorch/Geometrics.

### Dataset

Sample Dataset in XYZ format
- m300k
   - dmab ![dmol](./fig/mol_dmab.png)
   - ntp ![ntp](./fig/mol_ntp.png)
   - ntp_dimer

### Code

baseline: keras/tf + deepchem 

- featurizer
- data loader
- model (MPNN) by DGL and deepchem ![mpnn](.fig/mpnn_example.png)*

* Karlov, Dmitry S., et al. "graphDelta: MPNN scoring function for the affinity prediction of protein–ligand complexes." ACS omega 5.10 (2020): 5150-5159.

### Train

### Conversion
