### Technical Report: Analysis and Forecasting of Walmart Store Sales

### Analysis Notebook

https://github.com/tashfia-shoron/Analysis-and-Forecasting-of-Walmart-Store-Sales/blob/main/Analysis_and_Forecasting_of_Walmart_Store_Sales.ipynb

#### Objective
The objective of this analysis is to predict future weekly sales for Walmart stores accurately. This helps the store management plan inventory, optimize supply chain logistics, and schedule promotional events, especially during peak sales periods such as holidays.

#### Dataset Overview
The dataset spans weekly sales data for **45 Walmart stores** from **February 2010 to October 2012**. Each data entry contains:
- **Store**: Identifier for the store.
- **Date**: The week of sales.
- **Weekly_Sales**: Total sales for the given store and week.
- **Holiday_Flag**: Indicates if the week includes a major holiday (1 for holiday weeks, 0 for non-holiday weeks).
- **Temperature, Fuel_Price, CPI, Unemployment**: Economic indicators that may affect sales.

For this analysis, we focused on **Store 1** to develop and test models for forecasting.

#### Exploratory Data Analysis (EDA)

1. **Overall Sales Trend**:
   - A time series plot of weekly sales for Store 1 revealed noticeable cyclical patterns with significant peaks during known holidays, such as Thanksgiving and Christmas. These peaks suggest that holiday weeks greatly influence sales, confirming the need for targeted forecasting.

2. **Holiday Impact on Sales**:
   - A box plot comparing sales during holiday and non-holiday weeks showed that sales were significantly higher during holiday weeks. The median sales in holiday weeks were higher, and there was a larger spread in the data, indicating variability due to factors such as holiday promotions and increased customer spending.
   - **Key Insight**: Forecasting models need to account for holiday effects to improve prediction accuracy during peak periods.

3. **Sales Trends by Year**:
   - Analyzing sales trends for each year indicated that seasonal peaks were consistent, especially around the 11th month (November) and 12th month (December), aligning with major U.S. holidays.
   - **Observation**: Understanding these consistent peaks is crucial for planning stock and promotions.

4. **Correlation Analysis**:
   - A correlation matrix for weekly sales and economic factors (temperature, fuel price, CPI, and unemployment) showed:
     - **Weak positive correlation** between temperature and sales, suggesting that warmer weather might slightly influence shopping behavior.
     - **Minimal or negligible correlations** between sales and other economic indicators, implying that these variables alone do not significantly affect weekly sales.
   - **Insight**: While economic factors are part of the analysis, trends and seasonality play a more critical role in influencing weekly sales.

5. **Seasonality Check**:
   - A deeper analysis using autocorrelation functions (ACF) confirmed the presence of strong seasonality at a lag of approximately 52 weeks, representing yearly patterns. This insight directed the choice of using models that could incorporate seasonal components effectively.

#### Modeling Approaches
Multiple models were tested to identify the best method for accurate forecasting:

1. **Simple Exponential Smoothing**:
   - This model applied a simple weighted average of past observations to forecast future sales.
   - **Result**: Produced a baseline forecast with a flat prediction line that did not capture seasonal variations or trends effectively.
   - **Evaluation**: Useful as a benchmark but inadequate for dynamic, time series-like predictions.

2. **Holt’s Linear Trend Model**:
   - Added a linear trend to the simple exponential smoothing to capture upward or downward trends over time.
   - **Observation**: Provided better forecasts than simple smoothing, but the predictions were still linear, missing seasonal sales fluctuations.
   - **Limitation**: While the model introduced a trend, it did not capture the time series pattern seen in historical sales.

3. **Holt-Winters Additive Model**:
   - Included both a linear trend and an additive seasonal component to capture seasonality over 52 weeks.
   - **Result**: Significantly improved the forecast, providing dynamic, time series-like predictions that aligned with historical fluctuations.
   - **Evaluation Metrics**:
     - **Mean Absolute Error (MAE)** and **Root Mean Squared Error (RMSE)** indicated a reasonable match with actual sales, but with occasional overestimations during peak periods.

4. **SARIMA (Seasonal ARIMA)**:
   - The SARIMA model was applied to better capture both seasonality and trend in a more flexible framework.
   - **Model Parameters**:
     - **Order (p, d, q)**: Parameters for autoregression, differencing, and moving average.
     - **Seasonal Order (P, D, Q, S)**: Seasonal counterparts for autoregression, differencing, and moving average with a season length of 52 weeks.
   - **Result**: While SARIMA handled seasonality and trend, initial versions often led to over-predictions, especially during non-peak months like September.
   - **Adjustments**:
     - Parameters were tuned to reduce over-predictions by simplifying the model's complexity (lowering the autoregressive and seasonal components).
     - **Challenge**: Despite tuning, SARIMA sometimes amplified seasonal effects, leading to exaggerated peaks.

#### Model Comparison and Insights
- **Simple Exponential Smoothing**: Served as a baseline with no trend or seasonality.
- **Holt’s Linear Trend Model**: Captured trends but lacked seasonality.
- **Holt-Winters Additive Model**: Balanced trend and seasonality, providing realistic time series-style predictions.
- **SARIMA**: Showed potential for flexible modeling of seasonality and trend but needed careful tuning to avoid over-prediction.

**Best Performing Model**:
- **Holt-Winters Additive Model** was the most effective at producing time series-like predictions that captured both the trend and seasonality. It provided a good balance between under- and over-prediction, making it suitable for forecasting Walmart's weekly sales.

#### Final Insights and Recommendations
- **Holiday Planning**: Accurate forecasting of holiday sales peaks is essential for effective inventory and promotion planning. Future models should incorporate holiday indicators or external factors for further accuracy.
- **Model Complexity**: While SARIMA models offer flexibility, simpler models like Holt-Winters can often provide more reliable forecasts with easier tuning.


**Conclusion**:
The analysis showed that while simpler models establish a strong foundation, incorporating seasonality and trend through the **Holt-Winters Additive Model** yields more accurate and realistic forecasts. For further improvement, advanced machine learning techniques and external features can be explored.

**Reference**:
 - https://www.kaggle.com/datasets/yasserh/walmart-dataset/data
