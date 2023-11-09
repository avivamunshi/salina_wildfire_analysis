# DATA512 Project Part 1

This repository contains data and code for a human-centered data science project focused on understanding the impact of wildfires on the air quality of the city of Salina. The project's goal is to analyze historical data and make predictions for future years.

## Goal

The goal of this project is to predict the impact of smoke from wildfires on the air quality in Salina for 25 years based on existing data about AQI and Wildfire data in the USA. It involves analyzing historical data, including smoke estimates, air quality index (AQI), and fire-related information, to make these predictions.

## Licenses and API Information

- This project has been licensed under the [MIT License](https://github.com/avivamunshi/salina_wildfire_analysis/blob/main/LICENSE).     
- Further, some code written by Professor David McDonald has been used from the notebooks linked within the code as and when samples are used. The notebooks are licensed for use in DATA 512, a course in the UW MS Data Science degree program. This code is provided under the [Creative Commons CC-BY license](https://creativecommons.org/licenses/by/4.0/). Revision 1.0 - August 13, 2023.   
- Data about the wildfires has been extracted from the USGS website, and this has been provided by the [United States Geological Survey](https://www.usgs.gov/). USGS-authored or produced data and information are considered to be in the U.S. Public Domain. The dataset being used is the [Combined wildland fire datasets for the United States and certain territories, 1800s-Present (combined wildland fire polygons)](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81). The metadata can be found [here](https://www.sciencebase.gov/catalog/file/get/61aa537dd34eb622f699df81?f=__disk__d0%2F63%2F53%2Fd063532049be8e1bc83d1d3047b4df1a5cb56f15&transform=1&allowOpen=true).  


### Raw Data Files

The following raw data files are used in this project:
- The “Wildland Fire Polygons Fire Feature Data Open Source GeoJSON Files” were downloaded from the [Combined wildland fire datasets for the United States and certain territories, 1800s-Present (combined wildland fire polygons)](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81). From this, we used the file "USGS_Wildland_Fire_Combined_Dataset.json" as a base for our wildfire data for Salina. This data was then filtered to contain fires that occurred after 1963 within 1250 miles from Salina.  
  
### Intermediate Data Files

The intermediate_data folder in this repository contains the following dataframes:  

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

## Known Issues and Considerations

Please be aware of the following known issues and considerations when using this data and code:

- Data quality and completeness vary tremendously here. The accuracy of wildfire data is unknown due to there being absence of sophisticated technologies in certain eras.
- Model predictions may be subject to uncertainty and error.  
- Some blocks of code take between 20 mins - 1 hour to run. These are especially evident when loading features in wildfire data and pulling monthly AQI levels for Salina. Please make sure to have sufficient computational resources to carry out such an analysis.  

## Reproduction Steps

To reproduce the analysis and generate predictions, follow these steps:
1. Execute `src/HCDS Project Part 1 DAQ.ipynb`. This contains  
2. Execute `src/HCDS Project Part 1 Cleaning.ipynb`. This contains   
3. Execute `src/HCDS Project Part 1 AQI Pull.ipynb`. This contains  
4. Execute `src/HCDS Project Part 1 Modelling.ipynb`. This contains  

