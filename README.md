# Claude usage and O\*NET Job Zones: a replication and extension of the Anthropic Economic Index

**Matthew Jay Zuniga** — April 2026

A short public analysis exploring how Claude.ai usage is distributed across occupations at different levels of educational preparation, using the [Anthropic Economic Index](https://www.anthropic.com/economic-index) open data and the U.S. Department of Labor's [O\*NET Job Zones](https://www.onetonline.org/help/online/zones).

## The question

The Economic Index's March 2026 "Learning Curves" report documents that Claude adoption is **skill-biased**: early adopters with high-skill tasks benefit more from Claude than later, less-technical adopters. If that holds, we'd expect Claude conversation volume to be disproportionately concentrated in occupations requiring more formal education. This notebook makes that pattern visible.

## The result

Running the analysis in `aei_education_analysis.ipynb` produces two figures:

1. **Claude conversation coverage by O\*NET Job Zone** — how much conversation share falls into tasks belonging to each preparation level.
2. **Claude usage vs. occupational baseline** — how Claude's zone distribution compares to the underlying distribution of O\*NET occupations themselves, which corrects for the fact that higher zones contain more occupations by default.

The headline metric is an over-representation ratio: Claude's share of total usage in a zone, divided by that zone's share of all O\*NET occupations. Ratios above 1 indicate the zone is over-represented in Claude usage relative to its occupational baseline.

## How to reproduce

1. Clone this repo.
2. Install dependencies: `pip install pandas matplotlib jupyter`
3. Download `Job Zones.txt` from the [O\*NET Database downloads page](https://www.onetcenter.org/database.html) and place it in the repo root. (The notebook pulls the Anthropic Economic Index files directly from Hugging Face; O\*NET Job Zones is a separate file you need to fetch yourself.)
4. Open the notebook: `jupyter notebook aei_education_analysis.ipynb`
5. Run all cells.

## Data sources

- **Anthropic Economic Index**, February 2025 release: Handa, K., Tamkin, A., McCain, M., et al. (2025). [*Which Economic Tasks are Performed with AI? Evidence from Millions of Claude Conversations.*](https://arxiv.org/abs/2503.04761). Licensed CC-BY.
- **O\*NET Job Zones**: U.S. Department of Labor, Employment and Training Administration. Public resource.
- **March 2026 Learning Curves report** (referenced, not used directly): Massenkoff, M., Lyubich, E., McCrory, P., Appel, R., & Heller, R. (2026). [*Anthropic Economic Index report: Learning curves.*](https://www.anthropic.com/research/economic-index-march-2026-report)

## What this analysis covers

This is a descriptive replication with a narrow extension. The goal is to make the adoption-by-education-level pattern legible and to motivate follow-up work.

Three limits to flag upfront. ONET task-occupation mappings are many-to-many, which affects how raw conversation shares aggregate across zones. ONET Job Zones approximate occupational preparation requirements rather than individual worker education. The Economic Index sample covers Claude.ai consumer traffic only, so enterprise API usage and non-Claude AI tools are out of scope. None of these are fatal, but they shape what the analysis can and can't say — the patterns here are consistent with causal stories but don't settle them.

The notebook's final section lists specific extensions: running the same analysis on the March 2026 release, implementing a task-share division approach to the many-to-many problem, and weighting by BLS employment data.

## License

Code in this repo: MIT. The underlying Anthropic Economic Index data is licensed CC-BY by Anthropic; O\*NET data is a public U.S. government resource.
