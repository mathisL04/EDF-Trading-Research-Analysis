# 📈 Correlation Between Day-Ahead (DA) Prices and Gas Peaker Costs

> A quantitative research framework to analyze and exploit price spreads in short-term power trading using gas peaker fundamentals.

---

## 🧠 Project Overview

This project explores a trading hypothesis observed by EDF Day-Ahead traders:

> _"Within-day prices tend to trade below DA auction prices (adjusted for gas peaker strike prices) when the DA price clears above the cost of gas peaking generation."_

Using detailed settlement-period-level data from European power markets (EPEX and NordPool) and internal gas peaker cost forecasts, we develop and validate a systematic approach for identifying potential profit opportunities in the DA vs WD spread.

The research covers:
- Historical trend analysis
- Algorithmic implementation of the hypothesis
- Profitability testing across various trading intervals
- Automation using dynamic market data

---

## 🎯 Objectives

- Validate a correlation between DA auction prices and gas peaker strike costs.
- Compare DA vs WD price spreads and evaluate the strength of the trend.
- Identify profitable settlement periods across a range of trading days.
- Develop a real-time decision-making tool using forecasted gas peaker costs and DA auction forecasts.
- Simulate potential short trade entries and exits based on predictive conditions.

---

## 📊 Seasonal Limitations

This model is **seasonally sensitive**. During the **spring and summer months**, the model shows a higher predictive correlation and clearer profit zones. However, its reliability significantly **deteriorates in winter**, where:

- Power demand volatility increases
- Weather-related factors dominate the price structure
- DA markets are less aligned with peaker-based marginal costs
- REMIT events and outages become more frequent

> As a result, the model should **not be used blindly across the entire year** and must be **recalibrated seasonally** for robustness.

---

## 🔍 Method Summary

1. **Data Collection and Alignment**
   - Half-hourly and hourly prices from EPEX and NordPool
   - Internal gas peaker cost forecasts
   - Alignment of DA and WD prices with gas-adjusted spreads

2. **Hypothesis Definition**
   - When `(DA price - Gas Peaker Cost) > 0`, expect:
     ```
     WD price < DA price (adjusted)
     ```
   - Use spread comparison to identify "in-the-money" trades

3. **Profitability Testing**
   - Define DA and WD spreads
   - Highlight and count intervals where DA spread is positive and exceeds WD spread
   - Identify peak settlement periods for profitability (e.g., SP12–SP19 and SP37–SP45)

4. **Automation**
   - Process live data feeds via CSV from internal sources
   - Calculate real-time PnL opportunities
   - Simulate and track short positions based on algorithmic triggers

---

## 📦 Project Structure

```
📁 /data
    ├── Colab-DA-WD.xlsx          # Historical DA and WD prices
    ├── Colab-GPC.xlsx            # Gas peaker forecasted costs
    ├── Colab-PPF.xlsx            # Forecasted DA power prices
📁 /scripts
    ├── data_preprocessing.py     # Data cleaning and merging
    ├── pnl_analysis.py           # Spread analysis & PnL computation
    ├── trading_strategy.py       # Signal generation logic
📁 /visuals
    ├── daily_in_the_money.png
    ├── pnl_by_settlement_period.png
README.md
```

---

## 📈 Key Results

- ~**62.5% accuracy** in predicted "profitable" intervals over the February–July 2024 dataset
- Estimated **£32.9k average profit** on 100 MWh trades when the model triggers correctly
- Seasonal variation in profitability zones is clearly observable
- Automated pipeline handles **live data** and **historical overlays** for rapid comparison

---

## 🧰 Tools & Technologies Used

- **Python** – Data automation, visualization, and trade signal modeling
- **Pandas** – Time series processing, spread calculation, PnL simulation
- **Excel VBA** – Preliminary data manipulation and time granularity transformation (e.g., hourly to half-hourly)
- **FIS Aligne** – Integration with internal gas asset forecasts and DA price feeds

---

## 📌 Notes

- The model is not a financial product and is designed for academic and strategic testing purposes.
- It performs best under stable market conditions and should not be used during high-stress events without additional filters (e.g., weather, REMIT).

---
