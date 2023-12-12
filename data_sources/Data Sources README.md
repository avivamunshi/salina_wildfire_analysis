This directory contains the following data:

1. `2010_Census.csv, 2011_Census.csv, ... , 2021_Census.csv`: US Census Bureau Income and Industry Data. The primary dataset from the US Census Bureau (https://data.census.gov/) covers employment, industries, occupations, classes of workers, household income levels, and household structures for Salina, Kansas (2010-2021). This information is crucial to correlating economic indicators with smoke incidents. The data from the US Census Bureau is not subject to copyright in the United States, and a royalty-free, nonexclusive license is granted for use, copying, and derivative works outside of the United States.

The data files in particular are 2010_Census.csv, 2011_Census.csv, ... , 2021_Census.csv - representing Income and Industry Data from 2010 to 2021 in Salina.
Since the data extracted from this site spans 12 csvs and required a significant amount of data processing (refer 5-Data Cleaning.ipynb, Section 2: Cleaning Income and Industry data for Salina), I have instead provided details of the columns I have used in the analysis below:
- 'Salina_Count: The number of people in Salina employed in that industry/in the income bracket/amount the government was giving in aid for that particular year.
- 'Metrics': Categorical column with values "Industry" or "Income".
- 'Sub Metric': Sub category of the metric, encompasses different income brackets, industries in the city and different kinds of aid.
- 'Year': Corresponding year for the data.

2. `Salina_Monthly_Emp.csv` and `Salina_Monthly_Emp.csv`: Monthly Unemployment in SalinaBLS Data Finder Historical Employment and Unemployment data (https://www.bls.gov/bls/data_finder.htm). This resource under the US Bureau of Labor Statistics provides relevant information for analyzing employment and unemployment trends in Salina City. It is open for public use within the USA. Before processing, this dataset contains the following columns: 
- Series ID: Unique identifier for each row of the table.
- Year: The Year which the Employment and Unemployment is being calculated for. This dataset has data from 1990 to 2023.
- Period: Of the format "MO1", "M02" which means "Month 1", "Month 2" etc of each year. 
- Label: Of the format "Year Month"
- Value: Count of Employment and Unemployment for each of the months of a year.

Two csvs were extracted from this - Salina_Monthly_Employment.csv and Salina_Monthly_Unemployment.csv. 

3. `Employment by Industries.csv` was extracted from Data USA (https://datausa.io/profile/geo/salina-ks-31000US41460)

Data USA is an aggregate visualization engine with public datasets from many different sources including those from official US departments as well as educational institutions. We encourage the use of the site as a means of informational and educational purposes. All of the content on the site is presented under a [GNU Affero General Public License v3.0 (GPLv3)](https://www.gnu.org/licenses/agpl-3.0.txt)

This dataset has multiple columns, here is the list of them: 'ID Group', 'Group', 'ID Industry', 'Industry', 'ID Year', 'Year',
'Workforce by Industry and Gender', 'Workforce by Industry and Gender Moe', 'ACS Industry yg RCA','Geography', 'ID Geography', 'Slug Geography', 'Median Earnings','Median Earnings Moe', 'Workforce Prev', 'Workforce Growth', 'Median Earnings Prev', 'Median Earnings Growth', 'Share'
       
I have in particular only used the columns:
- Industry: Categorical column representing the different industries employing people in Salina.
- Workforce by Industry and Gender: Count of the number of people employed in that particular industry.
