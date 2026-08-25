# GARCH Volatility Modeling of Bitcoin

Solo project — Time Series Analysis (1MS014), Uppsala University, May 2026

## Overview
Bitcoin's daily USD closing price shows clear volatility clustering: calm periods followed by turbulent ones. This project fits a GARCH(1,1) model with Student-t innovations to 13 years of Bitcoin log-returns (April 2013 – May 2026, 4,763 daily observations) to capture and forecast this volatility.

## Method

- Log-returns computed as r_t = log(P_t) − log(P_{t-1})
- Confirmed volatility clustering via ACF/PACF of squared returns and Ljung-Box tests (p < 10⁻⁷¹ at lag 5 on squared returns)
- Fit GARCH(1,1) with a constant mean and Student-t distributed errors via maximum likelihood (train: 4,642 obs, test: 120 obs)
- Validated residuals via ACF and Ljung-Box tests on standardized residuals
- Produced a rolling one-step-ahead volatility forecast over the test period

## Key results

| Parameter | Estimate | p-value |
|---|---|---|
| μ (mean) | 0.1228 | 3.6×10⁻⁵ |
| ω | 0.2999 | 3.0×10⁻³ |
| α | 0.1300 | 5.1×10⁻¹⁸ |
| β | 0.8700 | ≈0 |
| ν (t-dist tails) | 3.12 | <10⁻¹⁷⁰ |

- Log-likelihood: −11,633.3
- Low ν (3.12) confirms Bitcoin's fat-tailed, extreme-move behavior — a Student-t distribution outperforms a normal assumption
- Post-fit residual diagnostics show no remaining autocorrelation in squared residuals — the GARCH structure captures the volatility dynamics
- Rolling forecasts responded appropriately to volatility spikes (e.g. a +15% single-day move in Feb 2026), consistent with known GARCH behavior: it can't predict a shock but adapts quickly once one occurs

## Report

Full writeup with figures and derivations: `Time_Series_Analysis_Project.pdf`
