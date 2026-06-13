# 📊 Value at Risk: Normal vs Student-t Distribution

Comparative analysis of risk modeling approaches using AAPL stock returns, examining how distributional assumptions impact Value at Risk (VaR) and Expected Shortfall (ES) estimates.

## 🎯 Objective

This project compares the **Normal distribution** and **Student-t distribution** for modeling daily log-returns of Apple stock, with a focus on:

- Calculating Value at Risk (VaR) at 95% confidence level
- Calculating Expected Shortfall (ES / CVaR)
- Backtesting both models against a crisis period (2008 financial crisis)
- Demonstrating why VaR alone can be misleading, and why ES is a better tail-risk measure sometimes

## 📈 Methodology

1. **Data preparation**: Daily log-returns computed from Apple closing prices
2. 2. **Calibration period** (2006-2007, "calm" period):
   - Estimate mean (μ) and volatility (σ) of log-returns
   - Fit a Normal distribution

3. **Normality check**:
   - Jarque-Bera test for normality
   - QQ-plot to visually inspect tail behavior
   - Kurtosis analysis (excess kurtosis = 4.58 → kurtosis = 7.58, far from 3 → fat tails confirmed)

4. **Student-t calibration**:
   - Fit Student-t distribution (degrees of freedom, location, scale) on the same data
   - Compute VaR95 and ES under Student-t

5. **Backtesting** (2008 crisis period):
   - Count VaR violations under both models
   - Compare violation rates to the theoretical 5% expectation

## 📊 Key Results

| Metric | Normal | Student-t |
|---|---|---|
| VaR 95% | -0.0320 | -0.0307 |
| Expected Shortfall (ES) | -0.04 | -0.16 |
| Kurtosis | 3 (assumed) | 7.58 (fitted) |

### 🔍 Main Finding

At the **95% threshold**, both distributions give nearly identical VaR estimates — the Student-t model doesn't appear more conservative here. **However**, the Expected Shortfall reveals a dramatic difference: the Student-t ES is **4x more severe** than the Normal ES.

**Interpretation**: The Student-t's fatter tails only become dominant *beyond* the 95% quantile. This means:
- VaR95 backtesting alone is **insufficient** to detect tail risk differences between models
- **Expected Shortfall** (or VaR99) is needed to reveal the true risk captured by fat-tailed distributions
- This empirically illustrates why **Basel III / FRTB** shifted regulatory capital requirements from VaR to Expected Shortfall

## 🛠️ Technologies

- Python 3
- pandas, numpy
- scipy.stats (norm, t, jarque_bera)
- matplotlib

## 📁 Project Structure
## 📚 Concepts Covered

- Log-returns and their statistical properties
- Value at Risk (VaR) — parametric approach (Normal & Student-t)
- Expected Shortfall (ES / CVaR)
- Distribution fitting (`scipy.stats.t.fit`)
- Normality testing (Jarque-Bera, QQ-plots, kurtosis)
- VaR backtesting / violation rate analysis
- Limitations of VaR vs ES as risk measures

## 📝 Possible Extensions

- Kupiec test for formal backtest validation
- GARCH model for time-varying volatility
- Multi-asset comparison
- Rolling-window calibration to avoid regime-change bias

## 👤 Author

ABDEL MOUSSA, aspiring Quantitative Analyst

---

*This project was developed as part of a personal initiative to explore quantitative risk management concepts.*
