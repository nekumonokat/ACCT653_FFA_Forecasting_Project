# ACCT653_FFA_Forecasting_Project
FFA Group Project: Forecasting quarterly nominal GDP growth rate in the US using python


### Directories

**Data Folder**
--| data/compustat_quarterly_financials.csv (not in use)
--| data/compustat_quarterly_financials2.csv
--| data/crsp_snp500_indexes.csv
--| data/GDP_Forecast_sampleSubmission.csv (for reference)
--| data/GDP_Forecast_test.csv (not in use)
--| data/GDP_Forecast_train.csv
--| data/GDP_PCA_for_test.csv

**Reference Folder**: only for developer's reference

**Files**
--| .gitignore
--| README.md
--| forecasting_gdp_old.ipynb
--| forecasting_gdp2_old.ipynb
--| forecasting_gdp3_old.ipynb
--| main.ipynb


### Data


### Notes

- We are currently using *compustat_quarterly_financials2* for accounting data, *compustat_quarterly_financials* only had assets, liabilities and net income.
- We are using *GDP_PCA_for_test* which is not accurate, but close enough data to the 2015 - 2020 NGDP data used in Kaggle. This is so we can have a better estimate of our RMSE to prevent us from needing to reupload our output to Kaggle when testing.
- *main.ipynb* will always be the most updated code file


### PROGRESS

`formula5 = "NGDP ~ year + revtq_lag + xrdq_growth_lag + invtq + ppentq + oibdpq"`
`formula6 = "NGDP ~ year + revtq_lag + xrdq_growth_lag + invtq + ppentq + oibdpq_lag"`

^ Same Kaggle score, but based on:
- Chisq test: `formula5` performs better
- RMSE score: `formula6` performs better
- Adj. R^2: `formula5` performs better

Tested Lasso, Ridge and ElasticNet on accounting macro, recognised `ppentq_lag` and `xrdq_lag` as strong consistent signals, but noted that regression performance not strong, suggesting accounting macro is insufficient as a standalone predictor of Nominal GDP Growth.