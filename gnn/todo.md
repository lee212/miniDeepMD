## Tasks
 
- [ ] input dataset
  - [x] with nwchem, https://github.com/nkkchem/CompMolNWChem_Thermo/tree/master/data
    - [x] 3D conversion via rdkit
  - [ ] ~~with updated script, https://github.com/PNNL-CompBio/CME-QM/tree/main/src~~
  - [ ] DFT calculation, https://github.com/nkkchem/CompMolNWChem_Thermo/tree/master/nwchem-scripts
    - [ ] Extracting nwchem output
- [ ] MPNN model
  - [x] with PyTorch Geometric, https://github.com/pyg-team/pytorch_geometric/blob/master/torch_geometric
  - [x] with DeepChem, https://github.com/deepchem/deepchem/blob/master/contrib/mpnn/mpnn.py
  - [ ] MAE metric
- [ ] Execution
  - [x] Shifter Image for nwchem
  - [ ] PyTorch / TensorFlow
- [ ] Other choices
  - [ ] DGL-LifeSci, https://github.com/dmlc/dgl/
  - [ ] OGB, e.g., PCQM4Mv2, https://ogb.stanford.edu/docs/lsc/leaderboards/#pcqm4mv2
