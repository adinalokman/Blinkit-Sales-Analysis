# Blinkit Sales & Marketing Analysis (Python)

## Overview
An exploratory analysis of a Blinkit retail dataset (8,523 rows) using Python. The project cleans the data, explores it, and answers nine business questions about how outlet and product characteristics relate to sales. Each result is checked for hidden explanations (such as differences in group size) before a conclusion is drawn.

**Notebook:** [`Blinkit_Sale_Analysis.ipynb`](Blinkit_Sale_Analysis.ipynb)
**Tools:** Python, pandas, Matplotlib

## Dataset
- `blinkit_data.csv`: 8,523 rows x 12 columns. Each row is one product sold at one specific outlet.
- **Product columns:** Item Identifier, Item Type, Item Fat Content, Item Weight, Item Visibility, Rating
- **Outlet columns:** Outlet Identifier, Outlet Establishment Year, Outlet Size, Outlet Location Type, Outlet Type
- **Outcome:** Sales

**Dataset limits that shape the conclusions**
- It is a snapshot with no sale dates, so trends over time cannot be studied.
- `Sales` is a value (revenue), not units sold.
- There is no customer-level data.

## Business Questions and Answers
| # | Question | Answer |
|---|---|---|
| 1 | Does outlet establishment year affect sales? | No. Average sales are ~RM139-143 for every year |
| 2 | Which outlet and location sell the most? | OUT035 and Tier 3 have the highest totals, but only because they list more products; per-product sales are the same |
| 3 | What sells best in each outlet type and location? | Fruits and Vegetables, Snack Foods and Household everywhere |
| 4 | Which product type sells the most? | Fruits and Vegetables, driven by its large number of products |
| 5 | Low Fat or Regular? | Low Fat is ~56% of food sales, but per-product sales are almost equal |
| 6 | Does visibility drive sales? | No (r = -0.006); only Soft Drinks shows a weak effect |
| 7 | Why do products underperform? | It is a product-level trait (97% consistent across outlets), not rating or fat content |
| 8 | Does rating drive sales? | No (r ~ 0.01), and location does not change that |
| 9 | Does weight drive sales? | No (r-squared = 0.07%); item type explains only ~1.25% |

## Main Finding
**Sales are almost entirely determined by the product itself.** The same product sells nearly the same amount in every outlet (standard deviation 1.15 across outlets vs 62.3 overall). None of the outlet or product characteristics tested explains sales to a meaningful degree.

## Data Quality Issues Found
| Issue | How it was handled |
|---|---|
| `Item Fat Content` had 5 labels for 2 categories | Standardized to Low Fat and Regular |
| `Outlet Size` inconsistent for 3 outlets | Set to each outlet's most frequent size; treated as unreliable and not used for conclusions |
| `Item Weight` missing for 1,463 rows, all from two outlets | Copied from the same product in other outlets (a product has the same weight everywhere); 4 rows left blank |
| `Item Visibility` = 0 for 526 rows | Excluded from the visibility question only, assuming they are unrecorded |
| Non-food items labeled "Low Fat" by default | Excluded from the Low Fat vs Regular comparison |
| `Rating` clusters at exactly 4.0 (~39% of rows) | Noted as a limitation |

## Techniques Demonstrated
- Data cleaning: label standardization, missing-value analysis and targeted imputation
- Group analysis with `groupby` (sum, mean and count together, to avoid misleading totals)
- Correlation (Pearson and Spearman) and effect size (r-squared)
- Stratification to test for hidden (confounding) variables
- Visualization with Matplotlib

## Limitations
- One-time snapshot: no trends or seasonality.
- Sales is a value, not units, so a high figure may reflect price rather than demand.
- Results show association, not causation.
- `Outlet Size` and `Rating` are unreliable columns.

## Recommendations
1. Grocery Stores list ~40% fewer products than other outlets; widening their range may raise total sales (to be tested with a pilot).
2. Review the product list centrally, since underperformance is product-level. Check units sold and margin before dropping any product.
3. Do not expect changes in visibility or rating alone to move sales; test with a controlled experiment.
4. Collect sale dates, units sold, price and margin to answer the questions this dataset cannot.

## How to Run
1. Install the libraries: `pip install pandas matplotlib`
2. Keep `blinkit_data.csv` in the same folder as the notebook.
3. Open `Blinkit_Sale_Analysis.ipynb` in VS Code or Jupyter and run all cells.

## Author
Nur Adina Faqiha
