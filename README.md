# miniDeepMD

miniDeepMD is a PyTorch implementation of an adversarial autoencoder (AAE) for
characterizing protein binding pockets and protein-ligand interactions from
molecular dynamics (MD) simulations. The codebase is originated from the
DeepDriveMD: Deep-Learning Driven Adaptive Molecular Simulations,
https://github.com/DeepDriveMD/DeepDriveMD-pipeline.


## Overview

miniDeepMD is to provide performance characterization for training 3D PointNet
based adversarial autoencoder (3d-AAE) represented by molecular structure in
latent space. The model is to suggest conformational states that may not be
fully sampled to characterize biologically relevant transitions betwee such
states (e.g., open/closed states of protein) by gradient-based optimization and
the discriminator. With AAE, a molecular structure is encoded into 3d space and
the distance between each encoded data point is used to recognize a
dissimilarity from the initial structure, i.e., changing states from open to
closed.

## Datasets

The sample dataset is included in the repo to quickly start a benchmark with a
small size of HDF5 input, β- β- α (BBA) protein (223 + 102 μs sampling across two
independent trajectories). The `point_cloud` is used for AAE and the shape of
the datasets like:

```
point_cloud              Dataset {1000, 3, 28}
contact_map              Dataset {1000}
fnc                      Dataset {1000}
rmsd                     Dataset {1000}
```

### Synthetic dataset (by generator)

Another option of obtaining a dataset is the synthetic dataset generator which
can take a size of atoms and residues to represent a molecular structure in a
small, medium and large volumes for a quantitative benchmark.

## Installation

### Required Packages

- pytorch 1.12.1
- python 3.7 or higher
- cuda 10.1.243 or higher
- cudatoolkit 10.2.89 or higher
- mpi4py

Packages for molecular dynamics

- mdtools: https://github.com/braceal/MD-tools.git
- molecules: https://github.com/braceal/molecules.git
- mdlearn: https://github.com/ramanathanlab/mdlearn.git

## Settings

Storage type can be changed, for example:
- disk mode
- host (cpu) memory mode

And other settings for benchmark in details can be adjusted in a yaml file. There are sample files provided for a quick reference: `settings` sub-directory in the repo.

## Quick Start

PyTorch Training starts with user parameters to specify GPU IDs for encoder, decoder and generator while reading a yaml file for settings, for example:
 
```
python train_minideepmd.py -c settings/machine_learning_stage_test.yaml --encoder_gpu 0 --decoder_gpu 0 --generator_gpu 0
```


# Reference

- Ramanathan, Arvind, et al. "Statistical inference for big data problems in molecular biophysics." Neural Information Processing Systems: Workshop on Big Learning. 2012.
- Bhowmik, Debsindhu, et al. "Deep clustering of protein folding simulations." BMC bioinformatics 19.18 (2018): 47-58.
- Lee, Hyungro, et al. "Deepdrivemd: Deep-learning driven adaptive molecular simulations for protein folding." 2019 IEEE/ACM Third Workshop on Deep Learning on Supercomputers (DLS). IEEE, 2019.
- Brace, Alexander, et al. "Coupling streaming AI and HPC ensembles to achieve 100–1000× faster biomolecular simulations." 2022 IEEE International Parallel and Distributed Processing Symposium (IPDPS). IEEE, 2022.

