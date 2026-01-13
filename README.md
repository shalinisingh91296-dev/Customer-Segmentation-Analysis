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

([<img width="385" height="123" alt="image" src="https://github.com/user-attachments/assets/3c1a454f-7b76-4c1e-b20b-773450b5b778" />])



# Core DAX measures for RFM
  * Recency =
             DATEDIFF (
    
            [Last Purchase Date],
    
            MAX ( Sales[OrderDate] ),
    
            DAY
    
            )
    * Frequency =
                   CALCULATE (
      
                   DISTINCTCOUNT ( Sales[OrderID] ),
      
                   ALLEXCEPT ( Sales, Sales[CustomerID] )
      
                 )

    * Monetary =
                 CALCULATE (
      
                  SUM ( Sales[Sales] ),
      
                  ALLEXCEPT ( Sales, Sales[CustomerID] )
      
                  )


# RFM scoring on scale of 1-5
  * Recency Score (Lower is better)
    
        Recency Score =
                        SWITCH (
                         TRUE(),
                         [Recency] <= 30, 5,
                         [Recency] <= 60, 4,
                         [Recency] <= 90, 3,
                         [Recency] <= 180, 2,
                                1
                              )

    
  * Frequency Score
  
       Frequency Score =
                        SWITCH (
                         TRUE(),
                        [Frequency] >= 20, 5,
                        [Frequency] >= 15, 4,
                        [Frequency] >= 10, 3,
                        [Frequency] >= 5, 2,
                                          1
                              )


* Monetory Score

     Monetary Score =
                      SWITCH (
                       TRUE(),
                      [Monetary] >= 10000, 5,
                      [Monetary] >= 7000, 4,
                      [Monetary] >= 4000, 3,
                      [Monetary] >= 2000, 2,
                                          1
                         )




# Customer Segment Logic
   * RFM Total Score
    
      RFM Score =
     
                 [Recency Score] + [Frequency Score] + [Monetary Score]

# Customer Segment Classification

       Customer Segment =
                          SWITCH (
                           TRUE(),
                          [RFM Score] >= 13, "Champions",
                          [RFM Score] >= 10, "Loyal Customers",
                          [RFM Score] >= 7, "Potential Loyalists",
                          [RFM Score] >= 5, "At Risk",
                                            "Lost Customers"
                                  )

    

# Dashboard Design( Power BI)
   Page 1: Customer Overview
   
   1.KPI Cards: 
      * Total Customers
      * Total Revenue
      * Avg Revenue per Customer
      
   2. Bar Chart: Customers by Segment
   3. Donut Chart: Revenue by Segment
   4. Line chart: Monthly Revenue
   

   Page 2: RFM Analysis
   1. Table: CustomerID | R | F | M | Segment
   2. Top 10 Customers by Revenue
   3. Category-wise spending by segment

   
      

# Business Insights
