# Analysis Metrics

Following Dutagaci et al. (2023). All residue numbers use yeast Rpb1 numbering (PDB 2e2h). Each metric is computed with MDAnalysis for both WT and I825T trajectories.

| # | Metric | Selection | What it reports |
|---|---|---|---|
| 1 | **RMSD of TL** | Trigger loop, residues 1078–1089 (after aligning on the protein core) | Overall TL conformational drift from the closed/folded starting state |
| 2 | **RMSF of TL and BH** | TL 1078–1089, bridge helix 824–844 | Per-residue flexibility; whether I825T changes local BH or TL mobility |
| 3 | **GTP distances** | GTP to R766, R1020, H1085, L1081 | Stability of NTP binding and TL–substrate contacts |
| 4 | **Mg distances** | Active-site Mg²⁺ to GTP phosphates / coordinating residues | Integrity of the catalytic metal site |
| 5 | **Latch distances** | R728–D760, R728–L808 | Opening/closing of the latch interactions near the active site |
