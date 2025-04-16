<h2 align="center">E-Commerce Data Analysis</h2>

Welcome to the **E-Commerce Data Analysis** project! This project demonstrates the use of Python for analyzing and visualizing e-commerce data to uncover meaningful insights and trends. Let's dive into the tools and techniques used.
## *📈Data Analysis Overview*
- [Monthly Sales Analysis](#1%EF%B8%8F⃣-monthly-sales-analysis)
- [Category-wise Sales Analysis](#2%EF%B8%8F⃣-category-wise-sales-analysis)
- [Sales Analysis By Sub-Category](#3%EF%B8%8F⃣-sales-analysis-by-sub-category)
- [Monthly Profit Analysis](#4%EF%B8%8F⃣-monthly-profit-analysis)
- [Profit by Category Analysis](#5%EF%B8%8F⃣-profit-by-category-analysis)
- [Profit by Sub-Category Analysis](#6%EF%B8%8F⃣-profit-by-sub-category-analysis)
- [Sales and Profit by Customer Segment](#7%EF%B8%8F⃣-sales-and-profit-by-customer-segment)
- [Sales-to-Profit Ratio Analysis](#8%EF%B8%8F⃣-sales-to-profit-ratio-analysis)
<h2 align="center">⚙️Data Preparation Setup</h2>

## *1. 📚Libraries Used*
Before starting the analysis, the following Python libraries will be utilized:

- **🧹 Pandas**: For efficient data cleaning, transformation, and manipulation.  
- **📊 Plotly Express**: For creating interactive and visually stunning data visualizations.

Ensure you have these libraries installed before proceeding. You can install them using:
```bash
pip install pandas plotly
```
Then,
```python
import pandas as pd
import plotly.express as px
```
## *2. 📂Uploading a CSV File*
After installing the required libraries, the first step is to upload the dataset. Use the following code to load the CSV file into a DataFrame:
```python
# Load the dataset
data = pd.read_csv('sample.csv', encoding='latin1')
```
🔍 Pro Tip: Always verify the encoding of your file to avoid loading errors. For most cases, latin1 works well for e-commerce datasets.
## *3. 📋Checking Data Types of Columns*
Once the dataset is loaded, you can check the data types and basic information about each column using the following code:
```python
# Display information about the dataset
data.info()
```
🚀 Why?: Knowing data types ensures proper handling during analysis, especially for date or categorical columns.
## *📆4. Converting Columns to Datetime*
If your dataset contains date columns that are not in the datetime format, you can convert them as follows:
- **🔄Converting a Single Column**
```python
# Convert a single column to datetime
data['Ship Date'] = pd.to_datetime(data['Ship Date'])
```
----------------OR----------------------
- **🔄Converting Multiple Columns**
```python
# Convert multiple columns to datetime using apply
data[["Order Date", "Ship Date"]] = data[["Order Date", "Ship Date"]].apply(pd.to_datetime)
```
🧠 Remember: Always ensure date columns are in datetime format for accurate filtering, grouping, and visualization.
## *📅5. Extracting Date Components for Analysis*
Time-based analysis often requires breaking down dates into specific components like Year, Month, Week, or Quarter. Use the code below to create these columns:
```python
# Extract specific components from the date
data['Year'] = data['Order Date'].dt.year       # Extract year
data['Month'] = data['Order Date'].dt.month     # Extract month
data['Quarter'] = data['Order Date'].dt.quarter # Extract quarter (1-4)
data['Week'] = data['Order Date'].dt.dayofweek  # Extract day of the week (0=Monday, 6=Sunday)
```
📈 Why Important?: These components help answer business-critical questions like monthly sales trends, quarterly profit margins, or weekly traffic patterns.
<h2 align="center">Data Analysis</h2>

## *1️⃣ Monthly Sales Analysis*
To analyze monthly sales, we calculate the total sales for each month and visualize the trend using a **line chart**.
This helps in identifying sales patterns over time.
```python
# Group data by Month and calculate total sales
Sales_by_month = data.groupby('Month')['Sales'].sum().reset_index()

# Create a Line Chart using Plotly
fig = px.line(Sales_by_month, x="Month", y="Sales", 
              title="Monthly Sales Trend", 
              labels={"Sales": "Total Sales"})

# Show the plot
fig.show()
```
result:![Image](https://github.com/user-attachments/assets/8918ceb4-38f5-4d42-927e-465cdc65e3b8)

## *2️⃣ Category-wise Sales Analysis*
For category-wise sales, we calculate the total sales for each category and visualize the distribution using a **pie chart**.
This helps in understanding the contribution of each category to overall sales.
```python
# Group data by category and calculate total sales
Sales_by_category = data.groupby('Category')['Sales'].sum().reset_index()

# Create a Pie Chart using Plotly
fig = px.pie(Sales_by_catogary, 
             names="Category", 
             values="Sales", 
             title="Sales Distribution by Category", 
             labels={"Sales": "Total Sales"},
             hole=0.4)  # Optional: Adds a donut-like hole for better visualization

# Optional: Customize text to show outside the pie chart
fig.update_traces(textposition='outside', textinfo='label+percent')

# Show the plot
fig.show()
```
Result:![Image](https://github.com/user-attachments/assets/d3dd22f0-cdc7-4305-997c-ef6504a28d7c)
## *3️⃣ Sales Analysis By Sub-Category*
To compare sub-category performance, we group sales by sub-categories and create a **bar chart**.
This is useful for identifying top-performing and underperforming sub-categories.
```python
# Group data by sub-category and calculate total sales
Sales_by_Sub_category = data.groupby('Sub-Category')['Sales'].sum().reset_index()

# Create a Bar Graph using Plotly
fig = px.bar(Sales_by_Sub_category, 
             x="Sub-Category", 
             y="Sales", 
             title="Sales by Sub-Category",
             labels={"Sales": "Total Sales"},
             color="Sub-Category",  # Optional: Color bars
             text="Sales")  # Display sales values on bar

# Optional: Place text outside the bars
fig.update_traces(textposition='outside')

#Show the plot
fig.show()
```
Result:![Image](https://github.com/user-attachments/assets/293b0574-d656-47cf-b6b3-c8a7b737a401)
## *4️⃣ Monthly Profit Analysis*
Analyzing monthly profit helps identify trends in profitability over time. A line chart visualizes these trends effectively.
```python
# Group data by Month and calculate total profit
profit_by_month = data.groupby('Month')['Profit'].sum().reset_index()

# Create a Line Chart using Plotly
fig = px.line(profit_by_month, 
              x="Month", 
              y="Profit",
              title="Monthly Profit Trend", 
              labels={"Profit": "Total Profit"})

# Show the plot
fig.show()
```
Result:![Image](https://github.com/user-attachments/assets/31a49e72-7084-4552-a14b-1162fb93a833)
## *5️⃣ Profit by Category Analysis*
This analysis provides insights into how profits are distributed across different categories. A pie chart is used to visualize the contribution of each category to the total profit.
```python
# Group data by category and calculate total profit
profit_by_category = data.groupby('Category')['Profit'].sum().reset_index()

# Create a Pie Chart using Plotly
fig = px.pie(profit_by_category, 
             names="Category", 
             values="Profit", 
             title="Profit Distribution by Category", 
             labels={"Profit": "Total Profit"},
             hole=0.4)  # Optional: Adds a donut-like hole for better visualization

# Optional: Customize text to show outside the pie chart
fig.update_traces(textposition='outside', textinfo='label+percent')

# Show the plot
fig.show()
```
Result:![Image](https://github.com/user-attachments/assets/21db4e9c-0c94-40ee-af9f-69e96d38d03d)
## *6️⃣ Profit by Sub-Category Analysis*
To dive deeper into profit trends, we analyze the profit by sub-categories. A bar chart is used to compare the profit performance of individual sub-categories, helping identify high and low-profit contributors.
```python
# Group data by sub-category and calculate total profit
profit_by_sub_category = data.groupby('Sub-Category')['Profit'].sum().reset_index()

# Create a Bar Graph using Plotly
fig = px.bar(profit_by_sub_category, 
             x="Sub-Category", 
             y="Profit", 
             title="Profit by Sub-Category",
             labels={"Profit": "Total Profit"},
             color="Sub-Category",  # Optional: Color bars based on profit values
             text="Profit")  # Display profit values on bars

# Show the plot
fig.show()
```
Result:![Image](https://github.com/user-attachments/assets/ad4667f1-9850-4de6-bfaf-aaf64a846634)
## *7️⃣ Sales and Profit by Customer Segment*

Analyze how sales and profit vary across customer segments using a **grouped bar chart**.
This helps in identifying the most profitable and highest-revenue-generating segments.
```python
# Group data by customer segment and calculate total sales and profit
Sales_and_Profit_By_Customer = data.groupby('Segment')[['Sales', 'Profit']].sum().reset_index()

# Melt the DataFrame to use for grouped bar chart
melted_data = Sales_and_Profit_By_Customer.melt(
              id_vars="Segment", 
              value_vars=["Sales", "Profit"],
              var_name="Metric", 
              value_name="Value")

# Create the grouped bar chart
fig = px.bar(melted_data, 
             x="Segment", 
             y="Value", 
             color="Metric", 
             barmode="group", 
             title="Sales and Profit by Segment",
             labels={"Value": "Amount", "Segment": "Customer Segment"})

# Show the plot
fig.show()
```
Result:![Image](https://github.com/user-attachments/assets/b4fd5b2d-92c4-4b60-bb49-066f3b81646d)


## *8️⃣ Sales-to-Profit Ratio Analysis*

The Sales-to-Profit Ratio measures how efficiently sales are converted into profit.
A higher ratio indicates lower profitability margins, while a lower ratio reflects better efficiency.

```python
# Group by 'Segment' and calculate total Sales-to-Profit ratio
Sales_Profit_Ratio = data.groupby('Segment')[['Sales', 'Profit']].sum().reset_index()
Sales_Profit_Ratio["Sales_to_Profit_Ratio"] = Sales_Profit_Ratio["Sales"] / Sales_Profit_Ratio["Profit"]

# Visualize the ratio using a bar chart
fig = px.bar(Sales_Profit_Ratio, 
            x="Segment", 
            y="Sales_to_Profit_Ratio", 
            title="Sales to Profit Ratio by Segment",
            color="Segment",  # Optional: Color bars based on the ratio
            labels={"Sales_to_Profit_Ratio": "Sales per Unit Profit", "Segment": "Customer Segment"},
            text="Sales_to_Profit_Ratio")

# Optional: Format text to show better
fig.update_traces(texttemplate='%{text:.2f}', textposition='inside', insidetextanchor='middle')

# Show the plot
fig.show()
```
Result:![Image](https://github.com/user-attachments/assets/9c929db0-93eb-4eaa-921a-77abb8137756)

# **📊Conclusion**
By modifying and reusing these analysis codes, **you can answer a wide range of business questions effectively and extract actionable insights!**
