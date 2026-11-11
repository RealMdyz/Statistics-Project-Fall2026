# Statistics Course Project — Fall 1405 (2026)

**Title:** Cigarette smoking status and self-reported sleep duration among U.S. adults (NHANES 2021–2023)
**Track:** A — NHANES August 2021 – August 2023
**Author:** Mohammad Yasin Zare

## Research question
Among U.S. adults aged 18+, do weekly average sleep duration and the share of short sleep (< 7 h/night)
differ between never, former and current cigarette smokers? Does the difference remain after accounting
for age and sex? Among current smokers, is the number of cigarettes per day related to sleep duration?

Full statistical framing: [`PROJECT_CARD.md`](PROJECT_CARD.md) (Persian).

## Key Phase 1 & 2 Results
* **Phase 1 (Descriptive):** Current smokers have the highest weighted share of short sleep (27.7%) compared to former (20.3%) and never smokers (16.8%). The mean sleep duration difference is small but the proportion of short sleepers differs notably. Differences are unadjusted for confounding factors like age.
* **Phase 2 (Probability):** Event A (Short Sleep) and Event B (Current Smoker) are not statistically independent ($P(A \cap B) \neq P(A)P(B)$). The conditional probability of short sleep given current smoking ($P(A|B) \approx 0.28$) is notably higher than the marginal probability ($P(A) \approx 0.20$). The distribution of short sleep counts in sub-samples of $n=50$ is extremely well approximated by a $Binomial(50, 0.199)$ model.

## How to reproduce
```bash
python -m venv .venv
.venv\Scripts\activate          # Windows  (source .venv/bin/activate on macOS/Linux)
pip install -r requirements.txt
python src/download_data.py     # downloads DEMO_L, SLQ_L, SMQ_L from CDC into data/raw/
```
Then run the notebooks **in order**:

| Notebook | What it does | Phase tasks |
|---|---|---|
| `notebooks/01_load_and_merge.ipynb` | Load, merge on `SEQN`, derive variables, build analytic sample + flow table | 1: 2, A.1, A.4 |
| `notebooks/02_data_quality.ipynb` | Missing data, special codes, ranges, logical consistency, quality table | 1: 5 |
| `notebooks/03_descriptive_stats.ipynb` | Frequency tables, center/spread, 6 figures, group comparison, weighted vs unweighted | 1: 6, 7, 8, 9, A.3 |
| `notebooks/04_probability_and_bayes.ipynb` | Events, marginal/joint/conditional probabilities, independence check, Bayes theorem | 2: 1, 2, 3, 4, 9, A.1, A.4 |
| `notebooks/05_distributions_and_moments.ipynb` | Expected value, variance, normal approximation, covariance, binomial model simulation | 2: 5, 6, 7, 8, A.2, A.3 |

Optional: `python src/build_phase1_report.py` and `python src/build_phase2_report.py` re-render the HTML reports to PDF (requires `playwright`).

## Repository layout
| Path | Content |
|---|---|
| `PROJECT_CARD.md` | Statistical framing of the project (Persian) |
| `data/README.md` | Data source, files, download date, rebuild steps |
| `src/download_data.py` | Reproducible download of raw NHANES files |
| `src/nhanes.py` | Shared loading, merging, variable derivation, analytic sample, weighted statistics |
| `src/build_phaseX_report.py` | Renders the HTML reports to PDF |
| `notebooks/` | Analysis notebooks, run in numeric order |
| `figures/` | Final figures used in the reports |
| `reports/phase1.pdf` | **Phase 1 report (Persian)** |
| `reports/phase2.pdf` | **Phase 2 report (Persian)** |

Raw and processed data are **not** stored in this repository (see `.gitignore`).

## Phase status
| Phase | Deadline | Tag | Status |
|---|---|---|---|
| 1 — Data & descriptive statistics | 12 Aban 1405 | `phase-1` | ✅ done |
| 2 — Probability | 27 Aban 1405 | `phase-2` | ✅ done |
| 3 — Inference | 27 Azar 1405 | `phase-3` | — |
| 4 — Regression | 15 Dey 1405 | `phase-4` | — |
| 5 — Robustness & final | 5 Bahman 1405 | `phase-5-final` | — |