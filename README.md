# Electricity Merit Order and Price Analysis
### Data Analytics Project | Python

Data analytics project examining electricity price formation, merit order dynamics, and the impact of the 2022 European energy crisis using Python.

---

## Table of Contents

- [Overview](#overview)
- [Business Problem](#business-problem)
- [Dataset](#dataset)
- [Tools and Technologies](#tools-and-technologies)
- [Project Structure](#project-structure)
- [Data Preparation and Feature Engineering](#data-preparation-and-feature-engineering)
- [Analysis](#analysis)
- [Key Findings](#key-findings)
- [How to Run This Project](#how-to-run-this-project)
- [Recommendations](#recommendations)
- [Author and Contact](#author-and-contact)

---

## Overview

This project analyses how wholesale electricity prices are determined in the German power market using 10 years of synthetic European 3-hourly electricity market data (2015-2024). The analysis focuses on the Merit Order mechanism - the pricing framework through which power plants are dispatched from lowest to highest marginal cost, with the final plant required to meet demand setting the market clearing price for all generators that hour.

The study covers 2015-2024 with particular focus on the 2022 European gas crisis - a period of extreme volatility following Russia's invasion of Ukraine, during which wholesale electricity prices rose 26.6x above pre-crisis levels.

---

## Business Problem

How are wholesale electricity prices determined in a liberalised power market, and how did the 2022 gas supply crisis transmit into electricity prices through the merit order mechanism?

This project aims to:

- Understand how the merit order mechanism determines wholesale electricity prices
- Quantify how the 2022 gas crisis transmitted into electricity prices
- Analyse the relationship between renewable share and wholesale prices
- Examine how price patterns by hour and month changed across market regimes
- Model the price impact of a 50% increase in wind capacity

---

## Dataset

- Source: Kaggle - European Power Markets 2015-2024 - Synthetic Merit Order Dataset
- Total Observations: 29,217 (Germany only - filtered from 146,082)
- Interval: 3-hourly snapshots across 10 years (8 readings per day)
- Year Range: 2015 to 2024
- Zero missing values across all analytical columns

| File | Rows | Purpose | Used |
|---|---|---|---|
| generation_mix.csv | 146,082 | Generation by fuel type per timestep | Yes |
| power_prices.csv | 146,085 | Wholesale price, demand, negative price flag | Yes |
| commodity_prices.csv | 3,653 | Daily gas, coal, and carbon permit prices | Yes |
| demand_features.csv | - | Daily demand with temperature features | No |
| price_zones.csv | - | Zone metadata for all 5 countries | No |

---

## Tools and Technologies

- Python (Pandas, Matplotlib, NumPy)
- Jupyter Notebook
- GitHub

---

## Project Structure

```
electricity-merit-order-analysis-python/
│
├── README.md
├── electricity_merit_order_analysis.ipynb
├── electricity_merit_order_report.pdf
└── data/
    ├── generation_mix.csv
    ├── power_prices.csv
    ├── commodity_prices.csv
    ├── demand_features.csv
    └── price_zones.csv
```

---

## Data Preparation and Feature Engineering

- Filtered all datasets to Germany (DE) only - reducing from 146,082 rows to 29,217
- Merged generation_mix and power_prices on datetime using inner join
- Merged commodity_prices onto master table using left join on date - daily prices applied across all 8 intraday readings
- Engineered marginal cost columns for gas and coal using standard power market parameters:
  - Gas marginal cost = gas price divided by 0.50 thermal efficiency plus 0.20 carbon emission factor
  - Coal marginal cost = coal price divided by 8.0 MWh per tonne converted to EUR plus 0.85 carbon emission factor
  - Wind and solar assigned 0 EUR/MWh marginal cost
  - Nuclear assigned 5 EUR/MWh and hydro 2 EUR/MWh

---

## Analysis

5 structured analytical questions answered using Python:

- Q1: Merit order supply stack for a representative winter hour
- Q2: How the 2022 gas crisis reshaped the supply stack vs normal years
- Q3: Does higher renewable share reduce wholesale prices
- Q4: How price patterns by hour and month changed across three market regimes
- Q5: What would 50% more wind capacity do to 2024 wholesale prices

---

## Key Findings

- 2022 annual median electricity price was 310.9 EUR/MWh - 26.6x above the 2019-2020 pre-crisis median of 11.7 EUR/MWh
- Gas prices rose 12x from 2019 baseline (21.9 EUR/MWh) to 2022 (269.6 EUR/MWh) - the merit order amplified this into a 26.6x electricity price increase
- Gas marginal cost peaked at 552 EUR/MWh in 2022 vs 46 EUR/MWh in 2019
- Within any single year higher renewable share correlates with lower prices - the merit order effect of renewables is confirmed
- In 2022 even hours with 60-70% renewable share had elevated prices - commodity price shocks dominated the renewable merit order effect
- Negative price hours peaked at 144 in 2018 and fell to exactly zero in both 2022 and 2023 - crisis-level gas prices made every MWh too valuable to curtail
- Post-crisis price floor in 2024 settled at 38.6 EUR/MWh - 3.3x above pre-crisis - driven by EU carbon price remaining structurally elevated at 57 EUR/tCO2
- 50% more wind capacity reduces average 2024 prices by 10.2 EUR/MWh - equivalent to approximately 5.1 billion EUR in annual consumer savings

---

## How to Run This Project

1. Clone the repository:

```
git clone https://github.com/manshasinha/electricity-merit-order-analysis-python
```

2. Install required libraries:

```
pip install pandas matplotlib numpy jupyter
```

3. Add dataset files to the data folder:

```
Place all 5 CSV files from the Kaggle dataset into the data/ folder
```

4. Open and run the notebook:

```
Open electricity_merit_order_analysis.ipynb in Jupyter Notebook
Run all cells sequentially
```

---

## Recommendations

- **Energy Security:** Renewable capacity alone may not fully protect electricity markets from commodity price shocks in the short run; complementary measures such as gas storage and demand flexibility remain important
- **Storage Investment:** As renewable penetration increases beyond levels modelled here additional storage capacity may be required to manage surplus generation and maintain system flexibility
- **Renewable Project Economics:** The post-crisis price floor of 38.6 EUR/MWh provides significantly stronger project economics for new renewable assets compared to the pre-crisis floor of 11.7 EUR/MWh
- **Price Forecasting:** Gas price forecasting dominates renewable share analysis for near-term electricity price prediction - any model excluding commodity price dynamics will systematically underperform during supply disruption scenarios

---

## Author and Contact

Mansha Sinha
Analyst

Email: manshasinha3110@gmail.com
LinkedIn: https://www.linkedin.com/in/mansha-sinha-9504a0214
