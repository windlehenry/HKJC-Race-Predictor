# Predictive Analytics: Hong Kong Jockey Club Horse Racing

This project explores whether machine learning can be used to predict the finishing position of horses at the Happy Valley Racecourse in Hong Kong.

I scraped historical race data directly from the Hong Kong Jockey Club (HKJC) website and built a full pipeline for analysis, feature engineering, and model evaluation. As someone who grew up in Hong Kong, this was a meaningful project for me personally — combining my interest in data science with something culturally familiar.

---

## Notebooks

- `HKJC_Scraping.ipynb`  
  Handles data collection by scraping the HKJC website using `requests`, `BeautifulSoup`, and `pandas`. Where scraping failed (due to structural issues or missing pages), I manually entered race data to complete the dataset.

- `HKJC_Main.ipynb`  
  Covers the end-to-end workflow:
  - Cleaning and preparing the data (handling missing values, removing unusable columns)
  - Feature engineering (standardizing formats, extracting date components, one-hot encoding, aggregating historical performance)
  - Exploratory Data Analysis (EDA) and visualizations
  - Building and evaluating machine learning models

---

## Project Objective

The goal was to predict the exact finishing position (1st, 2nd, 3rd, etc.) of each horse in a race. While perfect accuracy was never expected — horse racing is unpredictable by nature — I wanted to explore whether any patterns or signals could be found in the data.

Key variables used:
- Win Odds
- Finish Time
- Historical performance of Horse, Jockey, and Trainer
- Race metadata: draw position, declared weight, distance category

---

## Models and Results

### Random Forest Classifier

- **Baseline Test Accuracy**: ~13.7%
- **Improved Accuracy (with historical features)**: ~18.5%
- **Precision for 1st place**: 34%
- Most important features: `Win_Odds`, `Finish_Time`, and `Declared_Horse_Weight`
- Stable performance across cross-validation, but struggled with predicting exact ranks beyond the top positions

### Neural Network (Keras Sequential)

- **Training Accuracy**: 95%
- **Test Accuracy**: ~10.8%
- **Mean Absolute Error**: ~2.47 positions
- The model performed very well on the training data but struggled on the test set, indicating overfitting. Despite some tuning, it wasn't able to generalize effectively — likely due to the high noise and complexity of the race outcome data

---

## Approach Overview

1. **Data Collection**  
   Scraped race results for Happy Valley events using Python. Some data had to be entered manually due to inaccessible or inconsistent pages.

2. **Data Cleaning**  
   - Removed irrelevant or problematic columns like `RunningPosition` and `Horse No.`
   - Handled missing values and standardized time formats
   - Converted date fields into Year, Month, and Day

3. **Feature Engineering**  
   - One-hot encoded categorical fields (`Horse`, `Jockey`, `Trainer`)
   - Created distance categories and aggregated historical metrics (e.g., win rates, average finish time)

4. **Exploratory Data Analysis (EDA)**  
   - Visualized distributions and outliers
   - Analyzed feature correlations and performance differences between jockeys/trainers

5. **Modeling and Evaluation**  
   - Split data chronologically: first 80% for training, last 20% for testing
   - Compared Random Forest and Neural Network performance
   - Evaluated accuracy, precision, and error metrics

6. **Fine-Tuning**  
   - Enriched the dataset with historical stats for each horse, jockey, and trainer
   - Observed modest accuracy gains, especially in Random Forest

---

## Key Takeaways

- Predicting horse racing results is extremely difficult — often closer to predicting lottery numbers than structured outcomes
- There’s no single dominant predictor; win odds and finish times are the most useful, but still limited
- Historical performance features added some predictive power, but not enough to overcome the randomness
- Models performed better at identifying potential winners than ranking the full field
- The project shows that even when accuracy is limited, you can still extract valuable insights about what factors *might* matter

---

## Data Source

All data was scraped from:  
[https://racing.hkjc.com/racing/information/English/racing/LocalResults.aspx](https://racing.hkjc.com/racing/information/English/racing/LocalResults.aspx)

---

## Tools Used

- Python (Pandas, NumPy, Matplotlib, Seaborn)
- Scikit-learn (Random Forest)
- TensorFlow / Keras (Neural Network)
- BeautifulSoup and Requests (Web scraping)

---

## Final Thoughts

This project was equal parts technical challenge and personal interest — using data science to analyze something I’ve grown up around in Hong Kong. While high test accuracy may always be out of reach in this domain, the process of building, cleaning, and exploring gave me a much deeper understanding of the modeling pipeline and how to deal with noisy, real-world data.
