# Airline Passenger Time Series Analysis

Time series analysis of the classic AirPassengers dataset (monthly airline passengers, 1949-1960): rolling statistics, Augmented Dickey-Fuller (ADF) stationarity tests, and log transformation with differencing, as preparation for forecasting.

## Scenario
The goal is to understand passenger traffic trends and seasonality, and to assess whether the data is suitable for forecasting. Many forecasting models require a stationary series, so the analysis tests for stationarity and applies transformations when it is missing.

## Contents

| File | Description |
|---|---|
| `CG_C09_M03.ipynb` | Jupyter notebook with the full analysis |
| `AirPassengers.csv` | Monthly passenger counts (`time`, `value`) |

## Analysis Steps

0. Load the dataset
1. Convert the decimal-year `time` column to datetime, set `Month` as the index, and rename `value` to `Passengers`
2. Compute 12-month rolling mean and standard deviation
3. Run the Augmented Dickey-Fuller test (ADF statistic)
4. Check the p-value
5. Compare the ADF statistic with the critical values
6. Apply log transformation and first-order differencing
7. Run the ADF test again on the differenced data (statistic)
8. Check the p-value after differencing
9. Compare the ADF statistic with the critical values after differencing

## Key Findings

| | Original series | Log + first difference |
|---|---|---|
| ADF statistic | 0.8154 | -2.7171 |
| p-value | 0.9919 | 0.0711 |
| Critical values (1% / 5% / 10%) | -3.4817 / -2.8840 / -2.5788 | -3.4825 / -2.8844 / -2.5790 |

- The original series has a clear upward trend and seasonal swings that grow over time. The rolling mean and standard deviation both increase, and the ADF test fails to reject the unit root (p = 0.9919), so the series is **non-stationary**.
- After log transformation and first differencing, the series is stationary at the 10% level (p = 0.0711) but not at the 5% level.
- The remaining seasonality (12-month period) is the likely cause. A seasonal difference (lag 12) would be the next step before fitting a model such as SARIMA.

## Notes

- The `time` column is kept in the DataFrame after setting `Month` as the index