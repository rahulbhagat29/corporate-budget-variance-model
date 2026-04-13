# Corporate Budget Variance Analysis and Stress Test Model

**Tool:** Microsoft Excel (Advanced) | **Domain:** Finance | **Type:** Financial Modelling

---

## Business Question

Which cost centres and revenue lines are driving the largest budget deviations, what is the financial impact under stress, and what corrective action should management take?

---

## Decision

Product B requires an immediate product review — FY24 actuals ran 13% below budget on average, worsening each quarter. Operations cost inflation (+7% avg FY24) is accelerating and requires a procurement audit before FY25 budgeting. Services is the one segment consistently outperforming budget and warrants increased allocation.

Under severe stress (−12% revenue, +8% cost overrun), Net P&L drops from ₹765L to ₹316L — a 58.7% erosion. The business retains profitability but has no margin for simultaneous revenue and cost shocks beyond −15% and +9% respectively.

---

## Problem

The business had no structured framework to isolate which line items were driving budget deviation, quantify cumulative impact over 24 months, or model the P&L impact of demand and cost shocks before they materialised. Management decisions on budget reallocation were being made without a scenario-tested view of downside risk.

---

## What I Did

**Dataset:** Constructed a 192-row synthetic dataset modelled on mid-market Indian manufacturing benchmarks (FY2023–FY2024). Eight line items across five departments and three revenue lines. Monthly budget and actual figures with documented assumption notes for every input. No hardcoded calculations — all values traceable to named assumptions.

**Variance Engine:** Built a formula-driven variance engine with absolute variance, percentage variance, YTD cumulative variance, and RAG status (Green / Amber / Red) across all 192 rows. RAG logic differentiates correctly between revenue lines (adverse = below budget) and cost lines (adverse = above budget).

**Scenario and Sensitivity Analysis:** Two-input scenario model with live yellow input cells for Revenue Stress % and Cost Overrun %. All downstream stressed P&L figures update dynamically. Three named scenarios — Base, Moderate Stress (−5% rev, +3% cost), Severe Stress (−12% rev, +8% cost) — compared side by side. A 6×5 sensitivity table covering 30 combinations maps every revenue-cost stress intersection to a Net P&L outcome and flags loss territory in red.

**Executive Dashboard:** Four KPI tiles, a clustered bar chart (budget vs actual by line item), a monthly revenue trend line chart (FY24), a RAG summary with management action signals, and a key finding statement translating the analysis into CFO-level decisions.

**Excel skills demonstrated:** SUMPRODUCT with multi-condition arrays, cross-sheet formula linking, dynamic scenario inputs with downstream propagation, conditional RAG logic, financial chart construction, colour-coded financial modelling conventions (blue inputs, black formulas, green cross-sheet links).

---

## Key Findings

| Metric | Value |
|---|---|
| FY24 Budgeted Net P&L | ₹765 L |
| FY24 Actual Net P&L | ~₹667 L |
| Product B FY24 Variance | −13% avg (worsening each quarter) |
| Operations FY24 Cost Overrun | +7% avg (accelerating in FY24) |
| Moderate Stress Net P&L | ₹541 L (−33.5% vs budget) |
| Severe Stress Net P&L | ₹316 L (−58.7% vs budget) |
| Loss threshold | Revenue −15% AND Cost overrun +9% simultaneously |

---

## File Structure

```
Corporate_Variance_Model.xlsx
├── Data                  → 192-row budget vs actual input table (FY23–FY24)
├── Variance Engine       → Variance calculations, RAG status, YTD cumulative
├── Scenario Analysis     → Scenario inputs, stressed P&L, sensitivity table
└── Dashboard             → KPI tiles, charts, RAG summary, management actions
```

---

## Dataset Note

Synthetic dataset constructed to reflect mid-market Indian manufacturing P&L structure. Revenue and cost ratios benchmarked against publicly available Indian corporate annual reports. All assumption notes documented inline. Dataset is interview-defensible line by line.

---

*Part of Rahul Bhagat's Data Analytics Portfolio | [github.com/rahulbhagat29](https://github.com/rahulbhagat29)*

*Dashobard Link:[https://cap.so/s/4pg4sqgnb12yk18]*
