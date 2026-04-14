# How to Approach IPOs: Stock Performance Prediction of IPOs in the Turkish Stock Market 

## Overview

This project analyzes 247 BIST IPOs from 2013-2025 to determine which factors may predict post-IPO stock performance. Both pre and post-IPO data will be used to evaluate their relationship with stock returns at 12 and 24 months.

## Motivation

Investing and especially starting early is key for financial safety, and my journey started at 18 with IPOs thanks to my friends’ interest in high school. Since then, I’ve been constantly expanding my knowledge on investing, but the habit of IPO investing is still with me. I’ve experienced the pattern that during some periods, all the IPOs perform well in the first few weeks, and the number of people joining them increases during these times. However, this strategy feels shortsighted and doesn’t provide any long term gains since many, including me, sell out of the stocks after the initial decline in price.

## Data Sources & Collection

**1. IPO Stock Data**

- **Source:** Sermaye Piyasası Kurulu (SPK) 
- **Collection Method:** Downloaded official excel files 
- **Period:** Covers IPOs between 2013-2025
- **Features:** Company name and ticker, Free float ratio (halka açıklık oranı), Stock price at IPO, Post IPO nominal capital, Underwriter identity(aracı kurum), First day of trading date, Oversubscription rate and Investor Count
- **Preprocessing:** Convert any financial data to USD to account for inflation
- **Links:** [2013-2025 version](https://spk.gov.tr/ihrac-verileri/ilk-halka-arz-verileri), and [2020-2023 with oversubscription data version](https://spk.gov.tr/sirketler/duyurular-ve-veriler/ihrac-ve-halka-arz-verileri)

**2. Stock, BIST100 Index, and USD/TRY prices**

- **Source:** Yahoo Finance API
- **Collection Method:** Directly accessible in Python
- **Preprocessing:** Adjust prices to USD 

**3. Company Sector Data**

- **Source:** [Kamuyu Aydınlatma Platformu (KAP)](https://kap.org.tr/tr/Sektorler)
- **Collection Method:** Downloaded official excel files

**4. Data to Be Formulated From The Features Above**

- **BIST100 Momentum:** High momentum if above 200-day SMA, also calculate percentage distance from 200-day SMA
- **Market Cap:** Post-IPO nominal capital X Stock price at IPO 
- **Days of Consecutive 10% Gain After Listing (Tavan Serisi):** Directly from stock price data
- **Free Float Value:** Free float ratio X Market cap

## Data Preparation

### Concatenated all data in the excel files into two csv files

- 13 excels between 2013-2025 into ipo_main_cleaned.csv
- 4 excels between 2020-2023 with oversubscription data into ipo_overs_cleaned.csv
- Both csv files were also merged with sector excel file from KAP to include the sector as an attribute
- ipo_main_cleaned.csv later converted to ipo_final.csv after adding additional features

## Hypotheses

- Each hypothesis evaluated at 12 or 24 month time points separately to show mid/long term effects. (If applicable, some stock don’t yet have long term price data) 
- Oversubscription hypothesis only for IPOs between 2020-2023 since other data have that feature missing
- All tested at 12 month returns except 8th hypothesis

1. Companies with lower free float ratio perform better
2. Underwriter identity affects returns
3. Higher oversubscription increases returns
4. REIT (GYO) Sector stocks underperform
5. IPOs listed when BIST100 momentum is high perform better
6. Lower market cap results in higher returns
7. Lower free float value results in higher returns
8. More days of consecutive 10% gain results in better returns (24 months)

## Data Analysis Methods

### EDA:

- Visualization of returns in different time periods
- Sector return comparisons
- BIST100 high momentum periods visualization

### Hypothesis Testing Results:

- Significance Level: α = 0.05
  
1. Companies with lower free float ratio perform better:
- Spearman correlation: 0.0376
- P-value: 0.5634
- Fail to reject the null hypothesis
2. Underwriter identity affects returns
- Kruskal-Wallis statistic: 30.2935
- P-value: 0.0070
- Reject the null hypothesis
3. Higher oversubscription increases returns
- Spearman correlation: 0.1335
- P value: 0.151225
- Fail to reject the null hypothesis
4. REIT (GYO) Sector stocks underperform
- Mann-Whitney U statistic: 1802.0000
- P-value: 0.0078
- Reject the null hypothesis
5. IPOs listed when BIST100 momentum is high perform better
- Mann-Whitney U statistic: 2972.0000
- P-value: 0.6779
- Fail to reject the null hypothesis
6. Lower market cap results in higher returns
- Spearman correlation: -0.2813
- P value: 0.00001
- Reject the null hypothesis
7. Lower free float value results in higher returns
- Spearman correlation: -0.3051
- P value: 0.000002
- Reject the null hypothesis
8. More days of consecutive 10% gain results in better returns (at 24 months)
- Spearman correlation: 0.2434
- P value: 0.000481
- Reject the null hypothesis

### Key Findings:

- Low market cap and lower free float value are very strong indicators of outperformance 
- Underwriter identity affects returns, most likely since some underwriters do IPOs with lower market cap 
- 10% gain days also predict returns, was tested to see if they led to major crashes in price later on 
- GYO sector companies usually underperform 
- All findings are also practically significant since they show major price trends 

### ML:

- Machine learning methods like classification and regression will be used to see if returns can be effectively predicted

### AI Usage:

AI Tools (Claude, Gemini) were used for:
  - Merging tables, cleaning and feature generation while data processing
  - Learning python syntax for visualization, EDA and hypothesis testing 







