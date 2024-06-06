# Store-Sales-Data-Prediction

## Dataset Description
This repository has the code for predicting the sales for the thousands of product families sold at Favorita stores located in Ecuador. The training data includes dates, store and product information, whether that item was being promoted, as well as the sales numbers. Additional files include supplementary information that may be useful in building your models.

## File Descriptions and Data Field Information
*train.csv*
The training data, comprising time series of features store_nbr, family, and onpromotion as well as the target sales.
store_nbr identifies the store at which the products are sold.
family identifies the type of product sold.
sales gives the total sales for a product family at a particular store at a given date. Fractional values are possible since products can be sold in fractional units (1.5 kg of cheese, for instance, as opposed to 1 bag of chips).
onpromotion gives the total number of items in a product family that were being promoted at a store at a given date.

*test.csv*
The test data, having the same features as the training data. You will predict the target sales for the dates in this file.
The dates in the test data are for the 15 days after the last date in the training data.

*stores.csv*
Store metadata, including city, state, type, and cluster.
cluster is a grouping of similar stores.

*oil.csv*
Daily oil price. Includes values during both the train and test data timeframes. (Ecuador is an oil-dependent country and it's economical health is highly vulnerable to shocks in oil prices.)

*holidays_events.csv*
Holidays and Events, with metadata
NOTE: Pay special attention to the transferred column. A holiday that is transferred officially falls on that calendar day, but was moved to another date by the government. A transferred day is more like a normal day than a holiday. To find the day that it was actually celebrated, look for the corresponding row where type is Transfer. For example, the holiday Independencia de Guayaquil was transferred from 2012-10-09 to 2012-10-12, which means it was celebrated on 2012-10-12. Days that are type Bridge are extra days that are added to a holiday (e.g., to extend the break across a long weekend). These are frequently made up by the type Work Day which is a day not normally scheduled for work (e.g., Saturday) that is meant to payback the Bridge.
Additional holidays are days added a regular calendar holiday, for example, as typically happens around Christmas (making Christmas Eve a holiday).

Certainly! Here's a summary of the code provided:

### Objective:
The code implements a forecasting solution for sales data using machine learning models, specifically LightGBM, and various preprocessing techniques.

### Methodology:
1. **Data Preparation:**
   - The sales data is loaded and preprocessed, including handling missing values and encoding categorical variables.
   - Time series data for each product family is extracted and organized into a dictionary.
   - Covariates such as oil prices, holidays, and promotions are prepared and transformed.

2. **Model Training:**
   - Two methods are discussed: training a single machine learning model for all families and training separate models for each product family. The latter method performs better.
   - For each product family:
     - The data is prepared and transformed using pipelines to handle missing values, encode categorical variables, apply logarithmic transformations, and scale the data.
     - Various temporal covariates are generated to capture seasonality and trends.
     - Models are trained using LightGBM, considering different sets of parameters.

3. **Model Evaluation and Prediction:**
   - Models are evaluated based on Mean Square Error (MSE).
   - Predictions are made for future time periods using trained models.
   - Forecasts are inverse-transformed to the original scale.
   - Negative forecasts are set to zero to ensure they are meaningful.
   - Forecasts are concatenated with the test data and prepared for submission.

### Summary:
The code provides a comprehensive approach to forecasting sales data using machine learning techniques. It involves thorough data preprocessing, model training, and prediction steps. By training separate models for each product family and considering various covariates, the solution aims to provide accurate sales forecasts. The use of LightGBM models allows for efficient training and prediction, making it suitable for large-scale forecasting tasks.
