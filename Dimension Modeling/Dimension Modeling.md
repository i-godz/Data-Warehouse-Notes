## What is Dimension Modeling
- Methods used in data warehouse to organize the data in a way that is optimized for querying and analysis.
  
 ### Steps in Dimensional Modeling
 - Gather business requirement's (usability, performance)
 - Identify Granularity 
 - Identify Facts
 - Identify Dimensions 
 
 #### What is Granularity?
 - The level of detail at which data is collected and reported (Level of grain الي عايزين نحطه فكل record)
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
- ==Quantitative== data (category, period, country, product).
- Cant be aggregated.
#### 3- Attributes 
- Characteristic's of the dimension.

## Types of Facts 
### 1- Fact Tables
#### 1.1- Transactional 
- Contains detailed data at the most granular level.
- Each record represents a transaction.
- Continuously updated in real-time as new transactions occur.
- Stores high data volume.
#### 2.1- Periodic 
- Records measurements at regular time intervals either on daily, weekly or monthly basis.
- Each record represent the aggregated metric for that period.
- Updated periodically at the end of each reporting period.
- Stores low data volume.
#### 3.1- Accumulating 
- Record a running total of metrics to track commutative measurement like year-to-date, month-to-date, quarter-to-date totals.
- Each record represents the total from the beginning of time to that snapshot date.
- Updated incrementally as new transactions occur or new data becomes available.
- Stores historical data.
#### 3.4 Factless 
- Unlike other fact tables, a factless fact table does not contain any quantitative metrics or measures.
- Instead of numerical data, it captures events, occurrences, or relationships between different dimensions.
- Common examples include tracking events such as customer interactions, website clicks, student enrollments, or product relationships (e.g., which products are often purchased together).

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
[![click to zoom](https://byobi.wordpress.com/wp-content/uploads/2021/05/779d9-multiple-star-schemas-03.png?w=300&h=147)
- Constant and shared across multiple fact tables and has the same meaning.
- Example:  Date as a key, product id as a key.
### 2- Degenerate
 
![[Screenshot 2024-03-28 at 9.58.22 AM.png]]

- It refers to a data attribute that functions as a primary key in a fact table but lacks other descriptive attributes.
- Instead of being in its own table, it exists as a reference within the fact table.
### 3- Junk

![[Screenshot 2024-03-28 at 10.16.10 AM.png]]

- Contains a collection of random, low cardinality attributes that are unrelated to any fact table 
- They don't directly contribute to the facts being analyzed.
- Attributes like gender (M/F), status flag (active/inactive), or order status (pending/shipped/delivered).
- These attributes are grouped together to prevent creating fragmented dimensions, which can complicate analysis.
### 4- Role-Playing 

![[Screenshot 2024-03-28 at 10.26.28 AM.png]]

- One dimension is utilized in different contexts, each with its own description or role.
- A date dimension can serve as both order date and shipment date.
-  Instead of creating separate dimensions for each role, this approach minimizes duplication and simplifies the model.
- Different roles are distinguished using aliases to clarify their specific usage.
### 5- Outrigger 

![](https://i.imgur.com/KDfHoH5.png)

- A dimension which has a reference to another dimension table.
- The secondary dimension called outrigger dimension.
- Should be used ==carefully in limited cases==.
### 6- Shrunken Roll

![dPA43vE.png](https://i.imgur.com/dPA43vE.png)

- Subset of a larger, more granular dimension used for aggregating fact tables.
- High level of summary (زي اني اجيب توتال المبيعات عمستوي المدينة).
- Improve query performance by reducing the size of the dimension tables joined to the fact table.
### 7- Multi-valued 
- Has multiple values associated with a single record in the fact table.
- When the dimension has lower granularity than the fact.
- Sales order fact may be linked to multiple sales representatives or products.
- ==Bridge table== is used to handle the ==many-to-many relationship's== where it contains the foreign key of each dimension.
#### Example Tables:

![](https://i.imgur.com/3kzHjz4.png)

#### Output:
##### Implementation-1:

![](https://i.imgur.com/HJuIoFq.png)
##### Implementation-2:
- This implementation has solved the weighting but still has duplicates.
  
![](https://i.imgur.com/EjcaCHK.png)
##### Implementation-3:

![](https://i.imgur.com/sOc9rXb.png)

### 8- Slowly Changing
- Attribute values changes less frequently (زي العنوان لو نقلت سكن لازم يتغير).
#### Types of Handling:
- There are more types more than type-4 but they will be and abstract combination of type-1, type-2, type-3 like type-4.
##### Type-0:

![](https://i.imgur.com/pSuuxG6.png)

- Fixed Dimension.
- We don't change the current even the source changes.
##### Type-1: 

![](https://i.imgur.com/fU0mzbY.png)

- No History.
- No history is maintained, only the latest replaces the current.
##### Type-2: 

![](https://i.imgur.com/hPiFT3l.png)

- History is maintained.
- Series of history of records are maintained.
- Instead of making the TerminationDt NULL we can add infinite date to filter date more easily.
##### Type-3: 

![](https://i.imgur.com/HdvR4kd.png)

- Hybrid between type-1 and type-2.
- Only the last change and the latest new change is stored.
##### Type-4: 

![](https://i.imgur.com/RpPZeMT.png)

- Most commonly used.
- Splitting the data into two tables, first the current record and the second is the historical.
### 9- Fast Changing
- Attributes values changing rapidly.
#### Implementation:

![o8bT01W.png](https://i.imgur.com/o8bT01W.png)

- Identify the fast changing columns, this includes weight and blood pressure.
- Then create a junk dimension that stores the qualitative data with the fast changing columns.


![](https://i.imgur.com/x9LCBnL.png)

- Then create the mini dimension to map the relation between the tables.
- To get the start_date and end_date we can use the LEAD and LAG analytical functions in SQL. 
### 10- Heterogeneous
- This type works when we have a case that a company selling different product to the same base of customer. Every product has it different attributes.
- One famous example of this type assume an insurance company has two types of product like health and car. In this case Car insurance has different attributes than the health insurance.

![](https://i.imgur.com/QULJCsL.png)

### 11- Swappable 
- Dimension that has multiple alternative versions of itself that can be swapped at query time.
- Has different meaning, structure

![](https://i.imgur.com/euGU8yD.png)

#### Implementation:
- Direct join between Fact and Dimension with filter based on PartyType (run-time ). In this case Party includes some empty columns based on the type.
##### Logical views:
- Each view has its own number of columns and rows based on the type details.
- Pros: Easy for (managing, implementation) with consistent views.
- Cons: Performance and manage the authorization per view.   
##### Physical tables (Types & Sub-types):
- Pros: Performance, better design.
- Cons: Data redundancy, key could be duplicated (when join with fact), increase in data size, and ETL headache.
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
### 4- Multidimensional Model

![](https://i.imgur.com/cGmVS54.png)

- Consists of cells, ==Sparse== cubes has many empty cells and Dense ==has== few empty cells.
- Data cubes represents data in terms of dimension of facts.
- Each cell has aggregated data.
- Stores huge amount of data in a simplified way to increase efficiency. 
- Cubes has 4-12 dimension, but only 2-3 dimensions can be viewed.

#### Multidimensional Model Operations:
##### 1- Rollup:
- Summarizing or aggregating the dimensions from lower level to higher level.
- less detailed, more summarized view leading to reduce the grain.
  
![](https://i.imgur.com/ec6zK3J.png)
##### 2-Drill-down:
- Expands the data from higher level to lower level to view detailed information.
- Increase granularity.

![](https://i.imgur.com/LoKqc2P.png)
##### 3- Slice:
- Subset of cube from a single dimension.

![](https://i.imgur.com/aJxbytU.png)
##### 4- Dice:
- Subset of cube from multiple dimensions

![](https://i.imgur.com/xO6iIz1.png)