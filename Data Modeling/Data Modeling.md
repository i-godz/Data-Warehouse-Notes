## What is Data Modeling 
- Process of creating a conceptual representation of the structure and relationships of data within a specific domain.
- Involves identifying entities, attributes, and relationships to create a model that accurately reflects how data is organized and how it interacts within a system or organization.
- Serves as a blueprint for database design and helps ensure that data is organized efficiently, accurately, and in a way that meets the needs of the business or application.

## Types of Data Modeling 

### Conceptual

![[conceptual-data-modeling.png]]

- Defines ==what== the system contains.
- Represents a high-level and abstract understanding of business concepts.
- Focus on entities and their relationships without getting into technical details.

### Logical 

![[logical-data-modeling.png]]

- Defines ==how== the system should be implemented regardless the DMBS.
- Less abstract, translate the conceptual model into more detailed structure.
- Focus on the technical mapping of constraints rules and data structures.
- Involves normalization for data integrity.

### Physical 

![[physical-data-modeling.png]]

- Defines ==how== the system should be implemented using specific DMBS.
- Least abstract.
- Represent tables, columns, indexes, data types, indexes and other database specific structure.

## Surrogate vs Natural Key:

| Metric              | Surrogate                      | Natural                        |
| ------------------- | ------------------------------ | ------------------------------ |
| Unique              | Yes                            | Yes                            |
| Name                | Artificial, System generated   | Business key                   |
| Business Meaning    | Doesnt have a business meaning | has a business meaning         |
| Conceptual Relation | Doesn't relate                 | Part of conceptual design      |
| Creation            | System                         | Set of column(s) from the data |
### Surrogate or Natural Key:
#### Natural 
##### Pros:
- Key has a business meaning.
- No extra space or computation needed.
##### Cons:
- Could change over time.
- Difficult for maintenance.
#### Surrogate
##### Pros:
- Stable.
- Easy to maintain.
- Less disk I/O is required.
- Guaranteed to be unique.
- Simple key structure.
##### Cons:
- Has no business meaning.
- Extra column is included in the data.
