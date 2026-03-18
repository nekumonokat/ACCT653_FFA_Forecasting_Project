# ACCT653_FFA_Forecasting_Project
FFA Group Project: Forecasting quarterly nominal GDP growth rate in the US using python


### Directories

**Data Folder**

--| data/compustat_quarterly_financials.csv (IN USE)

--| data/compustat_quarterly_financials2.csv (not in use)

--| data/GDP_Forecast_test.csv (IN USE)

--| data/GDP_Forecast_train.csv (IN USE)

--| data/GDP_PCA_for_test.csv (IN USE for validation)

--| data/INDPRO_PC1.csv (IN USE)

--| data/UNRATE_CH1.csv (IN USE)


**Reference Folder**: only for developer's reference

**Files**

--| .gitignore

--| README.md

--| main.ipynb

--| draft.ipynb (co-lead's main file)

--| reference.ipynb


### Data


### Notes

- We are currently using *compustat_quarterly_financials2* for accounting data, *compustat_quarterly_financials* only had assets, liabilities and net income.
- We are using *GDP_PCA_for_test* which is not accurate, but close enough data to the 2015 - 2020 NGDP data used in Kaggle. This is so we can have a better estimate of our RMSE to prevent us from needing to reupload our output to Kaggle when testing.
- Original *main.ipynb* has been modified to *reference.ipynb* to modify structure. *draft.ipynb* is the co-lead's main working file, to be compiled and finalised in *main.ipynb*.
- *main.ipynb* will always be the most updated code file


### PROGRESS

**INCORRECT, REDONE IN DIFFERENT METHOD**

`formula5 = "NGDP ~ year + revtq_lag + xrdq_growth_lag + invtq + ppentq + oibdpq"`
`formula6 = "NGDP ~ year + revtq_lag + xrdq_growth_lag + invtq + ppentq + oibdpq_lag"`

^ Same Kaggle score, but based on:
- Chisq test: `formula5` performs better
- RMSE score: `formula6` performs better
- Adj. R^2: `formula5` performs better

Tested Lasso, Ridge and ElasticNet on accounting macro, recognised `ppentq_lag` and `xrdq_lag` as strong consistent signals, but noted that regression performance not strong, suggesting accounting macro is insufficient as a standalone predictor of Nominal GDP Growth.

**BASE MODEL**:
- trained model using `NGDP_lag1`
- conducted recursive forecasting on the test set - calculated RMSE and MAE
- validated base model's performance against `GDP_PCA`

**MODEL WITH NON-FINANCIAL EXTERNAL INDICATORS**:
- created indicators for `indpro` and `unrate`
- trained model using `NGDP_lag1`, `INDPRO_PC1`, `INDPRO_lag1`, `UNRATE_change`, and `UNRATE_spike`
- conducted recursive forecasting on the test set, validate performance against `GDP_PCA`
- define stress flags for `UNRATE_change` to capture extra penalty for spikes in unemployment rate
- conducted recursive forecasting on the test set, validate performance against `GDP_PCA`
- trained ML models: `Ridge`, `Random Forest`, `XGBoost` and designed ensemble model using stress flags
- conducted recursive forecasting on the test set, validate performance against `GDP_PCA`
- trained ensemble model with COVID-19 adjustments: used BEA data on GDP collapse and recovery bounce to offset spikes
- conducted recursive forecasting on the test set, validate performance against `GDP_PCA`

**MODEL WITH NON-FINANCIAL + FINANCIAL EXTERNAL INDICATORS**:
- created indicators for `invtq`, `oibdpq`, `ppentq`, `revtq` and `xrdq`
- trained ensemble model using NON-FINANCIAL macro and `corp_profit_growth_lag1`, `corp_revenue_growth_lag1`, `corp_capital_growth_lag1` and `corp_inventory_growth_lag1` with COVID-19 adjustments
- conducted recursive forecasting on the test set, validate performance against `GDP_PCA`