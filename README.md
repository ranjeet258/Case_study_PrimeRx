# Nexavir | PrimeRx Flow Case Study
### Alert-to-Treatment & Commercial Opportunity Analysis

## Overview

PrimeRx is a pharmaceutical company operating across the U.S. healthcare landscape. Its flagship product, **Nexavir (DRG001)**, is a treatment designed for high clinical need and broad prescriber adoption.

This case study analyzes PrimeRx's Rx flow, HCP, account, sales, and alert datasets collected over an 18-month period to answer a core commercial analytics question:

> Doctors (HCPs) are diagnosing patients who may need treatment, but not all of them are prescribing our drug. Where is the disconnect, and how should the sales team respond?

The analysis connects diagnostic activity (clinical alerts) with prescribing behavior (sales data) to identify high-value HCPs and accounts, uncover missed opportunities, and translate the findings into a data-driven field engagement plan.

## Business Problem

The datasets can be linked using `HCP_ID` to trace the patient journey from clinical signal to prescription. The analysis addresses four objectives:

1. Identify HCPs and accounts with high prescription and alert activity
2. Identify doctors receiving strong clinical signals but writing few or no prescriptions
3. Identify accounts with low prescription activity relative to their doctor base
4. Recommend HCPs and accounts that should be prioritized by the sales team

## Repository Structure

```
├── README.md
├── notebooks/
│   ├── Case_Study_1-2-3.ipynb      # Questions 1–3: Alert/Rx ranking, drop-off, competitor share
│   ├── Case_Study_4-5.ipynb        # Questions 4–5: Account-level opportunity and efficiency
│   └── Case_Study_6-7.ipynb        # Questions 6–7: Before/after lift and rep allocation strategy
├── data/
│   └── PrimeRx_Datasets.xlsx       # Source datasets: Alerts, Sales, Affiliation
├── results/
│   ├── Q1_Q2_Q3_Results.xlsx
│   ├── Q4_Q5_Results.xlsx
│   └── Q6_Q7_Results.xlsx
└── deliverable/
    └── PrimeRx-Case-Study-Final-PPT.pdf   # Client-facing presentation and executive summary
```

## Source Data

Three datasets capture different aspects of the patient treatment journey, joined on `HCP_ID`.

| Dataset | Rows | Key Columns | Purpose |
|---|---|---|---|
| **Alerts** | 9,537 | `Alert_ID`, `Alert_Date`, `HCP_ID`, `Lab_Result` (positive/negative) | Clinical signals indicating potential treatment need at the doctor level |
| **Sales** | 5,917 | `Prescription_ID`, `Prescription_Date`, `HCP_ID`, `Drug_Name`, `Drug_ID`, `Prescription_Volume` | Prescription activity across doctors and therapies |
| **Affiliation** | 216 | `HCP_ID`, `Account_ID`, `Account_Name` | Maps doctors to hospitals/clinics/accounts |

## Methodology

The analysis is organized into seven questions, each building on the last:

| # | Question | Notebook |
|---|---|---|
| Q1 | Who are the most active doctors, and are they helping our product? Top 10 by alert volume vs. Top 10 by prescription volume. | `Case_Study_1-2-3.ipynb` |
| Q2 | Which doctors see the need but don't act on it? HCPs with positive alerts and no prescribing activity within 30 days, plus a conversion funnel. | `Case_Study_1-2-3.ipynb` |
| Q3 | Among the top-alerting doctors, how much business is going to competitors? Our-drug vs. competitor prescription share. | `Case_Study_1-2-3.ipynb` |
| Q4 | Which hospitals are sitting on the biggest untapped opportunity? Account-level alert count vs. conversion ratio. | `Case_Study_4-5.ipynb` |
| Q5 | Which accounts represent the largest untapped prescription opportunity? Prescription volume per active doctor. | `Case_Study_4-5.ipynb` |
| Q6 | Did alerts actually change doctor behavior? 90-day before/after prescription lift, segmented into New Starters, Growers, and Non-Responders. | `Case_Study_6-7.ipynb` |
| Q7 | Commercial HCP prioritization — recommended field force (rep call) allocation across the three behavioral segments. | `Case_Study_6-7.ipynb` |

Each notebook loads the source datasets, performs the required joins/aggregations in pandas, and exports the corresponding output tables to the matching results workbook.

## Key Findings

- Overlap between the top alert-volume and top prescription-volume doctors is minimal — only one HCP appears on both Top 10 lists, indicating a weak link between clinical signal and prescribing action.
- 68 HCPs received multiple positive alerts but wrote zero prescriptions within 30 days — the largest source of conversion leakage.
- Four of the top ten alert-volume doctors (HCP041, HCP011, HCP021, HCP007) have no prescriptions for any drug, including competitors. This points to a prescriber-engagement gap rather than competitive loss.
- Among doctors who are prescribing, competitor share ranges from roughly 29% to 75%, with **Rivalex (DRG002)** capturing the largest share of diverted business.
- Account-level analysis shows that increasing volume among already-active prescribers (e.g., ACC003, ACC009, ACC012) offers a faster path to growth than recruiting new prescribers.
- Before/after lift analysis shows New Starters and Growers respond positively to alerts, while Non-Responders show a decline — suggesting diminishing returns from continued outreach to that segment.

## Recommendation

Field force capacity should be allocated by segment responsiveness rather than evenly across the HCP base:

| Segment | HCPs | % of Rep Calls | Rationale |
|---|---|---|---|
| New Starters | 64 | 50% | Strongest and most immediate prescribing response to alerts |
| Growers | 25 | 30% | Existing prescribers with high percentage lift; reinforce momentum |
| Non-Responders | 125 | 20% | Lower conversion likelihood; maintain minimum coverage only |

Priority accounts for near-term field engagement: **Riverside Health System, Northside General, and Eastview Medical** — each combines high alert volume with weak prescription conversion.

## Limitations

- The 18-month analysis window may mask seasonal effects in alert or prescribing activity.
- Drug-switching dynamics that occur outside the observed dataset are not captured.
- Conversion and lift metrics are based on available sales data only and do not account for formulary, access, or reimbursement constraints.

## Tools Used

- Python (pandas, matplotlib) via Jupyter Notebook
- Microsoft Excel for source data and output workbooks
- PowerPoint / PDF for the client-facing deliverable

## Deliverable

The full client presentation, including all charts, tables, and the executive summary, is available in `PrimeRx-Case-Study-Final-PPT.pdf`.

---
*This case study is prepared for internal analytical purposes. Data and findings are illustrative and based on a simulated PrimeRx/Nexavir dataset.*
