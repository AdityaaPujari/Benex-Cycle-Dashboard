# Benex-Cycle-Dashboard

## Introduction
Welcome to the Benex Cycle Dashboard, where data meets strategy in the pursuit of sales excellence. In a world where every decision counts, this dynamic tool serves as your compass, guiding you through the intricate landscape of Benex cycle sales. Let's embark on this journey together, harnessing the power of insights to drive impactful change and unlock new avenues of success.

#### The report consits of 2 pages
- Home Page
- Content Analysis
  
## Objective
Our main goal here is to boost Benex cycle sales and profitability. That's what we're ultimately trying to achieve.To do that, we need information. This data likely comes from our sales database. It tracks things like how many Benex cycles we've sold (quantity) and the total revenue we've generated, along with details about the products themselves (categories and subcategories). Additionally, it might show sales figures for different regions.

so following are some of our objectives needs to follow
- Connect and Transform the Raw data
- Create Relationships
- Create DAX measures
- Create a visualization and make meaningful insights

## Data Sourcing

so 1st step is to get the data file to the powerbi

Data Contains 6 sheets/Tables

1. Cycles Age Group with 4 rows and 2 columns
2. Cycles Gender with 2 rows and 2 columns
3. Cycles Product Categories with 3 rows and 2 columns
4. Cycles Product Subcategories with 17 rows and 3 columns
5. Cycles Products with 130 rows and 5 columns
6. Cycles Regions with 10 rows and 7 columns
7. FactTable with 1,63,072 rows and 8 columns

## Data Transformation/Cleaning
#### Once we have the data, we need to make sure it's accurate and usable. Imagine it like cleaning up your workspace before you start a project. We might need to fix any errors or inconsistencies in the data, and sometimes we might need to adjust the format to make it easier to analyze.
  
- Step 1 : Load data into Power BI Desktop, dataset is a Excel file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options. 
- Step 3 : It was observed that in none of the columns errors & empty values were present.
- Step 4 : Promote headers and change the data type
- Step 5: Close and apply 
## Data Modelling
### snap of data model structure
![model benex](https://github.com/AdityaaPujari/Benex-Cycle-Dashboard/assets/131788257/eaced936-e0af-4d22-90af-8b6d4762ee8a)
- it shows the snowflake structure
- fact table is main table where others table are connected



## Dax Created

Now comes the fun part – we get to see what the data tells us! We calculate key metrics like the total quantity of Benex cycles sold within a specific timeframe We also look at the total revenue generated and the total profit earned after accounting for costs. An important metric is the profit margin, which tells us what percentage of our revenue remains as profit.
If we have sales goals set, we can compare our actual sales figures (in thousands) to those goals and see how we're doing. We can also analyze trends over time to see if sales are increasing, decreasing, or staying steady. Finally, we can look at the top-selling products in different regions and see if there are any interesting patterns based on the product categories or subcategories.

- Trageted Revenue = 50000000
- Total Revenue = 
  SUMX(
    FactTable,
    FactTable[Quantity_Sold] * RELATED('Cycles Products'[Unit_Price]))
- Total COGS = 
  SUMX(
    FactTable,
    FactTable[Quantity_Sold]
          *
    RELATED('Cycles Products'[Unit_Cost]))
- Sub Category title = 
  "Top-"&'DYNAMIC TOP N'[DYNAMIC TOP N Value] &  "Product subcategory by revenue
- quantity sold = SUM(FactTable[Product_Key])
- Profit Margin = [Total Revenue]-[Total COGS]
- Product Title = 
  "Top-"&'DYNAMIC TOP N'[DYNAMIC TOP N Value] &  "Product by revenue
- Product Subcategory Ranking = VAR Product_Rank=
         RANKX(
          ALL( 'Cycles Product Subcategories'[SubCategory]), CALCULATE([Total Revenue]))
          RETURN
          IF(Product_Rank<='DYNAMIC TOP N'[DYNAMIC TOP N Value],[Total Revenue])
- Product Ranking = 
  VAR Product_Rank=RANKX(
    ALL('Cycles Products'[Product_New]), CALCULATE([Total Revenue]))
   RETURN
        IF(Product_Rank<='DYNAMIC TOP N'[DYNAMIC TOP N Value],[Total Revenue])

- pacificRevenue = CALCULATE([Total Revenue],KEEPFILTERS('Cycles Regions'[Continent]="pacific"))
- Europe Revenue = CALCULATE([Total Revenue],KEEPFILTERS(FILTER('Cycles Regions','Cycles Regions'[Continent]="europe")))
- North Aeric Revenue = CALCULATE([Total Revenue],KEEPFILTERS('Cycles Regions'[Continent]="north america"))
- We have also calculated the dynamic top N

![top n](https://github.com/AdityaaPujari/Benex-Cycle-Dashboard/assets/131788257/27e9b0f7-3b4a-4995-b47e-2067d00e6a4e)

- DYNAMIC TOP N = GENERATESERIES(1, 20, 1)
  

  

## Analysis and Visualization
### Benex Cycle dashboard
![benex 1](https://github.com/AdityaaPujari/Benex-Cycle-Dashboard/assets/131788257/4c586f18-9185-431f-b7fc-cbbdf30d0d92)


### Metrics: The key metrics displayed on the dashboard are likely:
- Total Quantity Sold: Total number of Benex cycles sold within a specific timeframe (e.g., month, quarter, year).
- Total Revenue: Total revenue generated from Benex cycle sales during the timeframe.
- Total Profit: Total profit earned after accounting for costs.
- Profit Margin: Percentage of revenue that remains as profit after factoring in costs.
- Sales Goals (Optional): Targets for each metric to measure performance against.
- Top Products by Revenue: The top-selling products in different regions along with their subcategories.

 ### Content Analysis 
![Benex 2](https://github.com/AdityaaPujari/Benex-Cycle-Dashboard/assets/131788257/d10e3197-5ccb-4690-aeb4-dd51bd4995ae)

- Highest profit margin in the month of dec is 1,34,48,465
- Highest profit margin in the year 2019 is 3,80,84,442


## Actionable Recommendations:
#### Based on the analysis of sales performance, profitability, and regional trends, insights are generated. These insights might suggest areas for improvement, such as
- Tailoring marketing campaigns to focus on popular products or subcategories in specific regions.
- Investigating cost-saving measures to improve profit margins.
- Exploring opportunities to develop new products or variations based on customer preferences.
- Action Items: Specific action items are defined based on the recommendations. These might involve developing and implementing targeted marketing campaigns, collaborating with product development teams to 
  explore new product ideas, or working with cost-reduction initiatives.
- Monitoring & Evaluation: The impact of the implemented actions is monitored and evaluated over time. This might involve tracking changes in sales performance, profitability, and customer behavior. The Benex 
  cycle dashboard can be used to monitor these changes and assess the effectiveness of the implemented strategies.

## Conclusion:
- Analysis of sales performance, profitability, and regional trends reveals actionable insights: tailor marketing campaigns to popular products in specific regions, explore cost-saving measures to enhance profit margins, and develop new products based on customer preferences. Action items include implementing targeted marketing, collaborating on product development, and initiating cost-saving initiatives. Monitoring involves tracking changes in sales, profitability, and customer behavior to evaluate strategy effectiveness using the Benex cycle dashboard. This iterative approach ensures ongoing improvement and competitiveness in the market.












