# COVID-19-and-Traffic-Collision-Analysis-in-Los-Angeles

### Table of Contents

  - [Project Overview](#project-overview)
  - [Data Sources](#Data-Sources)
  - [Tools](#Tools)
  - [Data Cleaning and Processing](#Data-Cleaning-and-Processing)
  - [Exploratory Data Analysis](#Exploratory-Data-Analysis)
  - [Dashboards and Visualizations](#Dashboards-and-Visualizations)
  - [Results](#Results)
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




### Results



### Future Work

1. Geographical Analysis:

### Limitations

1. Strong correlation =/= causation: While there is a significant negative correlation between the number of COVID-19 cases/deaths and the number of traffic collisions in Los Angeles, it does not necesarily mean that the pandemic...
   
2. The traffic dataset contains only reported collisions: A significant amount of traffic collisions go unreported and the percentage of unreported collisions may have changed during the pandemic pointing to more inaccuracies in the data.

3. Due to account access issues with Posit Cloud, the original R code and Shiny app are no longer available. However, the analysis and results are preserved in the final presentation and EDA documentation.
