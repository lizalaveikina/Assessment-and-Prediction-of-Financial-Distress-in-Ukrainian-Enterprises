# Data Description

## Source
The data were provided directly by [**YouControl**](https://youcontrol.com.ua), a Ukrainian legal and financial intelligence company, through its analytics platform [**YC.Market**](https://youcontrol.market). To ensure confidentiality, YouControl anonymized the data by replacing company registration numbers with unique firm identifiers.

## Confidentiality Notice
The raw data files are **not included** in this repository due to confidentiality constraints. This folder contains only documentation of the dataset structure, variable definitions, and the distress proxy construction.

## Dataset Overview
- **Observations:** 81,269 firm-year observations (70,351 in the analytical sample)
- **Unique firms:** 18,183
- **Time period:** 2018–2024
- **Columns:** 167 total (9 non-financial characteristics, 158 financial statement line items)
- **Industries:** Agriculture, Heavy Industry, Light Industry, Infrastructure, Trade, Other

## Sample Construction
The raw dataset includes all line items from Form 1 (balance sheet) and Form 2 (income statement). The following cleaning steps were applied:
- Firms with no recorded assets or revenues were removed
- Internal balance sheet identities were verified and inconsistent observations excluded
- Missing balance sheet values were replaced with zeros, reflecting absence of the item
- Non-negativity constraints were applied to key financial variables
- Firms with only one observation were excluded as lagged variables cannot be computed
- Observations isolated by gaps of more than one year were dropped

The resulting dataset is an unbalanced panel. Approximately 86.6% of firms have fully consecutive year coverage, and 19.8% are observed across all seven years.

## Industry Classification
Firms are classified into six industry groups based on the Ukrainian Classification of Economic Activities (KVED):

| Group | Description |
|-------|-------------|
| Agriculture | Sector A |
| Heavy Industry | Sector C (heavy) + Sector B (mining) |
| Light Industry | Sector C (light) |
| Infrastructure | Sectors D, H, F |
| Trade | Sector G |
| Other | All remaining sectors |

## Variables

### Financial Indicators
| Variable | Formula | Category |
|----------|---------|----------|
| ROA | Net Income / Total Assets | Profitability |
| EBIT to Assets | EBIT / Total Assets | Profitability |
| Gross Margin | Gross Profit / Net Revenue | Profitability |
| Current Ratio | Current Assets / Current Liabilities | Liquidity |
| Quick Ratio | (Current Assets - Inventories) / Current Liabilities | Liquidity |
| Working Capital/Assets | (Current Assets - Current Liabilities) / Total Assets | Liquidity |
| Total Liabilities to Assets | Total Liabilities / Total Assets | Leverage |
| Long-Term Liabilities to Assets | Long-Term Liabilities / Total Assets | Leverage |
| Short-Term Liabilities to Assets | Short-Term Liabilities / Total Assets | Leverage |
| Accounts Payable to Assets | Accounts Payable / Total Assets | Leverage |
| Has Debt | 1 if Total Debt > 0 | Leverage |
| Interest Coverage | EBIT / Financial Expenses | Solvency |
| Asset Turnover | Net Revenue / Total Assets | Activity |
| Payables Turnover | COGS / Accounts Payable | Activity |
| Investment Opportunities | (ΔPPE + Depreciation) / Lagged PPE | Investment Opportunities |
| Firm Size | ln(Total Assets) | Size |

## Financial Distress Proxy
A firm-year observation is classified as financially distressed if **at least two** of the following three criteria are simultaneously satisfied:

- **Criterion 1:** Negative EBITDA (EBITDA < 0)
- **Criterion 2:** Negative total equity (Total Equity < 0)
- **Criterion 3:** Revenue growth is negative and more than 0.5 standard deviations below the industry-year mean

| Criterion | N | Share (%) |
|-----------|---|-----------|
| EBITDA < 0 | 19,850 | 28.2 |
| Total Equity < 0 | 8,976 | 12.8 |
| Revenue Decline | 14,095 | 20.0 |
| **Composite (≥2 of 3)** | **9,670** | **13.7** |

The "at least two" threshold reduces the risk of false positives from relying on a single indicator. Each criterion captures a distinct dimension of financial health: operational profitability, balance sheet solvency, and revenue dynamics. Pairwise phi-coefficients between all three criteria are below 0.4, confirming that the criteria reflect different aspects of financial distress.

## Further Documentation
Full variable construction details are documented in `notebooks/01_data_preprocessing.ipynb`.
