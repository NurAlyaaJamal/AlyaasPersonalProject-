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

### Market overview
1. **The typical listing is priced at RM 1.0 million**, but the average is RM 1.88 million. A small number of very expensive listings pull the average up, so the median is the better measure.
2. **Half of all listings (50%) are priced under RM 1 million.** About 17% are under RM 500k, 33% fall in RM 500k–1M, 25% in RM 1–2M, 18% in RM 2–5M, and only 7% are above RM 5M.
3. **Typical size and price per sq ft:** the median built-up size is about 1,260 sq ft, and the median price is about RM 682 per sq ft.

### Property types
4. **Condominiums and serviced residences make up two-thirds of the market** (43% and 24% of listings).
5. **Serviced residences are the most expensive per sq ft among the main types, at about RM 928**, compared with RM 625 for condominiums and RM 602 for terrace houses. Their units are also small (about 1,000 sq ft median), so the price per sq ft is high even though the total price (about RM 850k) is not.
6. **Terrace and link houses give the most space for the money among landed homes**: a median of about 1,760 sq ft for about RM 1.1M, at about RM 602 per sq ft.
7. **Bungalows and semi-detached houses are a different price tier**, with a median price of about RM 4.0M and a median size of about 6,000 sq ft.
8. **Apartments and flats are the most affordable option**, at a median of about RM 325k and about RM 366 per sq ft.

### Areas
9. **Mont Kiara (5,215 listings) and KLCC (4,609) have the most listings**, followed by Cheras, Jalan Klang Lama (Old Klang Road), Setapak and Bukit Jalil.
10. **KLCC has the highest price per sq ft among the large areas, at about RM 1,323**, followed by KL Eco City (about RM 1,291), KL Sentral (about RM 1,289) and Bukit Bintang (about RM 1,106).
11. **The highest median prices are in prestige landed areas**: Taman Duta (about RM 12.0M), Country Heights Damansara (about RM 6.4M), Federal Hill (about RM 6.0M) and Damansara Heights (about RM 4.8M).
12. **Bangsar is the most expensive large area** by median price (about RM 3.2M across 1,771 listings), and it is also high at about RM 987 per sq ft.
13. **The cheapest areas are Bandar Tasik Selatan, Desa Petaling and Jinjang**, with medians of about RM 330k–360k and about RM 300–355 per sq ft.
14. **Price per sq ft does not always follow total price.** Taman Duta tops the median price chart, but its price per sq ft is only about RM 889 because its homes are very large. This is why the dashboard lets you rank by either measure.

### Bedrooms and furnishing
15. **Three-bedroom homes dominate, at 43% of listings.** Next are 4-bedroom (19%) and 2-bedroom (14%) homes, while studios are only about 2%.
16. **Partly furnished is the most common furnishing level (about 50%)**, followed by fully furnished (26%), unknown (14%) and unfurnished (11%).
17. **Serviced residences are the most likely to be fully furnished** (42%, against 28% for condominiums and 10% for terrace houses).
18. **Fully furnished listings have a higher median price per sq ft (about RM 823) than unfurnished ones (about RM 523).** This is partly because furnished units are mostly in pricier condo and serviced-residence areas, so it does not prove that furnishing alone adds value.

## Limitations
- Prices are **asking prices**, not completed transactions, so they are often higher than actual sale prices.
- Listings have no ID or date, so identical rows were treated as duplicates and trends over time can't be shown.
- Some size values were free text and were left blank.

## Screenshots
<img width="1770" height="630" alt="image" src="https://github.com/user-attachments/assets/dd891833-5a58-40a9-9299-d07346664b67" />


## Author
**Nur Alyaa Jamal** · http://linkedin.com/in/Nur-alyaa-jamal13
