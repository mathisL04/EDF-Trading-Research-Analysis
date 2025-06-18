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

## 📌 Additional Notes & Improvements

- ⚙️ **Automated Deployment**:  
  This model can be integrated into an automated pipeline for real-time monitoring of **prompt trades on a half-hourly basis**, directly using data streams from **FIS Aligne**.

- 📅 **Wider Historical Validation**:  
  Further analysis can be extended to a **5+ year historical window** of trade data and gas peaker cost forecasts. This would allow a **robust quantification of seasonal effects** and help validate the strength of the correlation year-over-year.

- 🧠 **Scalability to Live Trading**:  
  An automated implementation could be developed and deployed directly on the **Day-Ahead trading desk** as a decision support tool for short-term directional strategies.

- 📉 **Scope of This Paper**:  
  This analysis provides a **lightweight, first-level exploration** of the potential for strategy deployment. It suggests that a correlation exists and that this correlation can be **used to inform trades**, but:
  - It is **not a final implementation**
  - More parameters and exogenous variables should be considered at a higher operational level

- 🌦️ **Future Enhancements**:
  - Incorporate **weather patterns**, **REMIT events**, and **localized gas/power consumption** in Great Britain to improve model precision
  - Explore performance in **other markets** where the **power-to-gas price ratio is ~4x** and where infrastructure and market structure are comparable to the UK

---


## 🔭 Opening the Path Forward

This research provides a foundational framework to demonstrate that **a statistically meaningful and economically actionable correlation exists** between DA prices and gas peaker costs in GB electricity markets. However, this is just the beginning. The simplicity of the model is intentional — it creates a baseline structure that is understandable, replicable, and extendable. To further improve accuracy, adaptiveness, and applicability, several technical enhancements are possible:

---

### 📈 1. Expand the Historical Scope

- Integrate **5+ years of trading and peaker cost data**.
- Conduct correlation and profitability analysis **segmented by season** and **market regime**.
- Quantify how model accuracy changes across different years, fuel price cycles, and policy conditions.

---

### ⚙️ 2. Build a Real-Time Trading Pipeline

- Automate trade signal generation using **live prompt trades** on a **half-hourly basis**.
- Direct integration with **FIS Aligne** for both DA forecasts and internal peaker cost streams.
- Enable **real-time deployment** of the model on the Day-Ahead desk as a decision support tool.

---

### 🌦️ 3. Enrich with Weather & Demand Drivers

- Include **forecasted weather variables** (e.g., wind, temperature, solar irradiance).
- Add **localized gas and electricity consumption forecasts** for the GB grid.
- Use weather-adjusted demand expectations to filter false positives from price spread signals.

---

### 🧠 4. Improve the Cost Modeling Layer

- Implement a **dynamic gas peaker stack**, adjusting for real-time asset availability, thermal efficiency, and ambient conditions.
- Distinguish between peaker asset types (OCGT vs CCGT) to assign more precise marginal strike levels.

---

### ⚡ 5. Consider Market Locational Granularity

- Account for **zonal constraints** (e.g., north-south congestion in GB).
- Integrate **Transmission Constraint Balancing Services (TCBS)** and locational price separation data.
- Adapt the model to markets that exhibit **nodal or zonal pricing mechanisms**.

---

### 📊 6. Expand to Other Markets

- Test the model in **non-GB countries** with:
  - A **power-to-gas price ratio of ~4x**,
  - Clear marginal fuel-driven pricing logic,
  - Similar infrastructure maturity.
- Possible regions include parts of the **Nordics**, **Texas (ERCOT)**, or **continental Europe** under crisis pricing regimes.

---

### 📉 7. Model Probabilistic Confidence

- Quantify confidence levels for each signal (e.g., “75% chance DA > GPC yields profitable WD short”).
- Use bootstrapping or Bayesian methods to model **uncertainty**.
- Helps inform trader risk tolerance and strategy selection.

---

### 🧠 8. Build Explainable AI Layers

- Auto-generate **explanations** for each trade signal:
  > “DA price £93/MWh > GPC £85/MWh → Forecasted low wind → Expected WD reversion → Short Triggered”

- Improves **transparency** for traders, risk teams, and desk managers.

---

### 🔄 9. Integrate Cross-Market Signals

- Explore co-optimization opportunities:
  - Gas → Power → EUA (carbon)
  - Battery peaker vs gas peaker marginality
  - UK Power vs TTF gas cross-commodity pricing logic

- Enables the construction of a **multi-dimensional directional trading strategy**.

---

### 🧪 Final Note

This paper does not aim to be a final trading model. It is a **conceptual and data-driven demonstration** that this correlation exists and **can be exploited** as part of a structured trading framework. The real value lies in building upon this with more data, richer features, and intelligent integration into real-time workflows.

---
