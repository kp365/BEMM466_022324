# Monte Carlo Simulation for Risk Analysis in Public Infrastructure Projects

[![Python 3.12](https://img.shields.io/badge/python-3.12-blue.svg)](https://www.python.org/downloads/release/python-3120/) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repository contains a Python script for performing Monte Carlo simulations to analyze cost overruns and schedule delays in large-scale public infrastructure projects. The simulation is data-driven, using historical data from UK Government Major Projects Portfolio (GMPP) reports to model uncertainties, derive Work Breakdown Structures (WBS), and apply Critical Path Method (CPM) for probabilistic forecasting.

The code supports research questions from a dissertation on business analytics for risk management, including identifying key risk drivers, simulating outcomes, estimating contingencies, and recommending mitigation strategies.

## Table of Contents
•⁠  ⁠[Overview](#overview)
•⁠  ⁠[Features](#features)
•⁠  ⁠[Requirements](#requirements)
•⁠  ⁠[Installation](#installation)
•⁠  ⁠[Usage](#usage)
•⁠  ⁠[Data Sources](#data-sources)
•⁠  ⁠[Configuration Options](#configuration-options)
•⁠  ⁠[Outputs](#outputs)
•⁠  ⁠[Examples](#examples)
•⁠  ⁠[Contributing](#contributing)
•⁠  ⁠[License](#license)
•⁠  ⁠[Acknowledgments](#acknowledgments)

## Overview
Large public infrastructure projects often face significant cost overruns (e.g., >30-50%) and delays due to risks like regulatory hurdles, technical challenges, and funding issues. This script uses Monte Carlo methods to:
•⁠  ⁠Extract risk drivers from project narratives.
•⁠  ⁠Derive a simplified WBS and CPM graph based on data patterns.
•⁠  ⁠Simulate thousands of scenarios with probabilistic distributions (triangular or PERT/beta).
•⁠  ⁠Compute likelihoods of overruns, contingency needs, and sensitivity analyses.
•⁠  ⁠Generate visualizations (e.g., violin plots, ECDFs, heatmaps) and summaries for insights.

The approach aligns with literature on probabilistic risk modeling (e.g., Flyvbjerg et al.) and supports dissertation objectives for quantifying risks and informing policy.

## Features
•⁠  ⁠*Data Processing:* Loads and cleans GMPP CSV datasets; extracts overruns and risk drivers via regex lexicon.
•⁠  ⁠*WBS/CPM Derivation:* Dynamically infers task parameters and precedence from narratives and frequencies.
•⁠  ⁠*Simulation Engine:* Runs 100,000+ iterations with global shocks, risk multipliers, and cost-duration coupling.
•⁠  ⁠*Analyses:* CPM criticality, Spearman sensitivity, joint KDE, bootstrap ECDF bands, and scenario comparisons.
•⁠  ⁠*Visualizations:* Professional plots (violin, bar, heatmap, network diagram) with publication-ready styling.
•⁠  ⁠*Outputs:* CSVs (simulations, summaries), JSON (results), Markdown/JSON captions for figures.

## Requirements
•⁠  ⁠Python 3.12+
•⁠  ⁠Libraries (install via ⁠ pip install -r requirements.txt ⁠):
  - numpy
  - pandas
  - matplotlib
  - seaborn
  - scipy
  - networkx (optional, for enhanced CPM network diagrams)

No external installations beyond these are needed, as the code avoids internet access and uses built-in REPL-compatible libraries.

## Installation
1.⁠ ⁠Clone the repository:
   
⁠    git clone https://github.com/yourusername/monte-carlo-infrastructure-risk.git
   cd monte-carlo-infrastructure-risk
    ⁠
2.⁠ ⁠Install dependencies:
   
⁠    pip install -r requirements.txt
    ⁠
   (Create ⁠ requirements.txt ⁠ with the libraries listed above if not present.)

3.⁠ ⁠Place data files in the root directory (see [Data Sources](#data-sources)).

## Usage
1.⁠ ⁠Ensure the CSV data files are in the root folder (as listed in ⁠ FILE_PATHS ⁠).
2.⁠ ⁠Run the script:
   
⁠    python monte_carlo_simulation.py
    ⁠
3.⁠ ⁠The script will:
   - Load and clean data.
   - Extract drivers and overruns.
   - Derive WBS/CPM.
   - Run simulations.
   - Print results by research question (RQ1-RQ5).
   - Save plots, CSVs, and JSON outputs.

Example output snippet:

RQ3: Likelihood of overruns
- Mean Duration: XX.XX months | P90: XX.XX | Prob delay: XX.X%
- Mean Cost: £XXXX.XXm | P90: £XXXX.XXm | Prob overrun: XX.X%


Customize via config variables (e.g., ⁠ N_SIM=100_000 ⁠, ⁠ USE_CPM=True ⁠).

## Data Sources
The script processes the following GMPP CSV files (included in the repo or downloadable from UK government sources):
•⁠  ⁠⁠ BEIS_Government_Major_Projects_Portfolio_Data_March_2022.csv ⁠
•⁠  ⁠⁠ DESNZ_Government_Major_Projects_Portofolio_AR_Data_March_2024.csv ⁠
•⁠  ⁠⁠ GMPP_Government_Major_Projects_Portfolio_AR_Data_March_2022.csv ⁠
•⁠  ⁠⁠ GMPP_Government_Major_Projects_Portofolio_AR_Data_March_2023.csv ⁠
•⁠  ⁠⁠ CO_Government_Major_Projects_Portofolio_AR_Data_March_2024 (1).csv ⁠

These contain project details like baselines, forecasts, variances, and narratives. Sources: UK Infrastructure and Projects Authority (IPA) annual reports on major projects.

If files are missing, the script skips them gracefully.

## Configuration Options
Edit variables at the top of the script:
•⁠  ⁠⁠ FILE_PATHS ⁠: List of CSV paths.
•⁠  ⁠⁠ N_SIM ⁠: Number of simulations (default: 100,000).
•⁠  ⁠⁠ SAVE_PLOTS ⁠: Save figures (default: True).
•⁠  ⁠⁠ POSITIVE_OVERRUNS_ONLY ⁠: Filter to positive overruns (default: True).
•⁠  ⁠⁠ USE_SHRINKAGE_PRIOR ⁠: Blend empirical data with prior (default: True).
•⁠  ⁠⁠ PRIOR_MEAN/SD/STRENGTH ⁠: Bayesian prior for overruns.
•⁠  ⁠⁠ USE_CPM ⁠: Enable Critical Path Method (default: True).
•⁠  ⁠⁠ USE_PERT ⁠: Use PERT/beta distributions instead of triangular (default: False).
•⁠  ⁠⁠ DRIVER_LEXICON ⁠: Regex patterns for risk extraction (expandable).

## Outputs
•⁠  ⁠*CSVs:* ⁠ simulated_durations.csv ⁠, ⁠ simulated_costs.csv ⁠, ⁠ mcs_summary_table_table.csv ⁠, ⁠ cpm_slack_summary.csv ⁠.
•⁠  ⁠*JSON:* ⁠ mcs_results.json ⁠ (config, baselines, stats); ⁠ figure_captions.json ⁠ (plot metadata).
•⁠  ⁠*Markdown:* ⁠ figure_captions.md ⁠ (human-readable captions).
•⁠  ⁠*Plots (PNG):* e.g., ⁠ rq2_wbs_breakdown.png ⁠, ⁠ rq3_violins_adjusted.png ⁠, ⁠ cpm_network.png ⁠ (saved if ⁠ SAVE_PLOTS=True ⁠).
•⁠  ⁠*Console Summary:* Results mapped to research questions (RQ1-5), including means, percentiles, probabilities, sensitivities, and recommendations.

## Examples
•⁠  ⁠*Risk Drivers (RQ1):* Extracts and frequencies drivers like "regulatory delays" from narratives.
•⁠  ⁠*Model Setup (RQ2):* Prints baselines, multipliers, and saves WBS/CPM visuals.
•⁠  ⁠*Likelihoods (RQ3):* Computes P(overrun >20%), saves distributions/ECDFs.
•⁠  ⁠*Contingencies (RQ4):* Percentiles for buffers (e.g., P90 delta vs baseline).
•⁠  ⁠*Mitigation (RQ5):* Scenario with 10% risk reduction; highlights top sensitivities/criticalities.

For custom runs, adjust configs and re-run.

## Contributing
Contributions welcome! Fork the repo, make changes, and submit a pull request. Issues for bugs or enhancements.

•⁠  ⁠Report bugs: Open an issue with details.
•⁠  ⁠Add features: E.g., more distributions or advanced CPM solvers.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments
•⁠  ⁠Inspired by dissertation proposal on business analytics for risk management (University of Exeter, MSc Business Analytics).
•⁠  ⁠References: Flyvbjerg et al. (2002) on overruns; PMI risk standards.
•⁠  ⁠Data: UK IPA GMPP reports.
•⁠  ⁠Libraries: NumPy, Pandas, Matplotlib, Seaborn, SciPy.

Contact: Karan/kp618@exeter.ac.uk
