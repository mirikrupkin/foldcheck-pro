# FoldCheck-Pro: Automated Structural Integrity & Biophysical Validation Suite


[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/mirikrupkin/foldcheck-pro/blob/main/foldcheck-pro.ipynb)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10%2B-blue.svg)](https://www.python.org/)


**Author:** [Dr. Miri Krupkin](https://linkedin.com/in/mirikrupkin) (Applied AI Research Scientist & Computational Biologist) 
**Description:** Production-grade architecture for automated biophysical model validation, Hungarian-based multi-chain pairing, and integrated pLDDT/RASA structural state classification against empirical experimental ground truth.


---


## 🧬 Project Overview
`FoldCheck-Pro` is a high-throughput computational pipeline designed to bridge generative structural predictions (AlphaFold) with empirical validation data from Cryo-EM and X-ray crystallography (RCSB PDB). Standard structural alignments often break down when handling multi-chain asymmetry, signal peptide cleavage, or crystal packing contacts.


This suite introduces programmatic robustness checks, automated API ingestion from the EBI AlphaFold database, and advanced biophysical classification to flag generative model hallucination risks.


---


## 🛠️ Tech Stack
* **Language & Core:** Python 3.10+, NumPy (vectorized broadcasting), pandas
* **Structural Bioinformatics:** BioPython, py3Dmol, SciPy (`linear_sum_assignment`)
* **Testing & Infrastructure:** PyTest, EBI AlphaFold API, RCSB PDB REST architecture


---


## 📂 Repository Architecture

```text
foldcheck-pro/
│
├── src/
│   ├── fetcher.py        # Automated EBI API ingestion & coordinate downloading
│   ├── alignment.py      # Hungarian algorithm chain pairing & RMSD calculations
│   └── metrics.py        # Shrake-Rupley SASA / RASA calculation & pLDDT mapping
│
├── configs/
│   └── config.yaml       # Central configuration parameters
│
├── tests/
│   └── test_pipeline.py  # Pytest suite verifying data integrity and API handling
│
├── assets/               # Generated benchmark summaries and logs
└── foldcheck-pro.ipynb   # Master executable Jupyter notebook with interactive 3D viewer

```
---

## ⚙️ Key Technical Highlights

1. **Hungarian Algorithm Multi-Chain Matching (`src/alignment.py`):** Resolves complex multi-chain heterodimers (such as HIV-1 Reverse Transcriptase p66/p51 subunits) by framing chain pairing as an optimal linear assignment problem using `scipy.optimize.linear_sum_assignment` based on sequence similarity scores.
2. **Dual-Metric Superposition (RMSD & TM-Score):** Combines Kabsch least-squares alpha-carbon superposition (RMSD) with length-normalized spatial **TM-score** calculations to evaluate global structural topology independently of local outlier sensitivity.
3. **Modified Amino Acid & PTM Parsing:** Programmatically standardizes non-standard residues and post-translational modifications—including selenomethionine (`MSE`), phosphoserine/threonine/tyrosine (`SEP`, `TPO`, `PTR`), and the autocatalytically cyclized chromophore (`CRO`) in GFP—complete with VdW radius patching for Selenium and Phosphorus.
4. **Biophysical State Integration (`src/metrics.py`):** Computes Relative Accessible Surface Area (RASA) via Shrake-Rupley and maps it directly against atomic temperature factors (pLDDT) to dynamically classify residues into confident cores, flexible surfaces, or potential hallucination risks.
5. **Construct Trimming & Cofactor Conservation:** Automatically strips crystal lattice artifacts while preserving biologically vital cofactors (`GTP`, `GDP`, `MG`, `ZN`, `HEM`) during comparative alignment workflows.
6. **Interactive 3D Visualization & Custom URL Ingestion**: Renders synchronized, side-by-side Py3Dmol cartoon views comparing predictions against experimental ground truth, with native support for direct custom prediction URL ingestion (PDB and mmCIF formats) and an interactive sandbox mode for any UniProt ID.

---

## 🔬 Benchmarked Biological Case Studies

The interactive menu guides users through five distinct structural biology challenges:
* **[1] Green Fluorescent Protein - GFP:** Evaluates beta-barrel scaffold stability and internal cavity packing, featuring automated chromophore (`CRO`) mapping against the experimental crystal structure (`1EMA`).
* **[2] Lysozyme C:** Demonstrates automated N-terminal signal peptide cleavage handling, correctly pruning the 18-residue precursor region to match mature crystal ground truth (`1IEE`).
* **[3] Polyubiquitin-C:** Showcases repeating domain extraction, dynamically isolating a single 76-residue functional monomer from a massive ~685-residue repeating polyprotein chain (`1UBQ`).
* **[4] KRAS Oncology Target:** Successfully strips crystal lattice packing contacts from an asymmetric unit dimer to isolate the functional monomer (`4OBE`).
* **[5] HIV-1 RTase & Custom Sandbox:** Handles multi-chain heterodimer asymmetry (p66/p51 subunits) via custom prediction URL ingestion (bypassing raw precursor annotation bottlenecks) or evaluates any custom UniProt ID (`1REV`).

---

## 🚀 Quickstart & Usage


1. **Run via Google Colab:** Click the badge at the top of this file to launch the master notebook instantly.
2. **Interactive Explorer**: Run foldcheck-pro.ipynb interactively to test built-in case studies (Lysozyme C, HIV-1 RTase, Polyubiquitin-C, and KRAS) or input any custom AlphaFold UniProt ID.


## 📜 License


Distributed under the MIT License. See LICENSE for more information.
