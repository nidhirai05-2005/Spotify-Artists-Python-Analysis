# Spotify Artists Streaming Analysis using Python

## Project Overview
This project focuses on analyzing music streaming data of popular artists to identify patterns and insights related to **total streams, solo streams, collaborative streams, genres, countries, languages, gender, and artist career length**.
The project follows a complete **Exploratory Data Analysis (EDA)** workflow using Python. The dataset was cleaned, transformed, analyzed statistically, and visualized to extract meaningful insights from the data.


## Objectives
The main objectives of this project are:

* Analyze the total streaming performance of artists.
* Identify artists with the highest total streams.
* Compare solo and collaborative streaming performance.
* Analyze artist distribution by genre, country, and language.
* Compare male and female artist representation.
* Analyze the relationship between lead streams and total streams.
* Calculate career length based on debut year.
* Identify patterns and relationships between numerical variables.
* Create meaningful visualizations to communicate the findings.


## Dataset
The dataset contains information about **11 music artists** and their streaming performance.

### Main Features
| Column                     | Description                                     |
| -------------------------- | ----------------------------------------------- |
| Artist Name                | Name of the artist                              |
| Sex                        | Gender of the artist                            |
| Country of Origin          | Artist's country                                |
| Primary Language           | Main language used by the artist                |
| Primary Genre              | Main music genre                                |
| Artist Type                | Type of artist                                  |
| Debut Year                 | Year the artist started their career            |
| Total Streams              | Total streams in millions                       |
| Lead Streams               | Streams from lead performances in millions      |
| Feature Streams            | Streams from featured performances in millions  |
| Solo Streams               | Streams from solo work in millions              |
| % of Solo Streams          | Percentage of total streams from solo work      |
| Collaborative Streams      | Streams from collaborative work in millions     |
| % of Collaborative Streams | Percentage of total streams from collaborations |


## Technologies & Libraries
The project was developed using **Python**.


### Libraries Used
* **Pandas** — Data loading, cleaning, transformation, filtering, grouping, and analysis.
* **NumPy** — Numerical and statistical calculations.
* **Matplotlib** — Data visualization and chart creation.
* **Seaborn** — Statistical visualization and advanced charts.
* **Jupyter Notebook** — Development and analysis environment.


## Project Workflow
The project follows these steps:

Data Collection
      ↓
Data Loading
      ↓
Data Exploration
      ↓
Data Cleaning
      ↓
Feature Engineering
      ↓
Exploratory Data Analysis
      ↓
Statistical Analysis
      ↓
Data Visualization
      ↓
Business Insights
      ↓
Conclusion


## 1. Data Loading
The dataset was loaded using Pandas:
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv("spotify_artists.csv")
```

## 2. Data Exploration
Initial exploration was performed using:
```python
df.head()
df.tail()
df.shape
df.columns
df.info()
df.describe()
```
These functions were used to understand:
* Dataset structure
* Number of rows and columns
* Column names
* Data types
* Numerical statistics
* Overall data distribution


## 3. Data Cleaning
The dataset was checked for missing values and duplicate records.
```python
df.isnull().sum()
df.duplicated().sum()
```

Duplicate records were removed where necessary:
```python
df = df.drop_duplicates()
```

Column names were also cleaned by removing unnecessary spaces:
```python
df.columns = df.columns.str.strip()
```

## 4. Feature Engineering
New features were created to make the analysis more meaningful.

### Career Length
```python
current_year = 2026
df["Career_Years"] = current_year - df["Debut Year"]
```

### Lead vs Feature Stream Difference
```python
df["Lead_Feature_Difference"] = (
    df["Lead Streams (in millions)"] -
    df["Feature Streams (in millions)"]
)
```

### Collaboration Ratio
```python
df["Collaboration_Ratio"] = (
    df["Collaborative Streams (in millions)"] /
    df["Total Streams (in millions)"]
)
```

### Solo Ratio
```python
df["Solo_Ratio"] = (
    df["Solo Streams (in millions)"] /
    df["Total Streams (in millions)"]
)
```

## 5. Exploratory Data Analysis

Several business questions were answered during the analysis.
### Top Artists by Total Streams
```python
df.sort_values(
    by="Total Streams (in millions)",
    ascending=False
)[["Artist Name", "Total Streams (in millions)"]]
```

### Artists with Highest Solo Streams
```python
df.nlargest(
    10,
    "Solo Streams (in millions)"
)[["Artist Name", "Solo Streams (in millions)"]]
```

### Artists with Highest Collaborative Streams
```python
df.nlargest(
    10,
    "Collaborative Streams (in millions)"
)[["Artist Name", "Collaborative Streams (in millions)"]]
```

### Genre Distribution
```python
df["Primary Genre"].value_counts()
```

### Country Distribution
```python
df["Country of Origin"].value_counts()
```

### Language Distribution
```python
df["Primary Language"].value_counts()
```

### Gender Distribution
```python
df["Sex"].value_counts()
```


## 6. Statistical Analysis with NumPy

NumPy was used to calculate important statistical measures.
```python
np.mean(df["Total Streams (in millions)"])
np.median(df["Total Streams (in millions)"])
np.max(df["Total Streams (in millions)"])
np.min(df["Total Streams (in millions)"])
np.std(df["Total Streams (in millions)"])
```

These statistics helped understand the central tendency and variation in total streaming performance.

## 7. GroupBy Analysis
Pandas `groupby()` was used to compare streaming performance across different categories.

### Average Streams by Genre
```python
df.groupby(
    "Primary Genre"
)["Total Streams (in millions)"].mean()
```

### Average Streams by Country
```python
df.groupby(
    "Country of Origin"
)["Total Streams (in millions)"].mean()
```

### Average Streams by Gender
```python
df.groupby(
    "Sex"
)["Total Streams (in millions)"].mean()
```


## 8. Data Visualization
Matplotlib and Seaborn were used to create different visualizations.

### Visualizations Included
* Total Streams by Artist
* Genre Distribution
* Gender Distribution
* Country Distribution
* Language Distribution
* Correlation Heatmap
* Lead Streams vs Total Streams
* Genre-wise Streaming Performance
* Career Length vs Total Streams
* Box Plot for Streaming Distribution
* Histogram of Total Streams
* Pair Plot of Streaming Variables

### Example: Total Streams by Artist
```python
plt.figure(figsize=(12, 6))

sns.barplot(
    data=df,
    x="Artist Name",
    y="Total Streams (in millions)"
)

plt.xticks(rotation=90)
plt.title("Total Streams by Artist")
plt.show()
```

### Example: Correlation Heatmap
```python
numeric_df = df.select_dtypes(include=np.number)

plt.figure(figsize=(10, 8))

sns.heatmap(
    numeric_df.corr(),
    annot=True
)

plt.title("Correlation Heatmap")
plt.show()
```

---

## Key Insights
Based on the provided dataset, the analysis produced several observations:

* Drake has the highest total streaming value among the artists in this dataset.
* Taylor Swift has the highest percentage of solo streams, at approximately **88.7%**.
* Several artists have a high proportion of collaborative streams.
* Drake, Bad Bunny, Justin Bieber, and Travis Scott have more than **60% collaborative streams** in this dataset.
* Pop and Hip-Hop are strongly represented among the listed artists.
* English is the primary language for most artists in the dataset.
* The dataset contains artists from countries including the United States, Canada, Barbados, and the United Kingdom.
* Higher career length does not automatically correspond to higher total streams.
* Lead streams have a strong relationship with total streams because lead streams form a major component of overall streaming performance.


## Project Structure
```text
Spotify-Artists-Streaming-Analysis/
│
├── data/
│   └── spotify_artists.csv
│
├── notebook/
│   └── Spotify_Artists_Analysis.ipynb
│
├── images/
│   ├── total_streams.png
│   ├── genre_distribution.png
│   ├── gender_distribution.png
│   ├── correlation_heatmap.png
│   └── lead_vs_total_streams.png
│
├── README.md
└── requirements.txt
```

## Skills Demonstrated
Through this project, I demonstrated practical knowledge of:

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Data Cleaning
* Exploratory Data Analysis (EDA)
* Feature Engineering
* Statistical Analysis
* Data Aggregation
* Data Visualization
* Correlation Analysis
* Business Insight Generation

## Conclusion
This project demonstrates how Python can be used to transform raw music streaming data into meaningful insights through data cleaning, exploratory analysis, statistical analysis, feature engineering, and visualization.
The project provides practical experience with the complete data analytics workflow and demonstrates the use of Python's most important data analysis libraries.
