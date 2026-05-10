# Assessing Gann Square Effectiveness in Machine Learning-Based Stock Predictions

## Overview
A thesis exploring whether W.D. Gann's century-old geometric trading methods can enhance modern machine learning models for stock market prediction and trading.

This research investigates whether Gann's methods, often compared to "financial horoscopes," can provide valuable signals when integrated with modern machine learning (LSTM) and reinforcement learning (DQN) approaches.

## W.D. Gann's Core Premises
*   **Price, time, and pattern** are key factors in market behavior.
*   **Markets move in repeating cycles.**
*   **Price movements exhibit geometric relationships.**

### Key Gann Concepts Utilized:
*   **Square of Nine:** A numerical spiral chart creating geometric alignments, used to derive support and resistance levels that could act as future turning points.
*   **Gann Angles:** Straight lines drawn on price-time charts at specific fixed slopes (1×1, 2×1, etc.) that separate price action into zones of trend strength and provide continuous support/resistance references.
*   **Time Cycles:** Specific durations that often precede market reversals.

## Research Questions
1.  **Prediction Accuracy:** Can models augmented with multiple Gann-based features outperform standard machine learning models in terms of error metrics (RMSE, MAE, MAPE)?
2.  **Comparison with Technical Indicators:** Do Gann Square-derived support and resistance levels improve prediction accuracy over traditional technical indicators?
3.  **Trading Performance:** Does including Gann Square of Nine support/resistance levels as features improve the trading performance of a trading agent relative to a baseline agent using only price data?
4.  **Technical Indicators vs. Gann Features:** How does adding standard technical indicators affect the performance of trading agents compared to Gann-based features?
5.  **Gann Angle Enhancement:** Does incorporating Gann angle features further enhance agent performance beyond the Gann Square features?

## Data and Preprocessing
*   **Data Sources:** Daily OHLCV data from Yahoo Finance (2011-2023) for Microsoft (MSFT), Apple (AAPL), Google (GOOG), and Nifty 50 (NSEI).
*   **Preprocessing Steps:**
    *   Normalization using Min-Max scaling.
    *   21-day sliding windows for LSTM inputs.
    *   Chronological splitting (Training: 70%, Validation: 15%, Testing: 15%).
*   **Gann-Derived Features:**
    *   *Gann Square of Nine:* Resistance = (√P + 1)² | Support = (√P - 1)² (Where P is previous day's closing price)
    *   *Gann Angles:* LSTM uses 100-day rolling low as pivot; DQN uses dynamic pivot-based swing highs/lows.

## Methodology

### LSTM for Prediction
Long Short-Term Memory (LSTM) networks were used to forecast next-day closing prices using 21-day sliding windows of historical data.
*   **Baseline:** Raw OHLC (Open, High, Low, Close) values.
*   **Gann Square:** OHLC with support and resistance levels from Square of Nine.

### DQN for Trading
Deep Q-Network (DQN) reinforcement learning agents were deployed to make buy/sell/hold decisions and maximize returns.
*   **Technical Indicators:** OHLC with RSI, MACD, moving averages, and ATR.
*   **Gann Angle:** OHLC with angle-based features recalculated using rolling lookback.

## Key Findings

### LSTM Prediction Results
The baseline OHLC models consistently achieved the lowest errors. Adding technical indicators or Gann features generally degraded predictive performance. This suggests that Gann-derived features do not improve predictive accuracy for exact price forecasting.
*   **OHLC (Baseline):** Lowest RMSE (6.64) and MAE (5.20).
*   **OHLC + Gann Square/Angle:** Higher error rates.

### DQN Trading Results
Unlike prediction tasks, **Gann-based features significantly improved trading outcomes**.
*   **Baseline Win Rate:** 44.3% (OHLC-only agent)
*   **Gann Square Win Rate:** 50.3% (Highest win percentage)
*   **Gann Angle Return:** 59.6% (Best overall performance)

### Discussion: Why the Difference?
*   Gann features weren't designed to predict exact prices; they are geometric rather than statistical.
*   Reinforcement learning optimizes for decision-making, not prediction accuracy. Gann features highlight potential reversal zones, offering situational value for identifying potential turning points.
*   What fails as a predictor can succeed as a decision-support signal.

## Limitations and Future Work
**Limitations:**
*   Limited dataset scope (only 4 stocks).
*   Daily data only (no intraday testing).
*   Lightweight model architectures and basic evaluation metrics.

**Future Work:**
*   Expand to more stocks and asset classes.
*   Test with intraday/minute-level data.
*   Explore more sophisticated architectures.
*   Include risk-adjusted performance metrics.