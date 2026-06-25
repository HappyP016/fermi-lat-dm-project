# Environment Setup Notes

## Installed: 25 June 2026

### Conda environment: fermi
- Python: 3.11
- Fermitools: 2.4.0
- Fermipy: 1.4.2
- Astropy: 7.2.0
- NumPy: 2.4.6
- Scikit-learn: 1.9.0

### Key fix notes:
- WSL2 required .wslconfig with swap=4GB to solve conda environment
- Fermitools requires Python 3.11 (not 3.9)
- libmamba solver required for successful resolution on 8GB RAM

### To reactivate environment:
conda activate fermi
