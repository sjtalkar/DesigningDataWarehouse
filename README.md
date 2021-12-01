# Designing a Data Warehouse

Kimball Dimensional Modeling Techniques

Enterprise perspective: leveraging conformed dimensions for enterprise consistency and integration.
ETL will be done once and will the source fo truth for decision making.
A common ground has to be cleared and prepared for everyone to be making decisions based on the same set of facts.
The data source has to be backed by integrity.
Data must be current and must arrive in a timely fashion.
Dimensional models should not be designed by focusing on predefined reports or analyses; the design should center on measurement processes. The key is to focus on the organization's measurement events that are typically stable, unlike analyses that are constantly evolving.



- The idea that a measurement event in the physical world has a one-to-one relationship to a **single row** in the corresponding fact table is a bedrock principle for dimensional modeling. Everything else builds from this foundation.
- Source systems maintain little historical data; a good data warehouse can relieve the source systems of much of the responsibility for representing the past.
- Data in the queryable presentation area of the DW/BI system must be dimensional, atomic (complemented by performance-enhancing aggregates), business process-centric, and adhere to the enterprise data warehouse bus architecture. The data must not be structured according to individual departments' interpretation of the data.



You will see that facts are sometimes semi-additive or even non-additive.
- Semi-additive facts, such as account balances, cannot be summed across the time dimension.
- Non-additive facts, such as unit prices, can never be added.
- Fact tables tend to be deep in terms of the number of rows, but narrow in terms of the number of columns. 
- The fact table generally has its own primary key composed of a subset of the foreign keys. This key is often called a composite key.
- All fact tables have two or more foreign keys that connect to the dimension tables' primary keys


 #### Unless the text is unique for every row in the fact table, it belongs in the dimension table.
 - The dimension tables contain the textual context associated with a business process measurement event. They describe the “who, what, where, when, how, and why” associated with the event.
 - The designer should make every effort to put textual data into dimensions where they can be correlated more effectively with the other textual dimension attributes and consume much less space. You should not store redundant textual information in fact tables. 
 - There are usually a handful of dimensions that together uniquely identify each fact table row.
 - Dimension tables tend to have fewer rows than fact tables, but can be wide with many large text columns. 
 - Each dimension is defined by a single primary key , which serves as the basis for referential integrity with any given fact table to which it is joined.
 - Dimension attributes serve as the primary source of query constraints, groupings, and report labels.
 - Dimension tables often represent hierarchical relationships. For example, products roll up into brands and then into categories. For each row in the product dimension, you should store the associated brand and category description. The hierarchical descriptive information is stored redundantly in the spirit of ease of use and query performance.

#### Ambiguities
When triaging operational source data, it is sometimes unclear whether a numeric data element is a fact or dimension attribute. You often make the decision by asking whether the column is a measurement that takes on lots of values and participates in calculations (making it a fact) or is a discretely valued description that is more or less constant and participates in constraints and row labels (making it a dimensional attribute). 

# The  ETL
The primary mission of the ETL system is to hand off the dimension and fact tables in the delivery step, these subsystems are critical. Many of these defined subsystems focus on dimension table processing, such as surrogate key assignments, code lookups to provide appropriate descriptions, splitting, or combining columns to present the appropriate data values, or joining underlying third normal form table structures into flattened denormalized dimensions. In contrast, fact tables are typically large and time consuming to load, but preparing them for the presentation area is typically straightforward.

