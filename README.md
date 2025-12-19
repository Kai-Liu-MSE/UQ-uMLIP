**Uncertainty quantification for universal machine learning interatomic potentials**


# Pure W Dataset and Potentials

This repository contains datasets and interatomic potentials for **pure tungsten (W)**, used to study uncertainty-aware machine-learning interatomic potentials (uMLIPs) and mixed-precision training strategies.

## Directory Structure

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

#### `W_DFT.pckl.gzip`
Compressed pickle file containing the **DFT reference dataset** for pure tungsten:

- DFT energies
- DFT atomic forces
- Corresponding atomic configurations

This dataset serves as the ground truth for validation and benchmarking.

## Intended Use

The data and potentials in this repository can be used for:

- Benchmarking uMLIP uncertainty estimates  
- Studying mixed-precision training strategies  
- Training and validating ACE potentials with controlled DFT fractions  
- Analyzing energy–force consistency across different model fidelities  

## Notes

- All datasets correspond to **pure tungsten (W)** only.
- File formats are intended for Python-based workflows (e.g., ASE, PyACE).
- Users are encouraged to document any derived datasets or retrained potentials for reproducibility.
