# Flipkart Brand Sales Analysis

## Project Overview

An interactive dashboard built using **Power BI Desktop** to analyze Flipkart product sales, with a focus on **brand-level performance**, average sales, pricing, discounts, and customer ratings.

---

## Dataset Description

* Sourced dataset contains Flipkart listings (e.g., mobile products), cleansed via Power Query to remove duplicates, standardize brand names, convert numeric fields properly, and handle missing values ([GitHub][1]).
* Typical fields: `Brand`, `ProductName`, `SellingPrice`, `RetailPrice`, `UnitsSold`, `Discount%`, `OverallRating`, `ReviewCount`
* Metadata summary example:

  * \~28 product brands, hundreds of models, millions in total units sold, average discount \~4.54K (likely ₹4,540), average rating \~4.28, with average review counts in tens of thousands ([GitHub][1])

---

## Objective & Use Cases

* Present **brand-wise average units sold**, average selling price, average discount, and ratings comparisons.
* Identify **top-performing brands** by revenue and unit sales.
* Reveal insights on **discount strategy, pricing tiers**, and **consumer feedback dynamics**.
* Enable interactive exploration via slicers for brand, price category, and rating.

---

## Tools & Technology Stack

* **Power BI Desktop** for data cleansing (Power Query), modeling (DAX), and visualization.
* **Power Query** (M language): Clean and standardize `Brand` and `ProductName`, parse numeric values, handle missing records ([Medium][2], [GitHub][3], [GitHub][4])
* **DAX Measures** for brand-level KPIs like Average Units, Brand Revenue, Rank by Sales, etc.

---

## Data Processing Workflow

### Data Prep & Transformation

* Remove duplicates and null brand rows
* Standardize string formatting and numeric types for price, discount, rating
* If needed, extract brand names and product specs from composite fields using Power Query or Python preprocessing ([GitHub][4], [GitHub][1])

### Model Crafting & DAX Metrics

Define measures like:

```DAX
AvgUnitsSold = AVERAGE(Table[UnitsSold])
AvgSellingPrice = AVERAGE(Table[SellingPrice])
AvgDiscount = AVERAGE(Table[Discount])
TotalRevenue = SUMX(Table, Table[UnitsSold] * Table[SellingPrice])
RankByRevenue = RANKX(ALL(Table[Brand]), [TotalRevenue], , DESC)
```

Add category slicers (e.g., price tiers: budget/mid/flagship) via calculated columns in Power Query or DAX ([Reddit][5], [Medium][2])

---

## Visual Design & Layout

Adopt a clean dashboard layout:

* **Top KPIs**: Brand count, total revenue, overall average discount, average rating
* **Left pane**: Bar charts showing Top Brands by Units Sold and Revenue
* **Right pane**: Table/Matrix with brand, AvgUnits, AvgPrice, AvgDiscount, Revenue, Rank
* **Bottom section**: Price distribution charts or scatter plots (avg price vs units)
* Add **slicers** for Brand, Price Category, Rating, Discount Range ([Reddit][6], [learn.microsoft.com][7], [GitHub][8], [Medium][2])

---

## Key Insights (Examples from Real Analyses)

* Leading brands often account for \~25–30% of total units sold
* Discount-heavy brands attract volume but may not always yield the highest revenue
* Mid-range price categories typically dominate listing distributions (\~50–60%)
* Customer rating trends vs price—lower-priced brands often have lower average rating counts ([Medium][2], [GitHub][1])

## Instructions for Use

1. Open **Flipkart\_Dashboard.pbix** in Power BI Desktop.
2. Load/import the cleaned dataset or connect to the provided CSV.
3. Explore visuals: **click bars or use slicers** to filter by brand, rating, or price category.
4. Review measure logic via **Model view** → DAX expressions.
5. Export or publish via Power BI Service to share dashboards.
