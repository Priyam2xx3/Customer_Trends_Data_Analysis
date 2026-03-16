# Customer Shopping Behavior Analysis 🛒📊

## Overview
This is an end-to-end data analytics portfolio project that simulates a real-world corporate workflow. The project analyzes customer shopping behavior to uncover trends, improve customer engagement, and optimize marketing strategies. It covers the complete data analytics lifecycle: from data cleaning in **Python**, to deep exploratory data analysis using **SQL**, to building an interactive dashboard in **Power BI**.

## Business Problem Statement
A leading retail company wants to better understand its customers' shopping behavior to improve sales, customer satisfaction, and long-term loyalty. The management team is interested in uncovering which factors (such as discounts, seasons, demographics, and payment preferences) drive consumer decisions and repeat purchases. 

**Overarching Question:** *How can the company leverage customer shopping data to identify trends, improve customer engagement, and optimize marketing and product strategies?*

## Dataset Details
The dataset provides a snapshot of customer interactions and recent purchases. 
**Key Columns Included:**
- `customer_id`: Unique identifier for each customer.
- `age`, `gender`: Basic demographic details.
- `item_purchased`, `category`: The item bought and its broader category.
- `purchase_amount`: Total amount spent by the customer.
- `location`, `size`, `color`, `season`: Product and purchase details.
- `review_rating`: Customer's feedback rating.
- `subscription_status`: Whether the customer is part of a subscription service.
- `shipping_type`: Delivery method (e.g., Standard, Express).
- `discount_applied`: Indicates promotional activity.
- `previous_purchases`, `payment_method`, `frequency_of_purchases`: Transaction history summary.

## Tech Stack Used
* **Python (Pandas, SQLAlchemy):** Data manipulation, cleaning, and database loading.
* **PostgreSQL:** Advanced data querying and analysis.
* **Power BI:** Data visualization and interactive dashboard creation.

## Step-by-Step Workflow

### 1. Data Cleaning & Preprocessing (Python / Pandas)
* **Imputing Missing Values:** Handled missing `review_rating` values by replacing them with the *median* rating specific to their product `category` (to avoid bias).
* **Data Standardization:** Converted all column names to standard `snake_case` format (lowercase with underscores) for seamless SQL integration.
* **Feature Engineering:** * Created an `age_group` column (Young Adult, Adult, Middle-Aged, Senior) using `pd.qcut`.
    * Converted the textual `frequency_of_purchases` column into numeric `purchase_frequency_days` using custom mapping.
* **Data Reduction:** Identified and dropped redundant columns (`promo_code_used` duplicated `discount_applied`).
* **Database Integration:** Pushed the cleaned Pandas DataFrame directly into a local PostgreSQL database (`customer_behavior`) using `psycopg2` and `SQLAlchemy`.

### 2. Deep Data Analysis (PostgreSQL)
Connected to the database to answer critical business questions using advanced SQL queries (CTEs, Subqueries, Window Functions, Case Statements):
* **Revenue Segmentation:** Calculated total revenue split by gender.
* **Discount & Spend Analysis:** Identified customers who used a discount but still spent more than the overall average purchase amount using subqueries.
* **Product Performance:** Found the top 5 products with the highest average review ratings.
* **Shipping & Spend:** Compared the average purchase amounts between 'Standard' and 'Express' shipping.
* **Subscription Value:** Compared total revenue and average spend between subscribers and non-subscribers.
* **Discount Reliance:** Calculated the "discount rate" to find which products rely the most heavily on discounts to sell.
* **Customer Segmentation:** Used CTEs and CASE statements to segment customers into *New*, *Returning*, and *Loyal* tiers based on their number of previous purchases.
* **Category Leaders:** Used `ROW_NUMBER()` window functions to rank and find the top 3 most purchased products within every category.
* **Loyalty Pipeline:** Analyzed if repeat buyers (>5 previous purchases) are converting into subscribers.

### 3. Data Visualization & Dashboarding (Power BI)
Imported the dataset directly from PostgreSQL to Power BI to build an interactive, executive-ready dashboard.
* **Custom DAX Measures:** Created measures for *Total Customers*, *Average Purchase Amount*, and *Average Review Rating*.
* **Key Visuals:** * **Donut Chart:** Percentage of Customers by Subscription Status.
    * **Clustered Column Charts:** Revenue by Category & Sales by Category.
    * **Clustered Bar Charts:** Revenue by Age Group & Sales by Age Group.
* **Interactive Slicers:** Added vertical, horizontal, and list slicers for `Subscription Status`, `Gender`, `Category`, and `Shipping Type` to allow for dynamic data exploration.

## Key Insights & Recommendations
* *Gender-based Revenue Distribution: *(e.g., Male customers generate 60% of total revenue, indicating a stronger market share in this demographic.)*

Discount-Driven Spending: *(e.g., Surprisingly, customers who utilized a discount had a higher average purchase amount than the overall average, suggesting that promotions effectively encourage larger purchases.)*

High-Rated Product Categories: *(e.g., Gloves and Sandals are among the top-rated products by average review rating, presenting opportunities for premium pricing or featured marketing.)*

Shipping Preference and Order Value: *(e.g., Express shipping is associated with a significantly higher average order value compared to Standard shipping, recommending a potential push for faster delivery options as an up-sell.)*

Subscription Program Impact: *(e.g., Non-subscribed customers contribute a larger portion of total revenue despite having a similar average spend to subscribers, highlighting a critical area for improving the value proposition of the subscription model.)*

Revenue Leaders by Product: *(e.g., Within the 'Clothing' category, 'Blouse' is the top-performing item by total revenue.)*

Loyalty Conversion: *(e.g., Only a small fraction of repeat buyers are currently subscribed, indicating a missed opportunity for converting loyal customers into recurring revenue through subscriptions.)*

Target Demographics: *(e.g., Young Adults are the primary revenue drivers, followed by Middle-Aged Adults, suggesting that marketing efforts should remain focused on these age groups.)*

## How to Run This Project
1. Clone this repository to your local machine.
2. Ensure you have Jupyter Notebook, Python, and PostgreSQL installed.
3. Install the required Python libraries: `pip install pandas psycopg2-binary sqlalchemy`
4. Run the Jupyter Notebook to clean the CSV data and push it to your SQL database. *(Note: Update the `create_engine` credentials with your own PostgreSQL host, port, user, and password).*
5. Open PGAdmin or your preferred SQL IDE to execute the analysis queries.
6. Open the `.pbix` file in Power BI Desktop and update the data source settings to point to your local database.

## Credits
This project was inspired by and built following the comprehensive end-to-end data analytics tutorial by **Amlan Mohanty**.
