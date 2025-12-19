# Uncertainty quantification for universal machine learning interatomic potentials


## Pure W Dataset and Potentials

This repository contains datasets and interatomic potentials for **pure tungsten (W)**, used to study uncertainty-aware machine-learning interatomic potentials (uMLIPs) and mixed-precision training strategies.

### `Pure_W/`

This folder contains all data related to the pure tungsten system.

#### `W_uMLIP/`
This directory stores predictions from **20 different general-purpose uMLIPs**:

- Energies and atomic forces for approximately **1000 atomic configurations**
- Each configuration is evaluated independently by all 20 uMLIPs
- The data are intended for **uncertainty estimation**, ensemble statistics, and comparison against DFT reference values

#### `potentials/`
This directory contains **ACE interatomic potentials** trained on datasets with different levels of reference accuracy.

The **first digit of the filename** indicates the precision level of the training dataset:

| Label | Training dataset description |
|------:|-----------------------------|
| `0` | 100% DFT data (full DFT reference set) |
| `1` | Mixed-precision dataset with uncertainty cutoff \( U_c = 0.1 \), containing ~95% DFT data |
| `2` | Mixed-precision dataset with \( U_c = 0.5 \), containing ~39% DFT data |
| `3` | Mixed-precision dataset with \( U_c = 1.0 \), containing ~4% DFT data |
| `4` | Mixed-precision dataset with \( U_c = 10.0 \), containing ~3% DFT data |
| `5` | 100% uMLIP-generated data (no DFT) |

These potentials are designed to systematically assess how **training-set precision and DFT fraction** affect the performance of system-specific ACE models.

For each dataset, **five independently trained ACE potentials** were generated to assess training variability.  
The **last digit of the filename** denotes the **replicate index (0–4)**.


#### `W_DFT.pckl.gzip`
Compressed pickle file containing the **DFT reference dataset** for pure tungsten:

- DFT energies
- DFT atomic forces
- Corresponding atomic configurations

This dataset serves as the ground truth for validation and benchmarking.
