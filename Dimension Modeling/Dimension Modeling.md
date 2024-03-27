## What is Dimension Modeling
- Methods used in data warehouse to organize the data in a way that is optimized for querying and analysis.
  
 ### Steps in Dimensional Modeling
 - Gather requirement's (usability, performance)
 - Identify ==Granularity== 
 - Identify Facts
 - Identify Dimensions 
 
 #### What is Granularity?
 - The level of grain at which data is collected and reported.
 - The grain determines what a single row will represent in the fact table.
 - Grains is not always time/date.
 - Designed from the lowest possible grain (علشان لما يبقي قليل هتبقي سهل توصل للاعلي منه لكن العكس لا)
 
 ### Elements of Dimensional Modeling 
 #### 1- Fact Table
 - The ==primary== table in a dimensional model.
 - Contains key measurements facts, primary key and foreign keys of dimensions.
 - ==Qualitative== and ==transactional== data (profit, revenue).
 - Can be aggregated.
#### 2- Dimension Table
- Contains dimension of a fact and business reference data.
- ==Quantitative== data (category, period, country, product)
- Cant be aggregated.
#### 3- Attributes 
- Characteristic's of the dimension.

## Types of Facts 
### 1- Fact Tables
#### 1.1- Transactional 
- Contains detailed data at the most granular level.
- Each record represents a transaction.
- Continuously updated in real-time as new transactions occur.
- High data volume.
#### 2.1- Periodic 
- Records measurements at regular time intervals either on daily, weekly or monthly basis.
- Each record represent the aggregated metric for that period.
- Updated periodically at the end of each reporting period.
- Low data volume.
#### 3.1- Accumulating 
- Record a running total of metrics to track commutative measurement like year-to-date totals.
- Each record represents the total from the beginning of time to that snapshot date.
- Updated incrementally as new transactions occur or new data becomes available.
- Historical data.

### 2- Facts Columns
#### 2.1- Additive 
- Most flexible facts that can be aggregated across all columns.
- This includes sales, quantity or profit.
  
![[Pasted image 20240327053903.png]]

- Aggregating page_views by GeoId offers insights into site performance by cities/countries.
- Aggregating page_views by PageId reveals performance insights about individual pages within the website.
#### 2.2- Semi-Additive 
- Facts that can be aggregated across some dimension but not all.
- This includes balance, inventory, head count.
  ![[Pasted image 20240327055028.png]]
- Aggregating the population by country may result in incorrect totals, as populations cannot be combined across countries. For instance, adding populations of SG will result in 10,010,000 (5,000,000 + 5,010,000), which is incorrect.
- Aggregating population across time periods, such as years, to obtain the total population for a specific timeframe.
#### 2.3- Non-Additive 
- Facts that cant be aggregated at all.
- This includes ratios, percentages, price or any measure that doesn't makes sense to aggregate.
#### 2.4- Derived 
- Calculated measure from another basic measure.
- This includes profit = revenue - COGS.
#### 2.5- Textual 
- Qualitative or descriptive information that doesn't have any numerical values.
- This includes comments, notes or  description's associated with specific transaction, customer or product.

## Types of Dimensions

### 1- Conformed 
- Constant and shared across multiple fact tables.
- Example: customer dimension can be used in orders_fact and customer_service_fact .




## Dimension Modeling Schema

### 1- Star 
![[Pasted image 20240327045844.png]]
- Special case of snowflake schema.
- Multiple dimensions map to a single fact table.
- Denormalized 
- High performance due to less number of joins. 
- High data redundancy.
- High disk storage.
- Most common schema in the data mart.
- Read operations only.
### 2- Snowflake
![[snowflake-schema.png]]
- Multiple dimensions map to a multiple dimension tables.
- Normalized.
- Low performance due to less number of join.
- Low data redundancy.
- Low disk storage.
- Write and update operations only.
### 3- Galaxy
![[Pasted image 20240327045808.png]]
- Multiple dimension map to multiple fact tables ==(collection of STAR schema)==.
- Normalized.
- Low performance due to many joins.
-  Low data redundancy.
- Low disk storage.


