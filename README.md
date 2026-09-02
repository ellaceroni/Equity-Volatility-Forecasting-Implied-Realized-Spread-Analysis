# Equity Options Pricing & Volatility Analysis

Python analysis of equity option pricing, implied volatility, option Greeks, delta hedging, and the historical relationship between implied and realized volatility.

## Overview

This project examines equity volatility from both an option pricing and empirical perspective. The first section uses current SPY option data to estimate implied volatility across strikes and maturities. Black-Scholes prices and Greeks are implemented directly in Python, with implied volatility recovered numerically from observed option prices. The second section examines the historical relationship between VIX and subsequent S&P 500 realized volatility. The analysis tests whether implied volatility tends to exceed realized volatility and whether VIX contains information about future volatility.

## Methodology

### Option Pricing and Implied Volatility

- Implement Black-Scholes call pricing and analytical Delta, Gamma, and Vega.
- Recover implied volatility using numerical root finding.
- Use Treasury yields across short maturities as a proxy for the risk free rate curve.
- Estimate forward prices from near-ATM call-put pairs.
- Analyze implied volatility across strikes and expirations using forward log-moneyness.

SPY options are American-style, while the Black-Scholes and put-call parity frameworks used here are European. These models are therefore treated as approximations.

### Greeks and Delta Hedging

For a near-ATM option with approximately 30 days to expiration:

- Calculate Delta, Gamma, and Vega.
- Simulate an underlying price path using geometric Brownian motion.
- Recalculate Delta through time to illustrate the mechanics of dynamic delta hedging.

### Implied vs. Realized Volatility

Historical VIX data are compared with annualized S&P 500 volatility realized over the subsequent 21 trading days.

The analysis includes summary statistics for implied and realized volatility, the average implied-realized volatility spread, HAC-robust inference for the mean spread, a regression of future realized volatility on current implied volatility, and a comparison of implied and realized volatility across VIX regimes.

## Key Findings

- SPY option prices exhibit substantial variation in implied volatility across strikes and maturities, including a clear downside volatility skew.
- VIX has historically tended to exceed volatility subsequently realized by the S&P 500.
- The average implied-realized volatility spread is statistically significant using HAC standard errors.
- VIX is also significantly associated with subsequent realized volatility, indicating that implied volatility contains information about future market risk.
- The absolute implied-realized volatility gap tends to be larger during higher-volatility regimes.

These results show that implied volatility can contain useful information about future volatility while also tending to exceed subsequently realized volatility.
## File

`Equity_Options_Pricing_Volatility_Analysis.ipynb`
