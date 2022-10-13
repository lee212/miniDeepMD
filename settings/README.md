# Settings in YAML

```
#Output settings
experiment_directory: # base path to store results (no exist prior to run)
output_path: # Path to directory where trainer should write to

#Train settings
init_weights: # pre-trained model weights (.pt)
epochs: # number of epochs to train
batch_size: number of batch to train

# Model hyperparameters
latent_dim: # a latent space of size
ae_optimizer: # Encoder/Decoder optimizer params
disc_optimizer: # Discriminator optimizer params
encoder_filters: # Encoder filter sizes in Python List format
encoder_kekrnel_sizes: # Encoder kernel sizes in Python List format


```
