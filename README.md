<h1 align="center">🚖 Uber Data Analysis Project (Python)</h1>

<p align="center">
  <b>Exploratory Data Analysis of Uber Pickups in New York City</b><br>
  Pandas • NumPy • Seaborn • Plotly • Folium • Data Visualization
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-Data%20Analysis-blue?style=for-the-badge&logo=python">
  <img src="https://img.shields.io/badge/Library-Pandas-yellow?style=for-the-badge">
  <img src="https://img.shields.io/badge/Visualization-Seaborn%20%7C%20Plotly-green?style=for-the-badge">
</p>

---

## 📌 Project Overview

This project performs **Exploratory Data Analysis (EDA)** on Uber pickup data in New York City.

The main objective is to:

- Analyze monthly pickup trends  
- Identify weekday and hourly rush patterns  
- Examine dispatching base performance  
- Detect high-demand geographic areas  
- Perform automated pivot-based analysis  

The analysis is performed using Python and various data visualization libraries.

---

## 📂 Dataset Information

The dataset contains:

- **Date/Time** – Uber pickup timestamp  
- **Latitude (Lat)** – Pickup location latitude  
- **Longitude (Lon)** – Pickup location longitude  
- **Base / Dispatching Base Number** – Uber base company code  
- **Active Vehicles** – Number of active vehicles per base  

Data covers Uber pickups in **New York City (2014–2015)**.

---

## 🛠️ Technologies & Libraries Used

- Python  
- Pandas  
- NumPy  
- Matplotlib  
- Seaborn  
- Plotly  
- Folium  

---

## 🧹 Data Preprocessing & Cleaning

- Checked dataset shape  
- Removed duplicate records  
- Verified NULL values  
- Converted date column to datetime format  
- Extracted time-based features (Month, Weekday, Hour, Day, Minute)

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

uber_15 = pd.read_csv('uber-raw-data-janjune-15_sample.csv')

uber_15 = uber_15.drop_duplicates()
uber_15['Pickup_date'] = pd.to_datetime(uber_15["Pickup_date"])

uber_15['month'] = uber_15['Pickup_date'].dt.month_name()
uber_15['weekday'] = uber_15['Pickup_date'].dt.day_name()
uber_15['day'] = uber_15['Pickup_date'].dt.day
uber_15['hour'] = uber_15['Pickup_date'].dt.hour
uber_15['minute'] = uber_15['Pickup_date'].dt.minute
```

---

## 📊 Key Analysis Performed

### 1️⃣ Monthly Pickup Analysis

```python
uber_15['month'].value_counts().plot(kind='bar')
```

Identified which month had maximum Uber pickups.

---

### 2️⃣ Month vs Weekday Crosstab

```python
pivot = pd.crosstab(index=uber_15['month'], columns=uber_15['weekday'])
pivot.plot(kind='bar', figsize=(10,8))
```

Analyzed pickup distribution across months and weekdays.

---

### 3️⃣ Hourly Rush Analysis

```python
summary = uber_15.groupby(['weekday', 'hour'], as_index=False).size()

plt.figure(figsize=(8,6))
sns.pointplot(x='hour', y='size', hue='weekday', data=summary)
```

Identified peak demand hours across weekdays.

---

### 4️⃣ Dispatching Base Performance

```python
import plotly.express as px

px.box(x='dispatching_base_number', 
       y='active_vehicles', 
       data_frame=uber_foil)

px.violin(x='dispatching_base_number', 
          y='active_vehicles', 
          data_frame=uber_foil)
```

Compared active vehicles across different Uber bases.

---

### 5️⃣ Merging Multiple Datasets

```python
final = pd.DataFrame()

for file in files:
    current_df = pd.read_csv(path+'/'+file)
    final = pd.concat([current_df, final])

final.drop_duplicates(inplace=True)
```

Created consolidated dataset for advanced analysis.

---

### 6️⃣ Geographic Rush Analysis (Heatmap)

```python
from folium.plugins import HeatMap
import folium

basemap = folium.Map()
HeatMap(rush_uber).add_to(basemap)
basemap
```

Identified high-demand pickup areas using geospatial heatmap.

---

### 7️⃣ Day vs Hour Pivot Analysis

```python
pivot = final.groupby(['day', 'hour']).size().unstack()
pivot.style.background_gradient()
```

Analyzed rush patterns across days and hours.

---

### 8️⃣ Automation Function

```python
def gen_pivot_table(df, col1, col2):
    pivot = final.groupby(['day', 'hour']).size().unstack()
    return pivot.style.background_gradient()

gen_pivot_table(final, 'day', 'hour')
```

Automated pivot generation for flexible analysis.

---

## 📈 Key Insights

- Peak ride demand observed during evening commute hours.
- Weekend ride patterns differ from weekday trends.
- Midtown Manhattan shows highest pickup density.
- Certain dispatching bases manage more active vehicles.
- Heatmap clearly highlights high-traffic zones.

---

## 📂 Project Structure

```
uber-data-analysis-python/
│── README.md
│── uber-data-analysis.ipynb
│── uber-raw-data-janjune-15_sample.csv
```

---

## ▶️ How to Run This Project

1. Install Python (3.x)
2. Install required libraries:

```bash
pip install pandas numpy matplotlib seaborn plotly folium
```

3. Open Jupyter Notebook
4. Run all cells sequentially

---

## 🚀 Skills Demonstrated

- Data Cleaning  
- Feature Engineering  
- Exploratory Data Analysis  
- Time-Series Analysis  
- Geospatial Visualization  
- Data Merging & Transformation  
- Analytical Thinking  

---

## 👤 Author

**Navneet Prajapati**  
Aspiring Data Analyst  

🔗 LinkedIn: https://www.linkedin.com/in/navneet-prajapati-delhi  

---

⭐ If you found this project helpful, consider giving it a star!
