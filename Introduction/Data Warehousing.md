## What is Data Warehousing
- Central repository of integrated data from one or more different sources.
- Stores current and ==historical== data in a single place.
### Characteristics of Data Warehouse 
#### 1- Integration 
- Integrated environment which allow us to integrate from different sources.
#### 2- Time-Variant 
- Data is organized based on periods  (hourly, daily, weekly, monthly, quarterly, yearly).
#### 3- Subject-oriented 
- Organized around specific subjects or areas of interest within an organization, such as sales, finance, or marketing, rather than focusing on operational processes.
#### 4- Non-Volatile 
Once data is stored in the data warehouse, it is non-volatile, meaning it is not updated, deleted, or modified frequently like in operational databases. Instead, it is maintained for historical analysis and reporting purposes.

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

## Multi-Temperature data management model

### Hot Data
-  Frequently accessed, mission-critical data that requires high-performance storage and fast access times.
### Warm Data 
- Moderately accessed data that may not require real-time access but still needs to be readily available for analysis or operational purposes.
### Cold Data 
- Infrequently accessed or dormant data that is kept for compliance, regulatory, or long-term archival purposes.

#### Benefit's of Multi-Temperature data management model
- Cost reduction (لو عندنا ١٠٠ تيرا بايت ممكن نقسمهم مثلا ٥٠ تيرا بايت hot و ٥٠ تيرا بايت cold)
- Performance 
#### Implementation Process 
- Frequency of access 
- Data change rate 
- Identify which storage type is suitable for the project
