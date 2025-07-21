# Dual-Factor Equity Screening & Portfolio Builder

This repository contains a sophisticated Python script that performs a dual-factor analysis on Nifty 50 stocks to build a strategically optimized investment portfolio. The engine first scores stocks individually on **Momentum** and **Value** factors and then combines these scores to create a final, ranked list for portfolio construction.

## Table of Contents
- [Strategy Overview](#strategy-overview)
- [Part 1: Momentum Scoring](#part-1-momentum-scoring)
- [Part 2: Value Scoring](#part-2-value-scoring)
- [Part 3: Portfolio Construction](#part-3-portfolio-construction)
- [Technologies & Libraries](#technologies--libraries)
- [How to Run This Script](#how-to-run-this-script)

## Strategy Overview

The core of this project is a two-pronged approach to stock selection:

1.  **Momentum Analysis:** Identifies stocks that are currently exhibiting strong positive trends.
2.  **Value Analysis:** Identifies high-quality, potentially undervalued stocks based on fundamental financial health.

The final portfolio is built by combining these two distinct scores, aiming to invest in fundamentally sound companies that also have strong market momentum.

## Part 1: Momentum Scoring

The script first calculates a `Momentum Score` for each stock based on a weighted average of the following metrics:

* **3-Month Price Return** (30% weight)
* **6-Month Price Return** (20% weight)
* **Volatility-Adjusted 3M Return (Sharpe-Like Ratio)** (30% weight)
* **Price relative to 200-Day Moving Average** (20% weight)

Each stock is ranked on these metrics, and a final weighted `Momentum Score` is generated. The results are saved to `Nifty50_momentum_scores.xlsx`.

## Part 2: Value Scoring

Next, the script calculates a `Composite_Score` for value, which includes the renowned **Piotroski F-Score** to measure financial strength. The value score is a weighted average of the following normalized metrics:

* **Piotroski F-Score** (25% weight)
* **EV/EBITDA** (25% weight)
* **Return on Assets (ROA)** (15% weight)
* **Earnings Yield (E/P)** (10% weight)
* **Price-to-Earnings (P/E)** (10% weight)
* **Gross Margin** (10% weight)
* **Price-to-Book (P/B)** (5% weight)

The script ranks all companies based on this composite value score and saves the results to `Value_Strategy_Ranked.xlsx`.

## Part 3: Portfolio Construction

In the final step, the script combines the Momentum and Value scores with a 50/50 weighting to produce a final `Combined_Score`. Based on a user-provided total portfolio size, it then calculates the number of shares to purchase for each company using an equal-weight allocation.

To optimize capital usage, any leftover cash after the initial allocation is intelligently redistributed among the top 10 stocks with the highest `Combined_Score`.

The final, actionable portfolio is saved as `Nifty50_optimized_portfolio.xlsx`.

## Technologies & Libraries

* **Python 3**
* **Pandas:** For data manipulation and analysis.
* **NumPy:** For numerical operations.
* **yfinance:** For downloading historical market and fundamental data from Yahoo Finance.
* **tqdm:** For progress bars during data fetching.
* **google.colab:** For file upload/download functionality within Google Colab.

## How to Run This Script

This script is designed to be run in a Google Colab environment.

1.  **Prepare your stock list:** Create a CSV file containing the ticker symbols you want to analyze (e.g., from the Nifty 50). The file should have a header named `Ticker`.
2.  **Run the script:** Execute the cells in the notebook sequentially.
3.  **Upload your CSV:** When prompted, upload the ticker list file you prepared in step 1.
4.  **Enter Portfolio Size:** When prompted, enter the total amount in INR you wish to invest.
5.  **Download Results:** The script will automatically generate and download three Excel files containing the momentum scores, value scores, and the final optimized portfolio.
