# LexEuropa Legal Group — Case Performance Analytics

**A strategic, decision-ready Power BI report built for FP20 Analytics' ZoomCharts Challenge 39**

🏆 **Honorable Mention — ZoomCharts Challenge 39**

![Status](https://img.shields.io/badge/status-complete-0F9B8E) ![Tool](https://img.shields.io/badge/tool-Power%20BI-1B2A4A) ![Challenge](https://img.shields.io/badge/FP20%20Analytics-ZoomCharts%20Challenge%2039-6C5CE7)

---

## Table of Contents

- [Overview](#overview)
- [Recognition](#recognition)
- [The Brief](#the-brief)
- [Report Architecture](#report-architecture)
  - [Page 1 — The Profitability Compass](#page-1--the-profitability-compass)
  - [Page 2 — The Capacity Ledger](#page-2--the-capacity-ledger)
  - [Page 3 — The Client Portfolio](#page-3--the-client-portfolio)
- [Tooltip Pages](#tooltip-pages)
- [Design System](#design-system)
- [Data Model](#data-model)
- [DAX Measure Library](#dax-measure-library)
- [Calculated Columns](#calculated-columns)
- [Slicers & Interactivity](#slicers--interactivity)
- [Key Insights Surfaced](#key-insights-surfaced)
- [Tools & Tech Stack](#tools--tech-stack)
- [Lessons Learned](#lessons-learned)
- [Author](#author)

---

## Overview

This report was built for **LexEuropa Legal Group**, a fictional multi-office European legal practice, as an entry into **FP20 Analytics' ZoomCharts Challenge 39**. The brief called for more than a descriptive dashboard — it required a **narrative analytics product**: three pages, each answering one strategic question a partner or ops lead could act on immediately.

Judging criteria: **Intuitiveness, Interactivity, and Insightfulness** (15 points each, 45 total).

The guiding principle throughout the build: *don't just visualize the data — interpret it.* Every visual on every page had to answer, implicitly or explicitly: *"So what should a partner do differently after seeing this?"*

---

## Recognition

This report received an **Honorable Mention** in FP20 Analytics' ZoomCharts Challenge 39, recognized for the strength of its analytical storytelling and its use of dynamic, narrative DAX measures to drive plain-language insight callouts rather than static commentary.

---

## The Brief

| Requirement | Delivered |
|---|---|
| 3-page maximum, single distinct story per page | ✅ Profitability → Capacity → Client Value |
| Consistent design system (typography, spacing, semantic color) | ✅ See [Design System](#design-system) |
| ZoomCharts-style drill-down across dimensions | ✅ Practice Area → Case Type, Office → Lawyer/City, Industry → Company Size, Region → Country → Client |
| Dynamic (non-hardcoded) insight callouts | ✅ 3 page-level + 9 tooltip-page narrative measures |
| Presentation-ready, judged on Intuitiveness / Interactivity / Insightfulness | ✅ Honorable Mention |

---

## Report Architecture

### Page 1 — The Profitability Compass
**Strategic question:** *Is the firm's growth translating into more profit — or just more revenue?*

| Visual | Business Question | Type |
|---|---|---|
| Quarterly Revenue, Profit & Margin Trend | Is growth this year real profit growth, or volume growth? | Line chart, drill to Month |
| Revenue, Profit & Margin by Office Region | Which offices earn further investment vs. need a cost review? | Clustered column, drill to Office City |
| Revenue, Profit & Margin by Practice Area | Which practice areas deserve more senior talent? | Clustered column, drill to Case Type |

**KPI strip:** Total Revenue · Total Profit · Avg Profit Margin % · Total Outstanding · Total Active Cases

---

### Page 2 — The Capacity Ledger
**Strategic question:** *Are we overloading our best lawyers, and does risk/complexity actually erode profitability?*

| Visual | Business Question | Type |
|---|---|---|
| Revenue vs. Avg Utilization % by Lawyer (Legend: Seniority) | Are our highest-revenue lawyers also our most overstretched? | Scatter plot |
| Case Outcome Mix by Seniority | Does seniority actually win more cases? | 100% stacked column |
| Margin %, Win Rate % & Avg Days Open by Case Complexity | Does complexity earn its keep, or is it being absorbed unpaid? | Column + line combo, drill to Case Type |
| Lawyer Scorecard | Who are the firm's highest-leverage assets right now? | Table |

**KPI strip:** Avg Utilization % · Avg Workload Index · Avg Risk Score · % High Complexity Cases · Avg Days Open

---

### Page 3 — The Client Portfolio
**Strategic question:** *Which clients and outcomes are worth protecting, and what drives satisfaction?*

| Visual | Business Question | Type |
|---|---|---|
| Revenue by Industry (Legend: Strategic Client Flag) | Is the strategic-client push landing where we think it is? | Stacked column, drill to Company Size |
| Client Scorecard | Which clients are quietly most/least valuable beyond revenue? | Table |
| Avg Risk Score vs. Total Profit by Client Region | Is client risk exposure justified by the profit it returns? | Scatter plot, drill to Country → Client |

**KPI strip:** Avg Satisfaction Score · Strategic Client Revenue · Win Rate % · Revenue per Client · Top 10 Client Revenue Concentration %

---

## Tooltip Pages

Nine of the twelve visuals carry a dedicated tooltip page — reserved for visuals where a single hovered point (a quarter, an office, a lawyer, a client) hides context the base chart can't show. Each tooltip page is intentionally lightweight: **one small chart, 2 KPI cards, one dynamic insight sentence.**

| Base Visual | Tooltip Page Reveals |
|---|---|
| Quarterly Trend (P1) | Top practice area driving that quarter's growth |
| Region/Office (P1) | Weakest office inside the hovered region |
| Practice Area/Case Type (P1) | Strongest case type inside the hovered practice area |
| Revenue vs. Utilization scatter (P2) | Hovered lawyer's case outcome mix and win rate vs. department |
| Complexity chart (P2) | Widest margin gap by case type at that complexity level |
| Lawyer Scorecard row (P2) | 4-quarter utilization trend for that lawyer |
| Industry/Strategic Flag (P1) | Strategic vs. non-strategic satisfaction gap in that industry |
| Client Scorecard row (P3) | Client's YoY revenue and satisfaction trajectory |
| Risk vs. Profit scatter (P3) | Client's complexity mix vs. regional average |

*Not built:* the 100% stacked Case Outcome by Seniority visual (P2) — native segment hover already surfaces proportions; a tooltip page would add no new information.

---

## Design System

**Color palette (semantic, not decorative)**

| Role | Color | Hex |
|---|---|---|
| Primary / Revenue | Deep Navy | `#1B2A4A` |
| Profit / Positive | Teal | `#0F9B8E` |
| Risk / Alert / Negative | Amber-Red | `#D64550` |
| Neutral / Structure | Cool Gray | `#8A93A6` |
| Neutral / Background | Off-white | `#F5F7FA` |
| Accent / Strategic Highlight | Violet | `#6C5CE7` (used sparingly — strategic clients, top performers) |

**Typography**

| Role | Typeface |
|---|---|
| Headlines / KPI values | Space Grotesk |
| Body / labels / tooltips | IBM Plex Sans |
| Numeric / DAX-style callouts | IBM Plex Mono |

**Layout rules**
- Fixed 1920×1080 canvas per page, ~40px safe margins
- KPI strip fixed at top (~120px)
- Hero visual center-left, secondary visuals right rail
- Insight callout floating at bottom of each page
- Consistent slicer panel placement (top-right) across all 3 pages for navigation muscle memory
- Drill-down affordance (chevron icon) shown on every hierarchical visual

---

## Data Model

Star schema with the following core tables:

- **Fact_Cases** — case-grain fact table: Revenue, Profit, Outstanding Balance, Profit Margin %, Lawyer Utilization %, Workload Index, Risk Score, Days Open, Client Satisfaction Score
- **Dim_Date** — standard date dimension (Year, Quarter, Month)
- **Dim_Case** — Practice Area, Case Type, Case Complexity, Case Outcome, Case Status
- **Dim_Lawyer** — Lawyer Name, Department, Seniority, Employment Status, Years of Experience
- **Dim_Office** — Office City, Region, Lat/Long
- **Dim_Client** — Client Name, Industry, Company Size, Client Region, Client Country, Strategic Client Flag, Client Since Year

---

## DAX Measure Library

### Page 1 — Profitability

```dax
Total Revenue = SUM(Fact_Cases[Revenue (EUR)])

Total Profit = SUM(Fact_Cases[Profit (EUR)])

Avg Profit Margin % = DIVIDE([Total Profit], [Total Revenue])

Total Outstanding = SUM(Fact_Cases[Outstanding Balance (EUR)])

Revenue PY = CALCULATE([Total Revenue], SAMEPERIODLASTYEAR(Dim_Date[Date]))

Revenue YoY % = DIVIDE([Total Revenue] - [Revenue PY], [Revenue PY])
```

### Page 2 — Workload & Risk

```dax
Avg Utilization % = AVERAGE(Fact_Cases[Lawyer Utilization %])

Avg Workload Index = AVERAGE(Fact_Cases[Workload Index])

Avg Risk Score = AVERAGE(Fact_Cases[Risk Score])

% High Complexity Cases =
DIVIDE(
    CALCULATE(COUNTROWS(Fact_Cases), Dim_Case[Case Complexity] IN {"High","Critical"}),
    COUNTROWS(Fact_Cases)
)

Win Rate % =
DIVIDE(
    CALCULATE(COUNTROWS(Fact_Cases), Dim_Case[Case Outcome] = "Won"),
    CALCULATE(COUNTROWS(Fact_Cases), Dim_Case[Case Outcome] IN {"Won","Lost","Settled"})
)

Overloaded Lawyer Count =
VAR _lawyerUtilTable =
    ADDCOLUMNS(
        VALUES(Dim_Lawyer[Lawyer ID]),
        "@AvgUtil", CALCULATE(AVERAGE(Fact_Cases[Lawyer Utilization %]))
    )
RETURN
    COUNTROWS(FILTER(_lawyerUtilTable, [@AvgUtil] > 100))
```

### Page 3 — Client Value

```dax
Avg Satisfaction = AVERAGE(Fact_Cases[Client Satisfaction Score])

Strategic Client Revenue = CALCULATE([Total Revenue], Dim_Client[Strategic Client Flag] = "Yes")

Strategic Revenue Share % = DIVIDE([Strategic Client Revenue], [Total Revenue])

Revenue per Client = DIVIDE([Total Revenue], DISTINCTCOUNT(Fact_Cases[Client ID]))

% Promoter Clients =
DIVIDE(
    CALCULATE(DISTINCTCOUNT(Fact_Cases[Client ID]), Dim_Client[Satisfaction Tier] = "Promoter"),
    DISTINCTCOUNT(Fact_Cases[Client ID])
)

Top 10 Client Revenue Concentration % =
VAR _top10Revenue =
    CALCULATE([Total Revenue], TOPN(10, VALUES(Dim_Client[Client Name]), [Total Revenue], DESC))
RETURN
    DIVIDE(_top10Revenue, [Total Revenue])
```

### Dynamic Narrative Measures (page-level insight callouts)

```dax
Profit Concentration Insight =
VAR _top2PracticeAreas = TOPN(2, VALUES(Dim_Case[Practice Area]), [Total Profit], DESC)
VAR _top2Names = CONCATENATEX(_top2PracticeAreas, Dim_Case[Practice Area], " and ")
VAR _top2ProfitShare =
    DIVIDE(CALCULATE([Total Profit], _top2PracticeAreas), [Total Profit])
VAR _top2VolumeShare =
    DIVIDE(CALCULATE(COUNTROWS(Fact_Cases), _top2PracticeAreas), COUNTROWS(Fact_Cases))
RETURN
    _top2Names & " drive " & FORMAT(_top2ProfitShare, "0%") &
    " of total profit despite representing only " & FORMAT(_top2VolumeShare, "0%") &
    " of case volume — a case for reallocating senior associates toward these two areas."

Risk Margin Erosion Insight =
VAR _criticalMargin = CALCULATE([Avg Profit Margin %], Fact_Cases[Risk Band] = "Critical")
VAR _lowMargin = CALCULATE([Avg Profit Margin %], Fact_Cases[Risk Band] = "Low")
VAR _marginErosionPts = (_lowMargin - _criticalMargin) * 100
RETURN
    "Critical-risk cases erode profit margin by an average of " &
    FORMAT(_marginErosionPts, "0") & " points versus low-risk cases."

Strategic Retention Insight =
VAR _strategicShare = [Strategic Revenue Share %]
VAR _strategicSat = CALCULATE([Avg Satisfaction], Dim_Client[Strategic Client Flag] = "Yes")
VAR _nonStrategicSat = CALCULATE([Avg Satisfaction], Dim_Client[Strategic Client Flag] = "No")
VAR _satGap = _nonStrategicSat - _strategicSat
RETURN
    "Strategic clients generate " & FORMAT(_strategicShare, "0%") &
    " of total revenue, but trail non-strategic clients by " &
    FORMAT(_satGap, "0.0") & " points on satisfaction."
```

> Full library of all 9 tooltip-page narrative measures is maintained in the PBIX model documentation and available on request.

---

## Calculated Columns

| Column | Table | Logic |
|---|---|---|
| `Revenue Tier` | Fact_Cases | Bins Revenue into Low / Mid / High / Strategic bands |
| `Is Profitable Case` | Fact_Cases | Yes/No flag where Profit > 0 |
| `Risk Band` | Fact_Cases | Low (1–30) / Medium (31–60) / High (61–85) / Critical (86–100) from Risk Score |
| `Utilization Flag` | Fact_Cases | Over-capacity (>100%) / Optimal (70–100%) / Under-utilized (<70%) |
| `Client Tenure (Years)` | Dim_Client | Current year minus Client Since Year |
| `Satisfaction Tier` | Dim_Client | Detractor (1–5) / Passive (6–7) / Promoter (8–10) |

---

## Slicers & Interactivity

| Page | Slicers |
|---|---|
| Page 1 | Case Status · Case Outcome · Fee Arrangement Type |
| Page 2 | Department · Risk Band · Employment Status |
| Page 3 | Case Outcome · Satisfaction Tier · Client Tenure band · Practice Area |

Slicers are deliberately chosen to avoid duplicating any dimension already exposed via a visual's axis, legend, or drill path on the same page — every slicer adds a genuinely new filtering angle.

**Cross-filtering:** enabled on all category visuals — selecting a bar, bubble, or table row filters the rest of the page.
**Drill-down:** Practice Area → Case Type, Office Region → Office City, Industry → Company Size, Client Region → Country → Client Name.

---

## Key Insights Surfaced

- Two practice areas were found to drive a disproportionate share of total profit relative to case volume — a direct staffing reallocation signal.
- Critical-risk cases were shown to erode profit margin materially versus low-risk cases, without a corresponding fee adjustment — a pricing gap, not just a risk-management gap.
- Strategic-flagged clients carry the largest share of revenue but underperform on satisfaction relative to non-strategic clients — a retention risk hiding inside the firm's best accounts.

---

## Tools & Tech Stack

- **Power BI Desktop** — data modeling, DAX, report build
- **DAX** — measures, calculated columns, dynamic narrative text
- **ZoomCharts custom visuals** — drill-down scatter, timeline, and hierarchy visuals
- **Figma** — design system and layout planning
- **Star schema modeling** — Fact_Cases + 5 dimension tables

---

## Lessons Learned

The clearest takeaway from this build: **a chart that describes what happened is not the same as one that tells you what to do next.** Getting a report to that second bar — every page tied to one decision, every insight dynamically computed rather than hardcoded — was the actual work behind this Honorable Mention, more than any single visual choice.

A close second: data integrity has to be verified *before* a narrative measure is trusted to describe it. Several early insight callouts in this build were re-derived after tracing measures that were technically correct in isolation but wrong in context (row-level averages standing in for aggregate ratios, mismatched filter grains between a KPI card and its supporting chart). No insight is more trustworthy than the measure generating it.

---

## Author

**Emmy Adeyemi** — Senior Data Analyst & Power BI Developer
📺 YouTube: [youtube.com/@Emmy-The-Analyst](https://youtube.com/@Emmy-The-Analyst)
🌐 Portfolio: [emmy-portfolio.vercel.app](https://emmy-portfolio.vercel.app)
💼 Manifest Data — data literacy training & consultancy for African organizations

---

*Built for FP20 Analytics' ZoomCharts Challenge 39 — Honorable Mention.*
