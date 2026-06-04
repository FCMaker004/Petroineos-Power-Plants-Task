# Petroineos-Power-Plants-Task

## Overview

This project processes power plant generation data from multiple CSV files using the `Petroineos_AI_Tasks` Jupyter notebook. The notebook cleans the three plant data given, combines the processed files into a single `database.csv` file, retrieves the most recently updated records if records are changed, and produces quarterly aggregations and a country's total power production by technology, represented by Volume.

The project is implemented using Python and pandas.

## Repository Contents

- `power_plants_task.ipynb` — main Jupyter notebook containing complete solutions
- `gas_fr_plants.csv` — French gas plant production input data
- `gas_plants.csv` — Great Britain gas plant production input data
- `wind_plants.csv` — Great Britain wind plant production input data
- `database.csv` — combined database file generated upon execution of main Jupyter notebook
- `requirements.txt` — project dependency list
- `.gitignore` — files and folders excluded from version control (exculdes venv file)

## Methodology

The notebook defines a `PowerPlants` class that executes the full data processing pipeline.
### Data Cleaning

The `analyse_plant_data()` method:

1. reads each plant CSV file
2. removes any duplicate rows
3. converts dates into a consistent datetime object format
4. converts production volume values into numeric values for use in pivot tables in future functions
5. fills missing or invalid volume values with `0`
6. removes rows with negative production volumes
7. resets the DataFrame index after cleaning
   
### Data Preparation

The `load_new_data_from_file()` method:

- converts country codes into full country names
- adds an `updatedby` column
- adds an `updatetime` column
- standardises the final database column order
- prepares the cleaned data for saving

### Database Creation

The `save_new_data()` method saves the processed data into the file: `database.csv`. If the database already exists, the new data is combined with the existing database through the os library.

### Latest Data Retrieval

The `get_data_from_database()` method returns the most recently updated version of each plant record using the `updatetime` column incase they records are altered.

### Quarterly Aggregation

The `aggregate_data_to_quarterly()` method simply calculates quarterly summary statistics for each plant, specifcally:

1. mean production volume
2. median production volume
3. standard deviation of production volume

The quarters are defined as:

- Q1: January to March
- Q2: April to June
- Q3: July to September
- Q4: October to December

### Country-Level Aggregation

The `aggregate_data_to_country()` method aggregates total production volume by country and technology type

## How to run

1. Clone the repository and open cloned repository in VS Code.

```cmd
git clone https://github.com/FCMaker004/Petroineos-Power-Plants-Task.git
cd Petroineos-Power-Plants-Task
```

2. Create and activate virtual environment

```cmd
python -m venv .venv
.venv\Scripts\activate
```

3. Install required dependency
```cmd
pip install -r requirements.txt
```

## Author
Farhan Chowdhury










