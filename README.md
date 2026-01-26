**Data issues found & cleaning rules:**

- 1 duplicate value on the OrderID column

**No row was deleted** because the data was different for the rest of the details indicating "Human Error" during data entry

- Some of the entries were not linked to any salespeople.

a) Looked through the data to establish a pattern; if there was a specific salesperson based on city and country

b) No relationship/pattern was determined, no salespeople had a specific region assigned to them. These blank cells were filled with "Unattributed" as the salespeople

- Some of the entries were not linked to any sales channels

a) Looked through the data by salesperson and the city to establish if these were repeat/unique customers based on the customer segment

b) Blanks were filled as "Unattributed"

- Some of the orders had the unit prices as negative values

1) Unit Price Values: Created a new column Q and used this formula: =IF(\$P2<0,NA(),\$P2)

a) If the unit price is less than 0 (Negative), then the formula returns an "N/A" error but if not, it retains the original value

2) Standardized the % discounts using this formula: =IF(R2>0.3,0.3,R2)

a) If the discount value is greater than 30% (0.3), it standardizes the percentage to be "0.3/30%" but if its anything less, it returns the original percentage

- Some orders had the required date earlier than the date when the order was placed

a) Used the datedif formula on this column =DATEDIF(B2,C2,"D")

i. Column B contains the Order date

ii. Column C contains the Required date

b) 34 values returned a "Num" error indicating that the required date captured was earlier than the order date

c) To fix the "Num" Error, I added the formula =IFERROR(DATEDIF(B3,C3,"D"),"-")

This helped clear the error without changing the Required Date column therefore maintaining the integrity of the data

- The data was all in general format. I attributed all columns accordingly based on the data these columns contained

**Assumptions made:**

- That **all** monetary values are assumed to be in a single reporting currency as no currency field was provided.
- Highest percentage discount is assumed to be 30% - can be modified on the "Dashboard Visualization" tab cell V1

**Analysis Tasks:**

**_Findings and observations are derived from the pivot tables created on the "Analysis" tab on the Excel file_**

4) Build a cohort of first-time sales by Country and Month:

• Identify the first month each Country appears and calculate monthly revenue tracked from that start (cohort analysis).

5) ABC analysis by SKU within each ProductCategory using GrossRevenue:

• Classify SKUs into A (top 80%), B (next 15%), C (last 5%) of revenue per category.

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

- Best performing region is Asia that has driven 2,846,460.89 in sales for the past 3 years.
- In the Asia and Africa regions, the retail sales are higher than online. To promote more sales, it would be best to increase the count of salepeople assigned to these regions, those who can frequent the customers to improve aftersales.
- Online sales cannibalizes retails sales within the Americas and Europe regions:

| **Region** | **Online** | **Retail** |
| --- | --- | --- |
| Europe | 585,406.72 | 465,656.77 |
| Americas | 689,951.45 | 302,853.58 |

8) Service level proxy:

• Using LeadTimeDays, determine % of orders meeting a 7-day target by Country and Category.

**Observations:**

- 21.84% of orders meet the 7-day target set
- Majority of the orders are delivered within 20 days. This leadtime accounts for 5.38% of orders created
- The product category mostly delivered within the 7-day timeline are accessories at 31.82% and laptops at 28.05%.
- The greatest outliers are within the product category of monitors. 84.04% of orders for monitors are delivered outside the 7-day target

**Recommendations:**

- Check for delivery delays from vendors on the different products especially the monitors
- Outsource an order system/improve the capabilities of the current order system that would send alerts to the salepeople 2 days before the 7-day SLA

9) Price compliance:

• Share of orders with DiscountPct > 20% by Region and Salesperson; list outliers.
