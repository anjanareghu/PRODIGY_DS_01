# World Population Analysis

This project provides an analysis of world population data over time, using various data visualization techniques. The analysis is performed on the World Bank dataset, which contains population data for different countries and regions from 1960 to 2022.

## Dataset

The dataset used in this analysis is sourced from the World Bank, with the filename: `API_SP.POP.TOTL_DS2_en_csv_v2_3309470.csv`.

## Requirements

To run this project, you need to have the following Python packages installed:

- `numpy`
- `pandas`
- `matplotlib`
- `seaborn`
- `IPython`

You can install the required packages using pip:

```bash
pip install numpy pandas matplotlib seaborn
```

## Data Preprocessing

1. **Loading the Data**: The data is loaded from a CSV file, skipping the first 4 rows, and the last column is removed as it contains only empty values.
   
2. **Handling Missing Data**:
   - **Null Value Count (Before)**: The script first prints the count of missing values in each column.
   - **Dropping Duplicates**: Any duplicate rows in the data are dropped.
   - **Filling Missing Values**: Missing values are filled using forward fill (`ffill`), where the last valid observation is propagated forward.
   - **Dropping Columns**: Columns with more than 50% missing values are dropped.
   - **Null Value Count (After)**: The script prints the count of missing values after the preprocessing steps.

3. **Data Transformation**:
   - The dataset is melted to convert the wide format into a long format with `Year` and `Population` columns.

## Data Visualization

1. **World Population Over the Years**:
   - A bar plot is created to visualize the world population from 1960 to 2022.

2. **Distribution of All Data Over Years**:
   - A histogram is plotted to show the distribution of population data across all years.

3. **Year-wise Histograms**:
   - Histograms are created for each year to show the distribution of population data in individual years.

4. **Total Population per Year**:
   - A horizontal bar plot is created to visualize the total population for each year from 1960 to 2022.

5. **Country-wise Data (1960)**:
   - Bar plots are created for the top 20 countries with the lowest population data in 1960, showing the population trend from 1960 to 2022.

6. **Country-wise Data (2022)**:
   - Bar plots are created for the top 20 countries with the lowest population data in 2022, showing the population trend from 1960 to 2022.

## Usage

To run the analysis, execute the script in a Python environment that supports Jupyter notebooks or any Python IDE.
