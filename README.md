# MD Simulation of POLR2A p.Ile848Thr Variant

## Overview

Rotation 2 project (UC Merced, Dutagaci Lab, PI: Dr. Bercem Dutagaci) modeling the novel pathogenic POLR2A variant **I825T** (yeast Rpb1 numbering; human **p.Ile848Thr**), located in the bridge helix of RNA Polymerase II. Molecular dynamics (MD) simulations of the mutant are compared against wild type to characterize how the substitution perturbs the active-site dynamics.

## Biological Background

POLR2A encodes RPB1, the largest subunit of RNA Polymerase II (Pol II). De novo heterozygous POLR2A variants cause a neurodevelopmental disorder characterized by infantile-onset hypotonia and developmental delay.

Two mobile elements of the Pol II active site control nucleotide addition and translocation:

- **Bridge helix (BH)** — a long helix spanning the active-site cleft; its conformational changes are coupled to translocation.
- **Trigger loop (TL)** — folds over the incoming NTP to close the active site and promote catalysis.

The I825T substitution lies in the bridge helix, where it may alter BH–TL coupling, TL folding, and NTP positioning.

### Key residues (yeast Rpb1 numbering, PDB 2e2h)

| Element | Residues |
|---|---|
| Trigger loop (TL) | 1078–1089 |
| Bridge helix (BH) | 824–844 |
| Mutation site | I825 (→ T) |
| GTP contacts | R766, R1020, H1085, L1081 |
| Latch pairs | R728–D760, R728–L808 |

## Methods Pipeline

```
2e2h PDB  →  CHARMM-GUI system prep  →  OpenMM simulation (Google Colab)  →  MDAnalysis
```

1. **Structure** — Pol II elongation complex with GTP in the active site (PDB [2e2h](https://www.rcsb.org/structure/2E2H)).
2. **System preparation** — CHARMM-GUI: mutate I825T, solvate, ionize, generate CHARMM force-field inputs for WT and mutant.
3. **Simulation** — OpenMM on Google Colab GPUs.
4. **Analysis** — MDAnalysis:
   - RMSD of the trigger loop
   - RMSF of the trigger loop and bridge helix
   - GTP–residue contact distances
   - Mg²⁺ coordination distances
   - Latch distances

See [analysis/README.md](analysis/README.md) for metric definitions.

## Repo Structure

```
structures/    input PDB files (2e2h.pdb)
charmm-gui/    CHARMM-GUI outputs (git-ignored, large)
simulations/   OpenMM trajectories and outputs (git-ignored, large)
notebooks/     Colab / Jupyter notebooks for simulation and analysis
analysis/      analysis scripts, plots, and metric descriptions
environment.yml
```

## Setup

```bash
conda env create -f environment.yml
conda activate polr2a
```

## Usage

1. Upload `structures/2e2h.pdb` to CHARMM-GUI and build WT and I825T systems; download outputs into `charmm-gui/`.
2. Run the simulation notebook in `notebooks/` on Google Colab; save trajectories to `simulations/`.
3. Run the analysis notebooks/scripts against the trajectories to compute the metrics in [analysis/README.md](analysis/README.md).

## References

1. Haijes HA, et al. (2019). De novo heterozygous POLR2A variants cause a neurodevelopmental syndrome with profound infantile-onset hypotonia. *American Journal of Human Genetics*.
2. Hansen AW, et al. (2021). Germline mutation in POLR2A: a heterogeneous, multi-systemic developmental disorder characterized by transcriptional dysregulation. *HGG Advances*.
3. Dutagaci B, et al. (2023). Characterization of RNA polymerase II trigger loop mutations using molecular simulations and machine learning. *PLoS Computational Biology*.
