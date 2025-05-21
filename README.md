# COVID-19-and-Traffic-Collision-Analysis-in-Los-Angeles

### Table of Contents

  - [Project Overview](#project-overview)
  - [Data Sources](#Data-Sources)
  - [Tools](#Tools)
  - [Data Cleaning and Processing](#Data-Cleaning-and-Processing)
  - [Exploratory Data Analysis](#Exploratory-Data-Analysis)
  - [Dashboards and Visualizations](#Dashboards-and-Visualizations)
  - [Results](#Results)
  - [Conclusion](#Conclusion)
  - [Future Work](#Future-Work)
  - [Limitations](#Limitations)

### Project Overview

As COVID-19 cases surged and strict stay-at-home orders were implemented, many businesses transitioned to remote work, schools closed, and non-essential travel was discouraged or prohibited altogether. These changes led to a significant decrease in the number of vehicles on the road.

This project presents an in-depth analysis of the correlation between traffic collisions and the number of COVID-19 cases and deaths in Los Angeles, California, one of the largest cities in the U.S. and notorious for bad traffic.

The goal of this project is to identify whether a relationship exists between the number of COVID-19 cases and deaths and traffic collisions in Los Angeles. By examining trends during the pandemic, this analysis aims to discover how public health measures and behavioral shifts may have influenced road safety in a large urban environment.

### Project Questions

1. Is there a correlation between the number of COVID-19 deaths/cases and the number of traffic collisions in Los Angeles?
  
2. If there is a correlation found between this variables what is the nature of the relationship and what can we learn from it?

3. Which regression model is the most accuracte and can it be used to make future predictions?

### Data Sources

The data for this project was collected from the data.gov website. There are two .csv files that were exported from the website and then processed and analyzed in R studio:

1. The first dataset contains information on the number of deaths, cases, new cases and new deaths for both the city of Los Angeles and the State of California.
2019-2023

LA County Covid Cases: https://catalog.data.gov/dataset/la-county-covid-cases

2. The second dataset contains information on traffic collisions reported in Los Angeles. This dataset includes the date and time of the collision, the geographical information of the incident and the victim demographics.
 
https://catalog.data.gov/dataset/traffic-collision-data-from-2010-to-present

### Tools

![Excel](https://img.shields.io/badge/Microsoft_Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![RStudio](https://img.shields.io/badge/RStudio-75AADB?style=for-the-badge&logo=rstudio&logoColor=white)
![Shiny](https://img.shields.io/badge/Shiny-R%20Framework-006cab?style=for-the-badge&logo=r&logoColor=white)

  
### Data Cleaning and Processing

- Column Removal: Unnecessary columns were removed from both datasets to streamline the analysis. Examples include geographic markers (e.g., county, state), administrative codes, and unused fields (e.g., test counts, lat/long).

- Handling Missing Values: The only column with missing data was Victim.Age in the traffic dataset, which wasn’t essential to the correlation analysis. No rows were removed due to missing key variables like date or collision count.

- Date Formatting and Sorting: Dates were converted using as.Date() and sorted chronologically using order() to ensure time-based alignment.

- Deduplication: Duplicate rows were removed using the distinct() function in R.

- Column Renaming and Data Joining: The traffic dataset’s date column (Date.Occurred) was renamed to date to match the COVID-19 dataset. A full join was performed using full_join() to preserve pre-pandemic traffic data (2010–2019) and pandemic-era data (2020–2023).


### Exploratory Data Analysis

A full exploratory data analysis report is available in the EDA folder. Below is a summary of the EDA process:

✅ Univariate Analysis

- COVID-19 Case Variation: A wide range of daily new cases, with significant spikes and data irregularities early in the pandemic.
- Collision Victim Age: A near-normal distribution, with peaks in the early-to-late 20s, indicating younger drivers are more frequently involved.
- Gender Distribution: Male victims were significantly more common in reported collisions.

✅ Bivariate Analysis

- COVID Deaths vs. Cases: Strong linear correlation, validating data quality and pandemic progression.
- Traffic Collisions Over Time: Clear visual dip in daily collisions starting in early 2020, aligning with stay-at-home mandates.
- COVID Cases vs. Collisions: Apparent inverse relationship — as cases increased, traffic collisions decreased.

✅ High-Dimensional Analysis

- Scatterplot Matrix: Strong correlations between deaths, total cases, and new cases. Weak correlations between new deaths and new cases suggest reporting inconsistency.
- 3D Scatterplot (Cases, Deaths, Collisions): Revealed clusters likely corresponding to pandemic phases. Notable transition from high-collision, low-case areas to high-case, low-collision periods.

✅ Advanced Techniques Used

- Outlier Detection: Boxplots identified valid extreme values, confirming no extreme data entries.
- Multiple Linear Regression: Statistically significant model (p < 0.05 for both cases and deaths), with an R² of 0.736, indicating that ~74% of variation in collision counts can be explained by COVID case and death trends.
- K-means Clustering: Identified three natural groupings of data, representing different stages of the pandemic with distinct traffic-collision behavior.

### Visualizations

Polynomial Regression (6 degree):

##### Collisions vs Cases

![image](https://github.com/user-attachments/assets/1a2df61e-0a72-4d37-8f47-0b12dfc14975)

##### Collisions vs Deaths

![image](https://github.com/user-attachments/assets/d675eaff-9e5e-40a4-bed4-3e433e2b0638)

Fitting polynomial models produced significantly better results than the linear models. Not only are the
p-values very small but the Multiple R-squared values for the polynomial models (cases: 0.8647, deaths:
0.8774) are much higher than the values for the linear models (cases: 0.499, deaths: 0.703). This tells me
that the predictor variables explain much more of the variance in the response variable when fitting the
polynomial models to the data. Overall these models help me to see that there is a very clear correlation
between traffic collisions and cases/deaths. When traffic collisions were high cases/deaths were low vice versa.

### Results

The analysis revealed a strong and statistically significant relationship between the number of COVID-19 cases/deaths and the number of traffic collisions in Los Angeles. Multiple modeling techniques were used to evaluate the nature of this relationship:

1. Linear Regression
Linear regression models were first applied using total COVID-19 cases and deaths as predictors of total traffic collisions. Both models returned extremely low p-values (p < 2.2e-16), indicating a statistically significant relationship:

Cases model R² = 0.498

Deaths model R² = 0.703

While statistically significant, the linear trend did not visually capture the non-linear nature of the data distribution, indicating the need for more flexible models.

2. Polynomial Regression
Polynomial regression models (degree = 6) provided a far better fit:

Cases model R² = 0.865

Deaths model R² = 0.877

These models captured the curvature present in the data and revealed a clear inverse relationship: as COVID-19 cases and deaths increased, the number of daily traffic collisions decreased. The improvement in model fit confirms that the relationship between these variables is non-linear and more complex than what a simple linear regression can express.

3. Negative Binomial Regression
Given that the dependent variable (collision counts) is discrete and showed overdispersion, a negative binomial model was implemented. This model confirmed the significance of both predictors:

Positive relationship between COVID cases and collisions

Stronger negative relationship between COVID deaths and collisions

Although the model identified significant predictors, visual inspection suggested it still struggled to accurately fit the data, similar to linear models, but it performed better than a Poisson model previously used.

4. Principal Component Regression
Due to multicollinearity concerns between COVID case and death counts (confirmed by high VIF scores), PCA was employed. The first principal component explained over 96% of the variance, allowing it to be used as the sole predictor in a linear model:

Principal Component Model R² = 0.701

P-value < 2.2e-16

This model again confirmed a strong and negative correlation between the principal component (a combined measure of cases and deaths) and the number of traffic collisions.

### Conclusion

All four modeling approaches confirm a strong, statistically significant inverse relationship between COVID-19 metrics and traffic collisions. Polynomial regression best captured the trend and offered the highest explanatory power.Negative binomial regression was a better fit for overdispersed count data but didn’t outperform polynomial regression in visual accuracy. PCA helped reduce multicollinearity and still supported the key finding of a strong negative relationship.

Through extensive data cleaning, exploratory analysis, and multiple modeling techniques, the results consistently revealed a strong inverse relationship: as COVID-19 cases and deaths increased, the number of traffic collisions significantly decreased. Polynomial regression models provided the best fit, while negative binomial regression and principal component analysis further confirmed the strength and statistical significance of the correlation. These findings suggest that pandemic-related behavioral changes, such as lockdowns and reduced travel, had a measurable impact on road safety. While causation cannot be definitively concluded, this analysis highlights the interconnected nature of public health and transportation patterns and offers valuable insight for future traffic and safety policy planning during times of crisis.

### Future Work

1. Geographical Analysis:

### Limitations

1. Strong correlation =/= causation: While there is a significant negative correlation between the number of COVID-19 cases/deaths and the number of traffic collisions in Los Angeles, it does not necesarily mean that the pandemic...
   
2. The traffic dataset contains only reported collisions: A significant amount of traffic collisions go unreported and the percentage of unreported collisions may have changed during the pandemic pointing to more inaccuracies in the data.

3. Due to account access issues with Posit Cloud, the original R code and Shiny app are no longer available. However, the analysis and results are preserved in the final presentation and EDA documentation.
