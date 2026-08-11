<div align="center">

# 📊 Finance Performance & Budget Variance Analytics
### A Power BI Case Study — Revenue, Expense & Budget-vs-Actual Reporting for a SaaS Business

*From a raw four-sheet Excel workbook to a two-page, conformed-dimension star schema, a fully documented DAX layer, and a wireframed-then-built Power BI report.*

[![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=flat&logo=powerbi&logoColor=black)](#)
[![DAX](https://img.shields.io/badge/DAX-217346?style=flat&logo=microsoftexcel&logoColor=white)](#)
[![Power Query](https://img.shields.io/badge/Power%20Query-M-informational?style=flat)](#)
[![Star Schema](https://img.shields.io/badge/Data%20Model-Star%20Schema-10263F?style=flat)](#)

</div>

---

## Table of Contents

1. [Overview](#overview)
2. [Business Problem](#business-problem)
3. [Tools & Skills Demonstrated](#tools--skills-demonstrated)
4. [The Dataset](#the-dataset)
5. [Data Modeling — Star Schema](#data-modeling--star-schema)
6. [DAX Layer](#dax-layer)
7. [Design Process — From Wireframe to Report](#design-process--from-wireframe-to-report)
8. [Dashboard 1 — Revenue & Expense Performance](#dashboard-1--revenue--expense-performance)
9. [Dashboard 2 — Budget vs Actual Analysis](#dashboard-2--budget-vs-actual-analysis)
10. [Notable Problem-Solving Moments](#notable-problem-solving-moments)
11. [Repository Structure](#repository-structure)
12. [How to Explore This Project](#how-to-explore-this-project)
13. [What This Project Demonstrates](#what-this-project-demonstrates)
14. [Contact](#contact)

---

## Overview

This project takes a small SaaS company's general ledger — a plain four-sheet Excel export — and turns it into a two-page Power BI report built on a proper **star schema with two fact tables and five conformed dimensions**. It's designed to answer two distinct questions a finance function actually asks every month:

- **"How is the business performing right now?"** — revenue, expense, and margin, at a glance.
- **"Are we on plan, and where exactly did we drift?"** — a full budget-vs-actual variance breakdown, down to the individual account.

Every stage of the work is documented here: the raw data, the modeling decisions (and the trade-offs behind them), every DAX measure used to power the report, the wireframing process that shaped the final layout, and the two finished dashboards themselves.

> 📄 **[Read the full step-by-step build guide →](./docs/finance-junior-analyst-guide.html)**
> The guide this README summarizes — every DAX formula, every chart's exact field configuration, and the reasoning behind each modeling decision, written to be followed by anyone picking up the project cold.

---

## Business Problem

A small SaaS business had its financial data in two disconnected places — a transaction log and a separate budget spreadsheet — with no way to see them together. Finance could answer "what did we spend?" or "what did we plan to spend?" individually, but not "how far off were we, and on what specifically?" without a manual reconciliation in Excel every month.

The goal was a self-service report that:
- Gives leadership a fast read on revenue, expense, and margin trends
- Gives FP&A a precise, account-by-account view of budget variance
- Updates automatically as new transactions and budget lines are added
- Doesn't require a spreadsheet-join workaround that risks silently double-counting numbers (see [Notable Problem-Solving Moments](#notable-problem-solving-moments))

---

## Tools & Skills Demonstrated

| Category | Tools / Techniques |
|---|---|
| **Data Modeling** | Star schema design, conformed dimensions across two fact tables, surrogate vs. natural keys |
| **Data Transformation** | Power Query (M) — deduplication, column splitting, data-quality triage |
| **Analytics Layer** | DAX — `CALCULATE`, `DATEADD`, `DATESINPERIOD`, `RANKX`, time intelligence, variance analysis |
| **Visualization** | Power BI (line, clustered column/bar, donut, scatter/bubble, waterfall, multi-measure Card) |
| **UX / Design** | Wireframing in PowerPoint, proportional layout systems, custom color theory, iconography |
| **Documentation** | End-to-end technical write-up aimed at a junior analyst audience |

---

## The Dataset

The source is a single Excel workbook (`Finance.xlsx`) with four sheets:

| Sheet | Rows | What It Holds |
|---|---|---|
| `TRANSACTION` | 1,389 | Every actual ledger transaction, Jan 2022 – Dec 2024 — invoices, bills, deposits, journal entries |
| `BUDGET` | 1,229 | Planned amounts by account, department, and month |
| `ACCOUNTS` | 35 | The chart of accounts, with a built-in two-level P&L hierarchy |
| `DICTIONARY` | — | Plain-English definitions of every column |

A few things surfaced during exploration that shaped the model:

- **`TRANSACTION` and `BUDGET` sit at different grains** — one row per transaction vs. one row per account/department/month. Reconciling them meaningfully requires two fact tables, not a flattened join (more on why below).
- **A real data-quality issue**: the vendor list contains both `"LinkedIn"` and `"LinkedIn Ads"` — almost certainly the same vendor, entered inconsistently. Flagged rather than silently merged, since consolidating vendor identities is a judgment call, not a default.
- **`ACCOUNTS` already ships with a hierarchy** (`LEVEL_01` → `LEVEL_02` → account), which became the backbone of the Budget-to-Actual waterfall chart.

---

## Data Modeling — Star Schema

Two fact tables, five dimension tables — three of which are **conformed**, meaning both fact tables relate to the exact same copy of that dimension. That's what makes a "Budget vs Actual" comparison possible without a manual join: filter by account or department once, and both the plan and the actuals update together.

<p align="center">
  <img src="./docs/assets/star_schema.png" alt="Star schema entity-relationship diagram" width="900">
</p>

**Why two fact tables?** `Fact_Transactions` (one row = one real transaction) and `Fact_Budget` (one row = one planned amount per account/department/month) describe two fundamentally different things — what happened vs. what was planned. Forcing them into one table would mean picking a grain that's wrong for one of the two questions. Keeping them separate, connected through shared dimensions, is what lets a single slicer selection filter both "actual" and "planned" numbers at once.

**Why a natural key on `Dim_Account`?** `COD_ACCOUNT` is already a stable, unique, business-meaningful code — there's no need to manufacture a surrogate key when the source already provides one. (Other tables, like `Dim_Vendor`, *do* need a manufactured key — the raw data has no natural identifier for a vendor.)

---

## DAX Layer

Every KPI on both dashboards is built from three layers of measures:

1. **Base measures** — the actual number (`Total Revenue`, `Total Budget`, `Budget Variance ($)`, …)
2. **Prior-period measures** — the same number one month earlier, via `DATEADD`
3. **Sparkline / delta measures** — trailing-window and percent-change wrappers that power the "▲ +4.2% vs prior period" indicators

A representative sample:

```dax
Total Revenue =
CALCULATE ( SUM ( Fact_Transactions[Amount] ), Dim_RevenueExpenses[REVENUE/EXPENSES] = "REVENUE" )

Budget Variance ($) = [Total Actual] - [Total Budget]

Budget Variance (%) =
DIVIDE ( [Budget Variance ($)], [Total Budget] )

Accounts Over Budget =
VAR AccountVariance =
    ADDCOLUMNS (
        VALUES ( Dim_Account[ACCOUNT_NAME] ),
        "AcctVariance", [Total Actual] - [Total Budget]
    )
RETURN
    COUNTROWS ( FILTER ( AccountVariance, [AcctVariance] > 0 ) )

MoM Revenue Growth % =
VAR CurrRev = [Total Revenue]
VAR PrevRev = CALCULATE ( [Total Revenue], DATEADD ( Dim_Date[Date], -1, MONTH ) )
RETURN
    DIVIDE ( CurrRev - PrevRev, PrevRev )
```

The full reference — all 10 KPIs × 3 formula layers, plus the Waterfall chart's field configuration and the `Dim_Date` calendar table — is documented in full in **[the build guide](./docs/finance-junior-analyst-guide.html)**.

> 💡 **A deliberate simplification worth noting**: the donut charts on both pages plot base measures (`[Total Revenue]`, `[Budget Variance ($)]`) directly against a category column — no separate "% of total" measure required. Power BI's donut visual computes each slice's proportion automatically at render time. The extra measure is only worth writing if that percentage needs to appear somewhere *else*, like a tooltip or a card.

---

## Design Process — From Wireframe to Report

The report wasn't built visual-by-visual from a blank canvas — it started as a wireframe, went through a full design pass, and only then became the real thing.

### 1. Chart space allocated by chart type, not a uniform grid

A line chart needs width to show a trend's shape. A donut needs almost none — it's a fixed, circular composition. Giving every chart the same size ignores what each one is actually for. The layout instead uses a **mirrored two-panel grid**: each panel holds two compact charts and one "hero" chart that gets the full width of its panel — reserved for whichever chart most needs the room (a trend line, a bubble scatter, a waterfall).

<p align="center">
  <img src="./docs/assets/dashboard-1-wireframe.jpg" alt="Dashboard 1 wireframe — Revenue & Expense Performance" width="900">
</p>

### 2. A custom color palette, not a default theme

**"Emerald Ledger"** — chosen to read as executive and money-literate rather than generic corporate blue:

<p align="center">
  <img src="./docs/assets/palette.png" alt="Emerald Ledger color palette" width="900">
</p>

| Color | Hex | Role |
|---|---|---|
| Deep Navy | `#10263F` | Primary — headers, structure, trust |
| Emerald Green | `#1E8E5A` | Secondary — chart series, favorable movement |
| Amber Gold | `#D9A441` | Accent — used sparingly, one highlight at a time |
| Brick Red | `#B85C4C` | Reserved exclusively for unfavorable variance / negative deltas |
| Parchment White | `#F6F5F1` | Page background — warmer than flat gray |

This exact palette was carried through into the finished report as a custom Power BI theme — it isn't just a mockup color scheme.

### 3. The wireframe became the report's actual background guide

Rather than discarding the wireframe once building started, a stripped-down version of it — same box layout and KPI icons, but every chart title and label removed — was set as a low-opacity page background *inside* the real Power BI file. Real visuals were then built directly on top of the ghost outlines, guaranteeing pixel-accurate alignment to the original design intent.

<p align="center">
  <img src="./docs/assets/dashboard-1-background-guide.png" alt="The actual low-opacity background guide used inside Power BI" width="900">
</p>

### 4. Every KPI card carries more than a number

Each card shows the metric, a **trend delta vs. the prior period** (a colored triangle plus a percentage), and an icon that reflects what the metric actually means — a dollar sign for revenue, a warning triangle for a risk count, a star for a headline "bottom line" metric.

---

## Dashboard 1 — Revenue & Expense Performance

**Audience & question:** Leadership / general management — *"How is the business performing right now?"*

<p align="center">
  <img src="./docs/assets/dashboard-1-wireframe.jpg" alt="Dashboard 1 layout" width="900">
</p>

| KPI | What It Answers |
|---|---|
| Total Revenue | All money earned in the period |
| Total Expenses | All money spent in the period |
| Net Income | Revenue minus Expenses — the bottom line |
| Gross Margin % | Revenue remaining after direct costs, as a ratio |
| MoM Revenue Growth % | Is revenue trending up, flat, or down vs. last month |

| Chart | Type | What It Shows |
|---|---|---|
| Revenue & Expense Trend by Month | Line | The shape of both lines over time — widening or narrowing gap |
| Monthly Revenue vs Expense | Scatter (Bubble) | One bubble per month — X = Revenue, Y = Expense, size = Net Income |
| Revenue by Account | Clustered Column | Which specific revenue line is driving the total |
| Revenue Mix | Donut | Recurring vs. non-recurring revenue, as a proportion |
| Expense Mix | Donut | Where spend concentrates by category |
| Expenses by Department | Clustered Column | Which department is spending the most |

---

## Dashboard 2 — Budget vs Actual Analysis

**Audience & question:** FP&A / budget owners — *"Are we on plan, and where exactly did we drift?"*

<p align="center">
  <img src="./docs/assets/dashboard-2-wireframe.jpg" alt="Dashboard 2 layout" width="900">
</p>

**Key vocabulary, explained plainly in the build guide:**
- **Budget** — what was planned (`Fact_Budget`)
- **Actual** — what really happened (`Fact_Transactions`, rolled up to the same grain)
- **Variance** — Actual minus Budget; the entire dashboard is this one subtraction, sliced different ways
- **Account-by-account variance** — the same subtraction calculated per individual account rather than as one lump number, because *"we're $8,000 over"* is not actionable, but *"Advertising is $12,000 over, Travel is $4,000 under"* is

**Reading the waterfall (Budget-to-Actual Bridge):** first bar = Total Budget, floating bars = each category's variance (green steps up = over budget, red steps down = under), final bar = Total Actual — a visual bridge from the plan to the outcome.

| KPI | What It Answers |
|---|---|
| Total Budget | The plan, stated plainly |
| Total Actual | What really happened |
| Budget Variance ($) | Actual minus Budget, in dollars |
| Budget Variance (%) | The same gap, scaled for comparability across accounts |
| Accounts Over Budget | A count — how *widespread* the problem is, which one aggregate number can hide |

| Chart | Type | What It Shows |
|---|---|---|
| Budget vs Actual Trend by Month | Line | Is the plan/actual gap growing, or was it a one-off month |
| Budget-to-Actual Bridge | Waterfall | The full variance walk from plan to outcome, by P&L category |
| Budget Variance (%) by Department | Donut | Which department makes up the biggest share of the variance pool |
| Budget Variance ($) by Account | Donut | The account-level equivalent — share of the total variance dollar amount |
| Variance by Account | Clustered Bar | The same breakdown, ranked by magnitude rather than share |
| Variance by Department | Clustered Bar | Department variance, ranked by magnitude |

> Two chart types cover the same two breakdowns (account and department) deliberately — the donut shows *share*, the bar shows *magnitude*. An account can dominate the "share" donut while still being a small dollar figure if every other account's variance is even smaller; the bar chart is what confirms whether that share is actually a big number.

---

## Notable Problem-Solving Moments

A few real decisions worth calling out — the kind of thing that comes up in an interview conversation about this project:

**🔍 The Budget-vs-Actual fan-out trap.** An early flat-file reconciliation attempt joined budget to actuals on *Account + Month* alone. Several accounts (like Salary & Wages) are budgeted separately *per department*, so that join key silently matched one budget row to four actual rows — quadrupling the reported variance. The fix: a composite key of *Account + Department + Month*. Inside the actual star schema, this risk disappears entirely — `Fact_Budget` and `Fact_Transactions` relate to `Dim_Account` and `Dim_Class` independently, so a DAX measure (`[Total Actual] − [Total Budget]`) lets filter context do the work correctly without any manual join at all — a concrete example of why the star schema exists in the first place, not just a modeling formality.

**🔍 A slicer built on the fact table, not the dimension.** The Department slicer filters through `Fact_Budget[CLASS]` directly rather than through `Dim_Class`. It still works — but it's a reminder that a slicer only needs to point at *some* connected column, not necessarily a dimension table, and that tracing exactly which table and column a slicer is built on is the first debugging step when a filter doesn't behave as expected.

**🔍 `MonthShort` without a year.** Every trend chart groups by `Dim_Date[MonthShort]` rather than a year-aware field. Documented explicitly: with three years of data, an unfiltered chart will silently sum all three Januarys into a single "Jan" bar. Worth knowing before trusting an unfiltered trend chart's shape at face value.

---

## Repository Structure

```
📦 finance-analytics-dashboard
├── README.md                                   ← you are here
├── data/
│   └── Finance.xlsx                             ← source workbook (TRANSACTION, BUDGET, ACCOUNTS, DICTIONARY)
├── report/
│   └── Finance.pbix                             ← the finished Power BI report
├── design/
│   ├── finance-dashboard-wireframes.pptx        ← full wireframe deck (1920×1080)
│   └── palette.png                              ← Emerald Ledger swatches
└── docs/
    ├── finance-junior-analyst-guide.html         ← the complete build guide (data model, every DAX formula, chart configs)
    └── assets/
        ├── star_schema.png
        ├── dashboard-1-wireframe.jpg
        ├── dashboard-2-wireframe.jpg
        ├── dashboard-1-background-guide.png
        └── dashboard-2-background-guide.png
```

---

## How to Explore This Project

1. **Start with this README** for the overview and the design reasoning.
2. **Open [`docs/finance-junior-analyst-guide.html`](./docs/finance-junior-analyst-guide.html)** for the complete technical walkthrough — every table, every DAX formula, every chart's exact field configuration, written step-by-step.
3. **Open `report/Finance.pbix`** in Power BI Desktop to interact with the live report.
4. **Browse `design/finance-dashboard-wireframes.pptx`** to see the layout planning that preceded the build.

---

## What This Project Demonstrates

- Designing a **multi-fact-table star schema** with conformed dimensions — not just a single flat fact table
- Writing **layered DAX** (base → time intelligence → sparkline) rather than one-off formulas per visual
- Recognizing when *not* to write an extra measure (the donut charts) as much as when to write one
- **Diagnosing and fixing a real data-fan-out bug** before it reached the report
- Treating **wireframing as an actual design phase**, including a custom color palette and a reusable proportional layout system — then carrying that design through, unmodified, into the finished build
- Writing documentation clear enough for someone else to pick up the project with no prior context

---

## Contact

**Frank Agba**


*Built as part of a self-directed learning series — [Learn Data Analytics with InsightByFrank](#).*

</div>
