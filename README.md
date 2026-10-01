# BIOT 6900

Coursework for BIOT 6900: protein language models applied to target tractability
and variant effect prediction.

## Setup

```bash
conda env create -f environment.yml -p ./env   # or: mamba env create ...
conda activate ./env
jupyter lab
```

The notebooks were developed against Python 3.11 with pandas 3.0.5, numpy 2.4.6,
scikit-learn 1.9.1, scipy 1.17.1, and matplotlib 3.11.1. `environment.yml` is
exported `--from-history`, so versions are unpinned and will resolve to current
releases; pin them there if you need an exact rebuild.

## Layout

```
notebooks/     all lab notebooks, outputs committed so results are readable on GitHub
data/          gitignored — see data/README.md for how to obtain the Module 3 pack
structures/    PDB inputs for the Module 4 drug-pocket demo
environment.yml
```

Notebooks resolve paths relative to the repo root, so they run correctly whether
the kernel's working directory is `notebooks/` or the project root.

## Notebooks

| Notebook | What it does |
|---|---|
| `module1_setup.ipynb` | Environment check and Biopython / NCBI Entrez basics |
| `module3_part1_toy_model.ipynb` | Tractability prior on synthetic data |
| `module3_part2_real_data.ipynb` | The same prior on 1201 real proteins — the core lab |
| `module4_part1_toy_model.ipynb` | Module 4 toy model |
| `module4_demo_drug_pocket.ipynb` | Drug-pocket structural demo (py3Dmol viewers) |

## A note on Module 3 Part 2

The lab's main result is the gap between two ways of cross-validating the same model:

| Split | AUROC | Average precision |
|---|---|---|
| Random | 0.848 | 0.727 |
| Family | 0.732 | 0.548 |

Chance-level average precision is 0.334 (the positive fraction). The random split
is inflated because homologous proteins leak across folds; the family split is the
honest estimate. ESM-C 300M beats the 24x smaller ESM-2 35M on the random split
(0.848 vs 0.801) but is essentially tied once homology leakage is removed
(0.732 vs 0.730).
