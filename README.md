# Zomato Sales Analysis

## 📊 Project Overview

This project involves a comprehensive **Exploratory Data Analysis (EDA)** and **Key Performance Indicator (KPI) calculation** on a dataset of Zomato restaurants in Bangalore, India. The primary objective is to extract actionable insights into restaurant performance, market trends, and customer behavior to help stakeholders (e.g., Zomato, restaurant owners, potential investors) make data-driven decisions.

## 🚀 Goals and Objectives

The analysis aims to answer several key business questions:

* What is the **distribution of restaurants** across different locations in Bangalore?
* What are the **approximate total sales** and **average order value**?
* Which **locations and restaurant types** generate the highest approximate sales?
* What is the **impact of online ordering** and **table booking facilities** on restaurant ratings?
* How do **ratings, costs, and popularity (votes)** correlate?
* What are the **most popular and highest-rated cuisines**?
* How does the **availability of online order/table booking** vary across different locations?
* What is the **composition of restaurant types** within key locations?

## 📂 Dataset

The dataset used is `zomato.csv`, containing information about various restaurants in Bangalore. Key columns include:

* `name`: Name of the restaurant
* `online_order`: Whether online ordering is available (Yes/No)
* `book_table`: Whether table booking is available (Yes/No)
* `rate`: Aggregate rating of the restaurant (e.g., '4.1/5', 'NEW', '-')
* `votes`: Number of votes received
* `location`: Location of the restaurant
* `rest_type`: Type of restaurant (e.g., Casual Dining, Cafe, Quick Bites)
* `cuisines`: Cuisines offered by the restaurant
* `approx_cost`: Approximate cost for two people
* `listed_in(type)`: Type of listing (e.g., Delivery, Dine-out, Pubs and Bars)
* `listed_in(city)`: Area/sub-city where the restaurant is listed

## 🛠️ Methodology

The analysis followed a structured approach:

### 1. Data Loading & Initial Inspection
* Loaded the `zomato.csv` dataset into a Pandas DataFrame.
* Performed initial checks for shape, column names, data types, and missing values.

### 2. Data Preprocessing & Cleaning
* **Column Standardization**: Renamed columns for consistency (e.g., `approx_costfortwopeople` to `approx_cost`) and standardized names to lowercase, removing special characters.
* **Irrelevant Column Removal**: Dropped columns like `url`, `address`, `phone`, `menu_item`, `dish_liked`, and `reviews_list` as they were not directly used for the defined objectives.
* **Handling Missing Values**:
    * Rows with missing `rate` values were dropped.
    * Missing `approx_cost` and `votes` were imputed using their respective median/mean to retain valuable data.
* **Data Type Conversion**:
    * **`rate` Column**: Cleaned by removing the '/5' suffix, converting 'NEW' and '-' entries to `NaN`, and then converting to a numeric (float) type. A crucial step involved explicitly converting to `string` (`.astype(str)`) before applying string operations to avoid errors.
    * **`approx_cost` Column**: Cleaned by removing commas (e.g., '500,000' to '500000') and converted to a numeric (float) type.
    * **`votes` Column**: Converted to a numeric (integer) type.
    * **`online_order` & `book_table`**: Converted 'Yes'/'No' values to `1`/`0` for numerical analysis.
* **Outlier Treatment**: Applied the Interquartile Range (IQR) method to cap outliers in `votes` and `approx_cost` to ensure robust statistical measures.
* **Categorical Feature Grouping**: Grouped less frequent categories in `rest_type` (frequency < 1000), `location` (frequency < 300), and `cuisines` (frequency < 100) into an 'others' category. This significantly improved the clarity and interpretability of visualizations.

### 3. Key Performance Indicator (KPI) Calculation
* **Total Sales (Approximation)**: Summed the `approx_cost` column to estimate total potential sales.
* **Average Order Value (AOV)**: Calculated the mean of the `approx_cost` column.
* **Sales by Region/Restaurant Type**: Grouped data by `location` and `rest_type` to identify top contributors to approximate sales, presented in clear tabular formats.

### 4. Exploratory Data Analysis (EDA) & Visualizations
A wide range of visualizations were created to understand trends and relationships:
* **Distribution of Restaurants**: Bar plot showing the number of restaurants across different locations.
* **Online Order & Table Booking Availability**: Pie charts illustrating the percentage of restaurants offering these facilities.
* **Rating Trends**: Box plots showing the distribution of ratings across various restaurant types, and the impact of online order/table booking on ratings.
* **Cost vs. Rating**: Scatter plot exploring the relationship between approximate cost and rating.
* **Votes vs. Rating**: Scatter plot to see if higher votes correlate with higher ratings.
* **Location-wise Service Availability**: Bar plots visualizing the count of restaurants with/without online order and table booking facilities per location.
* **Restaurant Type Distribution by Location**: Bar plots showing the mix of restaurant types within specific areas.
* **Cuisine Analysis**: Bar plots for the most popular cuisines (by count), average rating by cuisine, and average cost by cuisine.
* **Overall Data Distributions**: Histograms for `rate` and `votes` to understand their overall distribution shapes.
* **Correlation Matrix**: Heatmap displaying the correlation coefficients between all numerical variables (`rate`, `approx_cost`, `votes`, `online_order`, `book_table`).

## 📈 Key Findings & Insights

* **Dominant Locations**: Identified Bangalore's hotspots for restaurants, indicating prime business areas.
* **Service Adoption**: Revealed the penetration rate of online ordering and table booking among restaurants.
* **Rating Drivers**: Explored whether offering online orders or table booking has a noticeable impact on restaurant ratings.
* **Pricing Trends**: Understood average costs for different cuisines and restaurant types.
* **Popular Cuisines**: Highlighted the most prevalent and highest-rated cuisines in the city.
* **Market Opportunities**: Insights from location-wise service availability could indicate underserved areas for online delivery or table booking.
* **Sales Performance**: Identified top-performing locations and restaurant types in terms of approximate sales.
* **Inter-variable Relationships**: Discovered correlations between numerical features, such as the relationship between votes and ratings.

## 🛠️ Technical Stack

* **Programming Language**: Python
* **Libraries**:
    * `pandas` for data manipulation and analysis.
    * `numpy` for numerical operations.
    * `matplotlib.pyplot` for basic plotting.
    * `seaborn` for enhanced statistical data visualization.
* **Environment**: Jupyter Notebook

## ⚠️ Limitations & Future Work

* **Data Granularity**: The dataset does not include unique `customer_id` or timestamped transaction data. This limits the ability to calculate advanced metrics like **Customer Lifetime Value (CLV)** and **Customer Retention Rate**, which would require more granular user behavior data.
* **Sales Approximation**: The 'sales' figures are approximations based on `approx_cost` for two people, not actual revenue from transactions.
* **Future Enhancements**:
    * Integrate actual transactional data to calculate precise CLV, retention rates, and revenue per customer.
    * Perform **sentiment analysis** on restaurant reviews (if detailed review text were available) to gauge customer sentiment more deeply.
    * Develop a **restaurant recommendation system** based on user preferences and restaurant attributes.

## 🚀 How to Run the Project

1.  **Clone the Repository:**
    ```bash
    git clone <repository-url>
    cd <repository-name>
    ```
2.  **Install Dependencies:**
    Make sure you have Python installed. Then install the necessary libraries:
    ```bash
    pip install pandas numpy matplotlib seaborn
    ```
3.  **Download the Dataset:**
    Place the `zomato.csv` file in the same directory as the Jupyter Notebook.
4.  **Run the Jupyter Notebook:**
    ```bash
    jupyter notebook "zomatosales analysis (1).ipynb"
    ```
    Open the notebook in your browser and run all cells sequentially.

---
