# Exploratory Data Analysis of the Ames Housing Dataset

Exploratory data analysis (no machine learning) of the Kaggle competition
**House Prices: Advanced Regression Techniques**, using `train.csv`
(about 1,460 rows x 81 columns).

The goal is to understand which factors drive house sale prices and to practise
the full EDA workflow.

## Guiding questions

1. How is `SalePrice` distributed? Is it skewed?
2. Which numerical features correlate most strongly with `SalePrice`?
3. Does `OverallQual` change price in a clear, ordered way?
4. Do some neighborhoods consistently cost more than others?
5. Are there outliers, and are they errors or real but unusual sales?
6. Which columns have missing values, and which of those are not truly missing?

## Project files

| File | Description |
|---|---|
| `house_prices_eda.ipynb` | The analysis notebook (Steps 1-10) |
| `train.csv` | Dataset, downloaded from Kaggle (not included in this repo) |
| `eda_dashboard.png` | 2x2 summary figure, created when the notebook is run |
| `requirements.txt` | Python dependencies |

## Setup

1. Download `train.csv` from the Kaggle competition page
   (https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data)
   and place it in the same folder as the notebook.
2. Create an environment and install the dependencies:

   ```bash
   python -m venv .venv
   source .venv/bin/activate        # Windows: .venv\Scripts\activate
   pip install -r requirements.txt
   ```
3. Start Jupyter and run all cells:

   ```bash
   jupyter notebook house_prices_eda.ipynb
   ```

Running the notebook saves `eda_dashboard.png` in the same folder.

## Notebook structure

| Section | Content | Step |
|---|---|---|
| 1. Introduction | Objective, dataset, questions | - |
| 2. Data loading | Shape, types, missing values | 1 |
| 3. Data understanding | Variable types, descriptive statistics | 2, 3 |
| 4. Data cleaning | Duplicates, labels, missing values, impossible values | 9 |
| 5. Univariate analysis | Distributions, boxplots, countplots | 4 |
| 6. Bivariate / multivariate | Correlation, covariance, scatter, pair plot, heatmap | 5, 6, 7 |
| 7. Outlier analysis | IQR and z-score methods | 8 |
| 8. Dashboard | Four-panel summary figure | 10 |
| 9. Conclusions | Insights and limitations | - |

## Key cleaning decisions

- `NA` in `PoolQC`, `Alley`, `Fence`, `FireplaceQu`, `GarageType` (and the other
  garage, basement, masonry and misc columns) means the feature is absent, so it
  is filled with `"None"` rather than dropped.
- `LotFrontage`: median grouped by `Neighborhood`.
- `MasVnrArea`: filled with 0.
- `GarageYrBlt`: filled with `YearBuilt` where there is no garage (an assumption).
- `Electrical`: the single missing value is filled with the mode.
- Outliers: houses with `GrLivArea > 4000` and `SalePrice < 300000` are removed
  (`df_clean`); large, expensive houses are kept.

## Limitations

- Correlation does not imply causation, and several features are correlated with each other.
- Pearson correlation only captures linear relationships.
- Fill strategies are assumptions and should be revisited for any modelling work.
- The data covers one city (Ames, Iowa) and one period, so results may not generalise.

## Tools

Python, pandas, NumPy, Matplotlib, Seaborn, SciPy, Jupyter Notebook.
