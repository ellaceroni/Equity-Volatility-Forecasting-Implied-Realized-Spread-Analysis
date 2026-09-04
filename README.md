# Equity Volatility Forecasting & Implied-Realized Spread Analysis

Python analysis of SPY option pricing and S&P 500 volatility. The project implements Black-Scholes implied volatility and Greeks, forecasts 21-day realized volatility with linear, Ridge, Lasso, and Random Forest models, and analyzes the VIX minus realized volatility spread.

## Overview

The project has two parts.

The first uses current SPY option data to study implied volatility across strikes and maturities. Black-Scholes prices and Greeks are implemented directly in Python, and implied volatility is recovered numerically from market prices.

The second uses historical VIX and S&P 500 data to study realized volatility. It tests whether VIX tends to exceed subsequent realized volatility, builds out-of-sample forecasts of 21-day realized volatility, and compares those forecasts with VIX.

## 1. Option Pricing and Implied Volatility

The option pricing section:

- Implements Black-Scholes call pricing.
- Calculates Delta, Gamma, and Vega.
- Recovers implied volatility with numerical root finding.
- Uses short-term Treasury yields as a proxy for the risk-free rate curve.
- Estimates forward prices from near-ATM call and put prices.
- Examines implied volatility across strikes and maturities using forward log-moneyness.

SPY options are American-style, while Black-Scholes and the put-call parity formula used here are European. These are treated as approximations.

## 2. Greeks and Delta Hedging

For a near-ATM SPY option with approximately 30 days to expiration, the project:

- Calculates Delta, Gamma, and Vega.
- Simulates an underlying price path using geometric Brownian motion.
- Recalculates Delta through time.
- Illustrates how a delta hedge changes as the underlying price and time to expiration change.

## 3. Historical Implied and Realized Volatility

VIX is compared with annualized S&P 500 volatility realized over the following 21 trading days.

The analysis includes:

- Summary statistics for VIX and future realized volatility.
- The average VIX minus realized-volatility spread.
- HAC-robust inference for the mean spread.
- A regression of future realized volatility on VIX.
- Comparison of the implied-realized spread across VIX regimes.

## 4. Realized Volatility Forecasting

The forecasting section uses market information available at each date to predict S&P 500 realized volatility over the next 21 trading days.

Features include:

- VIX.
- Realized volatility over 5, 21, and 63 trading days.
- Downside realized volatility.
- Recent S&P 500 returns.
- Recent market drawdown.
- Recent changes in VIX.
- Variation in VIX.

The models are:

- Linear Regression.
- Ridge Regression.
- Lasso Regression.
- Random Forest.

Models are evaluated using expanding-window out-of-sample testing. A 21-day gap is used between training and test periods to avoid overlap between forward realized volatility labels and the test sample.

Performance is compared using RMSE, MAE, out-of-sample R², and mean squared error relative to VIX.

## 5. Model Interpretation and Regime Analysis

Forecast performance is evaluated across four VIX regimes.

Ridge and Lasso coefficients are also used to examine which variables contribute most to the forecasts. Random Forest feature importance provides a nonlinear comparison.

## 6. Implied-Realized Spread Forecast

Because VIX is known at the forecast date, the realized volatility forecast can be converted into a forecast of the future spread:

\[
\text{Predicted Spread} = \text{VIX} - \widehat{\text{Future Realized Volatility}}
\]

The predicted spread is compared with the spread that is subsequently realized. Observations are also grouped into quintiles to test whether larger predicted spreads are followed by larger realized spreads.

## Key Findings

- SPY option prices show clear variation in implied volatility across strikes and maturities.
- VIX historically exceeds subsequent 21-day S&P 500 realized volatility on most observations.
- The average implied-realized volatility spread is positive and statistically significant.
- VIX contains useful information about future realized volatility.
- Ridge and Lasso provide the strongest out-of-sample forecasts.
- The regularized linear models reduce mean squared forecast error by about 16% relative to using VIX alone.
- The models outperform VIX across all four volatility regimes.
- Current implied volatility, recent realized volatility, and recent market drawdowns contain the most useful forecasting information.
- The highest predicted spread groups subsequently experience materially larger VIX minus realized volatility spreads than the lower groups.

## Data

- SPY option chains from Yahoo Finance.
- S&P 500 Index (`^GSPC`) from Yahoo Finance.
- VIX Index (`^VIX`) from Yahoo Finance.
- U.S. Treasury yields from FRED.

The historical analysis uses data from January 2010 through September 4, 2026.

## File

`Equity_Volatility_Forecasting_&_Implied_Realized_Spread_Analysis.ipynb`
