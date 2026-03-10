# BoomBikes-Linear-Regression
Multiple Linear Regression model to predict BoomBikes demand

BoomBikes Shared Bike Demand Prediction


BRIEF DESCRIPTION
-----------------
A multiple linear regression model to predict daily bike rental demand (cnt)
for BoomBikes in the American market. The model helps management understand
which variables significantly affect demand so they can plan fleet allocation,
pricing, and marketing strategies for post-COVID recovery.


--------------------------------------------------------------------------------
TABLE OF CONTENTS
--------------------------------------------------------------------------------
1. General Information
2. Conclusions
3. Technologies Used
4. Acknowledgements
5. Contact


--------------------------------------------------------------------------------
1. GENERAL INFORMATION
--------------------------------------------------------------------------------

Background:
  BoomBikes is a US-based bike-sharing service that suffered significant revenue
  loss during the COVID-19 pandemic. As lockdowns ease and the economy recovers,
  the company wants to understand which factors drive daily bike demand so it
  can optimise its operations and stand out from competitors.

Business Problem:
  The goal is to identify the key variables that predict the total number of
  daily bike rentals (cnt) and quantify how well those variables explain demand.
  This insight will help management:
    - Allocate bikes and docks efficiently across seasons and weather conditions.
    - Design targeted promotions for low-demand periods.
    - Benchmark demand dynamics when entering new markets.

Dataset:
  The dataset contains 730 daily observations from 2018 to 2019 covering:
    - Temporal features  : year, month, weekday, season, holiday, working day
    - Weather features   : temperature, apparent temperature, humidity,
                           wind speed, weather situation
    - Target variable    : cnt (total daily bike rentals = casual + registered)

Data Preparation Steps:
  - Dropped irrelevant columns: instant, dteday
  - Dropped leakage columns  : casual, registered (sub-components of cnt)
  - Mapped numeric codes to string labels for season, weathersit, mnth, weekday
  - Created dummy variables using drop_first=True to avoid the dummy variable trap
  - Converted boolean dummy columns to int (fix for newer pandas versions)
  - Dropped atemp due to near-perfect multicollinearity with temp (r = 0.99)
  - Applied MinMaxScaler to temp, hum, windspeed (fit on train set only)


--------------------------------------------------------------------------------
2. CONCLUSIONS
--------------------------------------------------------------------------------

Conclusion 1 - Temperature is the strongest demand driver:
  Temperature (temp) carries the largest positive coefficient in the final model
  (approx. +0.49 to +0.55 on scaled features). Warmer days consistently attract
  more riders. BoomBikes should maximise bike availability during warm months
  (June to September) and consider cold-weather promotions to smooth revenue dips.

Conclusion 2 - Year-over-year growth is real and significant:
  The year indicator (yr: 0 = 2018, 1 = 2019) is the second strongest predictor.
  Demand grew substantially from 2018 to 2019, confirming rising adoption of the
  bike-sharing service. Management should continue fleet expansion year-over-year
  as demand is on an upward trend.

Conclusion 3 - Adverse weather sharply suppresses demand:
  Days with light snow or rain (weathersit_LightSnowRain) carry the largest
  negative coefficient (approx. -0.28 to -0.32). Bad weather is the single
  biggest demand suppressor. Proactive maintenance scheduling during adverse
  weather forecasts and dynamic pricing on such days can help protect revenue.

Conclusion 4 - Season and month effects matter for planning:
  Fall records the highest median rentals while Spring is the weakest season.
  Months like September, July, and August show peak demand. BoomBikes should
  run targeted marketing campaigns and discounted memberships in spring months
  to lift off-peak numbers and even out seasonal revenue fluctuations.

Model Performance:
  +-------------+--------+
  | Dataset     |   R2   |
  +-------------+--------+
  | Train Set   | ~0.84  |
  | Test Set    | ~0.80  |
  +-------------+--------+
  The model explains approximately 80% of variance in unseen daily bike demand,
  which is strong enough for strategic business planning.


--------------------------------------------------------------------------------
3. TECHNOLOGIES USED
--------------------------------------------------------------------------------

  - Python            - 3.10
  - pandas            - 2.0
  - numpy             - 1.24
  - matplotlib        - 3.7
  - seaborn           - 0.12
  - scikit-learn      - 1.3
  - statsmodels       - 0.14
  - scipy             - 1.11
  - Jupyter Notebook  - 6.5


--------------------------------------------------------------------------------
4. ACKNOWLEDGEMENTS
--------------------------------------------------------------------------------

  - Dataset provided as part of the UpGrad / IIITB Machine Learning & AI
    Programme - Linear Regression Assignment.

  - Problem statement based on the BoomBikes bike-sharing case study designed
    to simulate a real-world consulting engagement.

  - Modelling approach follows standard OLS regression best practices:
    RFE for feature shortlisting, iterative p-value and VIF-based elimination,
    and residual analysis for assumption validation.

  - References:
      * Fanaee-T, Hadi, and Gama, Joao (2013). Event labeling combining
        ensemble detectors and background knowledge. Progress in Artificial
        Intelligence, Springer Berlin Heidelberg.
      * Statsmodels documentation: https://www.statsmodels.org
      * Scikit-learn documentation: https://scikit-learn.org


--------------------------------------------------------------------------------
5. CONTACT
--------------------------------------------------------------------------------

  Created by Keshav N
  Feel free to contact me for questions or collaboration!

  GitHub Repository: https://github.com/Keshav-gowda/BoomBikes-Linear-Regression
--------------------------------------------------------------------------------
Note: Please download the PDF to view all pages — GitHub only previews pages.
