# 🧪 MD Stats Auditor

**🔗 Try it: [md-stats-auditor-celes.streamlit.app](https://md-stats-auditor-celes.streamlit.app/)**

A statistics sanity-checker for molecular dynamics (MD) trajectory data.
Upload GROMACS-style `.xvg` files and get: a check for the classic
pseudoreplication pitfall (treating autocorrelated frames as independent
samples), the corrected replica-level statistics, effect sizes, and a
publication-style black-and-white bar chart with significance stars —
for two groups or more, one metric or several at once.

## Why

MD trajectories generate thousands of correlated frames per run. Running
a t-test (or ANOVA) on frames directly, instead of on independent
replicate means, routinely produces absurdly small p-values that don't
hold up to scrutiny. This tool exists to catch that mistake
automatically, alongside your existing MD analysis tools — it audits
results, it doesn't replace `gmx rms` / `gmx sasa` / etc.

## Features

- **Pseudoreplication check**: flags when the naive frame-level p-value
  is drastically smaller than the defensible replica-level p-value
- **2 or more groups per metric**: Welch's t-test for 2 groups;
  one-way ANOVA + Holm-corrected pairwise post-hoc tests for 3+
- **Batch mode**: check several metrics at once, with a second
  Holm-Bonferroni correction applied across the whole batch
- **Effect sizes**: Cohen's d, Hedges' g (small-sample corrected),
  eta-squared for ANOVA, with a plain-language size guide (negligible /
  small / medium / large)
- **Significance stars** (`*` `**` `***` `ns`) — applied only to the
  defensible replica-level/Holm-corrected result, never to the naive one
- **Mean ± SD or ± SEM**, selectable
- **Publication-style chart**: black & white, hatched bars per group,
  error bars, no gridlines, downloadable as 300 dpi PNG
- **Optional AI write-up**: a one-click, plain-language interpretation
  of the result(s) (requires your own Anthropic API key — never stored)

## Usage

1. Open the [live app](https://md-stats-auditor-celes.streamlit.app/)
2. Upload `.xvg` files named `<metric>_<group>_rep<N>.xvg`
   (e.g. `distance_rosavin_rep1.xvg`, `distance_rosin_rep2.xvg`,
   `distance_arabinose_rep1.xvg` — any number of groups, any number of
   metrics)
3. Select one or more metrics to check, click **Run audit**
4. Read the check, the corrected statistics, pairwise table, and chart
   for each metric, plus the batch-level correction if you selected more
   than one
5. (Optional) enter an Anthropic API key in the sidebar and click
   **Write this up with AI** for a plain-language paragraph covering
   everything you checked

## Status

Version 1, live and public. Source code is currently closed; a paid
tier is planned. Feedback and bug reports welcome — please open an
issue on this repository.

## License / usage terms

This project is licensed under the Business Source License 1.1: free to
use for personal, academic, and evaluation purposes. The app is provided
as-is; see the live app for full terms.
