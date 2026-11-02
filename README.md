# Wearable sensors reveal the physiological signature of human influenza infection

This repository contains the analysis and visualization code accompanying the manuscript Wearable sensors reveal the physiological signature of human influenza infection. The study examines wearable physiological measurements and clinical outcomes during influenza A(H3N2) inoculation in two human challenge studies (clinical trial number [NCT04978454](https://clinicaltrials.gov/study/NCT04978454) and [NCT06476275](https://clinicaltrials.gov/study/NCT06476275)). The analyses focus on heart rate (HR), respiratory rate (RR), heart rate variability (HRV), and temperature, and their associations with symptom scores and PCR viral load.

## Repository contents

| File | Purpose |
| --- | --- |
| `data_analysis_and_visualization.ipynb` | Assess wearable coverage, apply participant exclusions, summarize demographics, normalize HR to participant baselines, and visualize physiological and clinical trajectories. Includes analyses of measurements within recorded sleep windows. |
| `statistical_analysis.ipynb` | Analyze prepared sleep-derived wearable deviations using linear mixed-effects models, including pre/post-inoculation comparisons and associations with symptom scores and viral load. |
| `test_information.csv` | Participant metadata used by the notebooks. Inoculation timestamps are time-shifted to remove sensitive timing information. |

## Code availability

This repository contains the analysis and visualization code accompanying the manuscript *Wearable sensors reveal the physiological signature of human influenza infection*, currently under peer review.

The code is provided to facilitate editorial and peer review of the analyses presented in the manuscript. The underlying participant-level study data are not included due to privacy and institutional data-sharing restrictions.

Licensing terms for broader reuse of the code have not yet been established.

## Data availability

The underlying participant-level study data are not publicly available due to privacy and institutional data-sharing restrictions. Access to the study data may be considered upon reasonable request to the corresponding author, subject to applicable institutional approvals.

This repository provides the analysis code but does not include the wearable time series, sleep records, viral-load measurements, symptom scores, or prepared analysis datasets required to reproduce the analyses.

The data/ directory is excluded from version control. Consequently, the notebooks cannot be executed end to end from a fresh clone alone.

## Analysis overview

`data_analysis_and_visualization.ipynb` combines data from the CIVICs and Exhale studies. It checks device wear time, applies fixed participant exclusions, defines infection/symptom cohorts, calculates baseline-normalized HR, compares daytime and nighttime measurements, and generates figures. Later sections align wearable measurements with clinical assessments and participant-specific Oura sleep intervals.

`statistical_analysis.ipynb` uses prepared participant-day sleep measurements to analyze four deviations from baseline: HR, breathing rate, HRV, and temperature. Analyses focus on symptomatic infected participants and include:

- Pre/post-inoculation comparisons and comparisons of individual post-inoculation days with baseline.
- Associations with symptom scores and log10 PCR viral load.
- Models with participant-specific random intercepts, with additional models adjusted for sex, age, and BMI.
- Benjamini–Hochberg false discovery rate correction within the test families defined in the notebook.

The notebooks document their cohort definitions, day conventions, baseline calculations, and missing-value handling.

## Software environment

All analyses were performed using Python 3.11.11. The required Python dependencies are listed in requirements.txt.

To create a local environment and install the dependencies:

```bash
python3.11 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Dependency versions are currently unpinned, so this installation does not recreate the exact environment used for the publication.

## Running the notebooks

Execution requires authorized access to the original study data. For users who already have that access:

1. Run JupyterLab from the repository root with `jupyter lab` and select the Python environment containing the dependencies above.
2. Configure the input paths in the first cell of `data_analysis_and_visualization.ipynb`, including the external Oura sleep-data directories.
3. Supply the heart rate Parquet files and clinical CSV files referenced by that notebook.
4. For `statistical_analysis.ipynb`, supply `data/wearable_sleep.csv`, `data/viral_loads.csv`, `data/symptom_scores.csv`, and the compatible participant metadata in `test_information.csv`.
5. Run each notebook from top to bottom. Figures and statistical tables are displayed within the notebooks.

Participant identifiers, relative-day labels, and timestamps must align across inputs. Any timestamp shifts must be applied consistently to preserve the alignment between inoculation, wearable measurements, and sleep intervals.

## Authors and contact

**Code and analysis:** Jiamu Yang  
Department of Biomedical Engineering, Duke University

**Corresponding author:** Jessilyn P. Dunn, PhD  
Department of Biomedical Engineering, Duke University  
Email: jessilyn.dunn@duke.edu

This repository accompanies the manuscript *Wearable sensors reveal the physiological signature of human influenza infection*.

For questions regarding the study data or data access, please contact the corresponding author.