# How to Approach IPOs: Stock Performance Prediction of IPOs in the Turkish Stock Market 

## Overview

This project analyzes 220 BIST IPOs from 2013-2025 to determine which factors may predict post-IPO stock performance. Both pre and post-IPO data will be used to evaluate their relationship with stock returns at 1, 3, 6, 12, 24, 60 months.

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

- **BIST100 Momentum:** High momentum if above 200 day moving average
- **Market Cap:** Post-IPO nominal capital X stock price at IPO 
- **Days of Consecutive 10% Gain After Listing (Tavan Serisi):** Directly from stock price data

## Data Preparation

### Concatonated all data in the excel files into two cvs files

- 13 excels between 2013-2025 into ipo_main_cleaned.csv
- 4 excels between 2020-2023 with oversubscription data into ipo_overs_cleaned.csv
- Both csv files were also merged with sector excel file from KAP to include the sector as an attribute

## Hypotheses

- Each hypothesis evaluated at 1, 3, 6, 12, 24, 60 month time points separately to compare short term and long term effects. (If applicable, some stock don’t yet have long term price data) 
- Oversubscription hypothesis only for IPOs between 2020-2023 since other data have that feature missing 

1. Companies with lower free float ratio perform better
2. Underwriter identity affects returns
3. Higher Relative Oversubscription (compared to IPOs around that time period) increases returns
4. REIT (GYO) Sector stocks underperform
5. IPOs listed when BIST100 momentum is high perform better
6. Lower market cap results in higher returns
7. More days of consecutive 10% gain results in better returns (long term >= 12 months)

## Data Analysis Methods

### EDA:

- Visualization of returns in different time periods
- Sector return comparisons
- BIST100 high momentum periods visualization

### Hypothesis Testing:

- Each hypothesis w8ill be tested by comparing returns to see if any statistically significant evidence is found

### ML:

- Machine learning methods like classification will be used to see if returns can be effectively predicted 







