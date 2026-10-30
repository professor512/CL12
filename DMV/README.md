# 📊 DMV — Data Mining & Visualization Practicals

> A comprehensive guide to all practicals in the **DMV** folder, covering the theory, code workflow, and dataset requirements.

---

## Practicals Overview

| # | Practical | File | Dataset Required | Dataset File |
|---|-----------|------|-----------------|--------------|
| 1 | Weather API Data Collection & Visualization | `DMV_1_WeatherAPIcheck.ipynb` | ❌ No | Fetched live via OpenWeatherMap API |
| 2 | Telecom Customer Churn Analysis | `DMV_2_Telecom_Customer_Churn.ipynb` | ✅ Yes | `Telecom_Customer_Churn.csv` |
| 3 | Real Estate Price Analysis | `DMV_3_Real_Estate.ipynb` | ✅ Yes | `Bengaluru_House_Data.csv` |
| 4 (10B) | Delhi AQI Data Visualization | `DMV4_AQI.ipynb` | ✅ Yes | `delhi-weather-aqi-2025.csv` |
| 5 (11B) | Retail Sales Performance Analysis | `DMV5_Retail.ipynb` | ✅ Yes | `customer_shopping_data.csv` |

---

## 🌦️ Practical 1 — Weather API Data Collection & Visualization

**File:** `DMV_1_WeatherAPIcheck.ipynb`
**Dataset Required:** ❌ None (data fetched live from **OpenWeatherMap API**)

### What is it?
This practical demonstrates how to collect real-world weather data using a REST API and visualize it with various plots. It covers the full pipeline: API call → data parsing → transformation → visualization.

### What the Code Does (Step by Step):

1. **API Call:**
   ```python
   api_key = "..."  # Your OpenWeatherMap API key
   api_url = f"http://api.openweathermap.org/data/2.5/forecast?lat={lat}&lon={lon}&appid={api_key}"
   response = requests.get(api_url)
   weather_data = response.json()
   ```

2. **Parse JSON Response** – Extracts timestamps, temperature, humidity, wind speed, and weather description into a DataFrame.

3. **Data Cleaning:**
   - Fill missing values with 0
   - Convert Temperature from **Kelvin to Celsius**

4. **Resample to Daily Aggregates:**
   ```python
   daily_mean_temp = weather_df['Temperature'].resample('D').mean()
   ```

5. **Visualizations:**
   - Line plot: Mean Daily Temperature
   - Bar chart: Mean Daily Humidity
   - Scatter plot: Temperature vs. Wind Speed
   - Heatmap: Correlation between Temperature, Humidity, Wind Speed

### Key Concepts:
| Term | Meaning |
|------|---------|
| REST API | Interface to fetch data over HTTP from external services |
| JSON | JavaScript Object Notation — common format for API responses |
| Resampling | Aggregating time-series data by a time period (e.g., daily mean) |
| Correlation Heatmap | Shows pairwise correlations between numeric features |

---

## 📱 Practical 2 — Telecom Customer Churn Analysis

**File:** `DMV_2_Telecom_Customer_Churn.ipynb`
**Dataset Required:** ✅ **`Telecom_Customer_Churn.csv`** (present in `DMV/` folder)

### What is it?
Customer churn occurs when a customer stops using a service. This practical performs **Exploratory Data Analysis (EDA)** and builds predictive models to identify telecom customers likely to churn.

### Dataset (`Telecom_Customer_Churn.csv`):
- **7,043 telecom customers** with service and billing details
- Key columns: `tenure`, `MonthlyCharges`, `TotalCharges`, `Contract`, `InternetService`, `Churn` (target: Yes/No)

### What the Code Does (Step by Step):

1. **Load & Inspect Data:**
   ```python
   data = pd.read_csv("Telecom_Customer_Churn.csv")
   print(data.shape)
   data.info()
   ```

2. **Data Cleaning:**
   - Convert `TotalCharges` from text to numeric (blank values become NaN, then filled with 0)
   - Remove duplicates
   - Strip whitespace from categorical columns

3. **Data Type Standardization:**
   - `SeniorCitizen`, `Churn` → category
   - `tenure` → int, `MonthlyCharges` → float

4. **EDA Visualizations:**
   - Churn rate distribution
   - Monthly charges by churn status
   - Contract type vs. churn
   - Correlation heatmap of numeric features

5. **Feature Engineering & Model Training:**
   - Encode categorical variables
   - Train/test split
   - Classification model evaluation metrics

### Key Concepts:
| Term | Meaning |
|------|---------|
| Churn | When a customer stops using a service |
| EDA | Exploratory Data Analysis — understanding data before modeling |
| Label Encoding | Converting categorical text to numeric codes |
| Class Imbalance | When one class (e.g., churned) is much rarer than the other |

---

## 🏠 Practical 3 — Real Estate Price Analysis (Bengaluru)

**File:** `DMV_3_Real_Estate.ipynb`
**Dataset Required:** ✅ **`Bengaluru_House_Data.csv`** (present in `DMV/` folder)

### What is it?
This practical performs **data cleaning, feature engineering, and price prediction** on Bengaluru real estate data — one of the classic messy datasets that requires significant preprocessing before analysis.

### Dataset (`Bengaluru_House_Data.csv`):
- **13,000+ property listings** from Bengaluru
- Columns: `area_type`, `availability`, `location`, `size` (BHK), `society`, `total_sqft`, `bath`, `balcony`, `price`

### What the Code Does (Step by Step):

1. **Load Data:**
   ```python
   df1 = pd.read_csv("Bengaluru_House_Data.csv")
   ```

2. **Drop Irrelevant Columns:**
   ```python
   df2 = df1.drop(['area_type', 'society', 'balcony', 'availability'], axis='columns')
   ```

3. **Handle Missing Values** – Drop rows with NaN (small fraction of data)

4. **Extract BHK from `size`:**
   ```python
   df3['bhk'] = df3['size'].apply(lambda x: int(x.split(' ')[0]))
   ```
   - Converts "2 BHK" → 2, "3 Bedroom" → 3

5. **Handle `total_sqft` ranges** – Converts ranges like "1000-1200" to the average value

6. **Feature Engineering:**
   - Calculate `price_per_sqft` = price / total_sqft
   - Remove outliers using location-wise statistics

7. **Visualization:**
   - Price distribution by location
   - Price vs. sqft scatter plots
   - BHK-wise price comparisons

### Key Concepts:
| Term | Meaning |
|------|---------|
| Feature Engineering | Creating new useful columns from existing data |
| Outlier Removal | Eliminating data points that are statistically extreme |
| Price per Sqft | Normalized price metric for fair comparison |
| BHK | Bedroom-Hall-Kitchen — standard Indian housing unit |

---

## 🌫️ Practical 4 (Exp 10B) — Delhi AQI Data Visualization

**File:** `DMV4_AQI.ipynb`
**Dataset Required:** ✅ **`delhi-weather-aqi-2025.csv`** (present in `DMV/` folder)

### What is it?
This practical visualizes **Air Quality Index (AQI)** trends in Delhi across 2025 using time-series data. It demonstrates various matplotlib and seaborn plots to communicate pollution patterns.

### Dataset (`delhi-weather-aqi-2025.csv`):
- Hourly AQI readings across multiple Delhi locations throughout 2025
- Key columns: `date_ist`, `time_ist`, `location`, `aqi_index`, `pm2_5`, `pm10`, `co`, `no2`

### What the Code Does (Step by Step):

1. **Load & Explore:**
   ```python
   data = pd.read_csv("delhi-weather-aqi-2025.csv")
   print("Number of locations:", data["location"].nunique())
   ```

2. **Parse DateTime:**
   ```python
   data["datetime"] = pd.to_datetime(data["date_ist"] + " " + data["time_ist"], dayfirst=True)
   ```

3. **AQI Trend Plot** – Hourly average AQI over time (line plot)

4. **Daily Pollutant Trends** – Daily mean values of PM2.5, PM10, CO, NO2

5. **Location-wise Comparison** – AQI across different Delhi monitoring stations

6. **Heatmaps & Distribution Plots** – Pollution patterns by hour/day

### Key Concepts:
| Term | Meaning |
|------|---------|
| AQI | Air Quality Index — measures air pollution level |
| PM2.5 / PM10 | Fine/coarse particulate matter — major health hazards |
| Time-Series | Data indexed by time, analyzed for trends and patterns |
| Seaborn | Python visualization library built on top of matplotlib |

---

## 🛒 Practical 5 (Exp 11B) — Retail Sales Performance Analysis

**File:** `DMV5_Retail.ipynb`
**Dataset Required:** ✅ **`customer_shopping_data.csv`** (present in `DMV/` folder)

### What is it?
This practical analyzes **retail sales performance by region and category** using a customer shopping dataset from Istanbul malls. It demonstrates groupby aggregations, ranking, and multi-dimensional sales analysis.

### Dataset (`customer_shopping_data.csv`):
- **Customer transaction records** from 10 Istanbul shopping malls
- Key columns: `shopping_mall`, `category`, `quantity`, `price`, `gender`, `payment_method`, `invoice_date`

### What the Code Does (Step by Step):

1. **Load Data:**
   ```python
   df = pd.read_csv("customer_shopping_data.csv")
   ```

2. **Create Sales Amount:**
   ```python
   df["sales_amount"] = df["quantity"] * df["price"]
   ```

3. **Sales by Mall** – Total revenue per shopping mall:
   ```python
   mall_sales = df.groupby("shopping_mall")["sales_amount"].sum()
   ```

4. **Sales by Category** – Top-selling product categories

5. **Top-Performing Malls** – Ranked by total sales

6. **Mall × Category Analysis** – Multi-level groupby for cross-dimensional insights:
   ```python
   mall_category_sales = df.groupby(["shopping_mall", "category"])["sales_amount"].sum()
   ```

7. **Visualizations:**
   - Bar charts: Sales by mall and by category
   - Stacked bar charts: Category breakdown per mall
   - Pie charts: Revenue share by payment method
   - Trend analysis: Sales over time

### Key Concepts:
| Term | Meaning |
|------|---------|
| GroupBy | Aggregating data by one or more categorical columns |
| Sales Performance | Measuring revenue, units sold, and trends |
| Multi-level Index | Groupby with multiple keys creates a hierarchical index |
| Revenue Analysis | Breaking down total income by segment, region, or product |
