# ACCT653_FFA_Forecasting_Project
FFA Group Project: Forecasting quarterly nominal GDP growth rate in the US using python


### Directories

**Data Folder**
--| data/compustat_quarterly_financials.csv (not in use)

--| data/compustat_quarterly_financials2.csv (not in use)

--| data/crsp_snp500_indexes.csv (not in use)

--| data/GDP_Forecast_sampleSubmission.csv (for reference)

--| data/GDP_Forecast_test.csv (IN USE)

--| data/GDP_Forecast_train.csv (IN USE)

--| data/GDP_PCA_for_test.csv (IN USE for validation)

--| data/HOUST_PCA.csv (not in use)

--| data/INDPRO_PC1.csv

--| data/INDPRO_PCA.csv (IN USE)

--| data/UNRATE_CH1.csv

--| data/UNRATE_PCA.csv (IN USE)


**Reference Folder**: only for developer's reference

**Files**
--| .gitignore

--| README.md

--| main.ipynb

--| draft.ipynb (co-lead's main file)

--| reference.ipynb

--| ref_to_be_deleted.ipynb


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