## What is Data Warehousing
- Central repository of integrated data from one or more different sources.
- Stores current and ==historical== data in a single place.

## Data Warehouse Layers
![[DWH-Layers.png]]
## Database vs Data Warehouse

| Metric            | Database                    | Data Warehouse                     |
| ----------------- | --------------------------- | ---------------------------------- |
| Design Purpose    | to record data              | to analyze data                    |
| Transaction Type  | OLTP                        | OLAP                               |
| Orientation       | application-oriented        | subject-oriented                   |
| Data Freshness    | data available in real-time | data must be refreshed when needed |
| Modeling Approach | relational data modeling    | dimensional data modeling          |
| Data Volume       | GB/TB (<1000M)              | TB/PB (1000M>)                     |

## What is Data Marts
- Subsection of a data warehouse, where data has been partitioned out of overall data warehouse specifically for departments like sales, HR, marketing.
- Simplifies data access as we don't need to worry about giving access to data warehouse to everyone.

 ### In-memory Database
 - Usually used for data marts.
 - Highly optimized for query performance.
 - Eliminates response time coming from disk.
 - Scans data by columns not rows.
 - Large queries that takes time are broken down into multiple parts and processed in parallel.
#### Implementation Challenges:
 - Lose of all information when device losses power or is reset, leading to low durability.
 - Can be expensive due to the high cost of RAM compared to disk storage, where scaling up the memory capacity of servers to accommodate scalability can significantly increase infrastructure costs.
## Data Warehouse vs Data Lake
| Metric          | Data Warehouse          | Data Lakes                                     |
| --------------- | ----------------------- | ---------------------------------------------- |
| Data Type       | structured data         | structured, semi-structured, unstructured data |
| Data Processing | ETL data pre-proccesing | ELT data pre-proccesing                        |
| Schema          | predefined schema       | ad-hoc schema                                  |
| Data Quality    | high data quality       | low data quality                               |
| Scalability     | vertical scalable       | horizontal scalable                            |
