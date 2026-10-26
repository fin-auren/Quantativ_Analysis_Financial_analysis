# Quantative_Option_Chain_Analytics_Nifty_23_06_2026

# Motivation of this project 
* option chain analysis for collective market expectations.
* Open intreset reveals trader positing for long term as well as short term analysis
* Implied volatility reveals the uncertainity.
* Put/Call behaviour show resistance as well as support for the underlying assets.
--
## Some financial glossory:
**Strike Price :** The specific price at which the buyer can buy (call option) and sell (put option) the underlying market asset. The market's current price usually sits in the middle, dividing in-the-money (ITM) and out-of-the-money(OTM) strikes. 

**Call Open Intreset (OI) :** The total number of outstanding call contracts currently active. HIgh call OI shows a strong resistance level. 

**Call Change OI** : The total change in OI during a trading session tells us above of upcoming resistance/support.

- **Call Volume** : The total number of call contracts traded duing the current trading session, showing the most actively traded strike price. 

**Call IV - Implied Volatility** - A measure of the expected future volatility of the underlying asset. Higher IV shows higher option permiums. 

**Call LTP (Last Traded Price) :**   Current price of the market premium you need to pay to buy a call option at that strike price.



> Similarly we have put side glossary as : 


**Put OI (Open Interest) :** The total number of outstanding put contracts. High Put OI typically highlights a strong support level.

**Put Change OI:** The net change in open interest for that specific put strike during the day.

**Put Volume:** The total number of put contracts traded today.

**Put IV:** The implied volatility for the put option.

**Put LTP:** The current premium you would pay to buy a put option at that strike.

<h1> Dataset Description</h1>

**Source** - NSE Option Chain 
**Underlying Asset** - NIFTY 50
**Expiry Date** - 23 June 2026

<h1> Data Cleaning </h1>

- step 1 - Rename the columns for call and put options.
- step 2 - Rename duplicated header row for better reading.
- step 3 - replace '-' with NaN using 'numpy'.
- step 4 - convert string (10,550) into numeric value using new function.
- step 5 - Validation of the data.

## Summary Table 

|Metric        |Strike |Value    |Interpretation                 |
|--------------|-------|---------|-------------------------------|
|call_oi       |24200.0|205342.0 |Potential Resistance           |
|put_oi        |24000.0|202239.0 |Potential Support              |
|call_change_oi|24150.0|101025.0 |Maximum New Call Positions     |
|put_change_oi |24100.0|116663.0 |Maximum New Put Positions      |
|call_volume   |24100.0|7560987.0|Most Active Call Trading       |
|put_volume    |24100.0|8010738.0|Most Active Put Trading        |
|call_iv       |22400.0|94.67    |Highest Call Implied Volatility|
|put_iv        |21250.0|77.91    |Highest Put Implied Volatility |


# Reserach Findings : 
## Market position cluster :
The most option activity is concentrated between 24000-24200 region.

## Support Zone : 
Larger Put Open Intreset : 24000 

Put writers are concentrated at 24000, this strike act as a support zone. 

## Expected Trading zone : 
The expected trading zone is 24000 to 24200; Most common option-chain 

## New position Creation :
call_change_oi = 24150
put_change_oi = 24100

The fresh position are being created near the current market consensus zone. Trader are actively adjusting their position near 24100-24150 due to expiry of market is near by. 

**24100** is the most actively traded strike.

The highest call and put trading volumes are observed at a strike price of 24100 strike, suggesting that this this is the main battleground between bullish and bearish market participants where market is closed near by this price. 

**Highest Call Implied Volatility** and **Highest Put Implied Volatility** are observed at strikes far from the primary trading region, consistent with the volatilty observed in option markets. 


## Call Put Ratio
To gauge the market sentiment Put-Call Ratio (PCR) was computed using total open interset across all strikes which is defined below: 

$$
PCR = \frac{\text{Total Put OI}}{\text{Total Call OI}}
$$

And we found out PCR = 0.8716758967048529 which shows "**Market is slighlty bearish.**" based on following framework : 

| PCR       | Interpretation     |
| --------- | ------------------ |
| < 0.7     | Bearish            |
| 0.7 – 1.0 | Slightly Bearish   |
| 1.0 – 1.3 | Neutral / Balanced |
| > 1.3     | Bullish            |
| > 1.5     | Extremely Bullish  |


## Concentration Ratio:

$$
\text{Concentration Ratio} = \frac{\text{Top 5 OI}}{\text{{Total Oi}}}
$$

Show us the quantative metric of position where we used following critrion for market analysis

| Ratio  | Meaning                |
| ------ | ---------------------- |
| <20%   | Diffuse positioning    |
| 20–40% | Moderate concentration |
| >40%   | Strong concentration   |
| >60%   | Extremely concentrated |

## Results

|      |Metric|Top5_OI|Total_OI     |Percentage| 
|------|------|-------|-------------|----------|
|0     |Call OI concentration|853830.0  |2559036.0|33.365298|
|1     |Put  OI concentration|745974.0  |2230650.0|33.442001|

The top 5 call and put strikes accounts for about 33\% of the total call open interest indicating that market positioning is moderately concentrated around a small number of strikes showing good consensus among traders. 

Top 5 call Strikes : 
|index|strike|call_oi|
|-----|------|-------|
|60   |24200.0|205342.0|
|58   |24100.0|171128.0|
|62   |24300.0|162409.0|
|66   |24500.0|159722.0|
|59   |24150.0|155229.0|


Top 5 put Strikes : 
|index|strike|put_oi|
|-----|------|------|
|56   |24000.0|202239.0|
|58   |24100.0|166651.0|
|54   |23900.0|126352.0|
|52   |23800.0|125569.0|
|46   |23500.0|125163.0|

One observation we made that most of the top OI is concentrated around 24000 and 24200 

**Weighted Variance and Weighted Standard Deviation Results :**

|index|Metric                     |Value             |
|-----|---------------------------|------------------|
|0    |Wighted Variance           |280551.31820609374|
|1    |Weighted Standard Deviation|529.6709527679366 |

The miniumum value of strike is **21200** and max value of **26300** with a **weighted mean strike of 24596**. We find out a **Weighted Standard Deviation to be 529.67**. 

**Implied Volatility Analysis**
## Volatility Smile

Objective : Investigate the volatility structure embedded in NIFTY option prices.

Volatility Smile are implied volatility patterns that arise in pricing financial options a parameter that needs to be modified for the Black-Scholes formula to fit market prices. 
![Chart showing annual growth](IV_analysis.png)


|IV Summary Statistics |         |        |  | ||
|---|---------------------------|------------------|---------|---------|------|
|   |Metric                     |Call              |IV       |Put      |IV    |
|0  |Mean                       |IV                |30.562083|29.782708|      |
|1  |Median                     |IV                |25.790000|26.640000|      |
|2  |Std                        |IV                |18.443256|16.108505|      |
|3  |Min                        |IV                |11.590000|11.290000|      |
|4  |Max                        |IV                |94.670000|63.760000|      |
|Maximum IV Summary |                         |           |         |         |      |
|   |Metric                     |Strike            |IV       |         |      |
|0  |Maximum                    |Call              |IV       |22400.0  |94.67 |
|1  |Maximum                    |Put               |IV       |21850.0  |63.76 |
|Top 5 Call IV Strikes|                          |             |       ||      |
|   |strike                     |call_iv           |         |         |      |
|24 |22400.0                    |94.67             |         |         |      |
|26 |22500.0                    |64.58             |         |         |      |
|33 |22850.0                    |61.52             |         |         |      |
|16 |22000.0                    |58.40             |         |         |      |
|28 |22600.0                    |56.62             |         |         |      |
|Top|5  Put IV Strikes                       |               |       |  |      |
|   |strike                     |put_iv            |         |         |      |
|13 |21850.0                    |63.76             |         |         |      |
|16 |22000.0                    |59.69             |         |         |      |
|17 |22050.0                    |58.33             |         |         |      |
|18 |22100.0                    |57.67             |         |         |      |
|97 |26050.0                    |56.40             |         |         |      |

Both the curve reaches their minimum around 24000-24200 which is where maximum Call and Put OI resides. 
* Minimum IV =  24000-24200
* The lowest implied volatility occurs near the strikes with the highest concentration of OI. This suggest that market that market traders assign the highest prob to the price movements occuing within this region.
* Far away from 24100 IV increases dramatically. Options far from the primary trading region exhibit substantially higher implied volatility, reflecting greater uncertainty and lower liquidity.
* The graph is left side skew ; Call IV Max = 94.67; Put IV Max = 63.76;
* The left tail is steeper than the right tail. Market participants assign higer risk premiums to the large downside moves than to comparable upside moves. 

# Strike Vs Option with color representing Open Interset

This show where the market participants are concentrated. 

![Net OI plotted with strike](net_oi_heat_map.png)

Intrepretation: 
* Green - Put Dominance (Support)
* Red - Call Dominance (Resistance)
This becomes a visual map of support and resistance.

# Notebook Summary

This notebook conducts a historical backtest of a quantitative trading strategy on **Apple Inc. (AAPL)** stock for the year **2025**.

## 1. Setup and Packages
* Installs and imports essential quantitative analysis packages: `yfinance`, `pandas`, `numpy`, and `matplotlib`.

## 2. Methodology & Quantitative Strategy
* **Data Sourcing**: Downloads daily adjusted closing prices using the Yahoo Finance API (`yfinance`).
* **Technical Indicators Calculated**:
  * **Moving Average (MA)**: 50-day rolling mean.
  * **Bollinger Bands**: 20-day rolling mean ± 2 standard deviations.
  * **Relative Strength Index (RSI)**: 16-day rolling relative strength momentum indicator.
* **Trading Signal Rules**:
  * **BUY Signal (1)**: Triggered when the price is oversold (RSI < 20) **and** below the lower Bollinger Band.
  * **SELL Signal (-1)**: Triggered when the price is overbought (RSI > 80) **and** above the upper Bollinger Band.
* **Execution and Position Management**: Replaces neutral signals with a forward-fill mechanism to maintain active positions until an opposing trading trigger occurs.


# Notebook Summary Yahoo_Finance.ipynb

This notebook explores financial data for **HDFC Bank (HDFCBANK.NS)** (referenced as `msft` in some initial variables) using the `yfinance` library.

### 1. Dividend History Analysis (Cell `bYSyH9W6uyrA`)
* **Action**: Fetched historical dividend data for HDFC Bank.
* **Processing**: Parsed dates, converted dividends to numeric values, resampled data to a yearly frequency, and aggregated the total dividends per year.
* **Visualization**: Generated a line plot ("Total Dividends vs Year") showing a clear upward trend in annual dividend payouts from late 1990s through 2024, with a notable dip around 2020.

### 2. Library Inspection (Cell `RGbAIy1Ou3Vp`)
* **Action**: Inspected the attributes and functions available within the `yfinance` library using `dir(yf)` to check capabilities.

### 3. Ticker Information (Cell `0UEFBMxG7aiR`)
* **Action**: Printed the metadata and company profile dictionary (`msft.info`) for HDFC Bank. This confirmed details such as the company name, sector (Financial Services), industry (Banks - Regional), key corporate officers, and business operations.

### 4. Options Chain Exploration (Cell `XIKGGy7P7mJO`)
* **Action**: Attempted to retrieve option contract expiration dates and chain data for `HDFCBANK.NS`.
* **Result**: Returned an empty tuple `()` for available expiration dates. Consequently, the script determined that option chain data was unavailable for this ticker at the time of execution.
## 3. Backtest Results
* **Total Strategy Return**: **30.10%**
* **Total Buy & Hold Return**: **11.99%**
* **Visual Analysis**: Shows a performance comparison plot where the active trading strategy outperformed the static benchmark portfolio.


# Accumulative Swing Index (ASI) Trading Strategy — Notebook Summary

## Overview

This notebook implements the **Accumulative Swing Index (ASI)** to identify potential trading swings and backtest basic buy/sell signals using historical financial market data.

The workflow includes ASI calculation, swing high and low identification, swing-day detection, and a backtesting simulation to evaluate potential trading opportunities.

The notebook contains three main code cells, each serving a distinct purpose in the trading analysis workflow.

## 1\. First Cell: ASI Calculation and Swing Detection

**Cell ID:** `Nutd9ZTpPLmk`

### Purpose

Defines the core functions required to calculate the Accumulative Swing Index and identify potential market swing points.

### Key Features

- **`calculate_asi`****:** Calculates the Accumulative Swing Index using the parameter `a = 0.2`.
- **`identify_swings`****:** Identifies potential swing highs and swing lows in historical price data.
- **`is_swing_day`****:** Checks whether the current day qualifies as a swing day based on the identified swing conditions.

### Execution

- Loads and processes the dataset `INDUSINDBK.csv`.
- Applies the ASI calculation and swing detection logic.
- Evaluates the latest trading day's swing status.

### Output

text

```
Today's Swing Status: Not a Swing Day
```

### Interpretation

According to the implemented swing-detection logic, the latest trading day in the dataset does not qualify as a swing day.

## 2\. Second Cell: ASI Calculation with an Alternative Parameter

**Cell ID:** `Dz09y9jdQnEk`

### Purpose

Implements a similar ASI-based swing detection workflow while using a different parameter value to explore an alternative calculation configuration.

### Key Features

- Reuses the ASI calculation and swing identification approach.
- Sets the ASI parameter to `a = 0.1`.
- Evaluates swing conditions using a separate stock dataset.

### Execution

- Loads and processes the dataset `BANDHANBNK.csv`.
- Calculates the ASI using the alternative parameter.
- Checks whether the latest trading day is classified as a swing day.

### Output

text

```
Today's Swing Status: Not a Swing Day
```

### Interpretation

The implemented logic does not identify the latest trading day in the `BANDHANBNK.csv` dataset as a swing day.

Using a different ASI parameter provides an opportunity to compare strategy behavior, although the two outputs alone do not establish which parameter performs better.

## 3\. Third Cell: Backtesting Simulation

**Cell ID:** `aDNlO4KhPSef`

### Purpose

Attempts to simulate a trading strategy by pairing swing lows with subsequent swing highs to derive trade signals and calculate cumulative returns.

### Key Features

- Identifies potential swing-low entry points.
- Matches swing lows with subsequent swing highs.
- Generates potential buy and sell signals.
- Calculates trade returns and cumulative strategy performance.

### Current Status: Execution Error

The cell currently raises the following error:

text

```
NameError: name 'data' is not defined
```

### Cause

The variable `data` is referenced before it has been initialized or loaded in the cell's execution context.

The cell likely expects a Pandas DataFrame containing historical price data from a previous processing step. However, the variable may have a different name, may not have been created, or may not persist because the relevant notebook cell was not executed.

### Recommended Fix

Load the intended dataset and initialize `data` before running the backtesting logic.

For example, if the intended dataset is `INDUSINDBK.csv`:

python

```
import pandas as pd

data = pd.read_csv("INDUSINDBK.csv")

# Convert the date column if present.
if "Date" in data.columns:
    data["Date"] = pd.to_datetime(data["Date"])

# Inspect the dataset before running the backtest.
print(data.head())
print(data.columns)
```

Ensure that the column names and data structure match the requirements of the backtesting code. If the third cell is intended to use the `BANDHANBNK.csv` dataset instead, load that file accordingly.

The notebook should then be rerun in sequence to verify that the required variables and calculated swing points are available.

## 4\. Overall Workflow

The notebook follows this general analytical process:

1. Load historical stock price data.
2. Calculate the Accumulative Swing Index using the selected parameter.
3. Identify potential swing highs and swing lows.
4. Determine whether the latest trading day qualifies as a swing day.
5. Generate buy and sell signals by matching swing lows with subsequent swing highs.
6. Backtest the resulting signals.
7. Calculate individual trade returns and cumulative strategy performance.

## 5\. Key Findings

- **ASI implementation:** Two cells implement ASI-based swing detection using different parameter values.
- **Stock datasets:** The first two cells analyze `INDUSINDBK.csv` and `BANDHANBNK.csv`, respectively.
- **Swing-day outputs:** Both cells report that the latest evaluated trading day is not a swing day.
- **Backtesting limitation:** The third cell cannot currently execute because the `data` variable is undefined.
- **Next step:** Initialize the correct DataFrame, validate the expected price columns, and rerun the backtesting simulation.

## Conclusion

This notebook provides a foundation for exploring swing-trading strategies using the Accumulative Swing Index. It combines technical indicator calculations, market swing detection, and an intended backtesting framework.

Before drawing conclusions about profitability, the backtesting implementation should be corrected and validated. The strategy should also account for transaction costs, realistic execution prices, look-ahead bias, and appropriate risk management.

The reported swing-day statuses are outputs of the current implementation; they do not independently establish the effectiveness or predictive accuracy of the strategy.

# Notebook Summary: Simple Stock Trading & Technical Analysis

## 1\. Overview

This notebook explores two stock trading systems implemented in Python:

1. **Pure Python Stock Portfolio Simulator:** A basic trading application built without external libraries.
2. **Historical Backtesting System:** A rule-based trend-following strategy using `yfinance`, Pandas, and visualizations to evaluate historical trading performance.

The notebook combines fundamental portfolio management concepts with technical analysis and historical strategy testing.

## 2\. Key Components

### Part A: Interactive Stock Trading Simulator (No External Libraries)

This section implements a simple stock portfolio simulator using core Python programming concepts.

#### Classes Defined

**`Stock`**

- Represents a stock using its ticker symbol and current price.
- Supports dynamic price values for basic trading simulations.

**`Portfolio`**

- Maintains the available cash balance.
- Tracks the quantities of individual stocks owned.
- Supports basic buy and sell transactions.
- Enforces transactional constraints, such as preventing purchases when funds are insufficient and preventing sales of shares that are not owned.

#### User Interface

The notebook provides a text-based terminal menu that allows users to:

- Buy predefined stocks: `AAPL`, `GOOGL`, and `TSLA`.
- Sell shares held in the portfolio.
- View current portfolio holdings and cash balances.
- Monitor portfolio changes after transactions.

This section demonstrates object-oriented programming, transaction validation, and basic portfolio accounting without relying on external libraries.

### Part B: Rule-Based Backtesting Strategy (`TATAMOTORS.NS`)

This section evaluates a simple trend-following strategy using historical stock market data retrieved through the Yahoo Finance API with the `yfinance` Python library.

**Backtesting period:** January 1, 2024, to April 10, 2024.

#### Trading Protocols

**Buying Protocol**

- Generates a buy signal when the stock price increases for `b` consecutive days.
- The strategy uses `b = 1`, meaning a single day of price increase can trigger a buy signal.

**Selling Protocol**

- Generates a potential sell signal when the stock price decreases for `s` consecutive days.
- A sale is executed only when the position has generated a cumulative profit since the most recent purchase.
- The strategy uses `s = 1`, meaning a single day of price decrease can trigger a potential sell signal.

#### Functions Implemented

**`get_buying_selling_days(price_data, b, s)`**

- Identifies potential buy and sell signal dates.
- Uses rolling Pandas operations to evaluate consecutive price movements.
- Produces the dates required by the trading simulation.

**`check_cumulative_percent_change(...)`**

- Evaluates the percentage change between the purchase price and a potential selling price.
- Determines whether the position has achieved a positive cumulative return.
- Allows a sell signal to proceed only when the modeled holding period is profitable.

**`get_investing_result(df_stocks, starting_funds)`**

- Processes trading signals sequentially.
- Executes purchases and sales based on the strategy rules.
- Manages the available cash balance and stock holdings.
- Calculates the resulting portfolio performance and cumulative return.

## 3\. Backtesting Performance and Results

### Strategy Configuration

| Parameter | Value |
| --- | --- |
| Stock ticker | `TATAMOTORS.NS` |
| Company | Tata Motors Limited |
| Backtesting start date | January 1, 2024 |
| Backtesting end date | April 10, 2024 |
| Buy parameter (`b`) | 1 consecutive day of increase |
| Sell parameter (`s`) | 1 consecutive day of decrease |
| Initial funds | $10,000 |
| Reported return | +16% |

### Reported Performance

The notebook reports a **16% return** over the backtesting period, corresponding to a cumulative return factor of `0.16`.

Based on the stated initial funds of $10,000, a 16% gain would represent an illustrative profit of $1,600 and a final portfolio value of $11,600, assuming the reported return is calculated against the entire initial portfolio and all positions are valued consistently.

### Visualization

The notebook generates a chart showing historical closing prices alongside trading activity.

The visualization includes:

- **Daily Closing Prices:** Displays the historical price movement of Tata Motors.
- **Red Dashed Lines:** Mark buy events.
- **Blue Dashed Lines:** Mark sell events.
- **Gray Shaded Regions:** Highlight periods during which shares are held.

This chart helps illustrate how the strategy responds to short-term price movements and how long positions remain open.

## 4\. Key Findings

- **Portfolio Simulation:** Demonstrates basic stock trading operations, portfolio tracking, and cash management using pure Python.
- **Technical Signal Generation:** Uses consecutive daily price movements to generate potential buy and sell signals.
- **Profit-Based Selling:** Requires a positive cumulative return before executing a sell signal.
- **Historical Evaluation:** Tests the strategy against historical Tata Motors price data for the specified period.
- **Visual Analysis:** Provides a graphical representation of price trends, trading signals, and holding periods.

## 5\. Limitations and Considerations

Although the notebook provides a useful introduction to trading simulations and backtesting, several factors should be considered before using the strategy with real funds.

- **Transaction Costs:** Brokerage fees, taxes, and other trading costs may reduce profitability.
- **Slippage:** Actual execution prices may differ from the historical closing prices used in the simulation.
- **Signal Timing:** The implementation should ensure that signals derived from a day's closing price are not executed at that same close unless the execution assumption supports it.
- **Position Management:** The backtest should explicitly handle open positions, repeated signals, and the valuation of any unsold shares at the end of the period.
- **Currency Consistency:** Tata Motors is listed in India, so the currency used for historical prices should be reconciled with the stated $10,000 starting capital. The reported return is more interpretable when the portfolio and price data use a consistent currency.
- **Out-of-Sample Validation:** A profitable historical period does not guarantee future performance. The strategy should be evaluated across different market conditions and separate validation periods.
- **Benchmark Comparison:** Comparing the strategy against a buy-and-hold approach can help establish whether its trading rules provide additional value.

## Conclusion

This notebook demonstrates an end-to-end introduction to stock trading systems, combining a pure Python portfolio simulator with a historical, rule-based backtesting framework.

The first component illustrates portfolio management and transactional controls. The second uses historical market data, consecutive price movements, and profit-based exit conditions to simulate trading activity and visualize the results.

The reported **16% historical return** provides an initial performance measure for the selected strategy and period. However, transaction costs, realistic execution assumptions, currency consistency, and further validation should be addressed before treating this result as evidence of repeatable profitability.
