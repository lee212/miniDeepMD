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

### Output (using 1000 samples of bba dataset)

```

AAE3dModel(
  (encoder): Encoder(
    (conv): Sequential(
      (enc_conv1): Conv1d(3, 64, kernel_size=(5,), stride=(1,))
      (enc_relu1): ReLU(inplace=True)
      (enc_conv2): Conv1d(64, 128, kernel_size=(3,), stride=(1,))
      (enc_relu2): ReLU(inplace=True)
      (enc_conv3): Conv1d(128, 256, kernel_size=(3,), stride=(1,))
      (enc_relu3): ReLU(inplace=True)
      (enc_conv4): Conv1d(256, 256, kernel_size=(1,), stride=(1,))
      (enc_relu4): ReLU(inplace=True)
      (enc_conv5): Conv1d(256, 512, kernel_size=(1,), stride=(1,))
    )
    (fc): Sequential(
      (0): Linear(in_features=512, out_features=256, bias=True)
      (1): ReLU(inplace=True)
    )
    (mu_layer): Linear(in_features=256, out_features=10, bias=True)
    (std_layer): Linear(in_features=256, out_features=10, bias=True)
  )
  (generator): Generator(
    (model): Sequential(
      (gen_linear1): Linear(in_features=10, out_features=64, bias=True)
      (gen_relu1): ReLU(inplace=True)
      (gen_linear2): Linear(in_features=64, out_features=128, bias=True)
      (gen_relu2): ReLU(inplace=True)
      (gen_linear3): Linear(in_features=128, out_features=512, bias=True)
      (gen_relu3): ReLU(inplace=True)
      (gen_linear4): Linear(in_features=512, out_features=1024, bias=True)
      (gen_relu4): ReLU(inplace=True)
      (gen_linear5): Linear(in_features=1024, out_features=84, bias=True)
    )
  )
  (discriminator): Discriminator(
    (model): Sequential(
      (dis_linear1): Linear(in_features=10, out_features=512, bias=True)
      (dis_relu1): ReLU(inplace=True)
      (dis_linear2): Linear(in_features=512, out_features=512, bias=True)
      (dis_relu2): ReLU(inplace=True)
      (dis_linear3): Linear(in_features=512, out_features=128, bias=True)
      (dis_relu3): ReLU(inplace=True)
      (dis_linear4): Linear(in_features=128, out_features=64, bias=True)
      (dis_relu4): ReLU(inplace=True)
      (dis_linear5): Linear(in_features=64, out_features=1, bias=True)
    )
  )
)
Having 800 training and 200 validation samples.

Train Epoch: 1 [32/800 (4%)]    Loss_d: 0.551895    Loss_eg: 49.293213  Time: 1116.517
Train Epoch: 1 [64/800 (8%)]    Loss_d: 0.375362    Loss_eg: 30.693209  Time: 0.013
Train Epoch: 1 [96/800 (12%)]   Loss_d: 0.654449    Loss_eg: 26.188126  Time: 0.012
Train Epoch: 1 [128/800 (16%)]  Loss_d: 0.332529    Loss_eg: 20.292343  Time: 0.012
Train Epoch: 1 [160/800 (20%)]  Loss_d: 0.283047    Loss_eg: 17.256340  Time: 0.011
Train Epoch: 1 [192/800 (24%)]  Loss_d: 0.328628    Loss_eg: 14.860723  Time: 0.011

...(suppressed)...

Train Epoch: 10 [640/800 (80%)] Loss_d: -5.524131   Loss_eg: 12.296304  Time: 0.011
Train Epoch: 10 [672/800 (84%)] Loss_d: -5.410509   Loss_eg: 12.359403  Time: 0.011
Train Epoch: 10 [704/800 (88%)] Loss_d: -5.832216   Loss_eg: 12.373447  Time: 0.011
Train Epoch: 10 [736/800 (92%)] Loss_d: -5.510255   Loss_eg: 12.174291  Time: 0.011
Train Epoch: 10 [768/800 (96%)] Loss_d: -5.780591   Loss_eg: 12.515926  Time: 0.011
Train Epoch: 10 [800/800 (100%)]    Loss_d: -5.868246   Loss_eg: 11.977236  Time: 0.011
====> Epoch: 10 Average loss_d: -5.9173 loss_eg: 13.8505
====> Validation loss: 8.2766
```

# Reference

- Ramanathan, Arvind, et al. "Statistical inference for big data problems in molecular biophysics." Neural Information Processing Systems: Workshop on Big Learning. 2012.
- Bhowmik, Debsindhu, et al. "Deep clustering of protein folding simulations." BMC bioinformatics 19.18 (2018): 47-58.
- Lee, Hyungro, et al. "Deepdrivemd: Deep-learning driven adaptive molecular simulations for protein folding." 2019 IEEE/ACM Third Workshop on Deep Learning on Supercomputers (DLS). IEEE, 2019.
- Brace, Alexander, et al. "Coupling streaming AI and HPC ensembles to achieve 100–1000× faster biomolecular simulations." 2022 IEEE International Parallel and Distributed Processing Symposium (IPDPS). IEEE, 2022.

