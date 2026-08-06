# 🎮 Steam Games Dataset: Analytical Deep Dive

This project is a comprehensive data science exploration of the Steam PC gaming market. Using a dataset of over 125,000 games published on Steam, this analysis uncovers hidden market dynamics, engagement distributions, and the reality of game monetization. 

This repository contains the complete analytical workflow, from raw data cleaning to the final visualization dashboard.

---

## 🎯 Project Objectives
1. **Analyze Market Saturation:** Identify the distribution of engagement across the tens of thousands of games on Steam.
2. **Evaluate Pricing Models:** Determine if game price correlates with user satisfaction, and compare Free-to-Play against Paid models.
3. **Deconstruct Genres:** Understand how production labels (like "Indie") interact with traditional gameplay genres.
4. **Data Visualization:** Replace standard/default plots with advanced, bespoke data visualizations (Hexbins, Lorenz curves, Lollipop charts) designed to handle 100k+ overlapping data points cleanly.

---

## 📁 Repository Contents

*   [`steam_games_analysis.ipynb`](steam_games_analysis.ipynb): The core Jupyter Notebook. This is a fully executed, end-to-end analysis containing all Python code, data cleaning logic, feature engineering, and high-resolution visualizations. 
*   `README.md`: Project overview and methodology (this document).

*(Note: The raw dataset is ~380MB and is sourced directly from Kaggle via the `kagglehub` API in the notebook).*

---

## ⚙️ Methodology & Data Handling

Real-world datasets require heavy cleaning before they yield insights. Here is how the raw data was processed:

### 1. Fixing Schema Flaws
During the initial audit, an anomaly was identified: the `Release date` column contained string-based owner ranges (e.g., `"0 - 20000"`), while the `Estimated owners` column contained the actual numeric values. This source error was programmatically corrected.

### 2. Null Value Auditing
Columns containing 100% missing values (`Movies`, `Score rank`) were dropped. Columns with massive sparsity (like `Reviews` text, missing 90%+) were bypassed in favor of quantitative proxy metrics (Positive/Negative review counts).

### 3. Feature Engineering
To make the raw data actionable, new dimensions were engineered:
*   `total_reviews`: Normalizing engagement by combining positive and negative metrics.
*   `positive_ratio`: Calculating sentiment (handling divide-by-zero bounds).
*   `lang_count`: Parsing string arrays to count precise localization support per game.

### 4. Normalizing Categorical Arrays (Exploding Data)
Because games often have multiple genres (e.g., `"Action, Adventure, Indie"`), raw frequency counting is impossible. The dataset was preprocessed by splitting these strings into arrays and using pandas `.explode()` to pivot the arrays into individual rows, allowing for accurate, normalized frequency aggregations.

---

## 💡 Key Business Insights

The analysis yielded several critical insights into the Steam marketplace:

### 1. The "Invisible Majority"
The market is heavily saturated. **Over 34% of all games published on Steam have absolutely zero community engagement** (no reviews, zero concurrent players). 

### 2. The 1% Rule (Power Law Distribution)
Using a Lorenz curve analysis, the data mathematically proves that Steam is a 'winner-take-all' market. **The top 1% of games command over 84% of all user reviews generated on the platform.**

### 3. Price Does Not Dictate Quality
A correlation matrix and hexbin density plots reveal virtually zero correlation ($r \approx 0.01$) between a game's price and its positive review ratio. Furthermore, Free-to-Play games achieve a comparable positive rating ratio (~76%) to paid titles while driving significantly higher volume.

### 4. "Indie" is a Production Label, not a Genre
85.7% of games on Steam feature multiple overlapping genre tags. Over 35,000 games are tagged as *both* Indie and Action. The dominance of the "Indie" tag doesn't reflect a player preference for quirky games; it reflects the fact that the barrier to entry for independent publishing has vanished across all gameplay categories.

---

## 🚀 How to View the Analysis
You can open the `steam_games_analysis.ipynb` file directly in GitHub to read the executed code and view the charts. If you wish to run the code locally, ensure you have the required dependencies (`pandas`, `matplotlib`, `seaborn`, `scipy`, and `kagglehub`) installed.
