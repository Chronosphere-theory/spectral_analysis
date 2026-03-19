markdown
# Chronosphere Theory: Spectral Analysis

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.XXXXXXX.svg)](https://doi.org/10.5281/zenodo.XXXXXXX)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)

This repository contains the numerical code for the paper **"Chronosphere: Geometric Origin of Masses and Cosmological Parameters"** by A.Yu. Ogorodnikov (2026).

## Overview

The code implements numerical verification of the fundamental constant 
β = (π-3)/(4π) ≈ 0.011267585362... arising from the icosahedral structure of the 
Chronosphere boundary. It includes:

- Construction of the Cayley graph of the group A₅ with 15 involutions
- Computation of the angular Laplacian spectrum via representation theory
- Numerical diagonalization of the full Laplacian on ℋ_N = Γ_{A₅} × {0,…,N}
- Extraction of the logarithmic correction β ln n / N²
- Fits to meson spectra, cosmological data, and gravitational wave events

## Key Results

| N | β_numerical | Deviation from theory |
|---|-------------|----------------------|
| 10000 | 0.01126759 ± 0.00000001 | 0.31σ |

## Installation

```bash
git clone https://github.com/Chronosphere-theory/spectral_analysis.git
cd spectral_analysis
pip install -e .
Quick Start
python
from chronosphere import ChronosphereModel, compute_spectrum, extract_beta

# Create model with N=1000, μ=12
model = ChronosphereModel(N=1000, mu=12)
eigenvals = model.diagonalize()

# Extract β
beta, error = extract_beta(eigenvals, N=1000, mu=12)
print(f"β = {beta:.8f} ± {error:.8f}")
Repository Structure
chronosphere/ - Core Python package

notebooks/ - Jupyter notebooks reproducing all figures

data/ - Experimental data from PDG, GWTC-3, DESI

tests/ - Unit tests

docs/ - Documentation

results/ - Generated figures and tables

Reproducing the Paper
To reproduce all results from the paper:

bash
jupyter notebook notebooks/01_spectrum_A5.ipynb
jupyter notebook notebooks/02_numerical_verification.ipynb
jupyter notebook notebooks/03_meson_fits.ipynb
jupyter notebook notebooks/04_gwtc_analysis.ipynb
Citation
If you use this code in your research, please cite:

bibtex
@article{Ogorodnikov2026,
  title={Chronosphere: Geometric Origin of Masses and Cosmological Parameters},
  author={Ogorodnikov, A.Yu.},
  journal={Physical Review D},
  year={2026},
  note={arXiv:2603.xxxxx}
}
License
MIT License

Contact
A.Yu. Ogorodnikov - chronosphere.theory@gmail.com

text

### chronosphere/__init__.py

```python
"""
Chronosphere Theory: Spectral Analysis Package

This package implements numerical verification of the fundamental constant
β = (π-3)/(4π) arising from the icosahedral structure of the Chronosphere boundary.
"""

__version__ = "1.0.0"
__author__ = "A.Yu. Ogorodnikov"

from .graph_models import (
    A5CayleyGraph,
    ChronosphereModel,
    angular_laplacian_spectrum
)

from .spectrum import (
    compute_spectrum,
    exact_quadratic_part,
    extract_beta,
    beta_theoretical
)

from .analysis import (
    fit_meson_trajectory,
    fit_cosmological_H0,
    fit_gw_phase
)

from .utils import (
    set_plot_style,
    save_figure,
    load_meson_data,
    load_gwtc_data,
    load_cosmological_data
)

__all__ = [
    'A5CayleyGraph',
    'ChronosphereModel',
    'angular_laplacian_spectrum',
    'compute_spectrum',
    'exact_quadratic_part',
    'extract_beta',
    'beta_theoretical',
    'fit_meson_trajectory',
    'fit_cosmological_H0',
    'fit_gw_phase',
    'set_plot_style',
    'save_figure',
    'load_meson_data',
    'load_gwtc_data',
    'load_cosmological_data'
]
