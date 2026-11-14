# _Spondias mombin_ leaf extract: antibacterial activity and toxicity – data and analysis code

Data and Python code for the article:

> Adeyemi DK, Orojuekun DB, Abdullahi AS, Adeluola AO, Johnson OO, Ologunagba MO, Ishola IO, Abdulrahman U, Chijioke MC, Ayoola GA. Antibacterial activity and toxicological assessment of _Spondias mombin_ L. (Anacardiaceae) leaves against multidrug-resistant bacterial isolates from Lagos University Teaching Hospital, Nigeria. _Tropical Journal of Natural Product Research_ (manuscript TJNPR-2026-694; citation to be updated on publication).

The repository contains the notebooks and scripts that produce every statistic, table and figure reported in the article and its supplementary information.

## Contents

```

notebooks/
  01_Smombin_zone_of_inhibition_ANOVA.ipynb     agar well diffusion statistics
  02_Toxicity_ANOVA_Tukey.ipynb                 subacute, subchronic and reversibility statistics
scripts/
  make_smombin_anova_file.py                    raw zone sheet -> long-format ANOVA file
  make_figure2.py                               Fig. 2 of the article
results/                                        all outputs are written here
```

## Study design in brief

**Antibacterial assays.** Hydroethanolic (50% ethanol) leaf extract tested against 20 isolates: 18 characterised multidrug-resistant clinical isolates from Lagos University Teaching Hospital (ESBL-, AmpC- and carbapenemase-producing and efflux-positive strains) and _E. coli_ ATCC 25922 and _S. aureus_ ATCC 25923. Agar well diffusion at 400, 200 and 100 mg/mL in triplicate; MIC and MBC by agar dilution. The solvent control (distilled water) gave no inhibition and is not analysed.

**Toxicity studies.** Female Wistar rats given 40, 200 or 1000 mg/kg/day orally for 28 days (subacute) or 60 days (subchronic), and a satellite group observed for 14 days after 60 days of dosing (reversibility). Haematology (Mindray BC-3200) and serum biochemistry (Erba Mannheim XL-640) were measured on four animals per group.

## Statistical methods

| Analysis                                                                  | Notebook | Article                        |
| ------------------------------------------------------------------------- | -------- | ------------------------------ |
| One-way ANOVA of zone diameter by concentration, Tukey's HSD, eta squared | 01       | Section 3.2, Table S6          |
| ANOVA with isolate as a blocking factor                                   | 01       | Section 3.2, Table S6          |
| Two-way ANOVA, concentration x Gram reaction                              | 01       | Section 3.2, Fig. 2B, Table S6 |
| One-way ANOVA within each isolate                                         | 01       | Table 2                        |
| Shapiro-Wilk (residuals) and Levene tests                                 | 01, 02   | Tables S6, S8                  |
| One-way ANOVA per parameter, Tukey's HSD, eta squared                     | 02       | Tables 4-5, S2-S5, S7          |
| Kruskal-Wallis sensitivity analysis                                       | 02       | Table S8                       |

Significance: p < 0.05, marked with a single `*`. Tukey results are interpreted only where the ANOVA is significant. In the Tukey output, `meandiff` is the second group minus the first group of each comparison.

## How to run

Requires Python 3.10 or later (the analyses were run with Python 3.11).

```bash
git clone https://github.com/<account>/spondias-mombin-antibacterial-toxicity.git
cd spondias-mombin-antibacterial-toxicity
pip install -r requirements.txt

python scripts/make_smombin_anova_file.py   # optional: rebuilds data/processed/Smombin_zones_anova_file.csv
jupyter notebook notebooks/                 # run 01 and 02 (Kernel > Restart & Run All)
python scripts/make_figure2.py
```

The notebooks find the `data/` and `results/` folders whether they are started from the repository root or from `notebooks/`.

## Notes on the data

- Raw toxicity sheets are saved in Windows-1252 encoding; notebook 02 reads them as such and checks any Mean/SD columns against the individual readings.
- Test names are harmonised across studies (for example HDLC to HDL, SGPT to ALT, SGOT to AST).
- Direct bilirubin was measured only in the subacute study. It is analysed by notebook 02 but not reported in the article, which reports only the 31 parameters measured in all three studies.
- The raw zone sheet also contains levofloxacin readings for the same isolates. Those results are published separately: Abdullahi AS, Ayoola GA, Adeluola AO, et al. Experimental evaluation of levofloxacin efficacy against multidrug-resistant bacterial isolates at the Lagos University Teaching Hospital, Nigeria. _Bull Natl Res Cent._ 2026;50:66. https://doi.org/10.1186/s42269-026-01459-y
- There are no missing values. Isolates were de-identified laboratory stock cultures; no patient data are included.

## Ethics

Animal procedures were approved by the University of Lagos Research Ethics Committee (UNILAGREC/22/06/005).

## Licence

Code is released under the MIT Licence (see `LICENSE`). Data in `data/` are released under the Creative Commons Attribution 4.0 International licence (CC BY 4.0); please cite the article when reusing them.

## Contact

Corresponding author: Abubakar S. Abdullahi, Department of Pharmaceutical Chemistry, Faculty of Pharmacy, University of Lagos (ORCID 0000-0002-3896-3844), abubakarabdulsadiq@gmail.com
