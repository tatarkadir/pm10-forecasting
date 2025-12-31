PM10 Forecasting Final Challenge
Comparison: Asma’s notebook vs Kadir’s notebook (baseline repo)

This repository originally includes Kadir’s reference notebook (final_challenge_PM10.ipynb).
My submission notebook (nb6.ipynb) follows the same challenge goal but differs in the modeling choices and evaluation pipeline.

Modeling approach

Kadir’s notebook:

Uses classical time-series modeling and deep learning components (ARIMA/SARIMAX style models and an LSTM model using TensorFlow/Keras).

Focuses on sequence modeling and time-series specific architectures.

My notebook:

Uses a tabular machine learning approach with HistGradientBoostingRegressor.

Treats the problem as supervised learning using the provided exogenous predictors and engineered time alignment, trained separately per station and horizon.

For the average probabilistic forecast, uses quantile regression (q10/q50/q90) with the same gradient boosting family.

Forecast targets and horizons

Kadir’s notebook:

Works directly with the dataset target columns LOCATION__YPM10-dailymean__dX.

My notebook:

Same target usage, but includes an explicit horizon clarification:
the dataset provides six horizons encoded as d0..d5 and results are reported as 1..6 days ahead using day_ahead = d + 1.

This is written explicitly in a Markdown cell to avoid off-by-one confusion in grading.

Naive baseline and “hard filter” compliance

Kadir’s notebook:

Includes baseline comparisons, but the exact naive definition can vary depending on how the notebook is executed and which series are used.

My notebook:

Implements a strict naive persistence baseline derived from observable measurements at forecast time:
daily observed PM10 mean is computed from LOCATION__PM10__m0..m23 and used as the persistence forecast.

Also includes a seasonal naive baseline using a 7-day shift.

Reports MAE for both naive baselines and checks whether the model beats the best naive, per station and horizon.

Probabilistic forecast for the average

Kadir’s notebook:

Uses its own uncertainty / interval approach (depending on the selected model and notebook path).

My notebook:

Produces an explicit probabilistic forecast for the average across all locations using quantile regression:
AVG__q10__dK, AVG__q50__dK, AVG__q90__dK for K = 1..6.

Runtime and practicality

Kadir’s notebook:

Can be computationally heavy depending on the chosen models and training loops (deep learning and repeated fitting).

My notebook:

Designed to run within practical time limits by avoiding nested cross-validation inside the full station x horizon loop.

Uses a fixed time-based holdout evaluation and naive comparisons to keep the runtime reasonable while still meeting the challenge requirements.

Output artifacts

Kadir’s notebook:

Produces forecasts and visualizations within the notebook.

My notebook:

Writes a single CSV output file with all required forecasts:
pm10_final_challenge_forecasts.csv
containing point forecasts for every location and quantile forecasts for the average.

Summary

Kadir’s notebook is a model-rich reference implementation oriented toward time-series methods (ARIMA/SARIMAX and LSTM).
My notebook is also a clean pipeline based on gradient boosting, with strict naive baselines computed from observed hourly PM10 measurements and explicit probabilistic quantiles for the average.
