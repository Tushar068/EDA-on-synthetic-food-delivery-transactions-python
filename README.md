# 🍔 Exploratory Data Analysis — Synthetic Food Delivery Transactions

---

## 📌 Project Overview

This project performs a comprehensive **Exploratory Data Analysis (EDA)** on a synthetic food delivery dataset sourced from **Kaggle**. The dataset contains **10,000 orders spanning 2 years across 8 US cities**, covering customer behaviour, restaurant performance, delivery operations, and revenue patterns.

The goal of this analysis is to uncover meaningful business insights that can help a food delivery platform improve its operations, customer experience, and revenue strategy.

---

## 📂 Dataset Information

| Property | Details |
|---|---|
| Source | Kaggle |
| Rows | 10,000 |
| Columns | 31 |
| Time Period | 2 Years |
| Cities | New York, Los Angeles, Chicago, Houston, Phoenix, San Antonio, San Diego, Philadelphia |

### Key Columns

| Column | Description |
|---|---|
| `order_id` | Unique identifier for each order |
| `customer_loyalty_tier` | Bronze, Silver, or Gold tier |
| `customer_acquisition_channel` | How the customer was acquired |
| `restaurant_cuisine` | Type of cuisine |
| `restaurant_city` | City of the restaurant |
| `restaurant_rating` | Rating of the restaurant |
| `delivery_duration_actual` | Actual delivery time in minutes |
| `delivery_duration_estimated` | Estimated delivery time in minutes |
| `total_amount` | Total order value in dollars |
| `order_status` | Completed or Cancelled |
| `weather_precipitation` | Precipitation at time of order |
| `event_flag` | Special event like Valentine's Day |

---

## 🛠️ Libraries Used

- Pandas
- Numpy
- Matplotlib
- Seaborn

---

## 🔄 Project Workflow

```
Data Loading → Data Cleaning → Feature Engineering → 
Outlier Detection → Analysis → Visualizations → Conclusion
```

---

## 🧹 Data Cleaning

- Converted 3 columns from `object` to `datetime` — `customer_signup_date`, `order_timestamp`, `delivery_timestamp`
- Converted ID columns (`order_id`, `customer_id`, `restaurant_id`, `menu_item_id`) from `int64` to `str` since they are identifiers, not quantities
- Created `has_discount` binary flag from `discount_code` null values
- Created `has_event` binary flag from `event_flag` null values
- Filtered cancelled orders into a separate `df_delivered` dataframe (9,225 completed orders)

---

## ⚙️ Feature Engineering

| New Column | Description |
|---|---|
| `hour` | Hour extracted from `order_timestamp` |
| `month_name` | Month name extracted from `order_timestamp` |
| `Time_of_Day` | Morning / Afternoon / Evening / Night based on hour |
| `has_discount` | 1 if discount was applied, 0 otherwise |
| `has_event` | 1 if special event occurred, 0 otherwise |
| `signup_year` | Year extracted from `customer_signup_date` |

---

## 📊 Outlier Detection

Used the **IQR (Interquartile Range)** method to detect outliers across 6 numeric columns:

| Column | Lower Fence | Upper Fence | Outliers | Action |
|---|---|---|---|---|
| `total_amount` | -8.48 | 69.61 | 810 | Kept — genuine high value orders |
| `delivery_duration_actual` | 16.0 | 80.0 | 21 | Kept — extreme but possible delays |
| `tip` | -4.05 | 9.76 | 534 | Kept — genuine high tippers |
| `delivery_fee` | -0.99 | 11.06 | 0 | Clean |
| `item_price` | -9.81 | 49.92 | 0 | Clean |
| `restaurant_avg_prep_time` | -2.0 | 46.0 | 0 | Clean |

> No outliers were removed as they represent real business scenarios, not data entry errors.

---

## 🔍 Analysis

### 👤 Customer Behaviour
- **Bronze tier** places the most orders (6,042) but **Silver tier** spends the most on average ($36.33)
- All 5 acquisition channels contribute equally (~2,000 orders each) — **Email** brings the highest value customers ($35.94 avg)
- 2023 and 2024 signups are nearly equal — no strong signal that older customers order more

### 🚚 Delivery Performance
- **Phoenix** is the slowest city (50.05 min avg), **Los Angeles** is the fastest (44.73 min)
- **Restaurant 176** consistently exceeds estimated delivery time by ~10 minutes
- Higher precipitation moderately increases delivery time (correlation = 0.239)

### 💰 Revenue & Pricing
- **Indian** and **Fast Food** generate the highest average order value ($36.94 and $36.86)
- Discounts **reduce** average order value ($31.73 with discount vs $36.15 without) — discounts attract smaller orders
- **Pizza** contributes the most total revenue despite not having the highest average order value

### ⭐ Ratings
- **Chinese** restaurants are rated the highest (4.29)
- **Mexican** restaurants are rated the lowest (3.77) despite strong order volume

---

## 📈 Visualizations

11 visualizations created using **Matplotlib** and **Seaborn**:

| # | Chart Type | Question |
|---|---|---|
| 1 | Stacked Bar | Order volume by Time of Day — Weekday vs Weekend |
| 2 | Bar Chart | Order volume by hour of day |
| 3 | Horizontal Bar | Order volume by city |
| 4 | Violin Plot | Order value distribution by loyalty tier |
| 5 | Box Plot | Delivery duration by city |
| 6 | Bar Chart | Average restaurant rating by cuisine |
| 7 | Pie Chart | Order share by acquisition channel |
| 8 | Pie Chart | Order status distribution |
| 9 | Line Chart | Average order value by month |
| 10 | Histogram | Distribution of delivery duration |
| 11 | Scatter Plot | Precipitation vs delivery time by city |

---

## 📝 Key Findings & Conclusion

- 🌙 **Night** is the peak ordering time — targeted promotions would have the most reach
- 🏙️ **New York** gets the most orders, **Phoenix** the least
- 💳 Loyalty tier does **not** drive higher spending — Gold customers spend similar to Bronze
- 🌧️ Rain slightly increases delivery time but is **not** the main driver
- 📣 All marketing channels perform equally — no single channel dominates
- ✅ **92.25%** order completion rate — healthy and consistent platform operations
- 📅 Order value is **flat across all months** — no seasonal spikes

### 🚀 Opportunities for Improvement
1. Improve delivery speed in **Phoenix and San Antonio**
2. Investigate why **Gold tier** customers don't spend more than Bronze
3. Understand why **discounts reduce** order value instead of increasing it
4. Investigate why **Mexican cuisine** is rated lowest despite strong order volume

---

## 📁 Project Structure

```
📦 EDA_on_Synthetic_Food_Delivery_Transactions
 ┣ 📄 EDA_on_Synthetic_Food_Delivery_Transactions.ipynb
 ┣ 📄 synthetic_food_delivery_transactions.csv
 ┗ 📄 README.md
```

---

## 👤 Author

**Tushar**  
[GitHub](https://github.com/Tushar068) | [LinkedIn](https://www.linkedin.com/in/tushar-biswas03/)
