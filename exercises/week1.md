## Week 1 - exercises

Exercise 0 helps you set up a repository to use for exercises - we strongly recommend to complete his exercise.

### 0. Getting set up

Set up a GitHub repository for your exercise code.

Following settings are recommended:

* private repository
* gitignore for python code
* invite the four instructors to the repo with read access: `felipeangelimvieira`, `fkiraly`, `mtorabirad`, `garve`
* keep track of your python environment by using a `requirements.txt` (or environment manager specific file)
* create a new folder for each week, e.g., `week1`. We suggest using jupyter notebooks for the exercises.

Instructors will leave reviews as issues, so ensure that issues are activated in your repository.

Note: for setting up environments, you can use the requirements file from this repo.

### 1. Hello World

a. Load the airline dataset, fit the following models on the entire dataset, and make a forecast for 36 months:

* naive carry-forward
* a naive seasonal forecast with seasonality 12
* a naive seasonal forecast with seasonality 8

b. Plot the three forecasts together with the historical data - using `sktime` utilities or `matplotlib` directly.

Discuss whether it is sensible to assume a seasonality "12".


### 2. Basic time series exploratory analysis

In the "single time series" setting, it is advised to check time series for the following phenomena:

* seasonality - patterns repeated with periodicity
* presence of trend, absence of (weak) stationarity

If these are present, direct application of many models may fail or lead to sub-par results.

Perform a "classical" EDA (exploratory data analysis) on the airline dataset:

a. carry out ADS and KPSS tests for stationarity. These are also available in `statsmodels`

b. plot ACF and PACF to check for seasonality with a visual assisted, semi-quantitative method. You can use `pacf` from `statsmodels`. Important: ACF and PACF assume weak stationarity, hence the series needs to be stationary first before applying these. You can use `np.diff` to stationarize via differencing.


Does the time series exhibit seasonality or trend?


### 3. Dealing with trend and non-stationarity

Detrending and differencing are two common choices to ensure a time series is closer to (weakly) stationary - that is, in the regime that most forecasting algorithms assume. These are available as:"

* `Differencer`, requiring a choice of differencing order
* `Detrender`, requiring a choice of regression algorithm to detrend with

Build two forecasting pipelines with the `NaiveForecaster` (seasonality = 12), one using differencing only, one using detrending only.

Plot the two forecasts obtained from the above.


### 4. Auto-Seasonality - classical

The process of inspecting ACF and deriving seasonality can be automated using `sktime`,
by using the `PluginParamsForecaster` with `SeasonalityACF`.

Look at the docstring of `PluginParamsForecaster` and replicate the example to obtain
an auto-seasonality `NaiveForecaster`.

Recall from above:

* stationarization (e.g., differencing) has to be applied before estimating ACF
* stationarization should be carried out before most forecasters

Check different ways to "bracket" the auto-seasonality estimator and differencer.

How should the estimator be defined to ensure differencing happens to the data
passed to the seasonality estimator, and to the data passed to the forecaster?

Explore different options and plot the forecasts.


### 5. Auto-seasonality - machine learning

As an alternative, use `ForecastingGridSearchCV` to create a variant of the
seasonal naive estimator
that estimates the seasonality of the data using grid search.

Again, ensure that differencing happens before forecasting.

Where should the differencer be in the pipeline - inside or outside the grid search?


### 6. Benchmarking

Using `ForecastingBenchmark`, run a backtest on the airline data which includes:

* the auto-seasonal naive forecaster using `SeasonalityACF` - classical method
* the auto-seasonal naive forecaster using `ForecastingGridSearchCV` - ML method
* the seasonal naive forecaster with seasonality set to 12
* a direct reduction algorithm using linear regression after differencing (as shown in the workshops)
* a direct reduction algorithm using linear regression after differencing, and where you tune the window size via grid search.

Run a sensible backtest scenario using, e.g., expanding splitter or expanding greedy splitter; and a reasonable point prediction metric.

Inspect results. Check which seasonality was selected in the auto-seasonal forecaster(s).

Which forecasting algorithm out of the above would you consider "best" for this data? Why?


### 7. Benchmarking, part 2

Look at the shampoo dataset, from `load_shampoo_sales` in `sktime.datasets`.

a. carry out EDA, as in exercise 2 above.

b. run the benchmarking experiment, as in exercise 6, on the shampoo sales data.

Report and interpret your findings.

How does this compare to the airline dataset?


### 8. Mini-project

The folder `week1_data` contains (synthetic, stylized) sales data:

* `y.csv` contains sales value, per day, for 2020-2022.
* `X.csv` contains data on marketing (integer) and discounts (float), larger means more spend on one or the other.

Use what you have learnt to develop a "good" forecasting model.

* handling seasonality, trend
* using exogenous data
* calendar or seasonality features
* feature extraction
* benchmarking to reliably compare approaches

The (imaginary) stakeholders say that "good" means being able to forecast one month ahead of daily sales,
based on planned marketing spend and historical data, on the last of the previous month,
measured by arithmetic average of MAPE.

The discount spend is not known in advance, but the marketing spend is.

The model, if possible, should be simple and explainable, while performing well.

If there is a trade-off between performance and explainability, you can provide multiple models across the trade-off spectrum.
