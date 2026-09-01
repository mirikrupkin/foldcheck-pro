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
structural-ai-validation-suite/
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
└── foldcheck_pro.ipynb   # Master executable Jupyter notebook with interactive 3D viewer

```
---


## ⚙️ Key Technical Highlights


1. **Hungarian Algorithm Multi-Chain Matching (`src/alignment.py`):** Resolves complex multi-chain heterodimers (such as HIV-1 Reverse Transcriptase p66/p51 subunits) by framing chain pairing as an optimal linear assignment problem using `scipy.optimize.linear_sum_assignment` based on sequence similarity scores.
2. **Biophysical State Integration (`src/metrics.py`):** Computes Relative Accessible Surface Area (RASA) via Shrake-Rupley using optimized vectorization and maps it directly against atomic temperature factors (pLDDT) to dynamically classify residues into confident cores, flexible surfaces, or potential hallucination risks.
3. **Construct Trimming & Heteroatom Conservation:** Automatically strips crystal lattice artifacts while preserving biologically vital cofactors (`GTP`, `GDP`, `MG`, `ZN`, `HEM`) during comparative alignment workflows.
4. **Interactive 3D Visualization:** Renders synchronized, side-by-side Py3Dmol cartoon views comparing your prediction against the experimental crystal structure.
5. **Interactive CLI & Sandbox Mode:** Features pre-configured case studies highlighting classic bioinformatics edge cases, plus a custom sandbox mode for any UniProt ID.

---

## 🔬 Benchmarked Biological Case Studies

The interactive menu guides users through four distinct structural biology challenges:
* **[1] HIV-1 RTase:** Validates multi-chain asymmetry in a heterodimer (p66/p51).
* **[2] Lysozyme C:** Demonstrates automated N-terminal signal peptide cleavage handling (18 residues pruned).
* **[3] Polyubiquitin-C:** Showcases repeat domain extraction, finding a single 76-residue monomer within a massive ~685-residue repeating chain.
* **[4] KRAS Oncology Target:** Isolates a matching monomer from an asymmetric crystal dimer and strips interfering heteroatoms.
* **[5] Custom Sandbox:** Input any AlphaFold UniProt ID and optional experimental PDB code for custom validation.

---

## 🚀 Quickstart & Usage


1. **Run via Google Colab:** Click the badge at the top of this file to launch the master notebook instantly.
2. **Execute Tests Locally:**

```text
bash
pytest tests/ -v
```

3. **Interactive Explorer**: Run foldcheck_pro.ipynb interactively to test built-in case studies (Lysozyme C, HIV-1 RTase, Polyubiquitin-C, and KRAS) or input any custom AlphaFold UniProt ID.


## 📜 License


Distributed under the MIT License. See LICENSE for more information.
