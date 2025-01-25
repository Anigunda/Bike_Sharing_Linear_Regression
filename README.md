# Bike_Sharing_Linear_Regression
 
<span style="color:green">

## Problem Statement

</span>

A bike-sharing system is a service in which bikes are made available for shared use to individuals on a short-term basis for a price or free. BoomBikes, a US bike-sharing provider, has suffered considerable dips in their revenues due to the ongoing Corona pandemic. The company aims to understand the demand for shared bikes among the people after the quarantine situation ends to prepare and cater to the people's needs effectively.

<span style="color:green">

## Business Goal

</span>

Model the demand for shared bikes with the available independent variables to understand how the demands vary with different features. This model will help the management manipulate the business strategy to meet the demand levels and meet customer expectations.

<span style="color:green">

## Data Dictionary

</span>

- **instant:** Record index.
- **dteday:** Date in `dd-mm-yyyy` format.
- **season:** Season of the year (1 = Spring, 2 = Summer, 3 = Fall, 4 = Winter).
- **yr:** Year (0 = 2018, 1 = 2019).
- **mnth:** Month of the year (1 = January, ..., 12 = December).
- **holiday:** Indicates whether the day is a holiday (1 = Holiday, 0 = Not a Holiday).
- **weekday:** Day of the week (0 = Sunday, ..., 6 = Saturday).
- **workingday:** Indicates whether the day is a working day (1 = Working Day, 0 = Weekend or Holiday).
- **weathersit:** Weather situation:
    - 1: Clear, Few clouds, Partly cloudy.
    - 2: Mist + Cloudy, Mist + Few clouds.
    - 3: Light Snow, Light Rain, Thunderstorm, Scattered clouds.
    - 4: Heavy Rain, Ice Pellets, Snow, Fog.
- **temp:** Actual temperature in Celsius (normalized in the dataset).
- **atemp:** Perceived or "feeling" temperature in Celsius.
- **hum:** Humidity percentage.
- **windspeed:** Wind speed.
- **casual:** Count of casual users renting bikes.
- **registered:** Count of registered users renting bikes.
- **cnt:** Total count of rentals (sum of `casual` and `registered`).

<span style="color:green">

## High-Level Approach

</span>

<span style="color:green">

### 1. Data Understanding

</span>

- Reviewed the dataset structure, types of variables, and checked for missing values.
- Identified the target variable (`cnt`) and potential independent variables.

<span style="color:green">

### 2. Data Cleaning and Preprocessing

</span>

- Dropped unnecessary columns such as `instant`.
- Converted the `dteday` column into a datetime format for feature extraction.
- Removed `casual` and `registered` to avoid data leakage as they sum up to `cnt`.

<span style="color:green">

### 3. Feature Engineering

</span>

- Checked for highly correlated features like `temp` and `atemp` to avoid redundancy.
- Encoded categorical variables such as `season` and `weathersit` using one-hot encoding.

<span style="color:green">

### 4. Exploratory Data Analysis (EDA)

</span>

- Analyzed distributions of variables and visualized their relationships with the target variable.
- Examined correlations to understand significant predictors and potential multicollinearity.

<span style="color:green">

### 5. Model Building

</span>

- Split the data into training and testing sets.
- Built a multiple linear regression model to predict bike demand (`cnt`).
- Evaluated the model using metrics such as R-squared, Adjusted R-squared, and RMSE.

<span style="color:green">

### 6. Model Refinement

</span>

- Iteratively removed insignificant predictors based on p-values.
- Tested transformations and interactions for non-linear relationships.

<span style="color:green">

### 7. Insights and Recommendations

</span>

- Interpreted the model coefficients to provide actionable business insights.
- Suggested strategies to optimize bike-sharing operations based on the analysis.

<span style="color:green">

## Findings

</span>

<span style="color:green">

### Model Performance

</span>

<span style="color:green">

#### Train Data

</span>

- **R-squared**: 0.824
- **Adjusted R-squared**: 0.821
- **F-statistic**: 293.1 (p-value = 1.63e-183)
- All predictors are statistically significant (p-values < 0.05).

<span style="color:green">

#### Test Data

</span>

- **R-squared**: 0.731
- **Adjusted R-squared**: 0.720

<span style="color:green">

### Residual Analysis

</span>

- The residuals are randomly scattered around zero, indicating no clear pattern or heteroscedasticity.
- The residuals deviate from the theoretical quantiles at the tails, indicating non-normality.
- The residuals are slightly left-skewed and have heavier tails than a normal distribution.

<span style="color:green">

### Significant Predictors of Bike Demand

</span>

- **Positive Impact**:
    - `yr` (Year): Bike demand increases over time.
    - `atemp` (Feeling Temperature): Higher perceived temperatures lead to increased bike rentals.
    - `season_winter`: Winter season shows a slight positive impact on bike demand compared to spring.
- **Negative Impact**:
    - `holiday`: Bike demand decreases on holidays.
    - `windspeed`: Higher wind speeds reduce bike rentals.
    - `season_spring`: Spring season has a negative impact on bike demand compared to other seasons.
    - `weathersit`: Adverse weather conditions significantly reduce bike demand.

<span style="color:green">

## Recommendations for BoomBikes

</span>

1. **Business Strategy**:
     - Focus on marketing and promotions during favorable weather conditions.
     - Offer incentives or discounts during holidays and adverse weather conditions.
     - Plan for increased bike availability during peak seasons and years with expected growth in demand.

<span style="color:green">

## Final Regression Equation for Bike Demand Prediction

</span>

cnt = **0.2149** + **0.2417** * **`yr`** - **0.1020** * **`holiday`** + **0.4616** * **`atemp`** - **0.1286** * **`season_spring`** + **0.0613** * **`season_winter`** - **0.3296** * **`weathersit_Light Snow/Light Rain + Thunderstorm`** - **0.0678** * **`weathersit_Mist + Cloudy`**

#### Explanation of Terms:
- **Intercept (0.2149)**: Baseline bike demand when all predictors are zero.
- **yr (0.2417)**: Bike demand increases by 0.2417 units for each year.
- **holiday (-0.1020)**: Bike demand decreases by 0.1020 units on holidays.
- **atemp (0.4616)**: Bike demand increases by 0.4616 units for each unit increase in feeling temperature.
- **season_spring (-0.1286)**: Bike demand decreases by 0.1286 units during spring compared to the reference season.
- **season_winter (0.0613)**: Bike demand increases by 0.0613 units during winter compared to the reference season.
- **weathersit_Light Snow/Light Rain + Thunderstorm (-0.3296)**: Bike demand decreases by 0.3296 units during light snow, light rain, or thunderstorms.
- **weathersit_Mist + Cloudy (-0.0678)**: Bike demand decreases by 0.0678 units during misty or cloudy weather.

This model provides a strong fit for the data, explaining a significant portion of the variance in bike demand and offering actionable insights for BoomBikes to optimize their operations.