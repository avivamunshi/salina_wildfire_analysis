This directory folder contains the following data frames:

- `distance.csv`: Contains information about all fires occurring near Salina. 
  - **Columns**:
    - 'OBJECTID': Unique identifier for each fire feature.
    - 'shortest_dist': The shortest distance from the fire to Salina in miles.

- `miles.csv`: Contains information about fires occurring within 1250 miles of Salina. 
  - **Columns**:
    - 'OBJECTID': Unique identifier for each fire feature.
    - 'shortest_dist': The shortest distance from the fire to Salina in miles.

- `features.csv`: Contains details about fires that occurred after 1963. 
  - **Columns**:
    - 'OBJECTID': Unique identifier for each fire feature.
    - 'FireType': The type of the fire.
    - 'FireYear': The year in which the fire occurred.
    - 'GISAcres': The number of acres affected by the fire.
    - 'OverlapFlags': Flags indicating overlap within 1 or 2 regions.
      
- `filter.csv`: Combines data from `features.csv` and `miles.csv` based on the 'OBJECTID' column.
  - **Columns**:
    - 'OBJECTID': Unique identifier for each fire feature.
    - 'FireType': The type of the fire.
    - 'FireYear': The year in which the fire occurred.
    - 'GISAcres': The number of acres affected by the fire.
    - 'OverlapFlags': Flags indicating overlap within 1 or 2 regions.
    - 'shortest_dist': The shortest distance from the fire to Salina in miles.

- `smoke_est_without_agg.csv`: Provides estimates of the impact of smoke from wildfires on Salina. 
  - **Columns**:
    - 'FireYear': The year of the wildfire.
    - 'GISAcres': The number of acres burned by the wildfire.
    - 'shortest_dist': The distance between the wildfire and the city.
    - 'Smoke_Estimate': The estimated impact of smoke.

- `smoke_est.csv`: Provides estimates of the impact of smoke from wildfires on Salina, grouped by year. 
  - **Columns**:
    - 'FireYear': The year of the wildfire.
    - 'GISAcres': The number of acres burned by the wildfire.
    - 'shortest_dist': The distance between the wildfire and the city.
    - 'Smoke_Estimate': The estimated impact of smoke.

- `monthly_aqi.csv`: Contains monthly estimates of the AQI for Salina. 
  - **Columns**:
    - 'Year': The year of the monthly AQI estimate.
    - 'Month': The month of the AQI estimate.
    - 'AQI': The estimated Air Quality Index value for the corresponding year and month.

- `pred_df.csv`: Monthly fire season AQI data merged with `smoke_est.csv`, with imputed values in the missing AQI rows, and grouped by year.
  - **Columns**:
    - 'Year': The year of the monthly AQI estimate.
    - 'AQI': The mean estimated Air Quality Index value for the corresponding year.
    - 'GISAcres': The number of acres burned by the wildfire.
    - 'shortest_dist': The distance between the wildfire and the city.
    - 'Smoke_Estimate': The estimated impact of smoke. 

- `forecasted_values.csv`: Forecasted values of Smoke Estimate from 2021 to 2045. 
  - **Columns**:
    - 'Index': The date of the forecasted smoke estimated. There's one year for each date.
    - 'Forecasted_Values': The forecasted values of smoke estimate from 2021 to 2045.

- `aqi.csv`: Consolidated dataframe of AQI with corresponding year in the city of Salina. Obtained by filtering out fires not in the fire season and with imputed values.
  - **Columns**:
    - 'Year: The Year of the computed AQI.
    - 'AQI': The value of AQI.

- `income_industry.csv`: Dataframe containing information about the count of residents of Salina employed in different industries, in different income brackets, and various forms of aid given by the government officials of Salina from the years 2011 to 2021.
  - **Columns**:
    - 'Salina_Count: The number of people in Salina employed in that industry/in the income bracket/amount the government was giving in aid for that particular year.
    - 'Metrics': Categorical column with values "Industry" or "Income".
    - 'Sub Metric': Sub category of the metric, encompasses different income brackets, industries in the city and different kinds of aid.
    - 'Year': Corresponding year for the data.

- `analysis_1.csv`: Dataframe containing the employment, unemployment, smoke estimate and aqi values in salina. This is the result of a merge on the employment and unemployment numbers dataframe and pred_df.csv.
  - **Columns**:
    - 'Year: Years from 1990 to 2020.
    - 'Salina_Employment': Numbers for yearly employment in Salina.
    - 'Salina_Unemployment': Numbers for yearly unemployment in Salina.
    - 'Smoke_Estimate': The estimated impact of smoke. 
    - 'AQI': The mean estimated Air Quality Index value for the corresponding year.

- `analysis_2.csv`: Result of merging income_industry.csv and pred_df.csv.
  - 'Salina_Count: The number of people in Salina employed in that industry/in the income bracket/amount the government was giving in aid for that particular year.
    - 'Metrics': Categorical column with values "Industry" or "Income".
    - 'Sub Metric': Sub category of the metric, encompasses different income brackets, industries in the city and different kinds of aid.
    - 'Year': Corresponding year for the data.
    - 'AQI': The mean estimated Air Quality Index value for the corresponding year.
    - 'Smoke_Estimate': The estimated impact of smoke. 