# 📱 India Mobile Sales Dashboard — Power BI (Beginner Project)

## 🎯 Project Overview
This is my first Power BI dashboard built as a beginner 
project to learn data visualization, basic DAX measures, 
and dashboard design fundamentals.

The dashboard analyzes mobile phone sales data across 
major Indian cities, covering 5 mobile models, 12 months 
of sales data, 4,000+ transactions, and 4 payment methods.

---

## 📊 Dashboard Preview


<img width="964" height="539" alt="image" src="https://github.com/user-attachments/assets/4cf6d2ec-facb-4e36-81b2-0b22a7e7aaf9" />

---

## 🔍 Business Questions Answered

- Which mobile model generates the highest total sales?
- Which month had the highest and lowest units sold?
- How are customers rating their purchases?
- Which payment method is most preferred by customers?
- Which cities have the highest sales concentration?
- Which day of the week drives the most sales?

---

## 📈 Key Findings

- **Total Sales** crossed ₹769 Million across all models
- **iPhone SE** had the highest total sales at ₹59.5M 
  despite not having the highest transaction count
- **Vivo Y51** had the highest units sold at 1,429 
  with 283 transactions
- **March** recorded the highest monthly units sold 
  at 1,696 units
- **Saturday** is the strongest sales day — 
  ₹115M vs Wednesday low of ₹105M
- **UPI** and **Cash** together account for over 50% 
  of all transactions showing mixed digital adoption
- **5-star ratings** dominate with 1,490 reviews — 
  majority of customers are satisfied

---

## 🛠️ Tools & Skills Used

| Tool | Purpose |
|------|---------|
| Power BI Desktop | Dashboard building and visualization |
| Power Query | Data import and basic cleaning |
| DAX | Creating the Total Sales measure |
| Map Visual | Geographic sales distribution across India |

---

## 📐 DAX Measure Written

```DAX
Total Sales = SUM(Sales[Sales_Amount])
```

> This is my first DAX measure. In upcoming projects I will 
> be building advanced measures including time intelligence, 
> YoY comparisons, rolling averages, and what-if parameters.

---

## 📁 Dataset Details

- **Source:** Mobile sales data (CSV)
- **Rows:** ~4,000+ transactions
- **Cities covered:** Delhi, Mumbai, Bangalore, Hyderabad, 
  Chennai, Kolkata, Pune, Jaipur, Lucknow, and more
- **Models:** Galaxy S21, Vivo Y51, Galaxy Note 20, 
  OnePlus Nord, iPhone SE
- **Time period:** January — December (12 months)
- **Payment methods:** UPI, Debit Card, Credit Card, Cash

---

## 📌 Visuals Built

| Visual Type | What It Shows |
|-------------|--------------|
| KPI Cards (x4) | Total Sales, Units Sold, Transactions, Avg Price |
| Map Visual | Sales distribution across Indian cities |
| Line Chart | Monthly units sold trend |
| Bar Chart | Customer ratings distribution |
| Pie Chart | Transaction split by payment method |
| Bar Chart | Total sales by mobile model |
| Area Chart | Sales by day of the week |
| Table | Model-wise sales, quantity, transactions |
| Slicer | Month filter (January to December) |

---
