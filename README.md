# Predicting-Air-Quality-Index-in-India
A Silent Killer in India: Air Pollution 


# Background
Air pollution has become one of the largest environmental health threats around the globe. India is among one of the most polluted countries in the world. According to 2021 World Air Quality Report, 12 out of 15 most polluted regional cities are in India.


# Data Source

## Links
* Link of data source: https://www.kaggle.com/rohanrao/air-quality-data-in-india
* Link of google drive files: https://drive.google.com/drive/folders/1__L1wkqn_bNUYqnrGgfSCeMvaKmzIHJ7?usp=sharing
* Link of google colab: https://colab.research.google.com/drive/1VTzibDmWUCpjMejaE4oSgzyZejCQ-gox?usp=sharing

## Data Description
We will use a dataset in Kaggle which deals with air quality in India from 2015 to 2020, across various cities and stations. The variables include PM2.5, PM10, Air Quality Index (AQI), and gas concentrations for NO, NO2, CO, etc. There are 16 variables in total.

3 datasets are planned to be used:

   * `city_day.csv`: day-level air quality data for 26 cities from 2015 to 2020. After a quick clean-up, approximately 20,000 observations can be used for analysis.
   * `station_day.csv`: day-level air quality data for 110 stations from 2015 to 2020. Approximately 70,000 observations are valid to be used.
   * `stations.csv`: the city and state information for each station.


# Model Building
We implement various models for the AQI index at the station level.

Linear regression model, Gradient Boosting Regression, Neural Network, and SARIMA time series prediction model are used.

1. Our linear regression model achieves an R2 of 0.6823 and an MAE of 44.256. This is a simple linear regression model, which provides evidence that the features included in our model are relevant, with some room for hyperparameter tuning.
2. The best model is gradient boosting regression, with an R2 of 0.8788, and an MAE of 23.7028.
    * This model is built to train trees sequentially, one at a time, and each tree will correct the errors of the previous one. So it can capture the complex pattern within the data.
    * We set the n_estimators = 500, which is sufficient to correct the errors of previous trees.
3. Our neural network also has a good performance in prediction, with an R2 of 0.8624 and an MAE of 25.224 on testing data.
4. The time series forecasting for Delhi did a fairly good job in capturing the trend and seasonality, achieving an R2 of 0.5636 and an MAE of 59.002 on testing data. This is not the best model to predict AQI, but it provides some valuable insights in the pattern of AQI changes itself.

# Conclusion
## Findings
Throughout the project, we have come up with several findings:

### Spatial pattern
There’s a huge disparity in AQI across India. Among all the states we have collected data from, Mizoram, Meghalaya, Kerala, and Chandigarh have the best air quality based on averaged AQI, while Bihar, Uttar Pradesh, Delhi, and Gujarat have the worst air quality. The gap between these regions is also widening.
### Temporal pattern
Nationwide: by looking at the average AQI for each date across the country, we can identify that there are a clear trend and seasonality. Overall the averaged AQI is gradually decreasing, indicating an improvement in air quality, but the votality is also increasing which suggests more variance. AQI usually starts to rise up from around September, peaks from October to February which is mainly winter, and is usually at its bottom in the middle of the year which is mainly summer.
Delhi: after we specifically look into the time series data of Delhi, we noticed a similar pattern that showed across the nation.
### Feature importance
We have conducted PCA but found out that we would lose too much information if we try to reduce dimensions.
PM2.5 appears to be the most important feature in determining AQI, both in terms of its high correlation with AQI, and its importance in the models.


## Behind the data: air quality condition in India
### Seasonality
After we did research on India’s air quality, we found out that contributions from stubble burning and household emissions from cooking and space heating were significant fractions of the pollution pie, which can explain why AQI started to increase dramatically from September. Harvesting seasons which start around September could result in a significant increase in the number of fires; In the following months, the contribution from household emissions (including domestic cooking, space heating, water heating, and lighting) primarily drove poor air quality with the kick-in of winters.
Space heating and stubble burning mainly contribute to the production of PM2.5, which can partly explain the importance of PM2.5 in predicting AQI.
### Data Collection
After 2018, BJP (a political party) came into power after the congress. They came up with a lot of programs that ensure data collection by government agencies, which explains why we can see a significant increase in the number of cities/stations in our dataset after 2018.
### Emissions are the main cause
Emissions from stubble burning, household heating, vehicles, and power plants made up the majority of the air pollutant in India. The spatial and temporal patterns we see in the analysis are deeply knitted with the emissions.
## Challenges
### Hyperparameter tuning 
We spent some time experimenting with the parameters that can optimize the performance of our chosen model.
### Time series forecasting 
How to aggregate data. After inspecting the trend and seasonality of this time series data, we identified the seasonality period of 12 months. But our raw data is by date, which puts a high requirement on the computational ability of our computer if we set the period/freq to 365 when training our model. So eventually we chose to aggregate our data by week, which greatly reduced the number of observations, but can still capture the differences between each observation.
### How to combine the spatial and temporal data together.

## Potential Next Steps
* We could continue to tune our models, to achieve better performances (potentially)
* We could take a step further, to study which factors will have an impact on PM2.5, PM10, CO, etc. We can bring in factors like meteorological data, and emission data (like open fire data, stubble burning data, congestion data, power generation data).
* We could explore models using panel data which allows us to identify 1) cross-sectional differences and 2) changes over time. Hopefully, we can come up with a model that can capture the spatial disparities in India, as well as the temporal patterns.


# Other Deliverable: Medium Blog
Link: https://medium.com/@jiaxu7/a-silent-killer-in-india-air-pollution-7c3ec9663bdc

# Reference
1. Plotly Documentation: https://plotly.com/python/

2. Plotting Data Visualisation on the Map of India using GeoPandas in Python: https://shankhanilborthakur.medium.com/plotting-data-visualisation-on-the-map-of-india-using-geopandas-in-python-211bc88c1e4d

3. https://www.ceew.in/sites/default/files/ceew-study-on-controlling-delhi-air-pollution-2021_1.pdf
