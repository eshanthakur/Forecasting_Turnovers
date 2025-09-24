## Retail Assignment — Time Series Forecasting (ABS Retail Turnover)
Forecasting Australian retail turnover for a single ABS series.  
We compare **ETS (M,A,A)** with **ARIMA(1,0,1)(0,1,2)** (on a Box–Cox–transformed series with seasonal differencing), evaluate out-of-sample accuracy, run residual diagnostics, and produce 24-month forecasts with prediction intervals.

## Full Report

[Retail Assignment knit file.pdf](https://github.com/user-attachments/files/22517783/Retail.Assignment.knit.file.pdf)

## Data
- **Source:** ABS Retail Trade (via `fpp3::aus_retail`).
- **Series selection:** One valid `Series ID` is sampled **reproducibly** using a fixed seed.
- **Frequency:** Monthly.
- **Units:** Turnover in millions of dollars.

## Quick start
1. **Install** R (≥ 4.2) and RStudio.
2. **Packages:**
   ```r
   install.packages(c("fpp3","readabs","sessioninfo"))

## Methods (one-pager)
**Pre-processing**
Drop discontinued ABS series.
Fix random seed; sample one Series ID.
**Transform & stationarity**
Box–Cox lambda via Guerrero.
Seasonal differencing (lag 12) if required; KPSS to confirm.
**Model candidates**
ETS: automatic; ETS(M,A,A); ETS(A,A,A) on original scale.
ARIMA: stepwise & full search on Box–Cox scale; plus hand-picked seasonal specs.
**Model selection**
Compare AICc, residual diagnostics (Ljung–Box), and out-of-sample (2017–2018) accuracy (RMSE).
**Forecast**
24-month horizon with 80% prediction intervals.
Optional comparison to actual ABS updates via readabs.

## Results (highlights)
**Trend & seasonality**
Clear upward trend and strong December peaks.
**Seasonality by month**
Consistent pattern; validates using seasonal terms.
**Subseries view**
Within-month trends increasing over years.
**Out-of-sample performance (2017–2018)**. 
Both models capture seasonality;
ARIMA(1,0,1)(0,1,2) slightly lower RMSE in our run.
**Residual diagnostics (finalists).**
ARIMA passes Ljung–Box; ETS shows mild autocorrelation.

**Notes & limitations**
readabs::read_abs() requires internet and the ABS endpoint to be available.
COVID-era structural breaks degrade forecast accuracy for 2020 vs. pre-2020 behavior.
Results can vary with the sampled Series ID; the seed ensures reproducibility.

**References**
Hyndman, R.J., & Athanasopoulos, G. (2021). Forecasting: Principles and Practice (3e). OTexts.
R packages: fpp3, tsibble, fable, feasts, readabs.

