# 📊 Global Superstore Profitability Recovery Dashboard — Power BI

> **Business Context:** A retail CFO reported that despite consistent revenue growth,
> profit margins were under pressure. As the Data Analyst, I was tasked with identifying
> root causes of margin erosion, quantifying recoverable profit, and building a
> 5-page interactive decision-support dashboard for executive leadership.

---

## 📸 Dashboard Preview

### Page 1 — Executive Overview
<img width="1186" height="642" alt="image" src="https://github.com/user-attachments/assets/7d308542-1fe0-4ac7-a54b-d42c81288979" />


### Page 2 — Product Profitability Deep-Dive
<img width="1195" height="669" alt="image" src="https://github.com/user-attachments/assets/dda88c1c-730f-4640-b38c-8526bb479a64" />


### Page 3 — Discount Impact Analysis
<img width="1191" height="660" alt="image" src="https://github.com/user-attachments/assets/6e7bfb32-61b8-46ae-a558-bb39c92b5335" />


### Page 4 — Shipping & Operations
<img width="1192" height="665" alt="image" src="https://github.com/user-attachments/assets/16a3b74a-cfcd-4e98-a97c-cfa7ae4251a9" />


### Page 5 — Forecast & What-If Scenarios


### Data Model — Star Schema
<img width="992" height="652" alt="image" src="https://github.com/user-attachments/assets/232ac042-e2c9-4aed-ad23-5e3ea39dda41" />


---

## 🎯 The Business Problem

The CFO of SuperStore Global presented the following problem:

> *"Our revenue is growing year over year — but our profit margins
> are not keeping pace. Something is eroding our profitability and
> I need data-driven answers, not gut feelings."*

This dashboard was built to answer 6 critical business questions:

1. How is overall business performance trending vs last year?
2. Which product sub-categories generate high revenue but destroy margin?
3. Is our discount strategy helping revenue or killing profitability?
4. Which customer segment is most profitable — not just highest revenue?
5. Are our shipping operations efficient and what drives returns?
6. What does the next 6 months look like and what levers can we pull?

---

## 💡 Key Findings

> **Note:** All findings below are derived directly from the
> Global Superstore dataset as visualized in this dashboard.
> Update these numbers with your filtered/full dataset values
> after verifying each visual.

### Finding 1 — Discount Strategy Is Eroding Profit ⚠️
- The **Discount Impact Analysis** page (Page 3) shows a clear
  inverse relationship between discount depth and profit margin
- The combo chart "Impact of Discounts on Revenue and Profitability"
  visually proves: as discount bands increase, revenue rises but
  profit collapses
- The **what-if simulation** (Simulated Profit measure) allows
  leadership to drag a slider and see live profit recovery scenarios
- **Key business recommendation:** Cap discounts at 20% threshold

### Finding 2 — Product Profitability Is Uneven Across Sub-Categories 🪑
- The scatter chart "Revenue vs Profit: Product-Level Analysis"
  reveals which sub-categories fall in the danger quadrant
  (high revenue, low/negative profit)
- The "Profit Margin by Sub-Category" bar chart with conditional
  formatting immediately highlights underperforming products in red
- The matrix heatmap shows Category × Region combinations
  where margin is critically low

### Finding 3 — Segment Profitability Tells a Different Story 💼
- The "Segment-wise Profitability" visual on Page 1 shows
  revenue AND profit margin side by side per segment
- Consumer segment drives majority of revenue volume
- Corporate segment shows stronger profit margin per order
- **Recommendation:** Shift acquisition focus toward Corporate
  segment for margin improvement

### Finding 4 — Shipping Mode Directly Impacts Return Risk 🚚
- Page 4 "Shipping Speed vs Return Risk by Mode" combo chart
  shows the relationship between shipping speed and return rate
- The Gauge visual "Average Shipping Time" shows performance
  against the 3-day SLA target
- "Shipping Performance by Category & Mode" table with
  conditional formatting identifies highest-risk combinations

### Finding 5 — Revenue Is Growing But Profit Needs Attention 📈
- Page 1 KPI cards show YoY Revenue % and YoY Profit % with
  directional arrows — the gap between these two metrics is
  the core business story
- The Forecast page (Page 5) shows 6-month revenue projection
  with confidence interval
- Decomposition Tree on Page 5 enables self-serve root cause
  analysis of profit drivers

---

## 📊 Dashboard Pages — Full Breakdown

### Page 1: Executive Overview
**Business question:** Is the business healthy? What needs attention?

| Visual | Type | Purpose |
|--------|------|---------|
| Total Revenue | KPI Card | Revenue with YoY % change |
| Total Profit | KPI Card | Profit with YoY % change |
| Return Rate % | KPI Card | Return rate with YoY direction |
| Profit Margin KPI | KPI Card | Overall margin % |
| Total Orders | KPI Card | Order volume |
| Revenue Trend vs Last Year | Line Chart | Current vs prior year monthly trend |
| Revenue by Region | Column Chart | Regional revenue comparison |
| Segment-wise Profitability | Column Chart | Revenue + margin by segment |
| Executive Insights | Dynamic Text Card | Auto-updating narrative insight |
| Map Visual | Bubble Map | Geographic revenue distribution |
| Slicers | Dropdown | Segment, Year, Region Group |

---

### Page 2: Product Profitability Deep-Dive
**Business question:** Which products make money and which destroy it?

| Visual | Type | Purpose |
|--------|------|---------|
| Revenue vs Profit: Product-Level Analysis | Scatter Chart | Quadrant analysis — stars vs problem products |
| Profit Margin by Sub-Category | Bar Chart | Ranked with red/green conditional formatting |
| Category-wise Revenue by Segment | Bar Chart | Who buys each category |
| Top 5 Sub-Categories by Sales Volume | Funnel Chart | Volume-ranked product leaders |
| Insight Text Boxes | Text | Business interpretation of findings |

---

### Page 3: Discount Impact Analysis
**Business question:** Is discounting helping or hurting profitability?

| Visual | Type | Purpose |
|--------|------|---------|
| Impact of Discounts on Revenue and Profitability | Line + Column Combo | The headline insight visual |
| Discount vs Profitability by Sub-Category | Scatter + Trend Line | Statistical proof of discount-margin correlation |
| Simulated Profit | KPI Card | Live what-if scenario output |
| Profit Recovery | KPI Card | Recoverable profit from discount reduction |
| Discount Reduction Slicer | What-If Parameter | Interactive profit simulation slider |
| Dynamic Insight | Text Card | Auto-generated strategy recommendation |

---

### Page 4: Shipping & Operations
**Business question:** Are operations efficient and what drives returns?

| Visual | Type | Purpose |
|--------|------|---------|
| Shipping Speed vs Return Risk by Mode | Line + Column Combo | Speed vs return rate per shipping mode |
| Average Shipping Time | Gauge | Avg days vs 3-day SLA target |
| Shipping & Return Trends Over Time | Line Chart | Seasonal pattern detection |
| Shipping Performance by Category & Mode | Table | Full detail with conditional formatting |
| Average Shipping Cost by Product Category | Column Chart | Cost breakdown by category |

---

### Page 5: Forecast & What-If Scenarios
**Business question:** What happens next and what levers can we pull?

| Visual | Type | Purpose |
|--------|------|---------|
| Revenue Trend with 6-Month Forecast | Line + Forecast | Forward-looking revenue projection |
| Monthly Revenue Trend by Year | Line Chart | Multi-year seasonality comparison |
| Profit Drivers & Root Cause Analysis | Decomposition Tree | AI-powered drill-down into profit variance |
| Impact of Discount Strategy on Profitability | Column Chart | Scenario comparison visual |
| Forecast Dynamic Insight | Dynamic Text Card | Auto-narrative forecast summary |

---

## 🗄️ Data Model — Star Schema

```<img width="995" height="655" alt="image" src="https://github.com/user-attachments/assets/f572fc3a-30b8-4c68-b4a9-10e4ed6928b9" />


Supporting: Discount Reduction (What-If Parameter Table)
```

**Model decisions:**
- Single-directional filters on all relationships to prevent ambiguity
- Date_Table marked as official Date Table for time intelligence
- Dedicated MeasuresTable keeps all 27 measures organized
- Discount Band as calculated column for row-level classification

---

## 🧮 DAX Measures — Complete Reference

> See **[dax-measures.md](dax-measures.md)** for the full
> documented DAX code for all 27 measures with explanations.

### Measures built in this project:

| Category | Measures |
|----------|---------|
| Core Aggregations | Total Revenue, Total Profit, Total Orders, Total Quantity, Avg Discount |
| Ratios & KPIs | Profit Margin %, Return Rate %, Avg Days to Ship |
| Time Intelligence | Revenue LY, YoY Revenue %, Avg days to return LY |
| Scenario Modeling | Simulated Profit, Profit Recovery |
| Dynamic Text | Forecast Dynamic Insight, Final Insight, Shipping Insight, Product Insight, Dynamic Insight of Discount Strategy |
| Display & UX | Profit display, revenue display, Return display, Profit Color, Revenue Color, Profit Margin Color, Return YoY Color, Profit Margin KPI |
| Navigation | Dynamic Title Forecast, Dynamic Title Shipping & Operation |

---

## 🔧 How to Open This Project

**Step 1:** Download and install Power BI Desktop (free)
```
https://powerbi.microsoft.com/desktop
```

**Step 2:** Clone this repository
```bash
git clone https://github.com/AnanyaSharma2/Power-BI.git
```

**Step 3:** Open `salesstore.pbix` in Power BI Desktop

**Step 4:** If data source error appears:
```
Home → Transform Data → Data Source Settings →
Change Source → point to /data folder in this repo
```

**Step 5:** Click Refresh on the Home ribbon

---

## 🛠️ Technical Skills Demonstrated

### Power Query
- Data type correction and validation
- Custom column: Days to Ship calculation
- Column quality checks and null removal
- Multi-table loading (Orders, Date_Table)
- Column renaming for DAX compatibility

### Data Modeling
- Star schema architecture
- Proper Date Table with Mark as Date Table
- Relationship cardinality management
- Single-directional filter decisions
- Dedicated MeasuresTable organisation
- What-If parameter table integration

### DAX (27 measures across 6 categories)
- Core aggregations: SUM, DISTINCTCOUNT, AVERAGE
- Safe division: DIVIDE with zero fallback
- Time intelligence: SAMEPERIODLASTYEAR, DATESINPERIOD
- Iterator functions: SUMX for row-level scenarios
- Variables: VAR / RETURN pattern throughout
- Dynamic text: CONCATENATEX, FORMAT, ABS, IF, TOPN
- Conditional coloring: IF-based color measure pattern
- SWITCH(TRUE()) for classification logic

### Visualization (5 pages, 40+ visuals)
- KPI Cards with YoY directional indicators
- Line + Clustered Column combo charts
- Scatter charts with trend lines and constant reference lines
- Matrix with diverging heatmap conditional formatting
- Gauge with SLA target zones
- Decomposition Tree (AI visual) for root cause analysis
- 6-month revenue forecast with confidence band
- Funnel chart for volume ranking
- Dynamic text cards with auto-updating narrative
- Page Navigator buttons for professional navigation
- What-If parameter slicer with live simulation
- Conditional formatting: background color, data bars, font color

---

## 📁 Repository Structure

```
powerbi-profitability-dashboard/
│
├── README.md                        ← Project overview (you are here)
├── salesstore.pbix                  ← Power BI project file
├── dax-measures.md                  ← All 27 DAX measures documented
│
├── data/
│   ├── Orders.csv                   ← Main fact table
│   └── Date_Table_reference.md      ← Date table DAX for reference
│
└── screenshots/
    ├── 01_executive_overview.png
    ├── 02_product_profitability.png
    ├── 03_discount_impact.png
    ├── 04_shipping_operations.png
    ├── 05_forecast_whatif.png
    └── 06_data_model.png
```

---

## 📊 Dataset Information

| Property | Detail |
|----------|--------|
| Dataset | Global Superstore (Kaggle) |
| Main table | Orders |
| Key columns | Sales, Profit, Discount, Quantity, Ship Mode, Segment, Category, Region |
| Calculated column | Discount Band (No Discount / Low / Medium / High / Very High) |
| Date range | 2012 — 2015 |
| Segments | Consumer, Corporate, Home Office |
| Categories | Furniture, Office Supplies, Technology |
| Regions | Africa, Asia, Europe, North America, Oceania, South America, Other |
| Shipping modes | First Class, Second Class, Standard Class, Same Day |

---

## 🎤 How I Present This to a Hiring Manager

**30-second elevator pitch:**

> *"I built a 5-page Power BI dashboard to diagnose why a retail
> business was growing revenue but losing margin. The headline finding
> was that heavy discounting — specifically anything above 20% — was
> producing negative or near-zero profit on those orders. I quantified
> the impact and built an interactive what-if model so leadership could
> simulate profit recovery by adjusting the discount cap. I also built
> dynamic text cards that auto-generate written insights when slicers
> change — so the dashboard tells a story, not just shows numbers."*

---
