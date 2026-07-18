# Tableau Build Guide

## Purpose

This guide turns the cosmetics dataset into a Tableau workbook with interactive dashboards and reusable calculated fields.

## Rubric Alignment

- Data collection & extraction: use `data/cosmetics_sample.csv`
- Data preparation: clean and standardize the source fields before building visuals
- Data visualizations: create 5 unique worksheet visuals
- Dashboard: combine the sheets into one responsive workbook
- Story: build 3 to 5 scenes that walk through the insights
- Performance testing: validate filters, calculations, and load time on the 10,001-row dataset
- Web integration: publish the final dashboard and include the live link in the README
- Project demonstration & documentation: keep the report, executive summary, and notes in the repo

## 1. Connect the Data

1. Open Tableau Desktop.
2. Connect to the CSV file at `data/cosmetics_sample.csv`.
3. Verify field types:
   - `Product_ID`, `Reviews`, and `Launch_Year` as whole numbers
   - `Price`, `Rating`, and `Sales_USD` as decimals
   - `Brand`, `Category`, `Skin_Type`, `Ingredient_Type`, and `Country` as dimensions

## 2. Clean and Prepare

- Remove duplicate rows if your source data contains them.
- Standardize category names and skin-type labels.
- Filter out null values for required fields such as brand, category, price, and rating.
- Confirm the data has 10,001 rows so the workbook can be used for performance review.

## 3. Create Calculated Fields

### Price Band

```tableau
IF [Price] < 20 THEN "Low"
ELSEIF [Price] < 35 THEN "Mid"
ELSE "High"
END
```

### Rating Group

```tableau
IF [Rating] >= 4.5 THEN "Excellent"
ELSEIF [Rating] >= 4.0 THEN "Good"
ELSE "Average"
END
```

### Sales Band

```tableau
IF [Sales_USD] < 20000 THEN "Low"
ELSEIF [Sales_USD] < 35000 THEN "Medium"
ELSE "High"
END
```

### Popularity Score

```tableau
([Rating] * 20) + (SUM([Reviews]) / 100)
```

## 4. Build the Sheets

### Market Overview

- KPI cards for total products, average price, average rating, and total sales
- Category bar chart
- Year trend line

### Brand Performance

- Sales by brand
- Rating vs. sales scatter plot
- Top products table

### Pricing Analysis

- Price histogram
- Category box plot
- Brand and price band heatmap

### Skin-Type Suitability

- Skin-type stacked bar chart
- Category treemap
- Product suitability table

### Consumer Preference Trends

- Rating distribution
- Review count ranking
- Category preference bars

## 5. Add Filters

Apply global filters for:
- Brand
- Category
- Skin_Type
- Price Band
- Rating Group
- Launch_Year

## 6. Final Dashboard Layout

Recommended order:
1. Market Overview
2. Brand Performance
3. Pricing Analysis
4. Skin-Type Suitability
5. Consumer Preference Trends

Use consistent colors, shared filters, and dashboard actions for navigation.

## 7. Export

- Save the workbook as `Cosmetic_Insights.twbx`
- Export dashboard screenshots for reports or presentations
- Publish to Tableau Public if sharing online
