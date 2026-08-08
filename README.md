# Corporate Budget Variance Analysis and Stress Test Model

**Tool:** Microsoft Excel (Advanced) | **Domain:** Finance | **Type:** Financial Modelling

---

## Business Question

Which cost centres and revenue lines are driving the largest budget deviations, what is the financial impact under stress, and what corrective action should management take?

---

## Decision

Product B requires an immediate product review — FY24 actuals ran ~13% below budget on average, worsening each quarter. Operations cost inflation (+7% avg FY24) is accelerating and requires a procurement audit before FY25 budgeting. Services is the one segment consistently outperforming budget and warrants increased allocation.

Under severe stress (−12% revenue, +8% cost overrun), Net P&L drops from ₹765 L to ₹276 L — a 64% erosion. The business retains profitability across the entire modelled sensitivity grid (down to −15% revenue / +12% cost). Simultaneous shocks beyond the tested range would be required to push the company into loss territory.

---

## Problem

The business had no structured framework to isolate which line items were driving budget deviation, quantify cumulative impact over 24 months, or model the P&L impact of demand and cost shocks before they materialised. Management decisions on budget reallocation were being made without a scenario-tested view of downside risk.

Raw extracts arrived from multiple source systems (SAP dumps, legacy Excel, manual uploads, CSV imports) in inconsistent formats, making even basic variance analysis unreliable without heavy cleaning.

---

## Data Cleaning & Preparation

The starting point was a 200+ row raw extract (`Raw_Export`) containing every classic real-world data-quality problem:

| Issue | Examples encountered |
|-------|----------------------|
| Inconsistent date formats | `Jan-23`, `February 2024`, `2024-01`, `Mar/24`, `3/1/2024`, `SEP-22` |
| Broken FY / Quarter labels | `FY24`, `23`, `Financial Year 24`, `N/A`, blank, `q4`, `Quarter 2`, `Qtr 3`, `2` |
| Category spelling chaos | `Cost` / `Costs` / `Cst` / `Exp` / `Expense` / `Expenses` / `Revnue` / `Rev` / `Income` / `Sales Revenue` |
| Line-item name variants | `Product A` / `product a` / `Prod. A` / `A Product`; `Marketting` / `Markting` / `Mkt` / `Brand`; `HR` / `People` / `Human Resources`; `Operations` / `Manufacturing` / `Ops`; multiple Finance & Admin spellings |
| Mixed units & formats | Pure numbers, `Rs. 78.75`, `21.56 lakhs`, scientific notation (`1.1250e+02`), European decimals (`43,2`), full-rupee figures (`6160000`), blanks, `TBD`, negatives |
| Structural noise | Duplicate rows, grand-total / balance-check rows, flagged “verify this / old value / reconcile / duplicate?” notes |

**Cleaning steps applied:**

1. **Standardised temporal fields** — Parsed every date variant into a consistent `Mon-YY` month label, mapped all fiscal-year strings to `FY23` / `FY24`, and normalised quarters to `Q1`–`Q4`.
2. **Canonical category mapping** — Collapsed every revenue/cost spelling variant into exactly two values: `Revenue` or `Cost`.
3. **Canonical line-item mapping** — Reduced ~30 name variants to the eight business lines used throughout the model:  
   `Product A`, `Product B`, `Services`, `Operations`, `Sales`, `Marketing`, `HR`, `Finance & Admin`.
4. **Unit harmonisation** — Converted every amount into ₹ Lakhs (divided by 1,00,000 where full-rupee values appeared, stripped currency symbols and text suffixes, fixed scientific notation and European commas, treated blanks/TBD as missing).
5. **Deduplication & row validation** — Removed exact and near-duplicate rows, dropped non-line-item rows (grand totals, balance checks), and enforced one row per Month × Line Item combination.
6. **Assumption preservation** — Kept the original free-text assumption notes against every surviving row so auditability was not lost.

**Result:** A clean 192-row panel (8 line items × 24 months) stored in `Raw_Export_Clean` / `Raw_Export_Cleaned`. All downstream sheets (`Variance Engine`, `Scenario Analysis`, `Dashboard`) reference only the cleaned data via formulas — zero hardcoded values.

---

## What I Did

**Dataset:** Constructed a 192-row synthetic dataset modelled on mid-market Indian manufacturing benchmarks (FY2023–FY2024). Eight line items across five cost centres and three revenue lines. Monthly budget and actual figures with documented assumption notes for every input.

**Variance Engine:** Built a formula-driven variance engine with absolute variance, percentage variance, YTD cumulative variance, and RAG status (Green / Amber / Red) across all 192 rows. RAG logic differentiates correctly between revenue lines (adverse = below budget) and cost lines (adverse = above budget).

**Scenario and Sensitivity Analysis:** Two-input scenario model with live yellow input cells for Revenue Stress % and Cost Overrun %. All downstream stressed P&L figures update dynamically. Three named scenarios — Base, Moderate Stress (−5% rev, +3% cost), Severe Stress (−12% rev, +8% cost) — compared side by side. A 6×5 sensitivity table covering 30 combinations maps every revenue-cost stress intersection to a Net P&L outcome.

**Executive Dashboard:** Four KPI tiles, budget-vs-actual visualisation by line item, monthly trend context, RAG summary with management action signals, and a key-finding statement translating the analysis into CFO-level decisions.

**Excel skills demonstrated:** SUMPRODUCT with multi-condition arrays, cross-sheet formula linking, dynamic scenario inputs with downstream propagation, conditional RAG logic, financial chart construction, colour-coded financial modelling conventions (blue inputs, black formulas, green cross-sheet links).

---

## Key Findings

| Metric | Value |
|---|---|
| FY24 Budgeted Net P&L | ₹765 L |
| FY24 Actual Net P&L | ₹662 L |
| Product B FY24 Variance | −13% avg (worsening each quarter) |
| Operations FY24 Cost Overrun | +7% avg (accelerating in FY24) |
| Moderate Stress Net P&L (−5% rev / +3% cost) | ₹568 L (−26% vs budget) |
| Severe Stress Net P&L (−12% rev / +8% cost) | ₹276 L (−64% vs budget) |
| Lowest modelled Net P&L (−15% rev / +12% cost) | ₹114 L (still positive) |

Product B underperformance and Operations cost inflation together explain the large majority of the adverse variance. Services remains the only consistently outperforming revenue line.

---

## File Structure

```
Corporate_Variance_Model.xlsx
├── Raw_Export              → Original messy multi-source extract (unprocessed)
├── Raw_Export_Clean        → Intermediate cleaned panel
├── Raw_Export_Cleaned      → Final 192-row clean dataset (Month × Line Item)
├── Variance Engine         → Formula-driven abs/%/YTD variance + RAG status
├── Scenario Analysis       → Live stress inputs, named scenarios, 6×5 sensitivity table
└── Dashboard               → KPI tiles, charts, RAG summary, management actions
```

---

## Dataset Note

Synthetic dataset constructed to reflect mid-market Indian manufacturing P&L structure. Revenue and cost ratios benchmarked against publicly available Indian corporate annual reports. All assumption notes documented inline. Dataset is interview-defensible line by line. The raw extract deliberately retains the messiness typical of real multi-system extracts so the cleaning process itself is visible and reproducible.

---

*Part of Rahul Bhagat's Data Analytics Portfolio | [github.com/rahulbhagat29](https://github.com/rahulbhagat29)*

[https://1drv.ms/v/c/6839501f79224f0b/IQBp7SfwRVu2RIKnYGgKf9gKAdmFyzXmD92XlHbgT4vrkGA?e=MlMjlE]
