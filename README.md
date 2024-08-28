# World Population Analysis

This project involves analyzing world population data over time, using various data preprocessing and visualization techniques. The dataset used is sourced from the World Bank, containing population data from 1960 to 2022.

## Dataset

The dataset used is titled `API_SP.POP.TOTL_DS2_en_csv_v2_3309470.csv`. It contains the population figures for various countries and regions.

## Requirements

Make sure to have the following Python packages installed:

- `numpy`
- `pandas`
- `matplotlib`
- `seaborn`
- `IPython`

Install them using pip if necessary:

```bash
pip install numpy pandas matplotlib seaborn
```

## Code Explanation

### 1. **Loading and Initial Preprocessing**

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from IPython.display import display, HTML

file = 'API_SP.POP.TOTL_DS2_en_csv_v2_3309470.csv'
df = pd.read_csv(file, skiprows=4, encoding='ISO-8859-1')
df = df.iloc[:, :-1]  # Remove the last column, which is empty
```

- **Loading the Data**: The CSV file is read into a Pandas DataFrame. We skip the first 4 rows as they contain metadata, not data. The last column is dropped as it doesn't contain any useful information.

### 2. **Handling Missing Data**

```python
display(HTML('<b>Null Value count Before</b>'))
print(df.isnull().sum())
```

- **Counting Missing Values (Before)**: We first display the count of missing values in each column before any processing.

```python
df = df.drop_duplicates()  # Drop duplicate rows
df = df.fillna(method="ffill")  # Forward fill missing values
df = df.dropna(axis=1, thresh=df.shape[0]*0.5)  # Drop columns with >50% missing data
```

- **Dropping Duplicates**: Any duplicate rows are removed.
- **Filling Missing Values**: Missing values are forward-filled, meaning the last known value is carried forward to fill gaps.
- **Dropping Columns**: Columns with more than 50% missing data are dropped.

```python
display(HTML('<b>Null Value count After</b>'))
print(df.isnull().sum())
```

- **Counting Missing Values (After)**: We display the count of missing values again after preprocessing to ensure data cleanliness.

### 3. **Data Transformation**

```python
melted_df = pd.melt(df, id_vars=['Country Name', 'Country Code', 'Indicator Name', 'Indicator Code'], var_name='Year', value_name='Population')
display(HTML('<b>Head of Melted Data</b>'))
melted_df.head()
```

- **Melting the Data**: The DataFrame is reshaped from wide format to long format, where each row corresponds to a single year of population data for a given country.

### 4. **Visualizing World Population Over Time**

```python
filtered_df = melted_df[melted_df['Country Name'] == 'World']

plt.figure(figsize=(15, 10))
sns.barplot(x='Year', y='Population', data=filtered_df, color='y')
plt.title('World Population Over the Years', fontsize=20)
plt.xlabel('Year', fontsize=15)
plt.ylabel('Population', fontsize=15)
plt.xticks(rotation=90, fontsize=12)
plt.yticks(fontsize=12)
plt.show()
```

- **Filtering for World Data**: We filter the DataFrame to include only the world population data.
- **Bar Plot**: A bar plot is created to show the world population trend over the years.

### 5. **Distribution of Population Data**

```python
cols = [str(year) for year in range(1960, 2023)]
all_data = df[cols].values.flatten()  # Flatten data into a single array
plt.figure(figsize=(10, 6))
plt.hist(all_data, color='#8C564B', bins=20)
plt.xlabel('Values')
plt.ylabel('Frequency')
plt.title('Distribution of All Data Over Years')
plt.show()
```

- **Flattening Data**: We flatten the population data across all years into a single array for distribution analysis.
- **Histogram**: A histogram is plotted to visualize the frequency distribution of population data.

### 6. **Year-wise Histograms**

```python
for i in cols:
    plt.figure(figsize=(10, 6))
    plt.hist(df[i], color='#9467BD', bins=10)
    plt.xlabel(i)
    plt.ylabel('Frequency')
    plt.title(f'Population Distribution for {i}')
    plt.show()
```

- **Loop through Years**: For each year from 1960 to 2022, a histogram is created to show the distribution of population values for that year.

### 7. **Total Population per Year**

```python
total_values = df[years].sum()

plt.figure(figsize=(30, 30))
plt.barh(years, total_values, color='#191970')
plt.xlabel('Total Population')
plt.ylabel('Year')
plt.title('Total Population per Year')
plt.show()
```

- **Summing Population Data**: The population values are summed across all countries for each year.
- **Horizontal Bar Plot**: A horizontal bar plot is used to visualize the total population for each year.

### 8. **Country-wise Analysis for 1960 and 2022**

```python
# Top 20 countries with the lowest population in 1960
country_by_1960 = df.sort_values(by='1960').head(20).drop(df.columns[[1, 2, 3]], axis=1)
country_by_1960_t = country_by_1960.set_index('Country Name').T

for country_name, data_values in country_by_1960_t.iterrows():
    years = [str(year) for year in data_values.index]
    values = data_values.values.astype(float)
    plt.figure(figsize=(10, 5))
    sns.barplot(x=years, y=values, palette='viridis')
    plt.xlabel('Years')
    plt.ylabel('Population')
    plt.title(f"{country_name} - Population from 1960 to 2022")
    plt.xticks(rotation=90)
    plt.show()

# Top 20 countries with the lowest population in 2022
country_by_2022 = df.sort_values(by='2022').head(20).drop(df.columns[[1, 2, 3]], axis=1)
country_by_2022_t = country_by_2022.set_index('Country Name').T

for country_name, data_values in country_by_2022_t.iterrows():
    plt.figure(figsize=(10, 5))
    sns.barplot(x=data_values.index, y=data_values.values)
    plt.xlabel('Year')
    plt.ylabel('Population')
    plt.title(f"{country_name} - Population from 1960 to 2022")
    plt.xticks(rotation=90)
    plt.show()
```

- **Country-wise Analysis for 1960**: We focus on the top 20 countries with the lowest population in 1960 and visualize their population trend over the years using bar plots.
- **Country-wise Analysis for 2022**: Similarly, the top 20 countries with the lowest population in 2022 are analyzed and visualized.

## Usage

To run this analysis, execute the provided script in a Jupyter notebook or any Python environment.



For questions or feedback, you can reach the project maintainer at [your-email@example.com].

---

This README provides both a high-level overview and detailed explanations of the code, making it easier for others to understand and use your project.
