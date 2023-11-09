This directory folder contains the following data frames:

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

- `pred_df.csv`: Monthly AQI data merged with `smoke_est.csv`, with imputed values in the missing AQI rows, and grouped by year.
  - **Columns**:
    - 'Year': The year of the monthly AQI estimate.
    - 'AQI': The mean estimated Air Quality Index value for the corresponding year.
    - 'GISAcres': The number of acres burned by the wildfire.
    - 'shortest_dist': The distance between the wildfire and the city.
    - 'Smoke_Estimate': The estimated impact of smoke. 
