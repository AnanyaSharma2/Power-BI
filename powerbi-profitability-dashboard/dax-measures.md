# DAX Measures — Complete Reference
# Global Superstore Profitability Dashboard
# Power BI Project | MeasuresTable
# Total measures: 27

---

## 📁 CATEGORY 1 — Core Aggregations
> Foundation measures. Every other measure builds on these.

---

### Total Revenue
```dax
Total Revenue = 
SUM(Orders[Sales])
```
> Sums all values in the Sales column across every order line.
> Uses SUM not SUMX because no row-level calculation is needed —
> we are simply totalling an existing column.

---

### Total Profit
```dax
Total Profit = 
SUM(Orders[Profit])
```
> Sums all profit values. Note: Profit in the dataset is already
> calculated as Sales minus Cost — it can be negative for discounted
> orders where cost exceeds revenue.

---

### Total Orders
```dax
Total Orders = 
DISTINCTCOUNT(Orders[Order ID])
```
> Counts unique Order IDs — NOT total rows.
> Critical distinction: the Orders table has one row per ORDER LINE
> (one order with 3 products = 3 rows, same Order ID).
> DISTINCTCOUNT gives us actual order count, not line count.

---

### Total Quantity
```dax
Total Quantity = 
SUM(Orders[Quantity])
```
> Total units sold across all orders and products.

---

### Avg Discount
```dax
Avg Discount = 
AVERAGE(Orders[Discount])
```
> Average discount rate across all order lines.
> Discount column contains decimals (0.2 = 20% discount).
> Format this measure as Percentage in Measure Tools.

---

### Avg Days to Ship
```dax
Avg Days to Ship = 
AVERAGE(Orders[Days to Ship])
```
> Average number of days between Order Date and Ship Date.
> Requires the Days to Ship calculated column created in Power Query:
> = Duration.Days([Ship Date] - [Order Date])

---

## 📁 CATEGORY 2 — Ratios & KPIs

---

### Profit Margin %
```dax
Profit Margin % = 
DIVIDE(
    [Total Profit],
    [Total Revenue],
    0
)
```
> Profit as a percentage of revenue.
> DIVIDE used instead of / operator — returns 0 if revenue is zero
> rather than throwing a division by zero error.
> Format as Percentage with 1-2 decimal places.

---

### Profit Margin KPI
```dax
Profit Margin KPI = 
DIVIDE(
    [Total Profit],
    [Total Revenue],
    0
)
```
> Same calculation as Profit Margin % — created as a separate measure
> for use in the KPI card visual on Page 1 with specific formatting
> and conditional color applied separately via Profit Margin Color.

---

### Return Rate %
```dax
Return Rate % = 
VAR ReturnedOrders = 
    CALCULATE(
        DISTINCTCOUNT(Orders[Order ID]),
        Orders[Return Flag] = "Returned"
    )
RETURN
DIVIDE(ReturnedOrders, [Total Orders], 0)
```
> Percentage of orders that were returned.
> VAR stores the count of returned orders using CALCULATE to filter
> only rows where Return Flag = "Returned".
> RETURN divides by total orders to get the rate.

---

## 📁 CATEGORY 3 — Time Intelligence
> Requires Date_Table to be marked as Date Table in Power BI.
> All these measures return BLANK if Date_Table is not properly configured.

---

### Revenue LY
```dax
Revenue LY = 
CALCULATE(
    [Total Revenue],
    SAMEPERIODLASTYEAR(Date_Table[Date])
)
```
> Revenue for the exact same period in the prior year.
> CALCULATE modifies the filter context.
> SAMEPERIODLASTYEAR shifts the date filter back 12 months.
> Example: if current context is Jan-Jun 2015, this returns Jan-Jun 2014.

---

### YoY Revenue %
```dax
YoY Revenue % = 
DIVIDE(
    [Total Revenue] - [Revenue LY],
    [Revenue LY],
    0
)
```
> Year-over-year percentage change in revenue.
> Positive = growth. Negative = decline.
> Returns 0 if prior year data is absent (no error thrown).

---

### Avg days to return LY
```dax
Avg days to return ly = 
CALCULATE(
    [Avg Days to Ship],
    SAMEPERIODLASTYEAR(Date_Table[Date])
)
```
> Average shipping days for the same period last year.
> Used in shipping trend comparisons on Page 4.

---

## 📁 CATEGORY 4 — Scenario Modeling
> What-If parameter: "Discount Reduction" (0 to 1, step 0.05)
> Created via: Modeling → New Parameter

---

### Simulated Profit
```dax
Simulated Profit = 
VAR Reduction = 'Discount Reduction'[Discount Reduction Value]
RETURN
SUMX(
    Orders,
    Orders[Profit] + (Orders[Sales] * Orders[Discount] * Reduction)
)
```
> Calculates what profit would be if discounts were reduced by slider %.
> SUMX iterates row by row — for each order it recalculates profit
> as: actual profit + the recovered amount from reducing the discount.
> When Reduction slider = 0.3, simulates cutting all discounts by 30%.
> Updates live as the slicer moves.

---

### Profit Recovery
```dax
Profit Recovery = 
[Simulated Profit] - [Total Profit]
```
> The dollar amount of additional profit gained through discount reduction.
> Shown as "Potential Profit Recovery" KPI card on Page 3.
> A positive number = how much profit the business is leaving on the table.

---

## 📁 CATEGORY 5 — Dynamic Text Measures
> These generate auto-updating narrative sentences for Card visuals.
> The text changes automatically when slicers are applied.
> This is one of the most advanced and impressive Power BI techniques.

---

### Forecast Dynamic Insight
```dax
Forecast Dynamic Insight = 

VAR Growth = 
    DIVIDE(
        [Total Revenue] - [Revenue LY],
        [Revenue LY],
        0
    )

VAR Direction = 
    IF(
        Growth > 0, "increased",
        IF(Growth < 0, "decreased", "remained stable")
    )

VAR Percent = 
    FORMAT(ABS(Growth), "0.0%")

VAR TopCat = 
    TOPN(
        1,
        VALUES(Orders[Category]),
        [Total Revenue],
        DESC
    )

VAR Category = 
    CONCATENATEX(TopCat, Orders[Category], ", ")

RETURN
IF(
    ISBLANK(Growth),
    "No sufficient data to generate insight.",
    "Revenue has " & Direction & " by " & Percent &
    " compared to last year, mainly driven by " & Category & "."
)
```
> Generates a full English sentence describing revenue performance.
> Example output: "Revenue has increased by 18.5% compared to last year,
> mainly driven by Technology."
> VAR Growth — calculates YoY growth inline for reliability
> VAR Direction — converts numeric growth to descriptive word
> VAR Percent — formats growth as clean percentage string
> VAR TopCat — uses TOPN to find the #1 revenue category
> VAR Category — converts TOPN table result to text using CONCATENATEX
> RETURN — assembles all variables into one readable sentence

---

### Final Insight
```dax
Final Insight = 

VAR ProfitMargin = [Profit Margin %]

VAR MarginStatus = 
    IF(
        ProfitMargin > 0.15, "healthy",
        IF(ProfitMargin > 0.10, "moderate", "concerning")
    )

VAR TopSeg = 
    TOPN(
        1,
        VALUES(Orders[Segment]),
        [Total Revenue],
        DESC
    )

VAR Segment = 
    CONCATENATEX(TopSeg, Orders[Segment], ", ")

RETURN
IF(
    ISBLANK(ProfitMargin),
    "Insufficient data.",
    "Overall profit margin is " & FORMAT(ProfitMargin, "0.0%") &
    " — " & MarginStatus & ". " &
    "The " & Segment & " segment is the primary revenue driver."
)
```
> Generates executive summary insight for Page 1.
> Classifies margin health as healthy/moderate/concerning.
> Identifies the top contributing segment automatically.

---

### Shipping Insight
```dax
Shipping Insight = 

VAR AvgDays = [Avg Days to Ship]

VAR Status = 
    IF(
        AvgDays <= 3, "within SLA target",
        IF(AvgDays <= 5, "slightly above SLA target", "exceeding SLA target — action needed")
    )

RETURN
"Average shipping time is " & FORMAT(AvgDays, "0.0") &
" days — " & Status & "."
```
> Auto-generates shipping performance narrative for Page 4.
> Compares actual average against 3-day SLA target.
> Updates automatically when region or ship mode slicer changes.

---

### Product Insight
```dax
Product Insight = 

VAR TopSubCat = 
    TOPN(
        1,
        VALUES(Orders[Sub_Category]),
        [Total Revenue],
        DESC
    )

VAR TopName = 
    CONCATENATEX(TopSubCat, Orders[Sub_Category], ", ")

VAR WorstSubCat = 
    TOPN(
        1,
        VALUES(Orders[Sub_Category]),
        [Profit Margin %],
        ASC
    )

VAR WorstName = 
    CONCATENATEX(WorstSubCat, Orders[Sub_Category], ", ")

RETURN
"Top revenue sub-category: " & TopName &
". Lowest margin sub-category: " & WorstName & "."
```
> Identifies the highest revenue and lowest margin sub-categories
> dynamically. Updates when category or region filters are applied.

---

### Dynamic Insight of Discount Strategy & Profitability Impact
```dax
Dynamic Insight of Discount Strategy & Profitability Impact = 

VAR AvgDisc = [Avg Discount]

VAR DiscLevel = 
    IF(
        AvgDisc <= 0.10, "low",
        IF(AvgDisc <= 0.20, "moderate", "high")
    )

VAR Recovery = [Profit Recovery]

RETURN
"Current average discount is " & FORMAT(AvgDisc, "0.0%") &
" — classified as " & DiscLevel & " discounting. " &
"Simulated profit recovery potential: " &
FORMAT(Recovery, "$#,##0") & "."
```
> Generates the key insight narrative for Page 3.
> Classifies current discount level and states the simulated
> profit recovery from the what-if slider in dollar terms.

---

## 📁 CATEGORY 6 — Display, Color & UX Measures
> These measures control visual formatting — colors and labels.
> They make the dashboard react visually to data changes.

---

### Revenue Color
```dax
Revenue Color = 
IF([YoY Revenue %] >= 0, "#27AE60", "#E74C3C")
```
> Returns green hex if revenue is growing, red if declining.
> Used in conditional formatting of the Revenue KPI card.
> Green = #27AE60, Red = #E74C3C

---

### Profit Color
```dax
Profit Color = 
IF([Total Profit] >= 0, "#27AE60", "#E74C3C")
```
> Returns green if profit is positive, red if negative.
> Applied to profit display card font color.

---

### Profit Margin Color
```dax
Profit Margin Color = 
IF(
    [Profit Margin %] >= 0.15, "#27AE60",
    IF([Profit Margin %] >= 0.10, "#F39C12", "#E74C3C")
)
```
> Three-tier color system for margin health:
> Green (>=15%) = healthy margin
> Amber (10-15%) = moderate — monitor closely  
> Red (<10%) = critical — immediate attention needed

---

### Return YoY Color
```dax
Return YoY Color = 
VAR ReturnYoY = 
    DIVIDE(
        [Return Rate %] - CALCULATE([Return Rate %], SAMEPERIODLASTYEAR(Date_Table[Date])),
        CALCULATE([Return Rate %], SAMEPERIODLASTYEAR(Date_Table[Date])),
        0
    )
RETURN
IF(ReturnYoY <= 0, "#27AE60", "#E74C3C")
```
> For Return Rate, the logic is inverted:
> Fewer returns (negative YoY) = GREEN (good news)
> More returns (positive YoY) = RED (bad news)
> This measure feeds the Return Rate card color formatting.

---

### Profit display
```dax
Profit display = 
IF(
    [Total Profit] >= 1000000,
    FORMAT([Total Profit] / 1000000, "0.00") & "M",
    IF(
        [Total Profit] >= 1000,
        FORMAT([Total Profit] / 1000, "0.0") & "K",
        FORMAT([Total Profit], "$#,##0")
    )
)
```
> Converts raw profit number into clean display string.
> Automatically switches between M (millions), K (thousands),
> and full dollar format depending on the magnitude.
> Example: 1,250,000 → "1.25M" | 45,220 → "45.2K"

---

### revenue display
```dax
revenue display = 
IF(
    [Total Revenue] >= 1000000,
    FORMAT([Total Revenue] / 1000000, "0.00") & "M",
    IF(
        [Total Revenue] >= 1000,
        FORMAT([Total Revenue] / 1000, "0.0") & "K",
        FORMAT([Total Revenue], "$#,##0")
    )
)
```
> Same pattern as Profit display — formats revenue for clean
> card display with automatic M/K/$ unit switching.

---

### Return display
```dax
Return display = 
FORMAT([Return Rate %], "0.00%")
```
> Formats return rate as a clean percentage string for card display.

---

## 📁 CATEGORY 7 — Navigation & Titles
> Dynamic titles that update based on active slicer selections.

---

### Dynamic Title Forecast
```dax
Dynamic Title Forecast = 
VAR SelectedYear = 
    SELECTEDVALUE(Date_Table[Year], "All Years")
RETURN
"Revenue Forecast — " & SelectedYear
```
> Page title that includes the selected year from slicer.
> If no year selected: "Revenue Forecast — All Years"
> If 2015 selected: "Revenue Forecast — 2015"

---

### Dynamic Title Shipping & Operation
```dax
Dynamic Title Shipping & Operation = 
VAR SelectedYear = 
    SELECTEDVALUE(Date_Table[Year], "All Years")
VAR SelectedRegion = 
    SELECTEDVALUE(Orders[Region Group], "All Regions")
RETURN
"Shipping & Operations — " & SelectedRegion & " | " & SelectedYear
```
> Generates a dynamic page subtitle combining both active filters.
> Example: "Shipping & Operations — Europe | 2014"

---

## 📁 CALCULATED COLUMN (in Orders table)

### Discount Band
```dax
-- Right-click Orders table → New Column
Discount Band = 
SWITCH(
    TRUE(),
    Orders[Discount] = 0,         "No Discount",
    Orders[Discount] <= 0.10,     "Low (1–10%)",
    Orders[Discount] <= 0.20,     "Medium (11–20%)",
    Orders[Discount] <= 0.30,     "High (21–30%)",
                                   "Very High (31%+)"
)
```
> Row-level classification of every order into a discount tier.
> SWITCH(TRUE()) evaluates each condition top-to-bottom and returns
> the first match — more readable than nested IF statements.
> This is a COLUMN not a MEASURE — computed at refresh, stored in model.
> Used on Page 3 as the X-axis for discount impact analysis.

---

## 📁 DATE TABLE (New Table)

```dax
Date_Table = 
ADDCOLUMNS(
    CALENDAR(DATE(2012,1,1), DATE(2016,12,31)),
    "Year",          YEAR([Date]),
    "Month Number",  MONTH([Date]),
    "Month Name",    FORMAT([Date], "MMMM"),
    "Month Short",   FORMAT([Date], "MMM"),
    "Quarter",       "Q" & QUARTER([Date]),
    "Year-Month",    FORMAT([Date], "YYYY-MM"),
    "Week Number",   WEEKNUM([Date]),
    "Day Name",      FORMAT([Date], "DDDD"),
    "Is Weekend",    IF(WEEKDAY([Date], 2) >= 6, TRUE, FALSE)
)
```
> After creating: Table Tools → Mark as Date Table → select Date column.
> This step is MANDATORY for all time intelligence measures to work.

---

*27 measures | 1 calculated column | 1 Date Table*
*All measures stored in dedicated MeasuresTable for clean model organization*
