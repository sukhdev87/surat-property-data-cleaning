# Surat Property Data Cleaning

## Overview
This project focuses on cleaning a real estate dataset containing **4,526 property listings from Surat, Gujarat, India**.  
The raw data contained multiple quality issues including encoding errors, null values, outliers, and inconsistent formatting.  
All cleaning was performed using **Microsoft Excel — Power Query**.

---

## Dataset Info
| | |
|---|---|
| **Source** | Kaggle — Surat Property Listings |
| **Original Rows** | 4,526 |
| **Final Rows** | 4,526 |
| **Columns** | 11 |
| **Tool Used** | Microsoft Excel, Power Query |

---

## Problems Found
- Column names in inconsistent format (lowercase, snake_case)
- Extra whitespace in text columns
- Encoding error — `â‚¹` instead of `₹` in price columns
- Null and error values across multiple columns
- `Price` column had mixed formats — `₹45.4 Lac`, `₹1.2 Cr`, `Call for Price`
- `Square_Feet` column had text `sqft` mixed with numbers, plus extreme outliers (8,400,000 sqft)
- `Description` column had `Read more` appended to every cell
- `South -West` inconsistent spacing
- 3 accidental filter steps were removing 2,275 rows from the dataset

---

## Cleaning Steps

1. Column names renamed to Title_Case format — `property_name` → `Property_Name`
2. Columns reordered as per requirement
3. Trim and Clean applied on all columns — extra spaces removed
4. Errors replaced with `Unknown`
5. Null values replaced with `Unknown`
6. `South -West` replaced with `South - West` (spacing fix)
7. Encoding error fixed — `â‚¹` removed from `Price_Per_Sqft` and `Price` columns
8. `Price_Per_Sqft` — `per sqft` text removed, converted to Decimal Number
9. `Price_Per_Sqft` null values (6%) replaced with mean — **5171.31**
10. `Price_INR` new column created using Custom Column formula — Lac × 100,000 / Cr × 10,000,000 / Call for Price → null
11. `Price_INR` null values (3%) replaced with mean — **12,466,076.12**
12. Original `Price` column deleted
13. `Square_Feet` — `sqft` text removed, converted to number
14. `Square_Feet` errors (3%) replaced with median — **1,285** (mean avoided due to outliers like 8,400,000)
15. `Description` column — `Read more` text removed from all cells
16. `Floor` column — null/errors replaced with `Unknown`, kept as text format
17. Filtered Rows, Filtered Rows1, Filtered Rows2 — deleted from Applied Steps (were accidentally removing 2,275 rows)
18. Final row count verified — **4,526 rows** ✅

---

## Tools Used
- Microsoft Excel
- Power Query

---

## Files
- `data/original_data.csv` — raw messy data
- `data/cleaned_data.xlsx` — fully cleaned data

---

## Key Learnings
- Always check **Applied Steps** in Power Query — accidental filter steps can silently delete thousands of rows
- Use **Median** instead of Mean when outliers are present in numerical columns
- Encoding errors like `â‚¹` require text replacement before type conversion
- Mixed price formats (Lac/Cr) require Custom Column logic for standardization
