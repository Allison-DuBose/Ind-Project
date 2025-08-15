
# Project - Higher Education Consulting Analytics

In this project we took data about cars companies, models, engines, CC/battery capacities, horsepower, top speed, 0-100 km/h performance, prices (in US dollars), fuel types, seating capacity, and torque from 2025. This covers a wide variety of cars from EVs to standard fuel, sports cars to utility vans, and luxury to standard model cars. We sought to provide insights on how performance an price are related, is title really everything in price, how fast are the fastest cars going and other information that might interest car buers and enthusiasts.


## Authors

- [@Allison-DuBose](https://github.com/Allison-DuBose)

 
## Acknowledgements

 - [The Cars datasets was selected from kaggle.com](https://www.kaggle.com/datasets/abdulmalik1518/cars-datasets-2025)



## Key Libraries

- `seaborn`
- `matplotlib.pyplot`
- `pandas`
- `rapidfuzz`
- `numpy`
- `missingno`



## Data Disctionary

### 📘 Data Dictionary

| **Column Name**             | **Description**                                                                 |
|----------------------------|----------------------------------------------------------------------------------|
| Car Company Names           | The manufacturer or brand of the car.                                           |
| Car Models                  | The specific name or series of the car.                                         |
| Engine Types                | Information on engine specifications.                                           |
| CC/Battery Capacity         | Engine displacement in cubic centimeters or battery capacity for electric cars. |
| Horsepower (HP)             | The power output of the car's engine or motor.                                  |
| Top Speed                   | The maximum speed the car can achieve.                                          |
| 0-100 km/h Performance      | The time it takes for the car to accelerate from 0 to 100 km/h.                 |
| Price (in USD)              | The car's price listed in United States dollars.                                |
| Fuel Type                   | Specifies whether the car uses petrol, diesel, electricity, or hybrid systems.  |
| Seating Capacity            | The number of passengers the car can accommodate.                               |
| Torque                      | The rotational force the engine generates.                                      |

## Summary

# 🚗 Car Performance & Value Analysis

This project explores a dataset of cars, cleaning raw manufacturer data into structured, quantitative insights, and analyzing performance, price, and value across models and fuel types.

---

## 📊 Dataset Overview

**Original Dataset (`cars`)**
The raw data contains specs from various car manufacturers, including engine types, performance metrics, pricing, and seating capacity. However, many fields were stored as text with units or ranges (e.g., `"70-85 hp"`, `"$12,000-$15,000"`), requiring preprocessing.

**Cleaned Dataset (`cars_cleaned`)**
A cleaned and structured version of the dataset, with all numerical columns converted into usable float values and new performance/value metrics created.

---

## 🧹 Data Cleaning & Transformation

| Original Column         | Action                                                                   |
| ----------------------- | ------------------------------------------------------------------------ |
| `HorsePower`            | Removed "hp", handled ranges (`70-85 hp` → `77.5`), converted to float   |
| `Cars Prices`           | Removed "\$" and commas, handled ranges, converted to float (USD)        |
| `Torque`                | Removed "Nm", handled ranges, converted to float                         |
| `Seats`                 | Converted "2+2" to 4, took the **maximum** in ranges (e.g., `2-12 → 12`) |
| `CC/Battery Capacity`   | Removed "cc", converted to numeric (`float`)                             |
| `0-100 KM/H`            | Converted to float (in seconds)                                          |
| `Top Speed`             | Converted "km/h" to numeric                                              |
| `Fuel Types`, `Engines` | Preserved as categorical features                                        |

**Missing Values Handling:**

* **Dropped** rows missing: `Seats`, `Price_USD`, `0-100 KM/H`
* **Imputed** missing:

  * `HorsePower` → avg of similar `Engine` + `Torque` + `Top Speed`
  * `Torque` → avg of similar `Engine` + `HorsePower` + `Top Speed`
  * `CC/Battery` → avg of similar `Engine` + `HorsePower` + `Torque`

---

## 📈 Feature Engineering

New columns created:

| Column Name         | Description                                            |
| ------------------- | ------------------------------------------------------ |
| `Price_USD`         | Final cleaned price in USD                             |
| `HorsePower`        | Cleaned numerical horsepower                           |
| `Torque`            | Cleaned numerical torque                               |
| `speed_km_per_hr`   | Cleaned top speed                                      |
| `secs_0_to_100_kmh` | Acceleration time from 0 to 100 km/h                   |
| `performance_score` | Composite score: `(HorsePower × Speed) / Acceleration` |
| `USD_per_HP`        | Price divided by horsepower                            |
| `USD_per_Torque`    | Price divided by torque                                |

---

## 📊 Visualizations

We created the following visuals to explore relationships in the data:

### 📉 Distribution Plots

* **Histogram of Car Prices** (formatted in USD, with and without outliers)
* **Boxplot of Car Prices** to visualize outliers and spread

### 📊 Categorical Insights

* **Average HorsePower by Fuel Type**
* **Car Count by Price Bins** (`$0-50K`, `$50K-100K`, ..., `$1M+`) with labels

### 📈 Correlation Analysis

* **Heatmap of All Numeric Variables**
* **Price vs Performance Score Scatterplot** with **broken y-axis** to show high-end outliers clearly

### 💡 Value Analysis

* **Top 10 Best Value Cars** by:

  * USD per HorsePower
  * USD per Torque

---

## 📁 Files

| File                 | Description                                            |
| -------------------- | ------------------------------------------------------ |
| `cars.csv`           | Original raw car specs dataset                         |
| `cars_cleaned.csv`   | Cleaned dataset with numerical values and new features |
| `eda_notebook.ipynb` | All preprocessing, analysis, and visualizations        |

---

## 🚀 Next Steps

* Add **brand-based performance/value comparison**
* Explore **fuel efficiency vs performance**
* Build a **dashboard** (e.g., Streamlit or Plotly Dash)

