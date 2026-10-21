# fda-recall-compliance-analysis

# FDA Recall & Regulatory Action Analysis

**Does FDA enforcement follow product-safety risk?**

This team project explores how FDA recall patterns relate to regulatory enforcement. Using Python, we cleaned two FDA datasets, linked facilities through their FDA Establishment Identifier (FEI Number), and answered 15 questions about recall trends, severity, causes, enforcement activity, and geography.

Developed for **BA780 at Boston University’s Questrom School of Business**.

## Project overview

The analysis examines whether the product categories and facilities with more recall activity also receive more compliance actions. It uses exploratory data analysis and visualizations to identify patterns that could inform further investigation and inspection planning.

**Tools:** Python, pandas, NumPy, Matplotlib, and Google Colab.

## Data

Both datasets come from the [FDA Data Dashboard](https://datadashboard.fda.gov/).

| Dataset | Coverage in this notebook | Records |
| --- | --- | ---: |
| [Recalls](https://datadashboard.fda.gov/oii/cd/recalls.htm) | June 2012–September 2026 | 104,113 original product rows |
| Recalls after removing missing facility IDs | Same snapshot | 104,083 product rows representing 37,623 unique recall events |
| [Compliance Actions](https://datadashboard.fda.gov/oii/cd/complianceactions.htm) | 2008–2026 | 177,252 action records |

The recall events cover **10,231 facilities**, including **1,724 facilities** that also appear in the compliance-action dataset. The facility analysis retains recalling facilities with no matching action record.

A recall event can include multiple products. To avoid counting each product as a separate recall, the analysis counts each **Event ID** once. Compliance actions remain counts of action records, rather than unique companies.

## Main findings

| Area | Finding from the notebook |
| --- | --- |
| Recall severity | The Class I share of recall events increased from **10.4% in 2013 to 19.6% in 2025**. Class I event counts increased from 380 to 412. |
| Product categories | Excluding tobacco, medical devices represented **40.5% of recall events** and **15.2% of compliance actions**. Food/Cosmetics had the largest action share at 38.8%. |
| Serious recall causes | Keyword groups for undeclared allergens, Salmonella, and Listeria accounted for approximately **58% of Class I recall events**. |
| Enforcement trends | Outside tobacco, warning letters decreased from **779 in 2011 to 500 in 2025**. Seizures and injunctions combined decreased from **48 to 2**. |
| Facility recall history | The share of facilities with any recorded action was **13.5%** for those with one recall event and **46.4%** for those with more than 100 events. |
| Timing around actions | Among 735 facilities in the timing analysis, average recall events peaked at **0.54 per facility in the first observed action year**, compared with **0.20 three years later**. This is an association, not evidence of a causal effect. |

These results describe the notebook’s data snapshot and filters. Different questions use different time windows and inclusion rules.

## Analysis structure

The notebook includes a data dictionary, a cleaning log, charts, interpretations, and caveats for each question.

| Questions | Focus |
| --- | --- |
| Q1–Q5 | Recall trends and comparisons of recalls and actions by product type, state, and facility |
| Q6–Q9 | Recall severity, product categories, and reasons for recalls |
| Q10 | Changes in non-tobacco enforcement over time |
| Q11–Q13 | Facility recall count, severity, and timing around first observed actions |
| Q14–Q15 | State recall-reason patterns and comparisons of repeat recalls with action rates |

## Data preparation

- Replaced dash placeholders with missing values.
- Removed 30 recall rows without a facility ID and standardized FEI Numbers as integers.
- Filled missing state values with `No US State` and other missing fields with `Unknown`.
- Converted date fields to datetime and extracted the year.
- Checked for duplicate rows; none were found.
- Created an event-level recall table by retaining one row per Event ID.
- Joined recall and action counts by FEI Number, retaining facilities without matching actions.
- Kept high-recall facilities in the analysis and used medians and repeat-recall shares to address skewed counts.

Tobacco accounts for approximately 94% of action records, so it is excluded from selected product, state, and enforcement comparisons. The facility-history table uses the broader action dataset; tobacco is not excluded uniformly throughout the notebook.

## Run the notebook

The analysis is in [A06_FDA_Regulatory_Action_Analysis-4(1).ipynb](A06_FDA_Regulatory_Action_Analysis-4%281%29.ipynb). Upload the notebook alongside this README in the repository root to use this link.

### Google Colab

1. Download the notebook or open it from GitHub in [Google Colab](https://colab.research.google.com/).
2. Run the cells in order, starting with the imports and data-loading cells.
3. The notebook loads the CSV datasets through shared Google Drive download links. An internet connection and accessible links are required.

### Local Jupyter

Install the required packages:

```bash
python -m pip install pandas numpy matplotlib notebook
```

Launch Jupyter:

```bash
jupyter notebook
```

Open the notebook and run all cells from top to bottom. If a Google Drive link is unavailable, obtain the CSV exports from the FDA Dashboard and update the two `pd.read_csv()` paths. New exports may produce different results from the saved September 2026 snapshot.

## Limitations

- **Observational findings:** The analysis does not establish causation or prove that enforcement is insufficient.
- **Different observation periods:** Recall and action histories span different years. The earliest and latest recall years are partial.
- **Annual timing:** A recall and action in the same calendar year cannot be ordered precisely using the timing analysis. “First action” means first observed in this dataset.
- **Product and facility differences:** Recall counts do not account for production volume, facility size, exposure, or the number of people harmed. A voluntary recall may not require a separate compliance action.
- **Approximate reason groups:** Recall reasons are categorized using keywords. In Q8, 36.8% of events remain in `Other`; Q14 uses a separate grouping scheme.
- **Missing geography:** The label `No US State` represents a missing state value and does not, by itself, confirm that a facility is foreign. State information may also differ from the place of manufacture or distribution.
- **Relative state rankings:** Gaps between state percentile rankings are screening indicators, rather than proof of under-enforcement.

## Suggested next steps

Further work could combine recall histories with inspection records, facility size, and production volume to test whether recall count and severity help prioritize closer review. Food allergen and pathogen controls, repeat-recall facilities, and medical-device oversight are areas for further investigation.

## Team

**Team A06:** Malak Taoujni, Filip Handjiski, Fan-yu Chiu, Rislyn Raja, and Aryan Bajaj.

## Sources and acknowledgments

- U.S. Food and Drug Administration: [Recalls Dashboard](https://datadashboard.fda.gov/oii/cd/recalls.htm), [Compliance Actions Dashboard](https://datadashboard.fda.gov/oii/cd/complianceactions.htm), and [Recall Background and Definitions](https://www.fda.gov/safety/industry-guidance-recalls/recalls-background-and-definitions).
- The notebook includes a disclosure describing the team’s use of Claude for brainstorming, writing support, and code review/debugging. This README was prepared with ChatGPT assistance.
- This is an academic team project and is not affiliated with or endorsed by the FDA. No license for the team’s code is specified here; source-data availability does not automatically license the code.
