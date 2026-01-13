# Customer-Segmentation-Analysis

# Overview
I have built an end-to-end RFM based customer segmentation using Power BI and DAX. Analyzed customer purchasing behaviour to classify customers into champions, loyal, at risk, and lost segments. Designed interactive dashborads with KPIs, RFM scoring, and actionable insights that improved targeted marketing startegy and customer retention.


# Business Objective
To identify high-value customers, segment customers on purchasing behavior so that business can design targeted marketing strategies and improve customer retention and revenue.

# Dataset
I have used an e-commerce dataset for this project.
 
# Key questions this projects answers
1. Who is our most valuable customers?
2. Which customer segment contribute the most revenue?
3. What is the average revenue per customer by segment?

   
# Load Data into Power BI
1. Open Power BI desktop
2. Get Data-Excel/CSV
3. Loaded the E-commerce sales dataset
4. Open Power Query Editor and perform cleaning and transfromation.
   * Removed duplicates if any
   * Handled Null values
   * Ensured correct data types for each columns
5. Close and Apply     

# Data Modeling
Single fact table is enough for this project but we can still create a date table if we need some advaned DAX measures.
Date Table = 
              ADDCOLUMNS(
                     CALENDAR(DATE(2020,1,1),DATE(2025,12,31)),
                     "Year", YEAR([Date]),
                     "Month" FORMAT([Date], "MMM"),
                     "Month-Name",MONTH([Date])
                     )
                     
* Connect OrderDate-Date

# RFM Analysis Explaination


# Core DAX measures for RFM
# RFM scoring on scale of 1-5
# Customer Segment Logic
# Customer Segment Classification
# Dashboard Design
# Business Insights
