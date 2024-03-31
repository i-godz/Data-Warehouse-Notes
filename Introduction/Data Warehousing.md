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
- Once data is stored in the data warehouse, it is non-volatile, meaning it is not updated, deleted, or modified frequently like in operational databases. Instead, it is maintained for historical analysis and reporting purposes.

## Data Warehouse Layers
![[DWH-Layers.png]]

### Data Integration and ETL Layer:

![](https://i.imgur.com/knc21xH.png)

#### What is ETL?
- Core function in the data engineering and business intelligence teams.
- Preferred to unify ETL tools across team members and the organization.
- ETL becomes mandatory due to increase in data volume and variety of data types (structured, semi-structured, unstructured).
##### Extraction:
- Extracting the data from multiple data sources.
##### Transformation:
- Dropping duplicates.
- Trimming spaces and removing nulls.
- Adding or removing columns.
- Change of data granularity.
- Converting data types.
##### Loading:
- Loading the transformed data into the target table based on the required format.
#### Extraction Types:
##### 1- Initial Load:
- Initial extraction from the source data and and loading it into the target system (e.g., data warehouse or data lake).
- It is a one-time process that happens during the initial setup or migration of a data pipeline.
##### 2- Full Load:
- Extracts all data from the source system, overwriting or replacing the existing data in the target system.
- It is typically performed periodically (daily, weekly, monthly, or yearly) to refresh the data in the target system with the latest data from the source.
- Can be resource-intensive and time-consuming.
##### 3- Delta/Incremental Load:
- Loads the new data on a regular basis by setting a frequency that can be daily, weekly and monthly.
- The new data can be identified by using the "date" column in any table.
- Alternatively we can also identify by using by the primary key that is randomly generated.
#### ETL Best Practices:
##### 1- Auditing:
- Identify the abnormalities even if the ETL job doesn't have any errors/
- Conform the received rows are received into the targeted source (source = target + malformed)
- Identify the abnormal behavior if the source rows changed.
- Identify the abnormal behavior in the total aggregations.
##### 2- Logging:
-  ETL logging includes logs of any activities or events that occur in the ETL job before, during, and after every stage.
- Some types of events or metrics typically captured during ETL logging are "Start and stop events", "Status updates", "Errors and exceptions", 
  "Audit information", "Testing and debugging details".
##### 3- Rejection Handling:
- It means the data is not accurate or as expected when compared to the same source system.
- If we use this data as-is, we are risk affecting the quality of the business reports.
- To manage the malformed records, we need to "Define what is the meaning by well-formed records or accurate record" and  "Configure handling actions for the malformed records".
##### 4- Modularity:
- ETL architecture is not only the quality of data but also how the code is reusable and modularized.
- To achieve modularity we need to:
    - Design template jobs for each part of the system.
    - Standard methods and strategy for common tasks such as logging, error handling, and rejecting handling.
    - Reduce the duplicate code by creating common libraries for the ETL.
    - Create common functionality for unit testing.
##### 5- Data Lineage:
- Data Lineage is an essential part of our process to understand how this data transformed and where this data originated.
- It helps to make the trust in the data by connecting the target into the source.
- It helps with data tracing at the row level.
##### 6- Error Handling:
- Error handling answers the question "What should we do if the process failed?"
- We deal with errors using different strategies:
    - Fail safe / a.k.a. graceful shutdown/stop (ايه الحجات الي اعملها لما يحصل فيلاير؟ زي مثلا اريليز ريسورسس ).
    - Fail fast(لو عارف ان هيجيلي ٥ ريكورد وجالي ٤ فعلطول منغير تفكير يحصل ريجيكت).
    - Design error handling framework it includes: prevention and response.
##### 7- Atomicity:
- Atomicity refers to breaking more significant parts into smaller individual parts.
- It also refers to how to split bigger ETL process or job into smaller parts.
### ETL vs ELT:
- ELT is the same process as ELT but we switch the order of loading and transforming the data.

| Metric          | ETL                                                                                              | ELT                                                                                                                              |
| --------------- | ------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| Data Processing | Data is processed before loading into the target system.                                         | Data is loaded into the target system first and then transformed within the system.                                              |
| Transformations | Transformation occurs outside of the target system.                                              | Transformation occurs within the target system, leveraging its processing capabilities.                                          |
| Performance     | Can be slower for large datasets due to transformation before loading                            | Generally faster for large datasets as transformation happens in the target system                                               |
| Data Storage    | Requires staging area for transformed data                                                       | Requires less staging area as raw data is loaded first                                                                           |
| Data Quality    | Higher data quality as data is cleansed before loading                                           | Lower initial data quality as raw data is loaded first                                                                           |
| Maturity        | Has been the traditional approach to data integration and has been extensively used for decades. | Relatively newer concept compared to ETL but gaining popularity rapidly, especially with the rise of cloud-based data platforms. |
| Examples        | Informatica, IBM DataStage, Talend.                                                              | Apache Spark, Google BigQuery, Amazon Redshift.                                                                                  |
| Ideal for       | Well defined data models as data quality is critical.                                            | Agile environment's, on-the-go schema.                                                                                           |
| Business Value  | Reporting and Analytics.                                                                         | ML and Data Science.                                                                                                             |
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
- A data lake is a centralized repository that allows organizations to store all their structured and unstructured data at any scale.

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
