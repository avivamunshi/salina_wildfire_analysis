# DATA512 Project Part 1

## Intermediate data   
All these can be found in the intermediate_data folder in this repository. These are dataframes that have been created while running the python scripts.   

### `miles.csv`

- **Description**: Contains information about fires occurring within 1250 miles of Salina.
- **Columns**:
  - 'OBJECTID': Unique identifier for each fire feature.
  - 'shortest_dist': The shortest distance from the fire to Salina in miles.
- **Purpose**: Represents the result of filtering fires based on the specified distance condition.

### `features.csv`

- **Description**: Contains details about fires that occurred after 1963.
- **Columns**:
  - 'OBJECTID': Unique identifier for each fire feature.
  - 'FireType': The type of the fire.
  - 'FireYear': The year in which the fire occurred.
  - 'GISAcres': The number of acres affected by the fire.
  - 'OverlapFlags': Flags indicating overlap within 1 or 2 regions.
- **Purpose**: Represents data extracted from the original wildfire dataset based on the year condition.

### `filter.csv`

- **Description**: Combines data from `features.csv` and `miles.csv` based on the 'OBJECTID' column.
- **Columns**:
  - Data from both `features.csv` and `miles.csv` is combined.
- **Purpose**: Contains combined data, including fire attributes and the shortest distance from Salina. This DataFrame is used for estimating smoke and data processing.
