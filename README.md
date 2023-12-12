# Wildfire Analysis in Salina, KS

This repository contains data, code, and visualizations for a human-centered data science project focused on understanding the impact of wildfires on the air quality of the city of Salina. The project's goal is to analyze historical data and build a predictive model that should predict smoke estimates for every year for the next 25 years.  

## Goal

The goal of this project is to predict the impact of smoke from wildfires on the air quality in Salina for 25 years based on existing data about AQI and Wildfire data in the USA. 

## Licenses and API Information

- This project has been licensed under the [MIT License](https://github.com/avivamunshi/salina_wildfire_analysis/blob/main/LICENSE).     
- Further, some code written by Professor David McDonald has been used from the notebooks linked within the code as and when samples are used. The notebooks are licensed for use in DATA 512, a course in the UW MS Data Science degree program. This code is provided under the [Creative Commons CC-BY license](https://creativecommons.org/licenses/by/4.0/). Revision 1.0 - August 13, 2023.   
- Data about the wildfires has been extracted from the USGS website, and this has been provided by the [United States Geological Survey](https://www.usgs.gov/). USGS-authored or produced data and information are considered to be in the U.S. Public Domain. The dataset being used is the [Combined wildland fire datasets for the United States and certain territories, 1800s-Present (combined wildland fire polygons)](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81). The metadata can be found [here](https://www.sciencebase.gov/catalog/file/get/61aa537dd34eb622f699df81?f=__disk__d0%2F63%2F53%2Fd063532049be8e1bc83d1d3047b4df1a5cb56f15&transform=1&allowOpen=true).  


### Raw Data Files

The following raw data files are used in this project:

1. The “Wildland Fire Polygons Fire Feature Data Open Source GeoJSON Files” were downloaded from the [Combined wildland fire datasets for the United States and certain territories, 1800s-Present (combined wildland fire polygons)](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81). From this, we used the file "USGS_Wildland_Fire_Combined_Dataset.json" as a base for our wildfire data for Salina. This data was then filtered to contain fires that occurred after 1963 within 1250 miles from Salina.  

2. US Census Bureau Income and Industry Data. The primary dataset from the US Census Bureau (https://data.census.gov/) covers employment, industries, occupations, classes of workers, household income levels, and household structures for Salina, Kansas (2010-2021). This information is crucial to correlating economic indicators with smoke incidents. The data from the US Census Bureau is not subject to copyright in the United States, and a royalty-free, nonexclusive license is granted for use, copying, and derivative works outside of the United States.

Since the data extracted from this site spans 12 csvs and required a significant amount of data processing (refer 5-Data Cleaning.ipynb, Section 2: Cleaning Income and Industry data for Salina), I have instead provided details of the columns I have used in the analysis below:
- 'Salina_Count: The number of people in Salina employed in that industry/in the income bracket/amount the government was giving in aid for that particular year.
- 'Metrics': Categorical column with values "Industry" or "Income".
- 'Sub Metric': Sub category of the metric, encompasses different income brackets, industries in the city and different kinds of aid.
- 'Year': Corresponding year for the data.

3. BLS Data Finder Historical Employment and Unemployment data (https://www.bls.gov/bls/data_finder.htm). This resource under the US Bureau of Labor Statistics provides relevant information for analyzing employment and unemployment trends in Salina City. It is open for public use within the USA. Before processing, this dataset contains the following columns: 
- Series ID: Unique identifier for each row of the table.
- Year: The Year which the Employment and Unemployment is being calculated for. This dataset has data from 1990 to 2023.
- Period: Of the format "MO1", "M02" which means "Month 1", "Month 2" etc of each year. 
- Label: Of the format "Year Month"
- Value: Count of Employment and Unemployment for each of the months of a year.

Two csvs were extracted from this - Salina_Monthly_Employment.csv and Salina_Monthly_Unemployment.csv. These can be found in the data_sources directory.

4. Employment by Industries.csv was extracted from Data USA (https://datausa.io/profile/geo/salina-ks-31000US41460)

Data USA is an aggregate visualization engine with public datasets from many different sources including those from official US departments as well as educational institutions. We encourage the use of the site as a means of informational and educational purposes. All of the content on the site is presented under a [GNU Affero General Public License v3.0 (GPLv3)](https://www.gnu.org/licenses/agpl-3.0.txt)

This dataset has multiple columns, here is the list of them: 'ID Group', 'Group', 'ID Industry', 'Industry', 'ID Year', 'Year',
'Workforce by Industry and Gender', 'Workforce by Industry and Gender Moe', 'ACS Industry yg RCA','Geography', 'ID Geography', 'Slug Geography', 'Median Earnings','Median Earnings Moe', 'Workforce Prev', 'Workforce Growth', 'Median Earnings Prev', 'Median Earnings Growth', 'Share'
       
I have in particular only used the columns:
- Industry: Categorical column representing the different industries employing people in Salina.
- Workforce by Industry and Gender: Count of the number of people employed in that particular industry.


### Intermediate Data Files

The intermediate_data folder in this repository contains the following dataframes:  

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

## Results
Below is the outline of the result directory:

1. `Number of Fires and Distance from Salina.png`: Histogram showing the number of fires occurring every 50 mile distance from Salina up to the max specified distance.  
2. `Total Acres Burned.png`: Time series graph of total acres burned per year for the fires occurring in the specified distance from Salina.  

3. `Fire Smoke Estimate and AQI Estimate for Salina.png`: Time series graph containing fire smoke estimate and the AQI estimate for Salina.  

4. `Employment, Unemployment, Smoke Estimate and AQI.png`: Linear Regression Graph showing the correlations between Smoke Estimate, AQI, Employment and Unemployment.

5. `Linear Regression of Employment by Industry.png`: Linear Regression Graph showing the correlations between Four Industries - Construction, Manufacturing, Transportation and Agriculture - and the smoke estimate.

6. `Correlation Heatmap of Income Indicators.png`: Heatmap showing the correlation of smoke estimate vs different income brackets of the Salina residents.

7. `Correlation Heatmap of Aid.png`: Heatmap showing the correlation of smoke estimate vs different aid given by the government to the people.

8. `Forecasted Aid.csv`: Predicted funds that the government will have to give to individuals affected by the wildfires in Salina.

9. `AQI vs Smoke Estimate.png`: Scatterplot representation the relationship between my computed Smoke Estimate and AQI with confidence interval.

10. `Variation of AQI and Smoke Estimate by Year.png`: Time series graph of the values of AQI and Smoke Estimate over the years, with log scale.

## Reproduction Steps

To reproduce the analysis and generate predictions, follow these steps. All these notebooks can be found in the `src` directory of the repository.  

1. Download “Wildland Fire Polygons Fire Feature Data Open Source GeoJSON Files” from the [Combined wildland fire datasets for the United States and certain territories, 1800s-Present (combined wildland fire polygons)](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81). From this, import the file "USGS_Wildland_Fire_Combined_Dataset.json" using the code in `src/1-DAQ.ipynb`. This code contains the data analysis process to estimate the impact of wildfire smoke on Salina, Kansas. It involves reading the "USGS_Wildland_Fire_Combined_Dataset.json" GeoJSON dataset of wildfire occurrences, converting coordinates, calculating distances between Salina and wildfires, filtering relevant data, and performing checks. The output includes data frames with information on wildfire distances `intermediate_data/miles.csv`, fire attributes `intermediate_data/features.csv`, and an estimate of smoke impact `intermediate_data/filter.csv`.  
   
2. Execute `src/2-Cleaning.ipynb`. This notebook estimates the impact of wildfire smoke on Salina. It involves loading and filtering data, calculating factors like Smoke Factor and Overlap Factor, and applying a formula to compute the final **Smoke Estimate**. The results are grouped by year and exported to a CSV file named `intermediate_data/smoke_est.csv`.
   
3. Execute `src/3-AQI.ipynb`. This contains various data analysis and data retrieval tasks related to air quality and smoke estimates for Salina. It begins by loading and visualizing smoke estimate data. It then accesses the US EPA Air Quality System API to retrieve air quality monitoring information. You need to sign up to access this data, and this code block has been commented on and has a descriptor that will enable you to do the same. It is labeled "Uncomment this to sign up and get your username and APIKEY". The code computes monthly AQI estimates for the years 1963 to 2022, imputes missing AQI values, and calculates yearly averages. The final dataset combines smoke estimates and imputed AQI data, which is saved as `intermediate_data/pred_df.csv`.  
   
4. Execute `src/4-Modelling.ipynb`. This contains the predictive modeling, time series analysis, and data visualization tasks for smoke and fire-related data. The predicted values for the next 25 years have been stored and printed from the list 'forecasted_values'. The results of the visualizations have been saved to the directory `../results/`. These have been further discussed in the HCDS Project Part 1 Writeup.pdf.  

5. Execute `src/5-Data Cleaning.ipynb`. This notebook contains the data cleaning of the metrics chosen for Part 2 Analysis. These metrics are 1. Income and Industry data for Salina and 2. Unemployment and employment data for Salina. There are two resultant dataframes created in this - `intermediate_data/analysis_1.csv` and `intermediate_data/analysis_2.csv` - and these are both used to perform analysis wrt my Research Questions in 6-Questions.

6. Execute `sec/6-Questions.ipynb`. This notebook contains the analysis that answers my research questions. The results of each question have been saved to the directory `../results/`. These have been further discussed in the final project report.

## Known Issues and Considerations

Please be aware of the following known issues and considerations when using this data and code:

- Data quality and completeness vary tremendously here. The accuracy of wildfire data is unknown due to there being absence of sophisticated technologies in certain eras.
- Model predictions may be subject to uncertainty and error.  
- Some blocks of code take between 20 mins - 1 hour to run. These are especially evident when loading features in wildfire data and pulling monthly AQI levels for Salina. Please make sure to have sufficient computational resources to carry out such an analysis. 
- While the features used to gain correlation between different metrics show values which we can depend on, this is still data which is not adjusted for inflation and has not been deeply examined for statistical values.
