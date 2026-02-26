# 🔥 Regime-Aware Systematic Natural Gas Trading Model

## Overview

This project develops a regime-based systematic trading framework for **Henry Hub Natural Gas futures**.

The model identifies structurally different market environments using:

- Volatility clustering  
- Seasonality-adjusted storage surprises  
- Forward return diagnostics  
- Out-of-sample backtesting with transaction costs  

The objective is not prediction for its own sake — it is to determine whether fundamental stress regimes exhibit exploitable return asymmetry.

---

## Market Context

Natural gas markets are highly regime-dependent.

Periods of:

- Storage tightness  
- Supply disruptions  
- Weather-driven demand spikes  
- Elevated volatility  

often generate nonlinear price behavior.

Rather than fitting a black-box machine learning model, this framework explicitly defines regimes based on:

- **Volatility Stress**
- **Storage Surprise (relative to seasonal norms)**

This allows us to test whether structural stress environments produce persistent directional bias.

---

## Data Used

### 1. Henry Hub Daily Futures Prices

Used to compute:

- Log returns  
- Rolling volatility  
- Forward returns  

### 2. EIA Weekly Natural Gas Storage Data

Used to construct a seasonality-adjusted storage anomaly signal.

All signals are built strictly from information available at the time.

---

## Methodology

### 1️⃣ Storage Anomaly Construction

- Weekly storage change is calculated.
- Seasonal average weekly change is computed using ISO week grouping.
- Storage anomaly = Actual weekly change − Seasonal average.

This isolates unexpected tightness or looseness in supply.

---

### 2️⃣ Feature Engineering

- Daily log returns  
- 20-day rolling volatility  
- 5-day forward return (evaluation only)  
- 5-day momentum (diagnostic feature)  

---

### 3️⃣ Regime Definition

Thresholds:

- Volatility Stress = 75th percentile of rolling volatility  
- Tight Storage = 25th percentile of storage anomaly  
- Loose Storage = 75th percentile of storage anomaly  

Regimes:

**Bullish Stress (Regime = 1)**  
High volatility + negative storage anomaly (unexpected tightness)

**Bearish Stress (Regime = -1)**  
High volatility + positive storage anomaly (unexpected looseness)

**Neutral (Regime = 0)**  
All other conditions

This structure prioritizes interpretability and avoids continuous parameter overfitting.

---

### 4️⃣ Backtesting Framework

Train/Test split:

- Train: Pre-2019  
- Test: 2019 onward  

Signal = Regime  

Strategy return = Lagged signal × daily log return  

Transaction cost = 2 bps per signal change  

Performance metrics:

- Annualized Sharpe Ratio  
- Maximum Drawdown  
- Cumulative Return vs Market  

The strategy is evaluated strictly out-of-sample.

---

## Outputs

- Regime distribution statistics  
- Train vs Test Sharpe ratio  
- Max drawdown comparison  
- Yearly forward return diagnostics by regime  
- Strategy vs market cumulative return visualization  

---

## What This Demonstrates

- Structural understanding of natural gas market dynamics  
- Seasonality-adjusted fundamental modeling  
- Regime-based systematic thinking  
- Proper out-of-sample validation  
- Transaction cost awareness  
- Risk-adjusted evaluation  

The focus is robustness and interpretability rather than curve-fitted performance.

---

## Potential Extensions

- Dynamic threshold calibration  
- Regime transition probability modeling  
- Volatility-targeted position sizing  
- Weather anomaly integration  
- Multi-asset spread extension (e.g., Henry Hub vs global gas benchmarks)  

---

## Author

**Mohit Kumar**  
Energy Quant Research | LNG & Gas Market Modeling
