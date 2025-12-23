# Uncertainty Quantification for Universal Machine Learning Interatomic Potentials

This repository provides datasets, scripts, and trained interatomic potentials used in the study of **uncertainty quantification (UQ)** for **universal machine-learning interatomic potentials (uMLIPs)**.  
It accompanies the methodology proposed in:

> **K. Liu et al.**, *Heterogeneous ensemble enables a universal uncertainty metric for atomistic foundation models*,  
> **npj Computational Materials (2025)**.

The repository consists of two main parts:
1. Benchmarking uncertainty metrics on the **OMat24 dataset**
2. Application to **pure tungsten (W)** with mixed-precision ACE potentials

---

## 1. Benchmarking Uncertainty \( U \) on the OMat24 Dataset

This part evaluates the correlation between the proposed uncertainty metric \( U \) and prediction errors on the **OMat24 test set**, and determines optimal weights for a **heterogeneous ensemble** of uMLIPs.

### Directory Contents

#### `0-GRACE-2L-OMAT/` (and related folders)
Energy and force predictions produced by uMLIPs using the **ASE calculator interface**.

- A total of **21 uMLIPs** are included
- Due to GitHub file-size limitations, **only ~3% of the full dataset** used in the study is provided here
- The complete dataset is available upon request or via the original publication

#### `RMSE_of_Energy_Force_Predicted_by_UMLIP.ipynb`
Computes **energy and force RMSEs** of uMLIP predictions with respect to DFT reference values.

#### `Uncertainty Quantification.ipynb`
Computes the uncertainty metric \( U \) from uMLIP ensemble predictions.

- Demonstrates the correlation between \( U \) and prediction error
- Identifies the **optimal ensemble size (11 models)** for uncertainty estimation

---

## 2. Pure W Dataset and Potentials

This section contains datasets and trained interatomic potentials for **pure tungsten (W)**, used to demonstrate uncertainty-guided **mixed-precision training** of system-specific ACE models.

### `Pure_W/`

All data related to the pure W system.

---

### `W_uMLIP/`

Predictions from general-purpose uMLIPs:

- Energies and atomic forces for approximately **1000 atomic configurations**
- Each configuration is evaluated independently by **20 uMLIPs**
- Used for:
  - uncertainty estimation
  - ensemble statistics
  - comparison with DFT reference data

---

### `potentials/`

This directory contains **ACE interatomic potentials** trained on datasets with different levels of reference accuracy.

#### Naming convention

- The **first digit** of the filename indicates the **training-set precision**
- The **last digit** denotes the **replicate index**

| Label | Training dataset description |
|------:|-----------------------------|
| `0` | 100% DFT data (full DFT reference set) |
| `1` | Mixed-precision dataset with uncertainty cutoff \( U_c = 0.1 \), ~95% DFT |
| `2` | Mixed-precision dataset with \( U_c = 0.5 \), ~39% DFT |
| `3` | Mixed-precision dataset with \( U_c = 1.0 \), ~4% DFT |
| `4` | Mixed-precision dataset with \( U_c = 10.0 \), ~3% DFT |
| `5` | 100% uMLIP-generated data (no DFT) |

For each dataset, **five independently trained ACE potentials** were generated to assess training variability.  
The **last digit of the filename** denotes the **replicate index (0–4)**.

---

### `Testset/`

An independent W test set taken from:

> https://doi.org/10.1038/s41524-025-01599-1

It includes configurations involving:
- 2D grain boundaries
- 3D grain boundaries
- crack geometries
- liquid structures

---

### `W_DFT.pckl.gzip`

Compressed pickle file containing the **DFT reference dataset** for pure tungsten.

- DFT energies
- DFT atomic forces
- Corresponding atomic configurations

This dataset serves as the **ground truth** for validation and benchmarking.

---

### `Build_dataset_from_uMLIP_and_DFT.ipynb`

- Evaluates uncertainty \( U \) for configurations in the W dataset
- Constructs mixed-precision training sets using different uncertainty thresholds \( U_c \)
- Compares the accuracy of mixed datasets against the full DFT dataset

---

### `Test_W_ACE.ipynb`

Evaluates the performance of ACE potentials trained on different datasets using the independent W test set from  
https://doi.org/10.1038/s41524-025-01599-1.

---

## Notes

1. For the **MoNbTaW** system discussed in the article, the scripts for mixed-dataset construction and ACE testing are **identical** to those used for the W system.  
   The corresponding dataset is taken from:  
   https://doi.org/10.1016/j.ijplas.2025.104308

2. ACE potential testing follows scripts provided in:  
   https://github.com/Addition-P/Cu-W-ACE

3. If you use this repository or the mixed-precision dataset construction strategy, please cite:

```bibtex
@article{liu2025heterogeneous,
  title={Heterogeneous ensemble enables a universal uncertainty metric for atomistic foundation models},
  author={Liu, Kai and Wei, Zixiong and Gao, Wei and Dey, Poulumi and Sluiter, Marcel HF and Shuang, Fei},
  journal={npj Computational Materials},
  year={2025},
  publisher={Nature Publishing Group UK London}
}
