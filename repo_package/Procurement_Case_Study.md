# Procurement Performance & Risk Intelligence

## Executive Case Study

### 1. Business Context

Procurement performance is not defined by spend alone. Leadership needs to understand how much the organisation is spending, whether suppliers and purchase orders are performing as expected, where procurement leakage is occurring, and which exposures require action.

This Power BI solution was designed as an executive procurement intelligence report with three connected perspectives:

- **Spend & Procurement Health**
- **Operational Efficiency & Supplier Performance**
- **Supplier & Procurement Risk**

The source wireframe defines a 1920 × 1080 canvas, three report pages, KPI context lines, dynamic titles, latitude/longitude map labels, and field parameter toggles. fileciteturn0file0L4-L6

### 2. Business Questions

The report is built to answer five practical questions:

1. **How much are we spending and saving?**
2. **Where is spend concentrated by category, department and region?**
3. **Are suppliers delivering on time and within expected lead times?**
4. **How much spend is occurring outside preferred or contracted procurement channels?**
5. **Which supplier, payment and sourcing risks should management investigate first?**

### 3. Analytical Framework

The dashboard moves from outcome to diagnosis:

**Financial view** → spend, savings and purchasing volume

**Operational view** → lead time, delayed delivery, OTIF, maverick and off-contract spend

**Risk view** → ESG exposure, high risk supplier spend, single-source dependence, overdue payments and disputed invoices

This gives the report a clear decision path rather than a collection of unrelated charts.

### 4. Dashboard 1 — Executive Overview / Spend

**Decision objective:** establish the overall financial health of procurement.

Primary KPIs in the displayed 2024 view include:

| KPI | Displayed value |
|---|---:|
| Total Spend | 327.49M |
| Total Savings | 37.21M |
| Total Purchase Orders | 2K |
| Active Suppliers | 15 |
| Preferred Supplier Spend | 87.52M |

Supporting context lines show budget comparison, savings rate, spend per purchase order, preferred suppliers and preferred supplier spend percentage.

The visual layer includes:

- Total Budget vs Total Spend by Year Month
- Total Spend by Category
- Total Spend by Department
- Geographic supplier / spend mapping

### 5. Dashboard 2 — Operational Efficiency & Supplier Performance

**Decision objective:** understand whether procurement execution is efficient.

Displayed 2024 KPIs include:

| KPI | Displayed value |
|---|---:|
| Average Lead Time | 35.96 days |
| Delayed Deliveries | 616 |
| On Time Deliveries | 1K |
| Maverick Spend | 40.46M |
| Off-Contract Spend | 122.34M |

The supporting context lines show a maximum lead time of 90 days, delayed delivery rate of 35.86%, OTIF of 64.14%, maverick spend rate of 12.36%, and off-contract spend rate of 37.36% in the displayed view.

The analytical page then breaks performance down by department, category, supplier region and on-time delivery outcome.

### 6. Dashboard 3 — Risk Radar

**Decision objective:** identify procurement exposures that require investigation or intervention.

Displayed KPIs include:

| KPI | Displayed value |
|---|---:|
| Average ESG Score | 60.31 |
| High Risk Supplier Spend | 23.30M |
| Single Source Spend | 51.67M |
| Overdue Payments | 59.47M |
| Disputed Invoice Value | 51.94M |

Supporting context lines include maximum ESG score, high-risk spend percentage, single-source spend percentage, overdue payment percentage, and overdue invoice value.

The report then moves from aggregate risk into investigative analysis such as:

- Overdue Payments by Category
- Payment Risk Spend by Supplier Risk
- Overdue Payments by Invoice Status
- Purchase order and supplier level detail

### 7. Design System

The wireframe defines the **Indigo Slate** palette for enterprise procurement reporting. The visual specification assigns:

| Colour | Hex | Purpose |
|---|---|---|
| Deep Indigo | `#2E2960` | Headers and primary structure |
| Soft Violet | `#8B7FD9` | Standard chart series and icon badges |
| Copper Amber | `#E0A458` | Active states and selective highlights |
| Brick Red | `#BD4F44` | Risk / unfavourable conditions |
| Muted Green | `#3F9A63` | Favourable outcomes |
| Lavender White | `#F5F4FA` | Page background |

The design notes explicitly reserve Brick Red for high-risk suppliers, overdue and disputed conditions, while Muted Green is used for positive deltas, savings and on-time outcomes. fileciteturn0file0L8-L33

### 8. Power BI Techniques Demonstrated

The current `.pbix` package demonstrates a broad Power BI skill set:

- DAX KPI calculations
- context-aware KPI cards
- percentage and ratio calculations
- conditional status indicators
- year navigation
- interactive page navigation
- field parameter style metric switching
- dynamic chart titles
- geographic mapping using supplier latitude and longitude
- custom visual integration
- executive table design
- visual hierarchy and spacing
- wireframe led dashboard construction

### 9. Why the Wireframe Matters

The design was not created directly on a blank Power BI canvas. The original wireframe document defines the report structure first, including page dimensions, three dashboard pages, navigation logic, KPI context lines and analysis toggles. fileciteturn0file0L4-L6

That process improves consistency because the business story and visual hierarchy are established before individual charts are built.

### 10. Example Business Interpretation

The displayed 2024 view indicates that a meaningful portion of procurement spend sits outside preferred or contracted channels. Off-contract spend is shown at 122.34M, while preferred supplier spend is 87.52M. At the same time, operational performance shows 64.14% on-time delivery and 35.96 days average lead time.

The risk page adds another layer: 23.30M of high-risk supplier spend, 51.67M of single-source spend, and 59.47M of overdue payments. Together, these measures allow a management discussion that goes beyond "total spend" into procurement control, supplier resilience, service performance and working capital risk.

These interpretations are based on the displayed dashboard state and should be treated as portfolio examples, not universal procurement benchmarks.

### 11. Interview Talking Points

A strong project walkthrough can be structured as:

**Problem** — Procurement information is fragmented across spend, suppliers, operations and risk.

**Approach** — Build an executive Power BI model that groups decisions into spend, performance and risk.

**Engineering** — Use DAX, interactive navigation, contextual KPIs, parameter driven analysis and custom visuals.

**Design** — Start from a 1920 × 1080 wireframe and use a semantic palette so risk and favourable outcomes are immediately recognisable.

**Outcome** — Give leadership one report that helps answer what is happening, where it is happening, and where action is needed.

### 12. Future Enhancements

Potential next iterations could include:

- supplier concentration measures such as top 5 / top 10 spend share
- supplier scorecards
- savings opportunity waterfalls
- supplier risk trends over time
- contract compliance improvement scenarios
- procurement cycle time decomposition
- Power BI Service deployment with governed access and row-level security where required

These are proposed extensions rather than features claimed to already exist in the current file.
