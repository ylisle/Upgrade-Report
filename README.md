# Upgrade-Report
# ChimeraX & ISOLDE Molecular Dynamics Trajectory Tools

A suite of Python automation scripts designed for **UCSF ChimeraX** and **ISOLDE**. This repository provides automated workflows for preparing RNA-amino acid conjugates (mono- and bis-aminoacylation), monitoring molecular dynamics trajectory frames in real time, calculating geometric metrics (angles and bond distances), plotting statistical distributions, and exporting simulation data.

---

## Overview

When modeling aminoacylation or studying conformational flexibility in ISOLDE/ChimeraX, manual atom selection and geometric tracking across long trajectories can be repetitive and error-prone. 

This repository automates:
1. **Chemical Preparation**: Automated SMILES loading, atom selection, covalent bond formation, phosphate group deletion, and hydrogenation.
2. **Live Trajectory Tracking**: Background event handlers (`new frame` triggers) that calculate bond angles and distances per frame without slowing down the simulation.
3. **Statistical Analysis & Visualization**: Automated generation of publication-ready Matplotlib histograms featuring mean, modal peak, and standard deviation ($\pm 1\text{ SD}$) overlays.
4. **Data Export**: Convenient GUI file dialogs to save collected high-precision coordinate metrics to compressed NumPy `.npz` archives.

---

## Repository Structure

| File | Description |
| :--- | :--- |
| `duplex_prep.py` | Prepares RNA strand, attaches Phenylalanine to $O3'$, removes phosphate, hydrogenates, and measures baseline angles/distances. |
| `bisamino_acyl_prep.py` | Handles dual aminoacylation (Phenylalanine at $O3'$ and Serine at $O5'$). |
| `record_trajectory.py` | Real-time background frame recorder tracking $O5' \to \text{C9} \to \text{O1}$ angles and $O5' \to \text{C9}$ distances during ISOLDE runs. |
| `bisamino_record_trajectory.py` | Specialized recorder for custom atom triplets (e.g., `UNL 11 N1`, `UNL 6 C3`, `UNL 6 O2`). |
| `plot_distributions.py` | Plots interactive histograms with statistical overlays (Mean, Mode, SD) using Matplotlib. |
| `export_data.py` | Native Qt file-dialog script to export frame data as compressed `.npz` files. |

---

## Prerequisites & Installation

These scripts are built specifically to run inside UCSF ChimeraX with the ISOLDE plugin installed.

* **UCSF ChimeraX** (v1.4 or newer recommended)
* **ISOLDE Plugin**
* Python Environment Dependencies (*included in ChimeraX Python bundle*):
  * `numpy`
  * `matplotlib`
  * `Qt` (`PyQt5` / `PySide2` wrapper)

---

## Usage Guide

### 1. Preparation Phase
Open ChimeraX, load your initial RNA structure, and run the desired preparation script via the ChimeraX command line:

```cmd
open duplex_prep.py
