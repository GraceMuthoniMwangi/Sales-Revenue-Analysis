**Data issues found & cleaning rules:**

- 1 duplicate value on the OrderID column

**No row was deleted** because the data was different for the rest of the details indicating "Human Error" during data entry

- Some of the entries were not linked to any salespeople.

a) Looked through the data to establish a pattern; if there was a specific salesperson based on city and country

b) No relationship/pattern was determined; the regions were not specifically assigned to particular salespeople. These blank cells were filled with "Unattributed" as the salespeople

- Some of the entries were not linked to any sales channels

a) Looked through the data by salesperson and the city to establish if these were repeat/unique customers based on the customer segment

b) Blanks were filled as "Unattributed"

- Some of the orders had the unit prices as negative values

1) Unit Price Values

a) Standardized the negative unit prices by formatting the currency-related columns to accounting formats

2) Standardized the % discounts using this formula, using a variable cell U1 on the Dashboard Visualization tab

a) If the discount value is greater than the percentage in the variable cell, it standardizes the percentage to be "variable cell value" but if it's anything less, it returns the original percentage

- Some orders had the required date earlier than the date when the order was placed

a) Used the datedif formula on this column =DATEDIF(B2,C2,"D")

i. Column B contains the Order date

ii. Column C contains the Required date

b) 34 values returned a "Num" error indicating that the required date captured was earlier than the order date

c) To fix the "Num" Error, I added the formula =IFERROR(DATEDIF(B3,C3,"D"),"")

This helped clear the error without changing the Required Date column therefore maintaining the integrity of the data

- The data was all in general format. I attributed all columns accordingly based on the data these columns contained

**Assumptions made:**

- That **all** monetary values are assumed to be in a single reporting currency as no currency field was provided.

**Analysis Tasks:**

**_Findings and observations are derived from the pivot tables created on the "Analysis" tab on the Excel file_**

4) Build a cohort of first-time sales by Country and Month:

• Identify the first month each Country appears and calculate monthly revenue tracked from that start (cohort analysis).

**Findings/Observations:**

- All countries appear in January 2023 except for Japan, which made an appearance in March 2023
- The first country to make a sale in January 2023 is Canada

5) ABC analysis by SKU within each ProductCategory using GrossRevenue:

• Classify SKUs into A (top 80%), B (next 15%), C (last 5%) of revenue per category.

| Revenue drivers | Networking | Laptops | Printers | Monitors | Components | Phones | Accessories |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **80%** | **69** | **65** | **82** | **75** | **72** | **70** | **70** |
| **15%** | **13** | **12** | **15** | **14** | **14** | **13** | **13** |
| **5%** | **4** | **4** | **5** | **5** | **5** | **4** | **4** |
| &nbsp; | **16.40%** | **15.67%** | **14.75%** | **14.09%** | **13.94%** | **12.87%** | **12.28%** |

**Findings/Observations:**

- The highest revenue driver by product category is Networking with the least as categories
- The printers has the highest number of SKUs that are within the 80% gross revenue targets while laptops has the lowest number

6) Salesperson productivity:

• Compute Revenue/Order, Orders/Month, and GrossProfit/Order by Salesperson; highlight the top and bottom 3.

**Findings:**

- The 3 top performing salespeople are F. Müller with 51 orders, J. Njeri with 50 orders & B. Chen with 48 orders
- The 3 least performing salespeople are E. Garcia with 34 orders, N. Brown with 32 orders and G. Dubois with 30 orders.
- B. Chen has driven the highest gross profit of 315,969.97 overall with a total of 48 orders while N. Brown drives the least at 110,646.46 with a total of 32 orders.

**Causes:**

- The difference in the orders could be derived from different tenures of the salespeople
- The total profit by the salespeople is also determined by the % discounts given by the salespeople

**Recommendations:**

- Standardize the maximum discount that can be issued to a customer by all salespeople e.g Standard discount of 30% or lower
- Product trainings of the salespeople to ensure goods are never sold below the exact cost they were purchased for, from the vendors
- Ensure correct mapping of the data by the salespeople to ensure data is always correctly attributed

7) Channel mix & cannibalization:

• Compare revenue shares by Channel across Regions; identify where online cannibalizes retail (justify with data).

- The best performing region is Asia, which has driven 2,846,460.89 in sales for the past 3 years.
- In the Asia and Africa regions, the retail sales are higher than online. To increase sales, it would be best to increase the number of salespeople assigned to these regions, who can visit customers to improve after-sales.
- Online sales cannibalizes retails sales within the Americas and Europe regions:

| **Region** | **Online** | **Retail** |
| --- | --- | --- |
| Europe | 585,406.72 | 465,656.77 |
| Americas | 689,951.45 | 302,853.58 |

8) Service level proxy:

• Using LeadTimeDays, determine % of orders meeting a 7-day target by Country and Category.

**Observations:**

- 23.08% of orders meet the 7-day target set; 34 entries had an earlier required date than the actual order date
- The majority of orders are delivered within 20 days. This lead time accounts for 5.38% of orders created
- The product category mostly delivered within the 7-day timeline are accessories at 31.82% and laptops at 28.05%.
- The greatest outliers are within the product category of monitors. 84.04% of orders for monitors are delivered outside the 7-day target
- Majority of the products that are meeting the 7 day lead time are the printers with 32.04% of the orders meeting this leadtime. This however, is still relatively low as compared to the number of orders received.

**Recommendations:**

- Check for delivery delays from vendors on the different products especially the monitors
- Outsource an order system/improve the capabilities of the current order system that would send alerts to the salepeople 2 days before the 7-day SLA

9) Price compliance:

• Share of orders with DiscountPct > 20% by Region and Salesperson; list outliers.

**Findings:**

- 92 orders fall as outliers with the discount issued being more than 20%
- The region with the highest outliers in order is Americas, Asia, Africa and then Europe
- I. Johnson has a total of 11 orders that had discounts greater than 20%
- The highest discount, more than 50%, was issued by M. Rossi in the Africa region
