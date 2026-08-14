# Procurement Performance & Risk Intelligence

## Power BI Portfolio Case Study

**Executive procurement analytics across spend, supplier performance, payment risk, sourcing behaviour, and operational efficiency.**

> A recruiter focused Power BI case study built to show not only dashboard design, but also business thinking, risk analysis, KPI engineering, interactive navigation, and executive storytelling.

---

## 1. Project at a Glance

This project transforms procurement data into a three view Power BI experience designed around a practical executive question:

**Where is procurement creating value, and where is it creating risk?**

The report is organised into three analytical perspectives:

1. **Executive Overview / Spend** — What are we spending, saving, and buying?
2. **Operational Efficiency & Supplier Performance** — How efficiently are purchase orders and suppliers performing?
3. **Risk Radar** — Which suppliers, payments, sourcing patterns, and invoices require attention?

The final report uses a 1920 × 1080 executive layout, a consistent Indigo Slate visual system, KPI context lines, dynamic navigation, and interactive analysis across procurement dimensions. The accompanying wireframe document explicitly defines a 1920 × 1080 canvas, three report pages, dynamic titles, KPI context lines, latitude/longitude mapping, and field parameter toggles. fileciteturn0file0L4-L6

---

## 2. Why This Project Matters to a Business

Procurement teams do not only need a total spend number. They need to understand:

- whether spend is within plan
- where supplier and payment risks are concentrated
- whether deliveries are arriving on time
- how much spend is off contract or classified as maverick spend
- how much purchasing is concentrated with a small number of suppliers
- where savings opportunities may exist

This dashboard brings those questions into one decision environment instead of forcing stakeholders to interpret disconnected reports.

---

## 3. Executive Outcomes

The report is designed to help a procurement leader quickly identify:

**Spend pressure**

- Total Spend
- Total Savings
- Spend per Purchase Order
- Preferred Supplier Spend
- Off Contract Spend

**Operational pressure**

- Average Lead Time
- Delayed Deliveries
- On Time Deliveries
- Maverick Spend
- On Time In Full delivery rate

**Risk exposure**

- Average ESG Score
- High Risk Supplier Spend
- Single Source Spend
- Overdue Payments
- Disputed Invoice Value

These KPI groups are intentionally arranged to move from financial performance to operational efficiency and then to procurement risk.

---

## 4. Dashboard Architecture

### Page 1 — Executive Overview of Spend & Procurement Health

**Business question:**

> How healthy is procurement from a spend and purchasing perspective?

The report presents executive KPIs including:

- Total Spend
- Total Savings
- Total Purchase Orders
- Active Suppliers
- Preferred Supplier Spend

The main analytical views include:

- Total Budget and Total Spend by Year Month
- Total Spend by Category
- Total Spend by Department
- Geographic Spend using supplier latitude and longitude

The finished report also supports year navigation across **2022, 2023, and 2024**, with an analytical navigation layer for **Risk Radar, Performance, and Spend**.

---

### Page 2 — Operational Efficiency & Supplier Performance

**Business question:**

> Are procurement operations and suppliers delivering efficiently?

Key KPIs include:

- Average Lead Time (Days)
- Delayed Deliveries
- On Time Deliveries
- Maverick Spend
- Off Contract Spend

The report then analyses:

- Maverick Spend by Department
- Maverick Spend by Category
- Total Spend by Supplier Region
- Total Purchase Orders by On Time Delivery

The page uses interactive analysis tabs such as **Avg Lead Time, Delayed Deliveries, Maverick Spend, Off Contract Spend**, together with **Supplier Region, Supplier Risk, Supplier Status, and Supplier Tier** selections.

This design helps users shift from a broad operational KPI into a more focused supplier performance view without requiring separate report pages for every question.

---

### Page 3 — Risk Radar

**Business question:**

> Which suppliers or procurement activities present the greatest risk or opportunity for action?

Key KPIs include:

- Average ESG Score
- High Risk Supplier Spend
- Single Source Spend
- Overdue Payments
- Disputed Invoice Value

The finished report includes risk focused analysis such as:

- Overdue Payments by Category
- Payment Risk Spend by Supplier Risk
- Overdue Payments by Invoice Status
- Supplier and purchase order level detail

The detail view is designed to support investigation rather than only high level reporting, exposing fields such as purchase order ID, supplier name, department, country, status, on time delivery, total spend, and total savings.

---

## 5. Example Executive Findings

The report is configured to surface findings such as:

- **Preferred Supplier Spend:** 87.52M, representing 26.72% of total spend in the displayed view.
- **Off Contract Spend:** 122.34M, representing 37.36% of spend.
- **Maverick Spend:** 40.46M, representing 12.36% of spend.
- **On Time Delivery:** 64.14% in the displayed performance view.
- **Average Lead Time:** 35.96 days, with a maximum of 90 days.
- **High Risk Supplier Spend:** 23.30M, representing 6.87% of spend.
- **Single Source Spend:** 51.67M, representing 15.25% of spend.
- **Overdue Payments:** 59.47M, representing 17.55% of the displayed payment exposure.

These values are examples from the report view shown in the provided dashboard screenshots; they are not intended as universal business benchmarks.

---

## 6. What a Recruiter Should Notice

This project demonstrates more than visual formatting.

### Business analysis

The dashboard translates procurement data into decisions around:

- spend concentration
- contract compliance
- supplier risk
- payment risk
- delivery performance
- sourcing concentration
- savings

### Power BI engineering

The report demonstrates:

- KPI card design with contextual secondary metrics
- interactive report navigation
- year selection
- field parameter style analysis switching
- dynamic titles
- conditional performance indicators
- custom visual usage
- geographic mapping
- detailed drill style investigation

The wireframe specification explicitly calls out **dynamic titles**, **KPI context lines**, **lat/long map labels**, and **field parameter toggles**, showing that these interactions were part of the original design system rather than added as an afterthought. fileciteturn0file0L4-L6

### UX and visual storytelling

The design uses a clearly defined enterprise palette named **Indigo Slate**. The specification assigns:

| Role | Color |
|---|---|
| Primary / headers | `#2E2960` Deep Indigo |
| Secondary / charts | `#8B7FD9` Soft Violet |
| Accent / active states | `#E0A458` Copper Amber |
| Risk / unfavorable | `#BD4F44` Brick Red |
| Favorable outcomes | `#3F9A63` Muted Green |
| Page background | `#F5F4FA` Lavender White |

The palette documentation states that Brick Red is reserved for high risk, overdue, and disputed conditions, while Muted Green is the counterpart for positive deltas, savings, and on time outcomes. fileciteturn0file0L8-L33

---

## 7. Design Process

The project followed a deliberate **wireframe → build → refinement** workflow.

### Step 1 — Define the business questions

The report was structured around executive procurement questions instead of starting with available chart types.

### Step 2 — Build the wireframe

The dashboard was planned on a **1920 × 1080** canvas with three report pages. The wireframes define the placement of KPI cards, chart containers, page hierarchy, and interactive controls. fileciteturn0file0L4-L6

### Step 3 — Establish the visual system

The Indigo Slate palette was defined before dashboard construction, including dedicated semantic colours for risk and favourable performance. fileciteturn0file0L8-L33

### Step 4 — Engineer the Power BI report

The wireframe structure was translated into working Power BI pages, including navigation, KPI calculations, charts, tables, geographic analysis, and contextual indicators.

### Step 5 — Validate against the business story

The final pages were organised so that a reader can move naturally from:

**What are we spending? → How are operations performing? → What is creating risk?**

---

## 8. Core Procurement Metrics

| Metric | Business Meaning |
|---|---|
| Total Spend | Overall procurement expenditure |
| Total Savings | Value captured through procurement activity |
| Purchase Orders | Volume of purchasing transactions |
| Active Suppliers | Current supplier base |
| Preferred Supplier Spend | Spend directed to preferred suppliers |
| Average Lead Time | Average number of days from order to delivery |
| Delayed Deliveries | Orders not delivered within the expected timeline |
| OTIF / On Time Delivery | Delivery reliability indicator |
| Maverick Spend | Spend outside expected procurement processes |
| Off Contract Spend | Spend outside contracted supplier or purchasing arrangements |
| ESG Score | Supplier sustainability / responsibility indicator |
| High Risk Supplier Spend | Exposure linked to suppliers classified as high risk |
| Single Source Spend | Spend dependent on a single sourcing relationship |
| Overdue Payments | Payment exposure that has passed the expected payment timing |
| Disputed Invoice Value | Financial value tied to invoice disputes |

---

## 9. Technical Stack

| Layer | Technology / Capability |
|---|---|
| BI Platform | Microsoft Power BI |
| Data Preparation | Power Query |
| Analytical Calculations | DAX |
| Data Modelling | Relational modelling / dimensional thinking |
| Visualisation | Native Power BI visuals + custom visuals |
| Mapping | Latitude / Longitude based geographic analysis |
| UX | PowerPoint wireframing + Power BI layout engineering |
| Documentation | Markdown / GitHub repository structure |

---

## 10. Custom Visual & Interaction Layer

The Power BI package includes custom visuals related to **Icon Map Pro** and **Icon Map Slicer**. This supports the report's map based analysis and interactive filtering experience.

The report definition also contains registered custom theme resources and embedded wireframe assets, indicating that the visual design specification was carried into the Power BI file itself rather than existing only as an external mockup.

---

## 11. Portfolio Story

This project is best presented as a **procurement intelligence solution**, not simply a dashboard.

The analytical story is:

> **Financial performance** tells us where spend is going.
>
> **Operational performance** tells us whether procurement is executing efficiently.
>
> **Risk intelligence** tells us where management should intervene.

That framing is useful in interviews because it connects Power BI functionality directly to business action.

---

## 12. Repository Structure

Suggested recruiter friendly package:

```text
repo_package/
│
├── Procurement.pbix
├── README.md
│
├── docs/
│   ├── procurement-case-study.md
│   ├── procurement-data-dictionary.md
│   ├── procurement-dax-reference.md
│   └── assets/
│       ├── dashboard-risk-radar.png
│       ├── dashboard-performance.png
│       ├── dashboard-spend.png
│       ├── wireframe-risk-radar.png
│       ├── wireframe-performance.png
│       └── wireframe-spend.png
│
└── screenshots/
    ├── executive-overview.png
    ├── operational-performance.png
    └── risk-radar.png
```

---

## 13. How to Explore the Project

### For recruiters and hiring managers

Start with the three dashboard screenshots, then skim the sections on **Business Questions**, **Core Metrics**, and **What a Recruiter Should Notice**.

### For Power BI reviewers

Open the `.pbix` file and inspect:

- report page navigation
- KPI calculations
- field parameter interactions
- geographic visuals
- conditional performance indicators
- supplier detail table
- risk segmentation
- report theme

### For interview discussions

The strongest areas to discuss are:

1. Why procurement should be analysed through spend, efficiency, and risk lenses.
2. How KPI context lines make executive cards more useful than isolated numbers.
3. How field parameter style interactions let users explore different measures without creating many duplicated visuals.
4. Why risk indicators need semantic colour rules rather than arbitrary chart colours.
5. How wireframing improved consistency between the intended user experience and the final Power BI build.

---

## 14. Limitations & Next Steps

Potential future improvements include:

- adding a formal supplier scorecard page
- introducing supplier concentration measures such as top 5 / top 10 spend share
- adding a dedicated savings waterfall
- adding procurement cycle time decomposition
- introducing scenario analysis for contract compliance improvements
- adding a supplier risk trend over time
- publishing the report through Power BI Service with controlled row level security where required

These are extension opportunities rather than claims about features already present in the current file.

---

## 15. Portfolio Value

This project demonstrates the ability to move through the full analytics workflow:

**Business question → data preparation → modelling → DAX → visual design → interactive analysis → executive storytelling**

That is the core reason this project belongs in a data analyst / BI analyst portfolio. It shows the ability to build a report that is visually polished while remaining focused on business decisions.

---

## 16. Author

**InsightByFrank**  
Data Analyst | Power BI | SQL | Excel | Data Analytics

GitHub: [InsightByFrank](https://github.com/InsightByFrank)

---

## Recruiter Summary

> **Procurement Performance & Risk Intelligence** is a Power BI case study that turns procurement data into an executive decision tool covering spend, savings, supplier performance, payment exposure, sourcing concentration, delivery efficiency, and procurement risk. The project demonstrates Power BI dashboard engineering, DAX driven KPI design, interactive analysis, geographic visualisation, custom visual usage, wireframe led UX, and business focused storytelling.
