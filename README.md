# Crypto Trader Performance & Market Sentiment Analytics

I wanted to find out if crypto traders actually make money when everyone is hyped up and greedy, or if they just get caught in the FOMO trap. 

To figure this out, I took a massive trading ledger containing over 211,000 transaction records and mapped it directly against a daily Crypto Fear & Greed index. The goal was to see exactly how individual profitability, trade sizing, and risk habits change when the market swings between panic and extreme hype.

## Step-by-Step Workflow that I followed

I first needed to clean the data. Here is how I manually handled the data issues and built everything out from scratch:

### 1. Data Cleaning & Solving the Leverage Issue (Excel)
* **Wrangling the Rows:** I started with two raw spreadsheets: a massive transaction history (~211k rows) and a daily sentiment tracking file.
* **The Math Problem:** Originally, I wanted to calculate a clean leverage metric using raw position sizes. However, because some accounts had near-zero denominators, my formulas started spitting out crazy, distorted outliers that messed up the data.
* **My Pivot:** To keep the analysis clean and honest, I shifted gears and used **Average Trade Size (`Size USD`)** as my core risk metric instead. It perfectly shows how confident or aggressive traders are getting without any calculation bugs.

### 2. Modeling the Data (Tableau)
* **Connecting the Datasets:** Instead of writing long, heavy Python scripts or SQL joins that might slow down the workbook, I brought both files straight into Tableau's data modeling layer.
* **Fixing the Timestamps:** The transaction ledger used raw date-time stamps, so I normalized them down to a clean daily date format (`CLEAN_DATE`). Then, I built a logical relationship to link it directly to the sentiment calendar (`Date`). This perfectly synced all 211,000 rows without duplicating any data.

### 3. Metric Engineering & Dashboard Layout
* **Executive Summary Table:** I created a clean KPI table at the very top to show Total Net Profit (`Closed PnL`) and Total Trading Volume (`Size USD`). To make it look professional and readable at a glance, I formatted the raw text into Millions ($M) and Billions ($B).
* **Finding the Whales:** I built a segmentation sheet at the bottom by sorting individual accounts by their total profits. This instantly isolated two groups: disciplined "Whale Winners" who make millions, and "Emotional Outliers" who suffer heavy losses.

---

## What's in this Repository
* `Trader Analysis.twbx`: My complete, packaged Tableau Dashboard file with all data connections and charts inside.
* `insights_report.md`: A 1-page summary breaking down my data findings and two actionable strategy rules I created based on the math.

---

## How to Open and Intersect with the Dashboard

1. Download the `Trader Analysis.twbx` file from this repository.
2. Open it using **Tableau Desktop** or the free **Tableau Public** app.
3. **How to filter the data:** * The entire dashboard is interactive and runs off the **Total Profit vs Mood** bar chart (the one with the large colored bars for Fear and Greed).
   * **Click on any bar**,for example, click the big teal **Fear** bar. 
   * The whole dashboard will instantly filter itself. The trader segmentation list at the bottom will change to show you exactly which individual accounts made or lost money during that specific market mood.
   * **To reset it:** Just click the exact same bar a second time, and the filter will clear.
