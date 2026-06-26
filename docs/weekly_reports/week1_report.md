# Weekly Research Report
## Project: Fermi-LAT Dark Matter Limits in Dwarf Spheroidal Galaxies
**Author:** Happy Patil | Silver Oak University  
**GitHub:** github.com/HappyP016/fermi-lat-dm-project

---

# Week 1 Report (Days 1–4)
**Period:** 25 June 2026 — 26 June 2026  
**Total hours this week:** ~6–8 hrs (estimate)  
**Cumulative hours:** ~6–8 hrs

---

## 1. Summary
Successfully built a complete gamma-ray astrophysics research environment from scratch on a Windows 11 laptop using WSL2 + Ubuntu, resolved multiple installation challenges including RAM constraints and Python version mismatches, established a professional GitHub repository, and completed the first real data analysis — loading the Fermi-LAT 4FGL-DR4 catalog and producing spectral fingerprint figures for 7,195 gamma-ray sources.

---

## 2. What I Did (Technical Log)

- [x] Installed WSL2 + Ubuntu 22.04 on Windows 11 Pro (resolved "Package could not be registered" error via dism.exe)
- [x] Installed Miniconda3 inside Ubuntu
- [x] Configured Git globally (username, email, default branch)
- [x] Created GitHub account (HappyP016), generated SSH keypair, connected Ubuntu terminal to GitHub
- [x] Created dissertation repository `fermi-lat-dm-project` with professional folder structure
- [x] Wrote project README with status checklist
- [x] Created conda environment `fermi` with Python 3.11
- [x] Installed Fermitools 2.4.0 (resolved RAM issue using libmamba solver + .wslconfig swap=4GB)
- [x] Installed Fermipy 1.4.2 + full science stack (astropy 7.2.0, numpy 2.4.6, scikit-learn 1.9.0)
- [x] Verified full stack: `ALL SYSTEMS GO`
- [x] Launched Jupyter notebook server inside Ubuntu, accessed via Windows browser
- [x] Downloaded 4FGL-DR4 catalog (7.8MB FITS file) from FSSC
- [x] Loaded catalog with astropy: 7,195 sources, 79 columns
- [x] Built pandas DataFrame with 12 key ML features
- [x] Identified 2,563 unassociated sources (Tier 3 search space)
- [x] Produced spectral fingerprint figure (3-panel histogram: PL_Index, Variability_Index, |GLAT|)
- [x] Saved figure to results/figures/

---

## 3. What I Learned

### Technical
- WSL2 requires the `libmamba` solver on 8GB RAM — the default conda solver exhausts available memory during dependency resolution of large environments like Fermitools
- Fermitools 2.4.0 requires Python 3.11, not 3.9 — version mismatches produce `LibMambaUnsatisfiableError`
- Always work inside Ubuntu's home filesystem (`~`), never inside `/mnt/c/` — Windows filesystem access is dramatically slower for scientific computing
- Two terminal windows are required: one dedicated to running Jupyter server, one for all other shell commands
- FITS files are the standard data format in astronomy — loaded with `astropy.table.Table.read(hdu=1)`
- Column names in catalog FITS files don't always match paper documentation — always inspect with `cat.colnames` first

### Scientific
- The 4FGL-DR4 catalog contains 7,195 gamma-ray sources detected over 14 years of Fermi-LAT observations (50 MeV – 1 TeV)
- 2,563 sources (35.6%) are unassociated — no known counterpart at any other wavelength
- Dark matter subhalo candidates are expected to have: PL_Index ~ 2.0–2.4, LP_beta ~ 0 (no curvature), Variability_Index < 18.48 (non-variable), high |GLAT| (not in Galactic plane)
- The Variability_Index threshold of 18.48 corresponds to 99% confidence that a source is non-variable
- AGN (blazars) dominate the catalog (3,994 sources = 55.5%) and are highly variable — easy to separate from DM candidates
- Pulsars (320 sources) are the hardest class to separate from DM subhalo candidates — similar spectral index range

### Conceptual
- Independent reproduction of published results is itself a valid scientific contribution — it verifies methodology, builds skills, and extends analysis to new parameter space
- A GitHub repository with real data analysis is more convincing evidence of research capability than any personal statement paragraph in an MSc application
- Research environments fail constantly — the skill is systematic debugging, not avoiding errors

---

## 4. Problems Encountered & How I Solved Them

| Problem | Cause | Solution |
|---|---|---|
| `wsl --install` → "Package could not be registered" | Windows Subsystem for Linux features not fully enabled | Ran `dism.exe` to manually enable WSL + VirtualMachinePlatform features, then restarted |
| `conda create` → process Terminated | 8GB RAM exhausted by default conda dependency solver | Installed `conda-libmamba-solver`, set as default, added `swap=4GB` to `.wslconfig` |
| `conda create -n fermi python=3.9 fermitools` → `LibMambaUnsatisfiableError` | Fermitools 2.4.0 requires Python ≥ 3.11 | Changed to `python=3.11` |
| `wget` → Permission denied | Was in `/mnt/c/WINDOWS/system32` instead of home directory | Ran `cd ~` first, then re-ran wget |
| `FileNotFoundError` loading catalog | Forgot to download file to `data/raw/` before running notebook | Downloaded with wget in terminal, reran notebook cell |
| `KeyError: 'Spectral_Index'` | Column named `PL_Index` in this catalog version, not `Spectral_Index` | Inspected all column names with list comprehension, identified correct name |
| Unassociated mask returning 0 | Blank class encoded as `'--'` not empty string in this catalog | Updated mask to check for `'--'` string |

---

## 5. Results This Week

### Key Numbers
- 4FGL-DR4 catalog: **7,195 total sources**, **2,563 unassociated** (35.6%)
- Source class breakdown: AGN 3,994 | Unassociated 2,563 | Pulsar 320 | SNR/PWN 176 | Other 142
- Full science stack verified: Fermitools 2.4.0, Fermipy 1.4.2, Astropy 7.2.0, NumPy 2.4.6, scikit-learn 1.9.0

### Figures Produced
- `results/figures/spectral_fingerprints.png` — 3-panel histogram of PL_Index, Variability_Index, |GLAT| by source class

### Code Committed
- Initial repository structure + README
- Environment setup notes
- Notebook: `01_catalog_feature_analysis.ipynb`

---

## 6. Scientific Understanding Check
*To be filled in by student — answers in your own words*

**Q: What does the spectral index (PL_Index) physically represent?**
> [Your answer here]

**Q: Why are high-Galactic-latitude unassociated sources more likely to be DM subhalo candidates?**
> [Your answer here]

**Q: What is the purpose of the Variability_Index threshold at 18.48?**
> [Your answer here]

---

## 7. Literature This Week
*Papers to read before Week 2 — download PDFs at next wifi session*

| Paper | Authors | Priority |
|---|---|---|
| Particle Dark Matter: Evidence, Candidates and Constraints | Bertone, Hooper, Silk (2004) | 🔴 High |
| Indirect Detection of Dark Matter | Funk (2015) | 🔴 High |
| The Large Area Telescope on the Fermi Gamma-ray Space Telescope | Atwood et al. (2009) | 🔴 High |
| Fermipy: An open-source Python package for analysis of Fermi-LAT data | Wood et al. (2017) | 🔴 High |

---

## 8. Next Week Plan

- [ ] Answer the 3 scientific understanding check questions above — write them out fully
- [ ] Read Bertone et al. (2004) Sections 1–3 (Introduction + Evidence for DM)
- [ ] Complete spectral fingerprint analysis — describe what each plot shows scientifically
- [ ] Cell 5: Build feature correlation matrix (heatmap)
- [ ] Cell 6: First ML classifier — Random Forest on known sources
- [ ] Download Fermi-LAT background templates for Tier 1 pipeline (campus wifi)

---

## 9. Supervisor Notes

> Questions to ask university supervisor:
> - What is the required dissertation word/page count?
> - What citation style is required (APA/ADS)?
> - Is a university supervisor needed for the Fermi-LAT analysis, or is this self-directed?

---

## 10. MSc Application Relevance

This week's work demonstrates: independent Linux environment setup, professional version control with Git/GitHub, hands-on experience with real NASA gamma-ray telescope data (Fermi-LAT 4FGL-DR4), FITS file handling with Astropy, and systematic debugging of a complex scientific software stack — all directly relevant to MSc programs in high-energy astrophysics, astroparticle physics, and computational astrophysics at European universities.

---
*Report generated: 26 June 2026*  
*Next report due: 3 July 2026*
