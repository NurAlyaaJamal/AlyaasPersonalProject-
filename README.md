# KL Property Pulse 🏙️
**An Excel dashboard exploring asking prices, sizes and RM per sq ft across Kuala Lumpur's property market.**

## Overview
This project cleans a raw dataset of Kuala Lumpur property listings and turns it into an interactive Excel dashboard. It helps buyers, investors and agents see what different property types cost, which areas are priciest, and how much space a budget buys.

## Business Questions
- Which areas have the highest median prices and RM per sq ft?
- What does a typical property cost by type (condo, terrace, bungalow, etc.)?
- How are listings spread across price bands, bedroom counts and furnishing levels?

## Dataset
- **Source:** https://www.kaggle.com/datasets/dragonduck/property-listings-in-kuala-lumpur
- **Raw size:** 53,883 listings, 8 columns (Location, Price, Rooms, Bathrooms, Car Parks, Property Type, Size, Furnishing)
- **Cleaned size:** 48,804 listings

## Data Cleaning (Python / pandas)
| Step | What was done |
|---|---|
| Empty rows | Removed 25 listings that only had a location |
| Duplicates | Removed 4,460 exact duplicate rows |
| Missing / invalid price | Removed 200 rows with no price and 394 rows priced below RM 50,000 |
| Location | Stripped ", Kuala Lumpur", trimmed spaces, fixed capitalisation → `Area` |
| Rooms | Split values like "3+1" into `Bedrooms`, `Extra_Rooms`, `Total_Rooms`; Studio = 0 bedrooms |
| Property Type | Split into `Base_Type`, `Lot_Position` and `Storeys` |
| Size | Split into `Size_Type` (Built-up / Land area) and numeric `Size_sqft`; dimensions like "22x75" multiplied, acres converted |
| Furnishing | Merged blank and "Unknown" values |
| Outliers | Prices above RM 50 million flagged in `Price_Outlier_High` and excluded from the dashboard |

Removed rows and their reasons are kept in the `Removed_Rows` sheet for transparency.

## Dashboard Features
- Dropdown filters for **property type** and **ranking metric** (median price or RM per sq ft)
- Headline numbers: listings, median price, median RM per sq ft, median built-up size
- Top 10 areas, price bands, bedrooms and furnishing charts
- All figures are live Excel formulas (COUNTIFS, MEDIAN with array formulas), no pasted values

## Key Definitions
- **Median** is used instead of average, because a few very high prices skew averages.
- **RM per sq ft** uses built-up size between 200 and 20,000 sq ft only.
- **Ranked areas** need at least 20 listings under the current filter.

## Tools
Python (pandas, openpyxl) · Microsoft Excel

## Repository Structure
```
├── data/
│   └── Property_Listings_in_Kuala_Lumpur.xlsx   # raw data
├── clean_property_listings.py                    # cleaning script
├── Property_Listings_KL_Cleaned.xlsx             # cleaned data + removed rows + log
├── KL_Property_Dashboard.xlsx                    # final dashboard
└── README.md
```

## How to Run
```bash
pip install pandas numpy openpyxl
python clean_property_listings.py
```
Edit the `SRC` and `OUT` paths at the top of the script to match your folders.

## Key Insights
*(Fill these in after exploring the dashboard)*
- [e.g. Taman Duta and Country Heights Damansara have the highest median prices]
- [e.g. Most listings sit in the RM 500k–1M band]
- [e.g. Condominiums make up the largest share of listings]

## Limitations
- Prices are **asking prices**, not completed transactions, so they are often higher than actual sale prices.
- Listings have no ID or date, so identical rows were treated as duplicates and trends over time can't be shown.
- Some size values were free text and were left blank.

## Screenshots
<img width="1770" height="630" alt="image" src="https://github.com/user-attachments/assets/dd891833-5a58-40a9-9299-d07346664b67" />


## Author
**Nur Alyaa Jamal** · http://linkedin.com/in/Nur-alyaa-jamal13
